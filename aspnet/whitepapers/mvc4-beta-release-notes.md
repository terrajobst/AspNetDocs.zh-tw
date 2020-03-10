---
uid: whitepapers/mvc4-beta-release-notes
title: ASP.NET MVC 4 |Microsoft Docs
author: rick-anderson
description: 本檔說明適用于 Visual Studio 2010 的 ASP.NET MVC 4 Beta 發行版本。
ms.author: riande
ms.date: 09/09/2011
ms.assetid: 666407bb-81de-4319-89ba-0302c382a208
msc.legacyurl: /whitepapers/mvc4-beta-release-notes
msc.type: content
ms.openlocfilehash: 17800dfe091bbb7afb25f7f41e3bd885b882edb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523300"
---
# <a name="aspnet-mvc-4"></a><span data-ttu-id="76900-103">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="76900-103">ASP.NET MVC 4</span></span>

> <span data-ttu-id="76900-104">本檔說明適用于 Visual Studio 2010 的 ASP.NET MVC 4 Beta 發行版本。</span><span class="sxs-lookup"><span data-stu-id="76900-104">This document describes the release of ASP.NET MVC 4 Beta for Visual Studio 2010.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="76900-105">這不是最新版本。</span><span class="sxs-lookup"><span data-stu-id="76900-105">This is not the most current release.</span></span> <span data-ttu-id="76900-106">您可以在[這裡](mvc4-release-notes.md)取得 ASP.NET MVC 4 RC 版本資訊。</span><span class="sxs-lookup"><span data-stu-id="76900-106">The ASP.NET MVC 4 RC release notes are available [here](mvc4-release-notes.md).</span></span>

