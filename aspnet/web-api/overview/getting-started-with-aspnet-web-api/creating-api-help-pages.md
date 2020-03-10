---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: 建立 ASP.NET Web API 的說明頁面-ASP.NET 4。x
author: MikeWasson
description: 本教學課程與程式碼示範如何建立 ASP.NET 4.x 中 ASP.NET Web API 的說明頁面。
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 8308dab8bd66aa8f5a3c5fb4133fc7a3df78f671
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556872"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="b420a-103">建立 ASP.NET Web API 的說明頁面</span><span class="sxs-lookup"><span data-stu-id="b420a-103">Creating Help Pages for ASP.NET Web API</span></span>

<span data-ttu-id="b420a-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b420a-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b420a-105">本教學課程與程式碼示範如何建立 ASP.NET 4.x 中 ASP.NET Web API 的說明頁面。</span><span class="sxs-lookup"><span data-stu-id="b420a-105">This tutorial with code shows how to create help pages for ASP.NET Web API in ASP.NET 4.x.</span></span>

<span data-ttu-id="b420a-106">當您建立 Web API 時，建立說明頁通常會很有説明，讓其他開發人員知道如何呼叫您的 API。</span><span class="sxs-lookup"><span data-stu-id="b420a-106">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="b420a-107">您可以手動建立所有檔，但最好盡可能自動增加。</span><span class="sxs-lookup"><span data-stu-id="b420a-107">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span> <span data-ttu-id="b420a-108">為了讓這項工作更容易，ASP.NET Web API 在執行時間提供自動產生說明頁面的程式庫。</span><span class="sxs-lookup"><span data-stu-id="b420a-108">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="b420a-109">建立 API 說明頁面</span><span class="sxs-lookup"><span data-stu-id="b420a-109">Creating API Help Pages</span></span>

