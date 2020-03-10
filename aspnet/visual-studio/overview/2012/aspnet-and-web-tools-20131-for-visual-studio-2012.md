---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Visual Studio 2012 的 ASP.NET 和 Web 工具2013.1 版本資訊 |Microsoft Docs
author: microsoft
description: 本檔說明 Visual Studio 2012 的 ASP.NET 和 Web 工具2013.1 版本。
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 260af1018064d60d80cbb1002001f28c4daffffd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578439"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="ac432-103">適用於 Visual Studio 2012 的 ASP.NET 和 Web 工具 2013.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="ac432-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="ac432-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ac432-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="ac432-105">本檔說明 Visual Studio 2012 的 ASP.NET 和 Web 工具2013.1 版本。</span><span class="sxs-lookup"><span data-stu-id="ac432-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="ac432-106">內容</span><span class="sxs-lookup"><span data-stu-id="ac432-106">Contents</span></span>

- [<span data-ttu-id="ac432-107">安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="ac432-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="ac432-108">軟體需求</span><span class="sxs-lookup"><span data-stu-id="ac432-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="ac432-109">Visual Studio 2012 ASP.NET 和 Web 工具2013.1 的新功能</span><span class="sxs-lookup"><span data-stu-id="ac432-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="ac432-110">啟動程序</span><span class="sxs-lookup"><span data-stu-id="ac432-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="ac432-111">範本</span><span class="sxs-lookup"><span data-stu-id="ac432-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="ac432-112">ASP.NET MVC 5 範本</span><span class="sxs-lookup"><span data-stu-id="ac432-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="ac432-113">ASP.NET Web API 2 範本</span><span class="sxs-lookup"><span data-stu-id="ac432-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="ac432-114">專案範本</span><span class="sxs-lookup"><span data-stu-id="ac432-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="ac432-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="ac432-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="ac432-116">ASP.NET 的樣板</span><span class="sxs-lookup"><span data-stu-id="ac432-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="ac432-117">Razor 編輯器</span><span class="sxs-lookup"><span data-stu-id="ac432-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="ac432-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="ac432-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="ac432-119">已知問題和重大變更</span><span class="sxs-lookup"><span data-stu-id="ac432-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="ac432-120">ASP.NET 的樣板</span><span class="sxs-lookup"><span data-stu-id="ac432-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="ac432-121">MVC 和 Web API 架構-HTTP 404，找不到錯誤</span><span class="sxs-lookup"><span data-stu-id="ac432-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="ac432-122">Visual Studio Express 2012 for Web 會在新增 scaffold 專案後停止運作</span><span class="sxs-lookup"><span data-stu-id="ac432-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="ac432-123">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="ac432-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - <span data-ttu-id="ac432-124">[使用 [流覽] 或 F5 來查看 cshtml 檔案會導致伺服器錯誤](#browseissue)</span><span class="sxs-lookup"><span data-stu-id="ac432-124">[Viewing cshtml file with Browse With or F5 causes a server error](#browseissue)</span></span>
        - [<span data-ttu-id="ac432-125">Url 重寫和波狀符號（~）</span><span class="sxs-lookup"><span data-stu-id="ac432-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="ac432-126">範本</span><span class="sxs-lookup"><span data-stu-id="ac432-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="ac432-127">安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="ac432-127">Installation Notes</span></span>

<span data-ttu-id="ac432-128">[安裝](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids)適用于 Visual Studio 2012 的 ASP.NET 和 Web 工具2013.1。</span><span class="sxs-lookup"><span data-stu-id="ac432-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="ac432-129">軟體需求</span><span class="sxs-lookup"><span data-stu-id="ac432-129">Software Requirements</span></span>

<span data-ttu-id="ac432-130">您必須有 Visual Studio 2012 或 Visual Studio Express 2012 for Web。</span><span class="sxs-lookup"><span data-stu-id="ac432-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="ac432-131">Visual Studio 2012 ASP.NET 和 Web 工具2013.1 的新功能</span><span class="sxs-lookup"><span data-stu-id="ac432-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="ac432-132">從中</span><span class="sxs-lookup"><span data-stu-id="ac432-132">Bootstrap</span></span>

<span data-ttu-id="ac432-133">當您 scaffold MVC 5 控制器和 views 時，views 的標記會使用[啟動](http://getbootstrap.com/)程式。</span><span class="sxs-lookup"><span data-stu-id="ac432-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="ac432-134">範本</span><span class="sxs-lookup"><span data-stu-id="ac432-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="ac432-135">ASP.NET MVC 5 範本</span><span class="sxs-lookup"><span data-stu-id="ac432-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="ac432-136">我們已加入新的 MVC 5 範本。</span><span class="sxs-lookup"><span data-stu-id="ac432-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="ac432-137">它會參考最新的 MVC 5 NuGet 套件，您可以使用 [樣板] 來新增控制器和 views。</span><span class="sxs-lookup"><span data-stu-id="ac432-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="ac432-138">ASP.NET Web API 2 範本</span><span class="sxs-lookup"><span data-stu-id="ac432-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="ac432-139">我們已新增 Web API 2 範本。</span><span class="sxs-lookup"><span data-stu-id="ac432-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="ac432-140">它會參考最新的 Web API 2 NuGet 套件，您可以使用樣板來新增控制器和視圖。</span><span class="sxs-lookup"><span data-stu-id="ac432-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="ac432-141">項目範本</span><span class="sxs-lookup"><span data-stu-id="ac432-141">Item Templates</span></span>

<span data-ttu-id="ac432-142">我們新增了 MVC 5 views、Web Pages （Razor 3）和 Web API 2 控制器的新專案範本。</span><span class="sxs-lookup"><span data-stu-id="ac432-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="ac432-143">它們會在加入新專案時，將相關的 NuGet 套件安裝到專案。</span><span class="sxs-lookup"><span data-stu-id="ac432-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="ac432-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="ac432-144">Entity Framework 6</span></span>

<span data-ttu-id="ac432-145">當您使用 Entity Framework scaffold MVC 或 Web API 控制器時，我們會使用 Framework 6。</span><span class="sxs-lookup"><span data-stu-id="ac432-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="ac432-146">如需 Entity Framework 的詳細資訊，請參閱[Entity Framework 版本歷程記錄](https://msdn.com/data/jj574253)。</span><span class="sxs-lookup"><span data-stu-id="ac432-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="ac432-147">您也可以下載並安裝適用于 Visual Studio 2012 的 Entity Framework 6 工具。</span><span class="sxs-lookup"><span data-stu-id="ac432-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="ac432-148">請參閱[Get Entity Framework](https://msdn.com/data/ee712906#tooling)。</span><span class="sxs-lookup"><span data-stu-id="ac432-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="ac432-149">ASP.NET 的樣板</span><span class="sxs-lookup"><span data-stu-id="ac432-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="ac432-150">ASP.NET 樣板是用於 ASP.NET Web 應用程式的程式碼產生架構。</span><span class="sxs-lookup"><span data-stu-id="ac432-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="ac432-151">它可讓您輕鬆地將未定案程式碼加入至您的專案，以與資料模型互動。</span><span class="sxs-lookup"><span data-stu-id="ac432-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="ac432-152">在舊版的 Visual Studio 中，架構僅限於 ASP.NET MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="ac432-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="ac432-153">透過此更新，您現在可以使用任何 ASP.NET 專案的樣板，包括 Web Forms。</span><span class="sxs-lookup"><span data-stu-id="ac432-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="ac432-154">此更新不支援產生 Web form 專案的頁面，但您仍然可以將 MVC 相依性新增至專案，以使用具有 Web form 的樣板。</span><span class="sxs-lookup"><span data-stu-id="ac432-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="ac432-155">在未來的更新中，將會新增針對 Web form 產生網頁的支援。</span><span class="sxs-lookup"><span data-stu-id="ac432-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="ac432-156">使用 [樣板] 時，我們會確保專案中已安裝所有必要的相依性。</span><span class="sxs-lookup"><span data-stu-id="ac432-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="ac432-157">例如，如果您從 ASP.NET Web form 專案開始，然後使用樣板來新增 Web API 控制器，則會自動將所需的 NuGet 套件和參考新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="ac432-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="ac432-158">若要將 MVC 樣板加入至 Web form 專案，請加入**新的 Scaffold 專案**，然後在交談視窗中選取 [ **MVC 5**相依性]。</span><span class="sxs-lookup"><span data-stu-id="ac432-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="ac432-159">有兩個適用于樣板 MVC 的選項;最小和完整。</span><span class="sxs-lookup"><span data-stu-id="ac432-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="ac432-160">如果您選取 [最低]，則只會將 ASP.NET MVC 的 NuGet 套件和參考新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="ac432-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="ac432-161">如果您選取 [完整] 選項，則會加入最少的相依性，以及 MVC 專案所需的內容檔案。</span><span class="sxs-lookup"><span data-stu-id="ac432-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="ac432-162">支援架構的非同步控制器會使用 Entity Framework 6 的新異步功能。</span><span class="sxs-lookup"><span data-stu-id="ac432-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="ac432-163">如需詳細資訊和教學課程，請參閱 ASP.NET 架構的[總覽](../2013/aspnet-scaffolding-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ac432-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="ac432-164">這些教學課程會顯示具有 Visual Studio 2013 的樣板，但它們也適用于 Visual Studio 2012 的 ASP.NET 和 Web 工具2013.1。</span><span class="sxs-lookup"><span data-stu-id="ac432-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="ac432-165">Razor 編輯器</span><span class="sxs-lookup"><span data-stu-id="ac432-165">Razor Editor</span></span>

<span data-ttu-id="ac432-166">在此更新中，Visual Studio 2012 現在支援 Razor 3 工具/編輯。</span><span class="sxs-lookup"><span data-stu-id="ac432-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="ac432-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="ac432-167">NuGet 2.7</span></span>

<span data-ttu-id="ac432-168">NuGet 2.7 包含一組豐富的新功能，在[NuGet 2.7 版本](http://docs.nuget.org/docs/release-notes/nuget-2.7)資訊中有詳細的說明。</span><span class="sxs-lookup"><span data-stu-id="ac432-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="ac432-169">此版本的 NuGet 不需要使用者明確允許 NuGet 還原遺失的套件。</span><span class="sxs-lookup"><span data-stu-id="ac432-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="ac432-170">安裝 NuGet 2.7 時，使用者會隱含地同意自動還原遺失的套件。</span><span class="sxs-lookup"><span data-stu-id="ac432-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="ac432-171">使用者可以透過 Visual Studio 中的 NuGet 設定明確選擇不進行套件還原。</span><span class="sxs-lookup"><span data-stu-id="ac432-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="ac432-172">這種變更可簡化封裝還原的運作方式。</span><span class="sxs-lookup"><span data-stu-id="ac432-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="ac432-173">已知問題和重大變更</span><span class="sxs-lookup"><span data-stu-id="ac432-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="ac432-174">ASP.NET 的樣板</span><span class="sxs-lookup"><span data-stu-id="ac432-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="ac432-175">MVC 和 Web API 架構-HTTP 404，找不到錯誤</span><span class="sxs-lookup"><span data-stu-id="ac432-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="ac432-176">如果您在將 scaffold 專案新增至專案時遇到錯誤，您的專案可能會處於不一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="ac432-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="ac432-177">所做的部分變更會復原，但其他變更（例如已安裝的 NuGet 套件）將不會復原。</span><span class="sxs-lookup"><span data-stu-id="ac432-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="ac432-178">如果復原路由設定變更，使用者在流覽至 scaffold 專案時，會收到 HTTP 404 錯誤。</span><span class="sxs-lookup"><span data-stu-id="ac432-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="ac432-179">若要修正 MVC 的這個錯誤，請加入新的 scaffold 專案，然後選取 [MVC 5 相依性] （最小或完整）。</span><span class="sxs-lookup"><span data-stu-id="ac432-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="ac432-180">此程式會將所有必要的變更新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="ac432-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="ac432-181">若要修正 Web API 的這個錯誤：</span><span class="sxs-lookup"><span data-stu-id="ac432-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="ac432-182">將下列 WebApiConfig 類別新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="ac432-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="ac432-183">依照下列方式，在 WebApiConfig 中註冊應用程式\_Start 方法：</span><span class="sxs-lookup"><span data-stu-id="ac432-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="ac432-184">Visual Studio Express 2012 for Web 會在新增 scaffold 專案後停止運作</span><span class="sxs-lookup"><span data-stu-id="ac432-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="ac432-185">如果 Visual Studio Express 2012 for Web 會在使用 Entity Framework 新增 scaffold 專案後停止運作（例如具有動作的 Web API 2 控制器，使用 Entity Framework），可能是 Visual Studio Express 無法載入元件的原生映射。相依于 System.web. Extensions。</span><span class="sxs-lookup"><span data-stu-id="ac432-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="ac432-186">若要更正此問題，請將 Visual Studio Express 設定為使用 System.web 副檔名的 MSIL 映射：</span><span class="sxs-lookup"><span data-stu-id="ac432-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="ac432-187">在系統管理員模式中開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="ac432-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="ac432-188">前往%ProgramFiles%\Microsoft Visual Studio 11.0 \ Common7\IDE 或% ProgramFiles （x86）% \ Microsoft Visual Studio 11.0 \ Common7\IDE （適用于64位 Windows）。</span><span class="sxs-lookup"><span data-stu-id="ac432-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="ac432-189">在文字編輯器中開啟 VWDExpress。</span><span class="sxs-lookup"><span data-stu-id="ac432-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="ac432-190">在 &lt;設定&gt;/&lt;執行時間&gt; 元素底下新增下列程式程式碼：</span><span class="sxs-lookup"><span data-stu-id="ac432-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="ac432-191">重新開機 Web 的 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="ac432-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="ac432-192">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="ac432-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="ac432-193">使用 [流覽] 或 F5 來查看 cshtml 檔案會導致伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="ac432-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="ac432-194">當您在 Visual Studio 2012 中建立 MVC 5 專案時（或在 Visual Studio 2012 中開啟以 Visual Studio 2013 建立的 MVC 5 專案）並嘗試使用 [流覽方式] 或 F5 來查看 cshtml 檔案時，您會收到錯誤訊息，指出 **'/' 應用程式中的伺服器錯誤**。</span><span class="sxs-lookup"><span data-stu-id="ac432-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="ac432-195">伺服器嘗試流覽至 `http://localhost:XXXX/Views/../XXXX.cshtml`</span><span class="sxs-lookup"><span data-stu-id="ac432-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="ac432-196">若要解決此問題，請將專案中的 [**起始動作**] 設定變更為 [**特定頁面**]。</span><span class="sxs-lookup"><span data-stu-id="ac432-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="ac432-197">您不需要提供頁面的值。</span><span class="sxs-lookup"><span data-stu-id="ac432-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="ac432-198">進行這項變更之後，選取 [F5] 以流覽至您應用程式的根目錄（`http://localhost:XXXX`）。</span><span class="sxs-lookup"><span data-stu-id="ac432-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="ac432-199">這個行為與 Visual Studio 2013 中的 MVC 5 專案行為不同，因為**目前的頁面**設定會啟動開啟的頁面。</span><span class="sxs-lookup"><span data-stu-id="ac432-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="ac432-200">Url 重寫和波狀符號（~）</span><span class="sxs-lookup"><span data-stu-id="ac432-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="ac432-201">升級至 ASP.NET Razor 3 或 ASP.NET MVC 5 之後，如果您使用 URL 重寫，波狀符號（~）標記法可能無法再正常運作。</span><span class="sxs-lookup"><span data-stu-id="ac432-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="ac432-202">URL 重寫會影響 HTML 專案中的波狀符號（~）標記法（例如 &lt;A/&gt;、&lt;SCRIPT/&gt;、&lt;LINK/&gt;），因此波狀波不會再對應到根目錄。</span><span class="sxs-lookup"><span data-stu-id="ac432-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="ac432-203">例如，如果您將**asp.net/content**的要求重寫為**asp.net**，&lt;href = "~/content/"/&gt; 的 href 屬性會解析為 **/content/content/** ，而不是 **/** 。</span><span class="sxs-lookup"><span data-stu-id="ac432-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="ac432-204">若要抑制這項變更，您可以在每個網頁或 global.asax 的**應用程式\_BeginRequest**中，將**IIS\_WasUrlRewritten**內容設定為 false。</span><span class="sxs-lookup"><span data-stu-id="ac432-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="ac432-205">範本</span><span class="sxs-lookup"><span data-stu-id="ac432-205">Templates</span></span>

<span data-ttu-id="ac432-206">當您在 Windows 8.1 或 Windows Server 2012 R2 上建立具有 Visual Studio 2012 的 ASP.NET MVC 專案時，Visual Studio 會顯示錯誤訊息，指出「設定 Web [url] ASP.NET 4.5 失敗」。</span><span class="sxs-lookup"><span data-stu-id="ac432-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![設定錯誤](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="ac432-208">您會看到此錯誤，因為 Visual Studio 2012 不會在安裝于這些 Windows 版本時啟用 ASP.NET 4.5 功能。</span><span class="sxs-lookup"><span data-stu-id="ac432-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="ac432-209">若要啟用 ASP.NET 4.5，請執行 [[開啟或關閉 Windows 功能](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)] 中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="ac432-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![開啟或關閉 Windows 功能](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="ac432-211">或者，您可以透過命令列啟用 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="ac432-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="ac432-212">在系統管理員模式中開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="ac432-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="ac432-213">執行下列命令以啟用 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="ac432-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