- [<span data-ttu-id="76900-107">安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="76900-107">Installation Notes</span></span>](#_Toc303253802)
- [<span data-ttu-id="76900-108">文件</span><span class="sxs-lookup"><span data-stu-id="76900-108">Documentation</span></span>](#_Toc303253803)
- [<span data-ttu-id="76900-109">支援</span><span class="sxs-lookup"><span data-stu-id="76900-109">Support</span></span>](#_Toc303253804)
- [<span data-ttu-id="76900-110">軟體需求</span><span class="sxs-lookup"><span data-stu-id="76900-110">Software Requirements</span></span>](#_Toc303253805)
- [<span data-ttu-id="76900-111">將 ASP.NET MVC 3 專案升級至 ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="76900-111">Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4</span></span>](#_Toc303253806)
- [<span data-ttu-id="76900-112">ASP.NET MVC 4 Beta 的新功能</span><span class="sxs-lookup"><span data-stu-id="76900-112">New Features in ASP.NET MVC 4 Beta</span></span>](#_Toc303253807)

    - [<span data-ttu-id="76900-113">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="76900-113">ASP.NET Web API</span></span>](#_Toc317096197)
    - [<span data-ttu-id="76900-114">ASP.NET 單一頁面應用程式</span><span class="sxs-lookup"><span data-stu-id="76900-114">ASP.NET Single Page Application</span></span>](#_Toc317096198)
    - [<span data-ttu-id="76900-115">預設專案範本的增強功能</span><span class="sxs-lookup"><span data-stu-id="76900-115">Enhancements to Default Project Templates</span></span>](#_Toc303253808)
    - [<span data-ttu-id="76900-116">行動專案範本</span><span class="sxs-lookup"><span data-stu-id="76900-116">Mobile Project Template</span></span>](#_Toc303253809)
    - [<span data-ttu-id="76900-117">顯示模式</span><span class="sxs-lookup"><span data-stu-id="76900-117">Display Modes</span></span>](#_Toc303253810)
    - [<span data-ttu-id="76900-118">jQuery Mobile、視圖切換器和瀏覽器覆寫</span><span class="sxs-lookup"><span data-stu-id="76900-118">jQuery Mobile, the View Switcher, and Browser Overriding</span></span>](#_Toc303253811)
    - [<span data-ttu-id="76900-119">Visual Studio 中產生程式碼的配方</span><span class="sxs-lookup"><span data-stu-id="76900-119">Recipes for Code Generation in Visual Studio</span></span>](#_Toc303253812)
    - [<span data-ttu-id="76900-120">非同步控制器的工作支援</span><span class="sxs-lookup"><span data-stu-id="76900-120">Task Support for Asynchronous Controllers</span></span>](#_Toc303253813)
    - [<span data-ttu-id="76900-121">Azure SDK</span><span class="sxs-lookup"><span data-stu-id="76900-121">Azure SDK</span></span>](#_Toc303253814)
    - [<span data-ttu-id="76900-122">已知問題和重大變更</span><span class="sxs-lookup"><span data-stu-id="76900-122">Known Issues and Breaking Changes</span></span>](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a><span data-ttu-id="76900-123">安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="76900-123">Installation Notes</span></span>

<span data-ttu-id="76900-124">您可以使用 Web Platform Installer，從 [ [ASP.NET MVC 4](../mvc/mvc4.md) ] 首頁安裝適用于 Visual Studio 2010 的 ASP.NET Mvc 4 Beta。</span><span class="sxs-lookup"><span data-stu-id="76900-124">ASP.NET MVC 4 Beta for Visual Studio 2010 can be installed from the [ASP.NET MVC 4 home page](../mvc/mvc4.md) using the Web Platform Installer.</span></span>

<span data-ttu-id="76900-125">在安裝 ASP.NET MVC 4 Beta 之前，您必須先卸載任何先前安裝的 ASP.NET MVC 4 預覽。</span><span class="sxs-lookup"><span data-stu-id="76900-125">You must uninstall any previously installed previews of ASP.NET MVC 4 prior to installing ASP.NET MVC 4 Beta.</span></span>

<span data-ttu-id="76900-126">此版本與 .NET Framework 4.5 開發人員預覽版不相容。</span><span class="sxs-lookup"><span data-stu-id="76900-126">This release is not compatible with the .NET Framework 4.5 Developer Preview.</span></span> <span data-ttu-id="76900-127">您必須先卸載 .NET 4.5 開發人員預覽版，才能安裝 ASP.NET MVC 4 Beta 版。</span><span class="sxs-lookup"><span data-stu-id="76900-127">You must uninstall the .NET 4.5 Developer Preview before installing the ASP.NET MVC 4 Beta.</span></span>

<span data-ttu-id="76900-128">ASP.NET MVC 4 可以安裝，而且可以與 ASP.NET MVC 3 並存執行。</span><span class="sxs-lookup"><span data-stu-id="76900-128">ASP.NET MVC 4 can be installed and can run side-by-side with ASP.NET MVC 3.</span></span>

<a id="_Toc303253803"></a>
## <a name="documentation"></a><span data-ttu-id="76900-129">文件</span><span class="sxs-lookup"><span data-stu-id="76900-129">Documentation</span></span>

<span data-ttu-id="76900-130">ASP.NET MVC 文件位於 MSDN 網站上，其 URL 如下所示：</span><span class="sxs-lookup"><span data-stu-id="76900-130">Documentation for ASP.NET MVC is available on the MSDN website at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

<span data-ttu-id="76900-131">如需有關 ASP.NET MVC 的教學課程和其他資訊，請在 ASP.NET 網站的 MVC 4 頁面（[https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)）中找到。</span><span class="sxs-lookup"><span data-stu-id="76900-131">Tutorials and other information about ASP.NET MVC are available on the MVC 4 page of the ASP.NET website ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)).</span></span>

<a id="_Toc303253804"></a>
## <a name="support"></a><span data-ttu-id="76900-132">支援</span><span class="sxs-lookup"><span data-stu-id="76900-132">Support</span></span>

<span data-ttu-id="76900-133">這是預覽版本，並未正式支援。</span><span class="sxs-lookup"><span data-stu-id="76900-133">This is a preview release and is not officially supported.</span></span> <span data-ttu-id="76900-134">如果您有關于使用此版本的問題，請將其張貼至 ASP.NET MVC 論壇（[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)），其中 ASP.NET 社區的成員經常能夠提供非正式的支援。</span><span class="sxs-lookup"><span data-stu-id="76900-134">If you have questions about working with this release, post them to the ASP.NET MVC forum ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)), where members of the ASP.NET community are frequently able to provide informal support.</span></span>

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a><span data-ttu-id="76900-135">軟體需求</span><span class="sxs-lookup"><span data-stu-id="76900-135">Software Requirements</span></span>

<span data-ttu-id="76900-136">Visual Studio 的 ASP.NET MVC 4 元件需要 PowerShell 2.0，以及 Visual Studio 2010 Service Pack 1 或 Visual Web Developer Express 2010 （含 Service Pack 1）。</span><span class="sxs-lookup"><span data-stu-id="76900-136">The ASP.NET MVC 4 components for Visual Studio require PowerShell 2.0 and either Visual Studio 2010 with Service Pack 1 or Visual Web Developer Express 2010 with Service Pack 1.</span></span>

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a><span data-ttu-id="76900-137">將 ASP.NET MVC 3 專案升級至 ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="76900-137">Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4</span></span>

<span data-ttu-id="76900-138">ASP.NET MVC 4 可以與 ASP.NET MVC 3 並存安裝在同一部電腦上，讓您有彈性選擇何時將 ASP.NET MVC 3 應用程式升級為 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="76900-138">ASP.NET MVC 4 can be installed side by side with ASP.NET MVC 3 on the same computer, which gives you flexibility in choosing when to upgrade an ASP.NET MVC 3 application to ASP.NET MVC 4.</span></span>

<span data-ttu-id="76900-139">最簡單的升級方式是建立新的 ASP.NET MVC 4 專案，並將所有的視圖、控制器、程式碼和內容檔案從現有的 MVC 3 專案複製到新的專案，然後更新新專案中的元件參考，以符合舊的專案。</span><span class="sxs-lookup"><span data-stu-id="76900-139">The simplest way to upgrade is to create a new ASP.NET MVC 4 project and copy all the views, controllers, code, and content files from the existing MVC 3 project to the new project and then to update the assembly references in the new project to match the old project.</span></span> <span data-ttu-id="76900-140">如果您已變更 MVC 3 專案中的 web.config 檔案，則也必須將這些變更合併到 MVC 4 專案的 web.config 檔案中。</span><span class="sxs-lookup"><span data-stu-id="76900-140">If you have made changes to the Web.config file in the MVC 3 project, you must also merge those changes into the Web.config file in the MVC 4 project.</span></span>

<span data-ttu-id="76900-141">若要將現有的 ASP.NET MVC 3 應用程式手動升級為第4版，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="76900-141">To manually upgrade an existing ASP.NET MVC 3 application to version 4, do the following:</span></span>

1. <span data-ttu-id="76900-142">在專案的所有 web.config 檔案中（專案的根目錄中有一個，一個在 Views 資料夾，另一個位於專案中每個區域的 Views 資料夾中），取代下列文字的每個實例：</span><span class="sxs-lookup"><span data-stu-id="76900-142">In all Web.config files in the project (there is one in the root of the project, one in the Views folder, and one in the Views folder for each area in your project), replace every instance of the following text:</span></span>

    [!code-console[Main](mvc4-beta-release-notes/samples/sample1.cmd)]

    <span data-ttu-id="76900-143">具有下列對應的文字：</span><span class="sxs-lookup"><span data-stu-id="76900-143">with the following corresponding text:</span></span>

    [!code-console[Main](mvc4-beta-release-notes/samples/sample2.cmd)]
2. <span data-ttu-id="76900-144">在根 web.config 檔案中，將*網頁： Version*專案更新為 "2.0.0.0"，並加入值為 "true" 的新*PreserveLoginUrl*機碼：</span><span class="sxs-lookup"><span data-stu-id="76900-144">In the root Web.config file, update the *webPages:Version* element to "2.0.0.0" and add a new *PreserveLoginUrl* key that has the value "true":</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample3.xml)]
3. <span data-ttu-id="76900-145">在方案總管中，刪除*system.web*的參考（指向第3版的 DLL）。</span><span class="sxs-lookup"><span data-stu-id="76900-145">In Solution Explorer, delete the reference to *System.Web.Mvc* (which points to the version 3 DLL).</span></span> <span data-ttu-id="76900-146">然後加入*system.web*的參考（v 4.0.0.0）。</span><span class="sxs-lookup"><span data-stu-id="76900-146">Then add a reference to *System.Web.Mvc* (v4.0.0.0).</span></span> <span data-ttu-id="76900-147">特別是，請進行下列變更，以更新元件參考。</span><span class="sxs-lookup"><span data-stu-id="76900-147">In particular, make the following changes to update the assembly references.</span></span> <span data-ttu-id="76900-148">詳細資料如下：</span><span class="sxs-lookup"><span data-stu-id="76900-148">Here are the details:</span></span>

    1. <span data-ttu-id="76900-149">在方案總管中，刪除下列元件的參考：</span><span class="sxs-lookup"><span data-stu-id="76900-149">In Solution Explorer, delete the references to the following assemblies:</span></span> 

        - <span data-ttu-id="76900-150">*System.web. Mvc*（v 3.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="76900-150">*System.Web.Mvc*(v3.0.0.0)</span></span>
        - <span data-ttu-id="76900-151">*System.web*（1.0.0.0 版）</span><span class="sxs-lookup"><span data-stu-id="76900-151">*System.Web.WebPages*(v1.0.0.0)</span></span>
        - <span data-ttu-id="76900-152">*System.web*（1.0.0.0 版）</span><span class="sxs-lookup"><span data-stu-id="76900-152">*System.Web.Razor*(v1.0.0.0)</span></span>
        - <span data-ttu-id="76900-153">System.web. *Deployment*（1.0.0.0 版）</span><span class="sxs-lookup"><span data-stu-id="76900-153">*System.Web.WebPages.Deployment*(v1.0.0.0)</span></span>
        - <span data-ttu-id="76900-154">System.web。 *Razor*（1.0.0.0 版）</span><span class="sxs-lookup"><span data-stu-id="76900-154">*System.Web.WebPages.Razor*(v1.0.0.0)</span></span>
    2. <span data-ttu-id="76900-155">新增下列元件的參考：</span><span class="sxs-lookup"><span data-stu-id="76900-155">Add a references to the following assemblies:</span></span> 

        - <span data-ttu-id="76900-156">*System.web. Mvc*（v 4.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="76900-156">*System.Web.Mvc*(v4.0.0.0)</span></span>
        - <span data-ttu-id="76900-157">*System.web*（v 2.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="76900-157">*System.Web.WebPages*(v2.0.0.0)</span></span>
        - <span data-ttu-id="76900-158">*System.web*（v 2.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="76900-158">*System.Web.Razor*(v2.0.0.0)</span></span>
        - <span data-ttu-id="76900-159">System.web. *Deployment*（v 2.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="76900-159">*System.Web.WebPages.Deployment*(v2.0.0.0)</span></span>
        - <span data-ttu-id="76900-160">System.web. *Razor*（v 2.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="76900-160">*System.Web.WebPages.Razor*(v2.0.0.0)</span></span>
4. <span data-ttu-id="76900-161">在方案總管中，以滑鼠右鍵按一下專案名稱，然後選取 [卸載專案]。</span><span class="sxs-lookup"><span data-stu-id="76900-161">In Solution Explorer, right-click the project name and then select Unload Project.</span></span> <span data-ttu-id="76900-162">然後再次以滑鼠右鍵按一下名稱，然後選取 [編輯*專案*名稱 .csproj]。</span><span class="sxs-lookup"><span data-stu-id="76900-162">Then right-click the name again and select Edit *ProjectName*.csproj.</span></span>
5. <span data-ttu-id="76900-163">找出*ProjectTypeGuids*元素，並將 {E53F8FEA-EAE0-44A6-8774-FFD645390401} 取代為 {E3E379DF-F4C6-4180-9B81-6769533ABE47}。</span><span class="sxs-lookup"><span data-stu-id="76900-163">Locate the *ProjectTypeGuids* element and replace {E53F8FEA-EAE0-44A6-8774-FFD645390401} with {E3E379DF-F4C6-4180-9B81-6769533ABE47}.</span></span>
6. <span data-ttu-id="76900-164">儲存變更，關閉您編輯的專案（.csproj）檔案，以滑鼠右鍵按一下專案，然後選取 [重載專案]。</span><span class="sxs-lookup"><span data-stu-id="76900-164">Save the changes, close the project (.csproj) file you were editing, right-click the project, and then select Reload Project.</span></span>
7. <span data-ttu-id="76900-165">如果專案參考使用舊版 ASP.NET MVC 編譯的任何協力廠商程式庫，請開啟根 web.config 檔案，然後*在 [設定*] 區段下新增下列三個*bindingRedirect*元素：</span><span class="sxs-lookup"><span data-stu-id="76900-165">If the project references any third-party libraries that are compiled using previous versions of ASP.NET MVC, open the root Web.config file and add the following three *bindingRedirect* elements under the *configuration* section:</span></span> 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample4.xml)]

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4-beta"></a><span data-ttu-id="76900-166">ASP.NET MVC 4 Beta 的新功能</span><span class="sxs-lookup"><span data-stu-id="76900-166">New Features in ASP.NET MVC 4 Beta</span></span>

<span data-ttu-id="76900-167">本節說明 ASP.NET MVC 4 Beta 版本中引進的功能。</span><span class="sxs-lookup"><span data-stu-id="76900-167">This section describes features that have been introduced in the ASP.NET MVC 4 Beta release.</span></span>

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a><span data-ttu-id="76900-168">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="76900-168">ASP.NET Web API</span></span>

<span data-ttu-id="76900-169">ASP.NET MVC 4 現在包含 ASP.NET Web API，這是建立 HTTP 服務的新架構，可以連接到各種用戶端，包括瀏覽器和行動裝置。</span><span class="sxs-lookup"><span data-stu-id="76900-169">ASP.NET MVC 4 now includes ASP.NET Web API, a new framework for creating HTTP services that can reach a broad range of clients including browsers and mobile devices.</span></span> <span data-ttu-id="76900-170">ASP.NET Web API 也是建立 RESTful 服務的理想平臺。</span><span class="sxs-lookup"><span data-stu-id="76900-170">ASP.NET Web API is also an ideal platform for building RESTful services.</span></span>

<span data-ttu-id="76900-171">ASP.NET Web API 包含下列功能的支援：</span><span class="sxs-lookup"><span data-stu-id="76900-171">ASP.NET Web API includes support for the following features:</span></span>

- <span data-ttu-id="76900-172">**新式 HTTP 程式設計模型：** 使用新的強型別 HTTP 物件模型，直接存取和操作 Web Api 中的 HTTP 要求和回應。</span><span class="sxs-lookup"><span data-stu-id="76900-172">**Modern HTTP programming model:** Directly access and manipulate HTTP requests and responses in your Web APIs using a new, strongly typed HTTP object model.</span></span> <span data-ttu-id="76900-173">相同的程式設計模型和 HTTP 管線會透過新的 HttpClient 類型在用戶端上對稱使用。</span><span class="sxs-lookup"><span data-stu-id="76900-173">The same programming model and HTTP pipeline is symmetrically available on the client through the new HttpClient type.</span></span>
- <span data-ttu-id="76900-174">**完整的路由支援**： web api 現在支援一組完整的路由功能，一律是 web 堆疊的一部分，包括路由參數和條件約束。</span><span class="sxs-lookup"><span data-stu-id="76900-174">**Full support for routes**: Web APIs now support the full set of route capabilities that have always been a part of the Web stack, including route parameters and constraints.</span></span> <span data-ttu-id="76900-175">此外，對動作的對應具有對慣例的完整支援，因此您不再需要將屬性（例如 [HttpPost]）套用至您的類別和方法。</span><span class="sxs-lookup"><span data-stu-id="76900-175">Additionally, mapping to actions has full support for conventions, so you no longer need to apply attributes such as [HttpPost] to your classes and methods.</span></span>
- <span data-ttu-id="76900-176">**內容協商**：用戶端和伺服器可以一起使用，以判斷從 API 傳回之資料的正確格式。</span><span class="sxs-lookup"><span data-stu-id="76900-176">**Content negotiation**: The client and server can work together to determine the right format for data being returned from an API.</span></span> <span data-ttu-id="76900-177">我們提供 XML、JSON 和表單 URL 編碼格式的預設支援，您可以新增自己的格式器來擴充這項支援，或甚至取代預設的內容協商策略。</span><span class="sxs-lookup"><span data-stu-id="76900-177">We provide default support for XML, JSON, and Form URL-encoded formats, and you can extend this support by adding your own formatters, or even replace the default content negotiation strategy.</span></span>
- <span data-ttu-id="76900-178">**模型系結和驗證：** 模型系結器提供簡單的方法，可從 HTTP 要求的各個部分解壓縮資料，並將這些訊息部分轉換成可供 Web API 動作使用的 .NET 物件。</span><span class="sxs-lookup"><span data-stu-id="76900-178">**Model binding and validation:** Model binders provide an easy way to extract data from various parts of an HTTP request and convert those message parts into .NET objects which can be used by the Web API actions.</span></span>
- <span data-ttu-id="76900-179">**篩選器：** Web Api 現在支援篩選準則，包括知名的篩選準則，例如 [授權] 屬性。</span><span class="sxs-lookup"><span data-stu-id="76900-179">**Filters:** Web APIs now supports filters, including well-known filters such as the [Authorize] attribute.</span></span> <span data-ttu-id="76900-180">您可以撰寫並插入您自己的篩選準則，以進行動作、授權和例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="76900-180">You can author and plug in your own filters for actions, authorization and exception handling.</span></span>
- <span data-ttu-id="76900-181">**查詢撰寫：** 藉由只傳回 IQueryable&lt;T&gt;，您的 Web API 將支援透過 OData URL 慣例進行查詢。</span><span class="sxs-lookup"><span data-stu-id="76900-181">**Query composition:** By simply returning IQueryable&lt;T&gt;, your Web API will support querying via the OData URL conventions.</span></span>
- <span data-ttu-id="76900-182">已**改善 HTTP 詳細資料的可測試性：** Web API 動作現在可以與 HttpRequestMessage 和 HttpResponseMessage 的實例搭配使用，而不是在靜態內容物件中設定 HTTP 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="76900-182">**Improved testability of HTTP details:** Rather than setting HTTP details in static context objects, Web API actions can now work with instances of HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="76900-183">這些物件的泛型版本也存在，讓您除了 HTTP 類型之外，還可以使用您的自訂類型。</span><span class="sxs-lookup"><span data-stu-id="76900-183">Generic versions of these objects also exist to let you work with your custom types in addition to the HTTP types.</span></span>
- <span data-ttu-id="76900-184">**改善的控制反轉（IoC） Via DependencyResolver：** Web API 現在會使用 MVC 的相依性解析程式所執行的服務定位器模式，來取得許多不同設施的實例。</span><span class="sxs-lookup"><span data-stu-id="76900-184">**Improved Inversion of Control (IoC) via DependencyResolver:** Web API now uses the service locator pattern implemented by MVC's dependency resolver to obtain instances for many different facilities.</span></span>
- <span data-ttu-id="76900-185">以**程式碼為基礎的設定：** Web API 設定只會透過程式碼完成，讓您的設定檔保持乾淨。</span><span class="sxs-lookup"><span data-stu-id="76900-185">**Code-based configuration:** Web API configuration is accomplished solely through code, leaving your config files clean.</span></span>
- <span data-ttu-id="76900-186">**自我裝載：** Web Api 除了 IIS 之外，也可以裝載于您自己的進程中，同時仍然使用路由的完整功能和 Web API 的其他功能。</span><span class="sxs-lookup"><span data-stu-id="76900-186">**Self-host:** Web APIs can be hosted in your own process in addition to IIS while still using the full power of routes and other features of Web API.</span></span>

<span data-ttu-id="76900-187">如需 ASP.NET Web API 的詳細資訊，請流覽[https://www.asp.net/web-api](../web-api/index.md)。</span><span class="sxs-lookup"><span data-stu-id="76900-187">For more details on ASP.NET Web API please visit [https://www.asp.net/web-api](../web-api/index.md).</span></span>

<a id="_Toc317096198"></a>
### <a name="aspnet-single-page-application"></a><span data-ttu-id="76900-188">ASP.NET 單一頁面應用程式</span><span class="sxs-lookup"><span data-stu-id="76900-188">ASP.NET Single Page Application</span></span>

<span data-ttu-id="76900-189">ASP.NET MVC 4 現在提供了使用 JavaScript 和 Web Api 來建立單一頁面應用程式的體驗，並具有大量用戶端互動的早期預覽。</span><span class="sxs-lookup"><span data-stu-id="76900-189">ASP.NET MVC 4 now includes an early preview of the experience for building single page applications with significant client-side interactions using JavaScript and Web APIs.</span></span> <span data-ttu-id="76900-190">這種支援包括：</span><span class="sxs-lookup"><span data-stu-id="76900-190">This support includes:</span></span>

- <span data-ttu-id="76900-191">一組 JavaScript 程式庫，可與快取的資料進行更豐富的本機互動</span><span class="sxs-lookup"><span data-stu-id="76900-191">A set of JavaScript libraries for richer local interactions with cached data</span></span>
- <span data-ttu-id="76900-192">適用于工作單位和 DAL 支援的其他 Web API 元件</span><span class="sxs-lookup"><span data-stu-id="76900-192">Additional Web API components for unit of work and DAL support</span></span>
- <span data-ttu-id="76900-193">具有可快速開始使用之樣板的 MVC 專案範本</span><span class="sxs-lookup"><span data-stu-id="76900-193">An MVC project template with scaffolding to get started quickly</span></span>

<span data-ttu-id="76900-194">如需 ASP.NET MVC 4 中單一頁面應用程式支援的詳細資訊，請造訪[https://www.asp.net/single-page-application](../single-page-application/index.md)。</span><span class="sxs-lookup"><span data-stu-id="76900-194">For more details on the Single Page Application support in ASP.NET MVC 4 please visit [https://www.asp.net/single-page-application](../single-page-application/index.md).</span></span>

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a><span data-ttu-id="76900-195">預設專案範本的增強功能</span><span class="sxs-lookup"><span data-stu-id="76900-195">Enhancements to Default Project Templates</span></span>

<span data-ttu-id="76900-196">用來建立新 ASP.NET MVC 4 專案的範本已更新，以建立更現代化的網站：</span><span class="sxs-lookup"><span data-stu-id="76900-196">The template that is used to create new ASP.NET MVC 4 projects has been updated to create a more modern-looking website:</span></span>

![](mvc4-beta-release-notes/_static/image1.png)

<span data-ttu-id="76900-197">除了表面改良以外，新的範本中還有改進的功能。</span><span class="sxs-lookup"><span data-stu-id="76900-197">In addition to cosmetic improvements, there's improved functionality in the new template.</span></span> <span data-ttu-id="76900-198">此範本採用一種稱為適應性轉譯的技術，在桌面瀏覽器和行動瀏覽器中都不需要任何自訂。</span><span class="sxs-lookup"><span data-stu-id="76900-198">The template employs a technique called adaptive rendering to look good in both desktop browsers and mobile browsers without any customization.</span></span>

![](mvc4-beta-release-notes/_static/image2.png)

<span data-ttu-id="76900-199">若要查看作用中的調適型轉譯，您可以使用行動模擬器，或只嘗試調整桌面瀏覽器視窗的大小。</span><span class="sxs-lookup"><span data-stu-id="76900-199">To see adaptive rendering in action, you can use a mobile emulator or just try resizing the desktop browser window to be smaller.</span></span> <span data-ttu-id="76900-200">當瀏覽器視窗夠小時，頁面的版面配置就會變更。</span><span class="sxs-lookup"><span data-stu-id="76900-200">When the browser window gets small enough, the layout of the page will change.</span></span>

<span data-ttu-id="76900-201">預設專案範本的另一個增強功能是使用 JavaScript 來提供更豐富的 UI。</span><span class="sxs-lookup"><span data-stu-id="76900-201">Another enhancement to the default project template is the use of JavaScript to provide a richer UI.</span></span> <span data-ttu-id="76900-202">範本中使用的登入和註冊連結，是如何使用 jQuery UI 對話方塊來呈現豐富的登入畫面的範例：</span><span class="sxs-lookup"><span data-stu-id="76900-202">The Login and Register links that are used in the template are examples of how to use the jQuery UI Dialog to present a rich login screen:</span></span>

![](mvc4-beta-release-notes/_static/image3.png)

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a><span data-ttu-id="76900-203">行動專案範本</span><span class="sxs-lookup"><span data-stu-id="76900-203">Mobile Project Template</span></span>

<span data-ttu-id="76900-204">如果您要開始新的專案，並想要特別針對行動和平板電腦瀏覽器建立網站，則可以使用 [新增行動應用程式] 專案範本。</span><span class="sxs-lookup"><span data-stu-id="76900-204">If you're starting a new project and want to create a site specifically for mobile and tablet browsers, you can use the new Mobile Application project template.</span></span> <span data-ttu-id="76900-205">這是以 jQuery Mobile 為基礎，這是一個開放原始碼程式庫，可用於建立觸控優化的 UI：</span><span class="sxs-lookup"><span data-stu-id="76900-205">This is based on jQuery Mobile, an open-source library for building touch-optimized UI:</span></span>

![](mvc4-beta-release-notes/_static/image4.png)

<span data-ttu-id="76900-206">此範本包含與網際網路應用程式範本相同的應用程式結構（而且控制器程式碼幾乎完全相同），但它是使用 jQuery Mobile 樣式化，在觸控式行動裝置上外觀良好並表現良好。</span><span class="sxs-lookup"><span data-stu-id="76900-206">This template contains the same application structure as the Internet Application template (and the controller code is virtually identical), but it's styled using jQuery Mobile to look good and behave well on touch-based mobile devices.</span></span> <span data-ttu-id="76900-207">若要深入瞭解如何結構和樣式行動 UI，請參閱[JQuery mobile 專案網站](http://jquerymobile.com/)。</span><span class="sxs-lookup"><span data-stu-id="76900-207">To learn more about how to structure and style mobile UI, see the [jQuery Mobile project website](http://jquerymobile.com/).</span></span>

<span data-ttu-id="76900-208">如果您已經有想要新增行動優化視圖的桌面導向網站，或者您想要建立單一網站來提供不同的樣式視圖給桌上型電腦和行動瀏覽器，您可以使用新的顯示模式功能。</span><span class="sxs-lookup"><span data-stu-id="76900-208">If you already have a desktop-oriented site that you want to add mobile-optimized views to, or if you want to create a single site that serves differently styled views to desktop and mobile browsers, you can use the new Display Modes feature.</span></span> <span data-ttu-id="76900-209">(請參閱下節)。</span><span class="sxs-lookup"><span data-stu-id="76900-209">(See the next section.)</span></span>

<a id="_Toc303253810"></a>
### <a name="display-modes"></a><span data-ttu-id="76900-210">顯示模式</span><span class="sxs-lookup"><span data-stu-id="76900-210">Display Modes</span></span>

<span data-ttu-id="76900-211">新的顯示模式功能可讓應用程式根據提出要求的瀏覽器選取 views。</span><span class="sxs-lookup"><span data-stu-id="76900-211">The new Display Modes feature lets an application select views depending on the browser that's making the request.</span></span> <span data-ttu-id="76900-212">例如，如果桌面瀏覽器要求首頁，應用程式可能會使用 Views\Home\Index.cshtml 範本。</span><span class="sxs-lookup"><span data-stu-id="76900-212">For example, if a desktop browser requests the Home page, the application might use the Views\Home\Index.cshtml template.</span></span> <span data-ttu-id="76900-213">如果行動瀏覽器要求首頁，應用程式可能會傳回 Views\Home\Index.mobile.cshtml 範本。</span><span class="sxs-lookup"><span data-stu-id="76900-213">If a mobile browser requests the Home page, the application might return the Views\Home\Index.mobile.cshtml template.</span></span>

<span data-ttu-id="76900-214">您也可以針對特定瀏覽器類型覆寫版面配置和部分。</span><span class="sxs-lookup"><span data-stu-id="76900-214">Layouts and partials can also be overridden for particular browser types.</span></span> <span data-ttu-id="76900-215">例如:</span><span class="sxs-lookup"><span data-stu-id="76900-215">For example:</span></span>

- <span data-ttu-id="76900-216">如果您的 [Views\Shared] 資料夾同時包含 [\_配置] 和 [\_配置]，則應用程式預設會在行動瀏覽器的要求期間使用 \_的配置，而在其他要求期間則會 \_配置. cshtml。</span><span class="sxs-lookup"><span data-stu-id="76900-216">If your Views\Shared folder contains both the \_Layout.cshtml and \_Layout.mobile.cshtml templates, by default the application will use \_Layout.mobile.cshtml during requests from mobile browsers and \_Layout.cshtml during other requests.</span></span>
- <span data-ttu-id="76900-217">如果資料夾同時包含 \_MyPartial 和 \_MyPartial，則指令 @Html.Partial（"\_MyPartial"）會在行動瀏覽器的要求期間轉譯 \_MyPartial，並在其他要求期間 \_MyPartial. cshtml。</span><span class="sxs-lookup"><span data-stu-id="76900-217">If a folder contains both \_MyPartial.cshtml and \_MyPartial.mobile.cshtml, the instruction @Html.Partial("\_MyPartial") will render \_MyPartial.mobile.cshtml during requests from mobile browsers, and \_MyPartial.cshtml during other requests.</span></span>

<span data-ttu-id="76900-218">如果您想要為其他裝置建立更特定的視圖、配置或部分視圖，您可以註冊新的*DefaultDisplayMode*實例，以指定當要求符合特定條件時要搜尋的名稱。</span><span class="sxs-lookup"><span data-stu-id="76900-218">If you want to create more specific views, layouts, or partial views for other devices, you can register a new *DefaultDisplayMode* instance to specify which name to search for when a request satisfies particular conditions.</span></span> <span data-ttu-id="76900-219">例如，您可以將下列程式碼新增至 global.asax 檔案中的*應用程式\_Start*方法，將字串 "iPhone" 註冊為當 Apple iPhone 瀏覽器提出要求時適用的顯示模式：</span><span class="sxs-lookup"><span data-stu-id="76900-219">For example, you could add the following code to the *Application\_Start* method in the Global.asax file to register the string "iPhone" as a display mode that applies when the Apple iPhone browser makes a request:</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample5.cs)]

<span data-ttu-id="76900-220">在此程式碼執行之後，當 Apple iPhone 瀏覽器提出要求時，您的應用程式將會使用 Views\Shared\\_Layout iPhone. cshtml 配置（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="76900-220">After this code runs, when an Apple iPhone browser makes a request, your application will use the Views\Shared\\_Layout.iPhone.cshtml layout (if it exists).</span></span>

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-the-view-switcher-and-browser-overriding"></a><span data-ttu-id="76900-221">jQuery Mobile、視圖切換器和瀏覽器覆寫</span><span class="sxs-lookup"><span data-stu-id="76900-221">jQuery Mobile, the View Switcher, and Browser Overriding</span></span>

<span data-ttu-id="76900-222">jQuery Mobile 是一種開放原始碼程式庫，可用於建立觸控式優化的 web UI。</span><span class="sxs-lookup"><span data-stu-id="76900-222">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="76900-223">如果您想要搭配使用 jQuery Mobile 與 ASP.NET MVC 4 應用程式，您可以下載並安裝 NuGet 套件，以協助您開始著手。</span><span class="sxs-lookup"><span data-stu-id="76900-223">If you want to use jQuery Mobile with an ASP.NET MVC 4 application, you can download and install a NuGet package that helps you get started.</span></span> <span data-ttu-id="76900-224">若要從 Visual Studio 套件管理員主控台安裝它，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="76900-224">To install it from the Visual Studio Package Manager Console, type the following command:</span></span>

[!code-powershell[Main](mvc4-beta-release-notes/samples/sample6.ps1)]

<span data-ttu-id="76900-225">這會安裝 jQuery Mobile 和一些 helper 檔案，包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="76900-225">This installs jQuery Mobile and some helper files, including the following:</span></span>

- <span data-ttu-id="76900-226">Views/Shared/\_Layout，這是 jQuery Mobile 型版面配置。</span><span class="sxs-lookup"><span data-stu-id="76900-226">Views/Shared/\_Layout.Mobile.cshtml, which is a jQuery Mobile-based layout.</span></span>
- <span data-ttu-id="76900-227">View-切換器元件，其中包含 Views/Shared/\_ViewSwitcher 部分視圖和 ViewSwitcherController.cs 控制器。</span><span class="sxs-lookup"><span data-stu-id="76900-227">A view-switcher component, which consists of the Views/Shared/\_ViewSwitcher.cshtml partial view and the ViewSwitcherController.cs controller.</span></span>

<span data-ttu-id="76900-228">安裝套件之後，請使用行動瀏覽器執行應用程式（或對等的，如同 Firefox[使用者代理程式切換](http://chrispederick.com/work/user-agent-switcher/)器附加元件）。</span><span class="sxs-lookup"><span data-stu-id="76900-228">After you install the package, run your application using a mobile browser (or equivalent, like the Firefox [User Agent Switcher](http://chrispederick.com/work/user-agent-switcher/) add-on).</span></span> <span data-ttu-id="76900-229">您會看到頁面看起來相當不同，因為 jQuery Mobile 會處理版面配置和樣式設定。</span><span class="sxs-lookup"><span data-stu-id="76900-229">You'll see that your pages look quite different, because jQuery Mobile handles layout and styling.</span></span> <span data-ttu-id="76900-230">若要利用這一點，您可以執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="76900-230">To take advantage of this, you can do the following:</span></span>

- <span data-ttu-id="76900-231">依照稍早的[顯示模式](#_Toc303253810)（例如，建立 Views\Home\Index.mobile.cshtml 來覆寫行動瀏覽器的 Views\Home\Index.cshtml）中所述，建立特定的行動裝置視圖。</span><span class="sxs-lookup"><span data-stu-id="76900-231">Create mobile-specific view overrides as described under [Display Modes](#_Toc303253810) earlier (for example, create Views\Home\Index.mobile.cshtml to override Views\Home\Index.cshtml for mobile browsers).</span></span>
- <span data-ttu-id="76900-232">閱讀[JQuery mobile 檔](http://jquerymobile.com/)，以深入瞭解如何在行動裝置視圖中新增觸控優化的 UI 元素。</span><span class="sxs-lookup"><span data-stu-id="76900-232">Read the [jQuery Mobile documentation](http://jquerymobile.com/) to learn more about how to add touch-optimized UI elements in mobile views.</span></span>

<span data-ttu-id="76900-233">行動優化網頁的慣例是加入一個連結，其文字類似于桌面視圖或完整網站模式，可讓使用者切換至桌上出版本的頁面。</span><span class="sxs-lookup"><span data-stu-id="76900-233">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="76900-234">JQuery 封裝包含用於此用途的範例視圖-切換器元件。</span><span class="sxs-lookup"><span data-stu-id="76900-234">The jQuery.Mobile.MVC package includes a sample view-switcher component for this purpose.</span></span> <span data-ttu-id="76900-235">它會在預設的 Views\Shared\\_Layout 中使用，在轉譯頁面時看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="76900-235">It's used in the default Views\Shared\\_Layout.Mobile.cshtml view, and it looks like this when the page is rendered:</span></span>

![](mvc4-beta-release-notes/_static/image5.png)

<span data-ttu-id="76900-236">如果訪客按一下連結，就會切換到相同頁面的桌上出版本。</span><span class="sxs-lookup"><span data-stu-id="76900-236">If visitors click the link, they're switched to the desktop version of the same page.</span></span>

<span data-ttu-id="76900-237">因為您的桌上出版面配置預設不會包含視圖切換器，所以訪客不會有辦法進入行動模式。</span><span class="sxs-lookup"><span data-stu-id="76900-237">Because your desktop layout will not include a view switcher by default, visitors won't have a way to get to mobile mode.</span></span> <span data-ttu-id="76900-238">若要啟用這項操作，請將下列參考新增至您的桌上出版面配置 *\_ViewSwitcher* ，只在 *&lt;body&gt;* 元素內：</span><span class="sxs-lookup"><span data-stu-id="76900-238">To enable this, add the following reference to *\_ViewSwitcher* to your desktop layout, just inside the *&lt;body&gt;* element:</span></span>

[!code-cshtml[Main](mvc4-beta-release-notes/samples/sample7.cshtml)]

<span data-ttu-id="76900-239">「視圖切換器」會使用稱為「瀏覽器覆寫」的新功能。</span><span class="sxs-lookup"><span data-stu-id="76900-239">The view switcher uses a new feature called Browser Overriding.</span></span> <span data-ttu-id="76900-240">這項功能可讓您的應用程式將要求視為來自不同的瀏覽器（使用者代理程式），而不是實際來源。</span><span class="sxs-lookup"><span data-stu-id="76900-240">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they're actually from.</span></span> <span data-ttu-id="76900-241">下表列出瀏覽器覆寫所提供的方法。</span><span class="sxs-lookup"><span data-stu-id="76900-241">The following table lists the methods that Browser Overriding provides.</span></span>

| `HttpContext.SetOverriddenBrowser(userAgentString)` | <span data-ttu-id="76900-242">使用指定的使用者代理程式，覆寫要求的實際使用者代理程式值。</span><span class="sxs-lookup"><span data-stu-id="76900-242">Overrides the request's actual user agent value using the specified user agent.</span></span> |
| --- | --- |
| `HttpContext.GetOverriddenUserAgent()` | <span data-ttu-id="76900-243">傳回要求的使用者代理程式覆寫值，或如果未指定任何覆寫，則為實際的使用者代理字串。</span><span class="sxs-lookup"><span data-stu-id="76900-243">Returns the request's user agent override value, or the actual user agent string if no override has been specified.</span></span> |
| `HttpContext.GetOverriddenBrowser()` | <span data-ttu-id="76900-244">傳回*HttpBrowserCapabilitiesBase*實例，其對應至目前針對要求所設定的使用者代理程式（實際或已覆寫）。</span><span class="sxs-lookup"><span data-stu-id="76900-244">Returns an *HttpBrowserCapabilitiesBase* instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="76900-245">您可以使用這個值來取得*IsMobileDevice*之類的屬性。</span><span class="sxs-lookup"><span data-stu-id="76900-245">You can use this value to get properties such as *IsMobileDevice*.</span></span> |
| `HttpContext.ClearOverriddenBrowser()` | <span data-ttu-id="76900-246">移除目前要求之任何已覆寫的使用者代理程式。</span><span class="sxs-lookup"><span data-stu-id="76900-246">Removes any overridden user agent for the current request.</span></span> |

<span data-ttu-id="76900-247">瀏覽器覆寫是 ASP.NET MVC 4 的核心功能，即使您未安裝 jQuery. node.js 封裝也可以使用。</span><span class="sxs-lookup"><span data-stu-id="76900-247">Browser Overriding is a core feature of ASP.NET MVC 4 and is available even if you don't install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="76900-248">不過，它只會影響 [視圖]、[版面配置] 和 [局部視圖] 選取專案，而不會影響相依于*要求瀏覽器*物件的任何其他 ASP.NET 功能。</span><span class="sxs-lookup"><span data-stu-id="76900-248">However, it affects only view, layout, and partial-view selection — it does not affect any other ASP.NET feature that depends on the *Request.Browser* object.</span></span>

<span data-ttu-id="76900-249">根據預設，會使用 cookie 來儲存使用者代理程式覆寫。</span><span class="sxs-lookup"><span data-stu-id="76900-249">By default, the user-agent override is stored using a cookie.</span></span> <span data-ttu-id="76900-250">如果您想要將覆寫儲存在其他位置（例如，在資料庫中），您可以取代預設提供者（*BrowserOverrideStores*）。</span><span class="sxs-lookup"><span data-stu-id="76900-250">If you want to store the override elsewhere (for example, in a database), you can replace the default provider (*BrowserOverrideStores.Current*).</span></span> <span data-ttu-id="76900-251">此提供者的檔將提供給較新版本的 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="76900-251">Documentation for this provider will be available to accompany a later release of ASP.NET MVC.</span></span>

<a id="_Toc303253812"></a>
### <a name="recipes-for-code-generation-in-visual-studio"></a><span data-ttu-id="76900-252">Visual Studio 中產生程式碼的配方</span><span class="sxs-lookup"><span data-stu-id="76900-252">Recipes for Code Generation in Visual Studio</span></span>

<span data-ttu-id="76900-253">新的配方功能可讓 Visual Studio 根據您可以使用 NuGet 安裝的套件，產生解決方案特定的程式碼。</span><span class="sxs-lookup"><span data-stu-id="76900-253">The new Recipes feature enables Visual Studio to generate solution-specific code based on packages that you can install using NuGet.</span></span> <span data-ttu-id="76900-254">配方架構可讓開發人員輕鬆地撰寫程式碼產生外掛程式，您也可以用它來取代內建的程式碼產生器，以加入區域、新增控制器和加入視圖。</span><span class="sxs-lookup"><span data-stu-id="76900-254">The Recipes framework makes it easy for developers to write code-generation plugins, which you can also use to replace the built-in code generators for Add Area, Add Controller, and Add View.</span></span> <span data-ttu-id="76900-255">由於配方會部署為 NuGet 套件，因此可以輕鬆地簽入原始檔控制，並自動與專案上的所有開發人員共用。</span><span class="sxs-lookup"><span data-stu-id="76900-255">Because recipes are deployed as NuGet packages, they can easily be checked into source control and shared with all developers on the project automatically.</span></span> <span data-ttu-id="76900-256">它們也是以每個解決方案為基礎提供。</span><span class="sxs-lookup"><span data-stu-id="76900-256">They are also available on a per-solution basis.</span></span>

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a><span data-ttu-id="76900-257">非同步控制器的工作支援</span><span class="sxs-lookup"><span data-stu-id="76900-257">Task Support for Asynchronous Controllers</span></span>

<span data-ttu-id="76900-258">您現在可以將非同步動作方法撰寫為單一方法，以傳回*task*或 task 類型的物件 *&lt;ActionResult&gt;* 。</span><span class="sxs-lookup"><span data-stu-id="76900-258">You can now write asynchronous action methods as single methods that return an object of type *Task* or *Task&lt;ActionResult&gt;*.</span></span>

<span data-ttu-id="76900-259">例如，如果您使用的是 Visual C# 5 （或使用[非同步 CTP](https://msdn.microsoft.com/vstudio/async.aspx)），您可以建立如下所示的非同步動作方法：</span><span class="sxs-lookup"><span data-stu-id="76900-259">For example, if you're using Visual C# 5 (or using the [Async CTP](https://msdn.microsoft.com/vstudio/async.aspx)), you can create an asynchronous action method that looks like the following:</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample8.cs)]

<span data-ttu-id="76900-260">在上一個動作方法中，會以非同步方式呼叫*NewsService GetHeadlinesAsync*和*sportsService* ，而且不會封鎖執行緒集區中的執行緒。</span><span class="sxs-lookup"><span data-stu-id="76900-260">In the previous action method, the calls to *newsService.GetHeadlinesAsync* and *sportsService.GetScoresAsync* are called asynchronously and do not block a thread from the thread pool.</span></span>

<span data-ttu-id="76900-261">傳回*工作實例的*非同步動作方法也可以支援超時。</span><span class="sxs-lookup"><span data-stu-id="76900-261">Asynchronous action methods that return *Task* instances can also support timeouts.</span></span> <span data-ttu-id="76900-262">若要讓動作方法可取消，請將*CancellationToken*類型的參數新增至動作方法簽章。</span><span class="sxs-lookup"><span data-stu-id="76900-262">To make your action method cancellable, add a parameter of type *CancellationToken* to the action method signature.</span></span> <span data-ttu-id="76900-263">下列範例顯示的非同步動作方法，其超時時間為2500毫秒，且在發生超時時，會向用戶端顯示*TimedOut*的視圖。</span><span class="sxs-lookup"><span data-stu-id="76900-263">The following example shows an asynchronous action method that has a timeout of 2500 milliseconds and that displays a *TimedOut* view to the client if a timeout occurs.</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample9.cs)]

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a><span data-ttu-id="76900-264">Azure SDK</span><span class="sxs-lookup"><span data-stu-id="76900-264">Azure SDK</span></span>

<span data-ttu-id="76900-265">ASP.NET MVC 4 Beta 版支援2011年9月1.5 版的 Windows Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="76900-265">ASP.NET MVC 4 Beta supports the September 2011 1.5 release of the Windows Azure SDK.</span></span>

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="76900-266">已知問題和重大變更</span><span class="sxs-lookup"><span data-stu-id="76900-266">Known Issues and Breaking Changes</span></span>

- <span data-ttu-id="76900-267">**安裝 ASP.NET MVC 4 Beta 之後，在 cshtml 或 vbhtml 檔案內輸入程式碼片段或 JavaScript 後，Visual Studio 2010 Service Pack 1 CSHTML/VBHTML 編輯器中的 CSHTML/VBHTML 編輯器可能會暫停一段長時間。**</span><span class="sxs-lookup"><span data-stu-id="76900-267">**After installing ASP.NET MVC 4 Beta, the CSHTML/VBHTML editor in Visual Studio 2010 Service Pack 1 CSHTML/VBHTML editor may pause for a long time after typing snippet or JavaScript inside cshtml or vbhtml files.**</span></span> <span data-ttu-id="76900-268">這只會發生在剛建立但尚未編譯的 ASP.NET MVC 4 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="76900-268">This occurs only in ASP.NET MVC 4 applications which have just been created and have not yet been compiled.</span></span>

    <span data-ttu-id="76900-269">解決方法是編譯專案，以取得 bin 資料夾中的元件。</span><span class="sxs-lookup"><span data-stu-id="76900-269">The workaround is to compile the project to get the assemblies in the bin folder.</span></span> <span data-ttu-id="76900-270">請注意，如果您清除的專案會從 bin 資料夾中移除元件，則會傳回編輯器問題。</span><span class="sxs-lookup"><span data-stu-id="76900-270">Note, if you clean the project which removes the assemblies from the bin folder, the editor problem will come back.</span></span>

    <span data-ttu-id="76900-271">這將在下一版中更正。</span><span class="sxs-lookup"><span data-stu-id="76900-271">This will be corrected in the next release.</span></span>
- <span data-ttu-id="76900-272">**C#Visual Studio 11 Beta 的專案範本在 Global.asax.cs 中包含不正確的連接字串。**</span><span class="sxs-lookup"><span data-stu-id="76900-272">**C# Project templates for Visual Studio 11 Beta contain an incorrect connection string in Global.asax.cs.**</span></span> <span data-ttu-id="76900-273">在 Visual Studio 11 Beta 版中建立之專案的應用程式\_Start 方法中指定的預設連接包含 LocalDB 連接字串，其中包含非轉義的反斜線（\) 字元。</span><span class="sxs-lookup"><span data-stu-id="76900-273">The default connection specified in the Application\_Start method for projects created in Visual Studio 11 Beta contain a LocalDB connection string which contains an unescaped backslash (\) character.</span></span> <span data-ttu-id="76900-274">這會導致嘗試存取 Entity Framework DbCoNtext 時發生連接錯誤，這會產生 SqlException。</span><span class="sxs-lookup"><span data-stu-id="76900-274">This results in a connection error upon attempts to access a Entity Framework DbContext, which generates a SqlException.</span></span>

    <span data-ttu-id="76900-275">若要更正此問題，請將應用程式中的反斜線字元\_Start Global.asax.cs 方法中，使其如下所示：</span><span class="sxs-lookup"><span data-stu-id="76900-275">To correct this issue, escape the backslash character in the App\_Start method of Global.asax.cs so that it reads as follows:</span></span>

    [!code-csharp[Main](mvc4-beta-release-notes/samples/sample10.cs)]
- <span data-ttu-id="76900-276">**在 .NET 4.0 底下執行時，以 .NET 4.5 為目標的 MVC 4 應用程式會在嘗試存取 Http.sys 元件時擲回 FileLoadException。**</span><span class="sxs-lookup"><span data-stu-id="76900-276">**ASP.NET MVC 4 applications which target .NET 4.5 will throw a FileLoadException upon attempt to access the System.Net.Http.dll assembly when run under .NET 4.0.**</span></span> <span data-ttu-id="76900-277">ASP.NET 在 .NET 4.5 底下建立的 MVC 4 應用程式包含系結重新導向，會導致 FileLoadException 指出「無法載入檔案或元件 ' System .Net. Http ' 或它的其中一個相依性」。</span><span class="sxs-lookup"><span data-stu-id="76900-277">ASP.NET MVC 4 applications created under .NET 4.5 contain a binding redirect that will result in a FileLoadException which that states "Could not load file or assembly 'System.Net.Http' or one of its dependencies."</span></span> <span data-ttu-id="76900-278">當應用程式在已安裝 .NET 4.0 的系統上執行時。</span><span class="sxs-lookup"><span data-stu-id="76900-278">when the application is executed on a system with .NET 4.0 installed.</span></span> <span data-ttu-id="76900-279">若要更正此問題，請從 web.config 移除下列系結重新導向：</span><span class="sxs-lookup"><span data-stu-id="76900-279">To correct this issue, remove the following binding redirect from web.config:</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample11.xml)]

    <span data-ttu-id="76900-280">已修改之 web.config 中的元件繫結項目應如下所示：</span><span class="sxs-lookup"><span data-stu-id="76900-280">The assembly binding element in the modified web.config should appear as follows:</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample12.xml)]
- <span data-ttu-id="76900-281">在<strong>區域內叫用</strong><strong>時，Visual Basic 專案中的「新增控制器」專案範本會產生不正確的命名空間</strong>。</span><span class="sxs-lookup"><span data-stu-id="76900-281"><strong>The "Add Controller" item template in Visual Basic projects generates an incorrect namespace when invoked</strong><strong>from inside an area.</strong></span></span> <span data-ttu-id="76900-282">當您將控制器加入至使用 Visual Basic 之 ASP.NET MVC 專案中的區域時，專案範本會將錯誤的命名空間插入控制器中。</span><span class="sxs-lookup"><span data-stu-id="76900-282">When you add a controller to an area in an ASP.NET MVC project that uses Visual Basic, the item template inserts the wrong namespace into the controller.</span></span> <span data-ttu-id="76900-283">當您流覽至控制器中的任何動作時，結果會是「找不到檔案」錯誤。</span><span class="sxs-lookup"><span data-stu-id="76900-283">The result is a "file not found" error when you navigate to any action in the controller.</span></span>  
  
  <span data-ttu-id="76900-284">產生的命名空間會省略根命名空間之後的所有內容。</span><span class="sxs-lookup"><span data-stu-id="76900-284">The generated namespace omits everything after the root namespace.</span></span> <span data-ttu-id="76900-285">例如，所產生的命名空間是*RootNamespace* ，但應該是*RootNamespace. AreaName. 控制器*。</span><span class="sxs-lookup"><span data-stu-id="76900-285">For example, the namespace generated is *RootNamespace* but should be *RootNamespace.Areas.AreaName.Controllers* .</span></span>
- <span data-ttu-id="76900-286">**Razor View 引擎中的重大變更。**</span><span class="sxs-lookup"><span data-stu-id="76900-286">**Breaking changes in the Razor View Engine.**</span></span> <span data-ttu-id="76900-287">在重寫 Razor 剖析器的過程中，下列類型已從*system.web*移除：</span><span class="sxs-lookup"><span data-stu-id="76900-287">As part of a rewrite of the Razor parser, the following types were removed from *System.Web.Mvc.Razor*:</span></span> 

    - <span data-ttu-id="76900-288">*ModelSpan*</span><span class="sxs-lookup"><span data-stu-id="76900-288">*ModelSpan*</span></span>
    - <span data-ttu-id="76900-289">*MvcVBRazorCodeGenerator*</span><span class="sxs-lookup"><span data-stu-id="76900-289">*MvcVBRazorCodeGenerator*</span></span>
    - <span data-ttu-id="76900-290">*MvcCSharpRazorCodeGenerator*</span><span class="sxs-lookup"><span data-stu-id="76900-290">*MvcCSharpRazorCodeGenerator*</span></span>
    - <span data-ttu-id="76900-291">*MvcVBRazorCodeParser*</span><span class="sxs-lookup"><span data-stu-id="76900-291">*MvcVBRazorCodeParser*</span></span>

  <span data-ttu-id="76900-292">下列方法也已移除：</span><span class="sxs-lookup"><span data-stu-id="76900-292">The following methods were also removed:</span></span> 

    - <span data-ttu-id="76900-293">*MvcCSharpRazorCodeParser. ParseInheritsStatement （System.web. CodeBlockInfo）*</span><span class="sxs-lookup"><span data-stu-id="76900-293">*MvcCSharpRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span></span>
    - <span data-ttu-id="76900-294">*MvcWebPageRazorHost. DecorateCodeGenerator （System.web. RazorCodeGenerator）*</span><span class="sxs-lookup"><span data-stu-id="76900-294">*MvcWebPageRazorHost.DecorateCodeGenerator(System.Web.Razor.Generator.RazorCodeGenerator)*</span></span>
    - <span data-ttu-id="76900-295">*MvcVBRazorCodeParser. ParseInheritsStatement （System.web. CodeBlockInfo）*</span><span class="sxs-lookup"><span data-stu-id="76900-295">*MvcVBRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span></span>
- <span data-ttu-id="76900-296">**當 WebData 包含在 ASP.NET MVC 4 應用程式的/bin 目錄中時，它會接管用於表單驗證的 URL。**</span><span class="sxs-lookup"><span data-stu-id="76900-296">**When WebMatrix.WebData.dll is included in the /bin directory of an ASP.NET MVC 4 apps, it takes over the URL for forms authentication.**</span></span> <span data-ttu-id="76900-297">將 WebData 新增至您的應用程式（例如，在使用 [新增可部署的相依性] 對話方塊時，選取 [使用 Razor 語法 ASP.NET Web Pages]）將會覆寫驗證登入重新導向至/account/logon，而非預設 ASP.NET MVC 帳戶控制器所預期的/account/login。</span><span class="sxs-lookup"><span data-stu-id="76900-297">Adding the WebMatrix.WebData.dll assembly to your application (for example, by selecting "ASP.NET Web Pages with Razor Syntax" when using the Add Deployable Dependencies dialog) will override the authentication login redirect to /account/logon rather than /account/login as expected by the default ASP.NET MVC Account Controller.</span></span> <span data-ttu-id="76900-298">若要避免此行為，並使用已在 web.config 的驗證區段中指定的 URL，您可以新增名為 PreserveLoginUrl 的 appSetting，並將它設定為 true：</span><span class="sxs-lookup"><span data-stu-id="76900-298">To prevent this behavior and use the URL specified already in the authentication section of web.config, you can add an appSetting called PreserveLoginUrl and set it to true:</span></span> 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample13.xml)]
- <span data-ttu-id="76900-299">**嘗試安裝 ASP.NET MVC 4 以進行 Visual Studio 2010 和 Visual Web Developer 2010 的並存安裝時，NuGet 套件管理員無法安裝。**</span><span class="sxs-lookup"><span data-stu-id="76900-299">**The NuGet package manager fails to install when attempting to install ASP.NET MVC 4 for side by side installations of Visual Studio 2010 and Visual Web Developer 2010.**</span></span> <span data-ttu-id="76900-300">若要與 ASP.NET MVC 4 並存執行 Visual Studio 2010 和 Visual Web Developer 2010，您必須在兩個版本的 Visual Studio 都已安裝之後，安裝 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="76900-300">To run Visual Studio 2010 and Visual Web Developer 2010 side by side with ASP.NET MVC 4 you must install ASP.NET MVC 4 after both versions of Visual Studio have already been installed.</span></span>
- <span data-ttu-id="76900-301">**如果已卸載必要條件，卸載 ASP.NET MVC 4 會失敗。**</span><span class="sxs-lookup"><span data-stu-id="76900-301">**Uninstalling ASP.NET MVC 4 fails if prerequisites have already been uninstalled.**</span></span> <span data-ttu-id="76900-302">若要完全卸載 ASP.NET MVC 4you，必須先卸載 ASP.NET MVC 4，然後再卸載 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="76900-302">To cleanly uninstall ASP.NET MVC 4you must uninstall ASP.NET MVC 4 prior to uninstalling Visual Studio.</span></span>
- <span data-ttu-id="76900-303">**執行預設的 Web API 專案會顯示不正確地指示使用者使用 RegisterApis 方法（不存在）來新增路由的指示。**</span><span class="sxs-lookup"><span data-stu-id="76900-303">**Running a default Web API project shows instructions that incorrectly direct the user to add routes using the RegisterApis method, which doesn't exist.**</span></span> <span data-ttu-id="76900-304">您應該使用 ASP.NET 路由表，在 RegisterRoutes 方法中新增路由。</span><span class="sxs-lookup"><span data-stu-id="76900-304">Routes should be added in the RegisterRoutes method using the ASP.NET route table.</span></span>
- <span data-ttu-id="76900-305">**安裝 ASP.NET MVC 4 Beta 中斷 ASP.NET MVC 3 RTM 應用程式。**</span><span class="sxs-lookup"><span data-stu-id="76900-305">**Installing ASP.NET MVC 4 Beta breaks ASP.NET MVC 3 RTM applications.**</span></span> <span data-ttu-id="76900-306">ASP.NET 使用 RTM 版本建立的 MVC 3 應用程式（不含 ASP.NET MVC 3 工具更新版本）需要進行下列變更，才能與 ASP.NET MVC 4 Beta 並存使用。</span><span class="sxs-lookup"><span data-stu-id="76900-306">ASP.NET MVC 3 applications that were created with the RTM release (not with the ASP.NET MVC 3 Tools Update release) require the following changes in order to work side-by-side with ASP.NET MVC 4 Beta.</span></span> <span data-ttu-id="76900-307">建立專案而不進行這些更新，會導致編譯錯誤。</span><span class="sxs-lookup"><span data-stu-id="76900-307">Building the project without making these updates results in compilation errors.</span></span> 

    <span data-ttu-id="76900-308">**必要的更新**</span><span class="sxs-lookup"><span data-stu-id="76900-308">**Required updates**</span></span>

  1. <span data-ttu-id="76900-309">在根 web.config 檔案中，加入新的 *&lt;appSettings&gt;* 專案，其中包含主要*網頁： Version*和值*1.0.0.0*。</span><span class="sxs-lookup"><span data-stu-id="76900-309">In the root Web.config file, add a new *&lt;appSettings&gt;* entry with the key *webPages:Version* and the value *1.0.0.0*.</span></span>

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample14.xml)]
  2. <span data-ttu-id="76900-310">在方案總管中，以滑鼠右鍵按一下專案名稱，然後選取 [卸載專案]。</span><span class="sxs-lookup"><span data-stu-id="76900-310">In Solution Explorer, right-click the project name and then select Unload Project.</span></span> <span data-ttu-id="76900-311">然後再次以滑鼠右鍵按一下名稱，然後選取 [編輯*專案*名稱 .csproj]。</span><span class="sxs-lookup"><span data-stu-id="76900-311">Then right-click the name again and select Edit *ProjectName*.csproj.</span></span>
  3. <span data-ttu-id="76900-312">找出下列元件參考：</span><span class="sxs-lookup"><span data-stu-id="76900-312">Locate the following assembly references:</span></span> 

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample15.xml)]

      <span data-ttu-id="76900-313">將其取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="76900-313">Replace them with the following:</span></span>

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample16.xml)]
  4. <span data-ttu-id="76900-314">儲存變更，關閉您正在編輯的專案（.csproj）檔案，然後以滑鼠右鍵按一下專案，然後選取 [重載]。</span><span class="sxs-lookup"><span data-stu-id="76900-314">Save the changes, close the project (.csproj) file you were editing, and then right-click the project and select Reload.</span></span>