<span data-ttu-id="b420a-110">安裝[ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。</span><span class="sxs-lookup"><span data-stu-id="b420a-110">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="b420a-111">此更新會將說明頁面整合到 Web API 專案範本中。</span><span class="sxs-lookup"><span data-stu-id="b420a-111">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="b420a-112">接下來，建立新的 ASP.NET MVC 4 專案，然後選取 [Web API] 專案範本。</span><span class="sxs-lookup"><span data-stu-id="b420a-112">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="b420a-113">專案範本會建立名為 `ValuesController`的範例 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="b420a-113">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="b420a-114">此範本也會建立 API 說明頁面。</span><span class="sxs-lookup"><span data-stu-id="b420a-114">The template also creates the API help pages.</span></span> <span data-ttu-id="b420a-115">[說明] 頁面的所有程式碼檔案都會放在專案的 [區域] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="b420a-115">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="b420a-116">當您執行應用程式時，首頁會包含 [API 說明] 頁面的連結。</span><span class="sxs-lookup"><span data-stu-id="b420a-116">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="b420a-117">從首頁中，相對路徑為/Help。</span><span class="sxs-lookup"><span data-stu-id="b420a-117">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="b420a-118">此連結會將您帶入 API 摘要頁面。</span><span class="sxs-lookup"><span data-stu-id="b420a-118">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="b420a-119">此頁面的 MVC 視圖會定義在區域/HelpPage/Views/Help/Index. cshtml 中。</span><span class="sxs-lookup"><span data-stu-id="b420a-119">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="b420a-120">您可以編輯此頁面來修改版面配置、簡介、標題、樣式等等。</span><span class="sxs-lookup"><span data-stu-id="b420a-120">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="b420a-121">頁面的主要部分是以控制器分組的 Api 資料表。</span><span class="sxs-lookup"><span data-stu-id="b420a-121">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="b420a-122">系統會使用**IApiExplorer**介面，以動態方式產生資料表專案。</span><span class="sxs-lookup"><span data-stu-id="b420a-122">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="b420a-123">（稍後我會詳細討論此介面）。如果您加入新的 API 控制器，則資料表會在執行時間自動更新。</span><span class="sxs-lookup"><span data-stu-id="b420a-123">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="b420a-124">[API] 欄位會列出 HTTP 方法和相對 URI。</span><span class="sxs-lookup"><span data-stu-id="b420a-124">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="b420a-125">[描述] 資料行包含每個 API 的檔。</span><span class="sxs-lookup"><span data-stu-id="b420a-125">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="b420a-126">一開始，檔只是預留位置文字。</span><span class="sxs-lookup"><span data-stu-id="b420a-126">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="b420a-127">在下一節中，我將示範如何從 XML 批註新增檔。</span><span class="sxs-lookup"><span data-stu-id="b420a-127">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="b420a-128">每個 API 都有頁面的連結，其中包含更詳細的資訊，包括範例要求和回應主體。</span><span class="sxs-lookup"><span data-stu-id="b420a-128">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="b420a-129">將說明頁面加入至現有的專案</span><span class="sxs-lookup"><span data-stu-id="b420a-129">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="b420a-130">您可以使用 NuGet 套件管理員，將說明頁面新增至現有的 Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="b420a-130">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="b420a-131">從不同于「Web API」範本的專案範本開始，此選項很有用。</span><span class="sxs-lookup"><span data-stu-id="b420a-131">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="b420a-132">從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="b420a-132">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="b420a-133">在 [[套件管理員主控台](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)] 視窗中，輸入下列其中一個命令：</span><span class="sxs-lookup"><span data-stu-id="b420a-133">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="b420a-134">針對**C#** 應用程式： `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span><span class="sxs-lookup"><span data-stu-id="b420a-134">For a **C#** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span></span>

<span data-ttu-id="b420a-135">針對**Visual Basic**應用程式： `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span><span class="sxs-lookup"><span data-stu-id="b420a-135">For a **Visual Basic** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span></span>

<span data-ttu-id="b420a-136">有兩個套件，一個用於C# ，一個用於 Visual Basic。</span><span class="sxs-lookup"><span data-stu-id="b420a-136">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="b420a-137">請務必使用符合您專案的對應項。</span><span class="sxs-lookup"><span data-stu-id="b420a-137">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="b420a-138">此命令會安裝必要的元件，並加入說明頁面（位於 [區域]/[HelpPage] 資料夾）的 MVC views。</span><span class="sxs-lookup"><span data-stu-id="b420a-138">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="b420a-139">您必須手動新增 [說明] 頁面的連結。</span><span class="sxs-lookup"><span data-stu-id="b420a-139">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="b420a-140">URI 為/Help。</span><span class="sxs-lookup"><span data-stu-id="b420a-140">The URI is /Help.</span></span> <span data-ttu-id="b420a-141">若要在 razor 視圖中建立連結，請新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="b420a-141">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="b420a-142">此外，請務必註冊區域。</span><span class="sxs-lookup"><span data-stu-id="b420a-142">Also, make sure to register areas.</span></span> <span data-ttu-id="b420a-143">在 global.asax 檔案中，將下列程式碼新增至**應用程式\_Start**方法（如果尚未這麼做）：</span><span class="sxs-lookup"><span data-stu-id="b420a-143">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="b420a-144">新增 API 檔</span><span class="sxs-lookup"><span data-stu-id="b420a-144">Adding API Documentation</span></span>

<span data-ttu-id="b420a-145">根據預設，說明頁面會有檔的預留位置字串。</span><span class="sxs-lookup"><span data-stu-id="b420a-145">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="b420a-146">您可以使用[XML 檔批註](https://msdn.microsoft.com/library/b2s063f7.aspx)來建立檔。</span><span class="sxs-lookup"><span data-stu-id="b420a-146">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="b420a-147">若要啟用這項功能，請開啟檔案區域/HelpPage/應用程式\_Start/HelpPageConfig，並取消批註下列程式程式碼：</span><span class="sxs-lookup"><span data-stu-id="b420a-147">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="b420a-148">現在啟用 XML 檔。</span><span class="sxs-lookup"><span data-stu-id="b420a-148">Now enable XML documentation.</span></span> <span data-ttu-id="b420a-149">在方案總管中，以滑鼠右鍵按一下專案，然後選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="b420a-149">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="b420a-150">選取 [**組建**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b420a-150">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="b420a-151">在 [**輸出**] 下，檢查**XML**檔檔案。</span><span class="sxs-lookup"><span data-stu-id="b420a-151">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="b420a-152">在編輯方塊中，輸入 "App\_Data/xml"。</span><span class="sxs-lookup"><span data-stu-id="b420a-152">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="b420a-153">接下來，開啟 `ValuesController` API 控制器的程式碼，其定義于/Controllers/ValuesController.cs。</span><span class="sxs-lookup"><span data-stu-id="b420a-153">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesController.cs.</span></span> <span data-ttu-id="b420a-154">將一些檔批註新增至控制器方法。</span><span class="sxs-lookup"><span data-stu-id="b420a-154">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="b420a-155">例如:</span><span class="sxs-lookup"><span data-stu-id="b420a-155">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="b420a-156">提示：如果您將插入號放在方法上方的那一行，並輸入三個正斜線，Visual Studio 會自動插入 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="b420a-156">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="b420a-157">然後您可以填入空白。</span><span class="sxs-lookup"><span data-stu-id="b420a-157">Then you can fill in the blanks.</span></span>

<span data-ttu-id="b420a-158">現在，再次建立並執行應用程式，並流覽至 [說明] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b420a-158">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="b420a-159">檔字串應該會出現在 API 資料表中。</span><span class="sxs-lookup"><span data-stu-id="b420a-159">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="b420a-160">[說明] 頁面會在執行時間從 XML 檔案讀取字串。</span><span class="sxs-lookup"><span data-stu-id="b420a-160">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="b420a-161">（當您部署應用程式時，請務必部署 XML 檔案）。</span><span class="sxs-lookup"><span data-stu-id="b420a-161">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="b420a-162">幕後</span><span class="sxs-lookup"><span data-stu-id="b420a-162">Under the Hood</span></span>

<span data-ttu-id="b420a-163">[說明] 頁面是以**ApiExplorer**類別為基礎，這是 Web API 架構的一部分。</span><span class="sxs-lookup"><span data-stu-id="b420a-163">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="b420a-164">**ApiExplorer**類別會提供用來建立說明頁的原始材料。</span><span class="sxs-lookup"><span data-stu-id="b420a-164">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="b420a-165">針對每個 API， **ApiExplorer**包含描述 API 的**ApiDescription** 。</span><span class="sxs-lookup"><span data-stu-id="b420a-165">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="b420a-166">基於此目的，「API」會定義為 HTTP 方法和相對 URI 的組合。</span><span class="sxs-lookup"><span data-stu-id="b420a-166">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="b420a-167">例如，以下是一些不同的 Api：</span><span class="sxs-lookup"><span data-stu-id="b420a-167">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="b420a-168">取得/api/Products</span><span class="sxs-lookup"><span data-stu-id="b420a-168">GET /api/Products</span></span>
- <span data-ttu-id="b420a-169">取得/api/Products/{id}</span><span class="sxs-lookup"><span data-stu-id="b420a-169">GET /api/Products/{id}</span></span>
- <span data-ttu-id="b420a-170">張貼/api/Products</span><span class="sxs-lookup"><span data-stu-id="b420a-170">POST /api/Products</span></span>

<span data-ttu-id="b420a-171">如果控制器動作支援多個 HTTP 方法，則**ApiExplorer**會將每個方法視為不同的 API。</span><span class="sxs-lookup"><span data-stu-id="b420a-171">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="b420a-172">若要隱藏**ApiExplorer**中的 API，請將**ApiExplorerSettings**屬性新增至動作，並將*IgnoreApi*設定為 true。</span><span class="sxs-lookup"><span data-stu-id="b420a-172">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="b420a-173">您也可以將此屬性新增至控制器，以排除整個控制器。</span><span class="sxs-lookup"><span data-stu-id="b420a-173">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="b420a-174">ApiExplorer 類別會從**IDocumentationProvider**介面取得檔字串。</span><span class="sxs-lookup"><span data-stu-id="b420a-174">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="b420a-175">如您稍早所見，說明頁面程式庫提供了從 XML 檔字串取得檔的**IDocumentationProvider** 。</span><span class="sxs-lookup"><span data-stu-id="b420a-175">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="b420a-176">此程式碼位於/Areas/HelpPage/XmlDocumentationProvider.cs。</span><span class="sxs-lookup"><span data-stu-id="b420a-176">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="b420a-177">您可以撰寫自己的**IDocumentationProvider**，以從另一個來源取得檔。</span><span class="sxs-lookup"><span data-stu-id="b420a-177">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="b420a-178">若要連線，請呼叫**SetDocumentationProvider**擴充方法（定義于**HelpPageConfigurationExtensions** ）</span><span class="sxs-lookup"><span data-stu-id="b420a-178">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="b420a-179">**ApiExplorer**會自動呼叫**IDocumentationProvider**介面，以取得每個 API 的檔字串。</span><span class="sxs-lookup"><span data-stu-id="b420a-179">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="b420a-180">它會將它們儲存在**ApiDescription**和**ApiParameterDescription**物件的**檔**屬性中。</span><span class="sxs-lookup"><span data-stu-id="b420a-180">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b420a-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b420a-181">Next Steps</span></span>

<span data-ttu-id="b420a-182">您不限於此處顯示的說明頁面。</span><span class="sxs-lookup"><span data-stu-id="b420a-182">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="b420a-183">事實上， **ApiExplorer**並不限於建立說明頁面。</span><span class="sxs-lookup"><span data-stu-id="b420a-183">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="b420a-184">Yao Huang Lin 已經撰寫了一些絕佳的 blog 文章，讓您有現成的想法：</span><span class="sxs-lookup"><span data-stu-id="b420a-184">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="b420a-185">將簡單的測試用戶端新增至 ASP.NET Web API 說明頁面</span><span class="sxs-lookup"><span data-stu-id="b420a-185">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="b420a-186">讓 ASP.NET Web API 的說明頁面在自我裝載的服務上工作</span><span class="sxs-lookup"><span data-stu-id="b420a-186">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="b420a-187">ASP.NET Web API 的設計階段產生說明頁面（或用戶端）</span><span class="sxs-lookup"><span data-stu-id="b420a-187">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="b420a-188">Advanced Help Page 自訂專案</span><span class="sxs-lookup"><span data-stu-id="b420a-188">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
