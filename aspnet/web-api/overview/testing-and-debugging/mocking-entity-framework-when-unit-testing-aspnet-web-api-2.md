---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: 當單元測試 ASP.NET Web API 2 時模擬 Entity Framework |Microsoft Docs
author: Rick-Anderson
description: 本指引和應用程式示範如何為使用 Entity Framework 的 Web API 2 應用程式建立單元測試。 它會顯示如何修改 。
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555087"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a><span data-ttu-id="f29be-104">單元測試 ASP.NET Web API 2 時的模擬 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="f29be-104">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="f29be-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f29be-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="f29be-106">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="f29be-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="f29be-107">本指引和應用程式示範如何為使用 Entity Framework 的 Web API 2 應用程式建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="f29be-107">This guidance and application demonstrate how to create unit tests for your Web API 2 application that uses the Entity Framework.</span></span> <span data-ttu-id="f29be-108">它會顯示如何修改 scaffold 控制器，以啟用傳遞內容物件進行測試，以及如何建立可與 Entity Framework 搭配使用的測試物件。</span><span class="sxs-lookup"><span data-stu-id="f29be-108">It shows how to modify the scaffolded controller to enable passing a context object for testing, and how to create test objects that work with Entity Framework.</span></span>
>
> <span data-ttu-id="f29be-109">如需使用 ASP.NET Web API 進行單元測試的簡介，請參閱[使用 ASP.NET Web API 2 進行單元測試](unit-testing-with-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="f29be-109">For an introduction to unit testing with ASP.NET Web API, see [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md).</span></span>
>
> <span data-ttu-id="f29be-110">本教學課程假設您已熟悉 ASP.NET Web API 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="f29be-110">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="f29be-111">如需入門教學課程，請參閱[使用 ASP.NET Web API 2 的消費者入門](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="f29be-111">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f29be-112">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="f29be-112">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="f29be-113">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f29be-113">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="f29be-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="f29be-114">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="f29be-115">本主題內容</span><span class="sxs-lookup"><span data-stu-id="f29be-115">In this topic</span></span>

<span data-ttu-id="f29be-116">本主題包含下列各節：</span><span class="sxs-lookup"><span data-stu-id="f29be-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="f29be-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="f29be-117">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="f29be-118">下載程式代碼</span><span class="sxs-lookup"><span data-stu-id="f29be-118">Download code</span></span>](#download)
- [<span data-ttu-id="f29be-119">使用單元測試專案建立應用程式</span><span class="sxs-lookup"><span data-stu-id="f29be-119">Create application with unit test project</span></span>](#appwithunittest)
- [<span data-ttu-id="f29be-120">建立模型類別</span><span class="sxs-lookup"><span data-stu-id="f29be-120">Create the model class</span></span>](#modelclass)
- [<span data-ttu-id="f29be-121">新增控制器</span><span class="sxs-lookup"><span data-stu-id="f29be-121">Add the controller</span></span>](#controller)
- [<span data-ttu-id="f29be-122">新增相依性插入</span><span class="sxs-lookup"><span data-stu-id="f29be-122">Add dependency injection</span></span>](#dependency)
- [<span data-ttu-id="f29be-123">在測試專案中安裝 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="f29be-123">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="f29be-124">建立測試內容</span><span class="sxs-lookup"><span data-stu-id="f29be-124">Create test context</span></span>](#testcontext)
- [<span data-ttu-id="f29be-125">建立測試</span><span class="sxs-lookup"><span data-stu-id="f29be-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="f29be-126">執行測試</span><span class="sxs-lookup"><span data-stu-id="f29be-126">Run tests</span></span>](#runtests)

<span data-ttu-id="f29be-127">如果您已完成[使用 ASP.NET Web API 2 進行單元測試](unit-testing-with-aspnet-web-api.md)中的步驟，您可以跳至[新增控制器](#controller)一節。</span><span class="sxs-lookup"><span data-stu-id="f29be-127">If you have already completed the steps in [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), you can skip to the section [Add the controller](#controller).</span></span>

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="f29be-128">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f29be-128">Prerequisites</span></span>

<span data-ttu-id="f29be-129">Visual Studio 2017 的社區、Professional 或 Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="f29be-129">Visual Studio 2017 Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="f29be-130">下載程式碼</span><span class="sxs-lookup"><span data-stu-id="f29be-130">Download code</span></span>

<span data-ttu-id="f29be-131">下載[已完成的專案](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)。</span><span class="sxs-lookup"><span data-stu-id="f29be-131">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="f29be-132">可下載的專案包含本主題的單元測試程式碼和[單元測試 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)主題。</span><span class="sxs-lookup"><span data-stu-id="f29be-132">The downloadable project includes unit test code for this topic and for the [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="f29be-133">使用單元測試專案建立應用程式</span><span class="sxs-lookup"><span data-stu-id="f29be-133">Create application with unit test project</span></span>

<span data-ttu-id="f29be-134">建立應用程式或將單元測試專案加入至現有的應用程式時，您可以建立單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="f29be-134">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="f29be-135">本教學課程會示範如何在建立應用程式時建立單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="f29be-135">This tutorial shows creating a unit test project when creating the application.</span></span>

<span data-ttu-id="f29be-136">建立名為**StoreApp**的新 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f29be-136">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

<span data-ttu-id="f29be-137">在 [新增 ASP.NET 專案] 視窗中，選取 [**空白**] 範本，並新增 Web API 的 [資料夾] 和 [核心參考]。</span><span class="sxs-lookup"><span data-stu-id="f29be-137">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="f29be-138">選取 [**加入單元測試**] 選項。</span><span class="sxs-lookup"><span data-stu-id="f29be-138">Select the **Add unit tests** option.</span></span> <span data-ttu-id="f29be-139">單元測試專案會自動命名為**StoreApp**。</span><span class="sxs-lookup"><span data-stu-id="f29be-139">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="f29be-140">您可以保留此名稱。</span><span class="sxs-lookup"><span data-stu-id="f29be-140">You can keep this name.</span></span>

![建立單元測試專案](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

<span data-ttu-id="f29be-142">建立應用程式之後，您會看到它包含兩個專案- **StoreApp**和**StoreApp。測試**。</span><span class="sxs-lookup"><span data-stu-id="f29be-142">After creating the application, you will see it contains two projects - **StoreApp** and **StoreApp.Tests**.</span></span>

<a id="modelclass"></a>
## <a name="create-the-model-class"></a><span data-ttu-id="f29be-143">建立模型類別</span><span class="sxs-lookup"><span data-stu-id="f29be-143">Create the model class</span></span>

<span data-ttu-id="f29be-144">在您的 StoreApp 專案中，將類別檔案新增至名為**Product.cs**的 [**模型**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f29be-144">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="f29be-145">以下列程式碼取代檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="f29be-145">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

<span data-ttu-id="f29be-146">建置方案。</span><span class="sxs-lookup"><span data-stu-id="f29be-146">Build the solution.</span></span>

<a id="controller"></a>
## <a name="add-the-controller"></a><span data-ttu-id="f29be-147">新增控制器</span><span class="sxs-lookup"><span data-stu-id="f29be-147">Add the controller</span></span>

<span data-ttu-id="f29be-148">以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [**加入**] 和 [**新增 scaffold 專案**]。</span><span class="sxs-lookup"><span data-stu-id="f29be-148">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="f29be-149">使用 [Entity Framework] 選取 [具有動作的 Web API 2 控制器]。</span><span class="sxs-lookup"><span data-stu-id="f29be-149">Select Web API 2 Controller with actions, using Entity Framework.</span></span>

![加入新的控制器](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

<span data-ttu-id="f29be-151">設定下列的值：</span><span class="sxs-lookup"><span data-stu-id="f29be-151">Set the following values:</span></span>

- <span data-ttu-id="f29be-152">控制器名稱： **ProductController**</span><span class="sxs-lookup"><span data-stu-id="f29be-152">Controller name: **ProductController**</span></span>
- <span data-ttu-id="f29be-153">模型類別：**產品**</span><span class="sxs-lookup"><span data-stu-id="f29be-153">Model class: **Product**</span></span>
- <span data-ttu-id="f29be-154">資料內容類別： [選取**新的資料內容**] 按鈕，它會填入下列所示的值。</span><span class="sxs-lookup"><span data-stu-id="f29be-154">Data context class: [Select **New data context** button which fills in the values seen below]</span></span>

![指定控制器](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

<span data-ttu-id="f29be-156">按一下 [**新增**]，以自動產生的程式碼建立控制器。</span><span class="sxs-lookup"><span data-stu-id="f29be-156">Click **Add** to create the controller with automatically-generated code.</span></span> <span data-ttu-id="f29be-157">此程式碼包含用來建立、抓取、更新及刪除 Product 類別實例的方法。</span><span class="sxs-lookup"><span data-stu-id="f29be-157">The code includes methods for creating, retrieving, updating and deleting instances of the Product class.</span></span> <span data-ttu-id="f29be-158">下列程式碼顯示新增產品的方法。</span><span class="sxs-lookup"><span data-stu-id="f29be-158">The following code shows the method for add a Product.</span></span> <span data-ttu-id="f29be-159">請注意，方法會傳回**應傳回 iHTTPactionresult**的實例。</span><span class="sxs-lookup"><span data-stu-id="f29be-159">Notice that the method returns an instance of **IHttpActionResult**.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

<span data-ttu-id="f29be-160">應傳回 iHTTPactionresult 是 Web API 2 中的其中一項新功能，可簡化單元測試的開發。</span><span class="sxs-lookup"><span data-stu-id="f29be-160">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span>

<span data-ttu-id="f29be-161">在下一節中，您將自訂產生的程式碼，以加速將測試物件傳遞至控制器。</span><span class="sxs-lookup"><span data-stu-id="f29be-161">In the next section, you will customize the generated code to facilitate passing test objects to the controller.</span></span>

<a id="dependency"></a>
## <a name="add-dependency-injection"></a><span data-ttu-id="f29be-162">新增相依性插入</span><span class="sxs-lookup"><span data-stu-id="f29be-162">Add dependency injection</span></span>

<span data-ttu-id="f29be-163">目前，ProductController 類別已硬式編碼，可使用 StoreAppCoNtext 類別的實例。</span><span class="sxs-lookup"><span data-stu-id="f29be-163">Currently, the ProductController class is hard-coded to use an instance of the StoreAppContext class.</span></span> <span data-ttu-id="f29be-164">您將使用稱為「相依性插入」的模式來修改您的應用程式，並移除該硬式編碼的相依性。</span><span class="sxs-lookup"><span data-stu-id="f29be-164">You will use a pattern called dependency injection to modify your application and remove that hard-coded dependency.</span></span> <span data-ttu-id="f29be-165">藉由中斷此相依性，您可以在測試時傳入 mock 物件。</span><span class="sxs-lookup"><span data-stu-id="f29be-165">By breaking this dependency, you can pass in a mock object when testing.</span></span>

<span data-ttu-id="f29be-166">以滑鼠右鍵按一下 [**模型**] 資料夾，然後新增名為**IStoreAppCoNtext**的新介面。</span><span class="sxs-lookup"><span data-stu-id="f29be-166">Right-click the **Models** folder, and add a new interface named **IStoreAppContext**.</span></span>

<span data-ttu-id="f29be-167">使用下列程式碼取代程式碼。</span><span class="sxs-lookup"><span data-stu-id="f29be-167">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

<span data-ttu-id="f29be-168">開啟 StoreAppCoNtext.cs 檔案，並進行下列反白顯示的變更。</span><span class="sxs-lookup"><span data-stu-id="f29be-168">Open the StoreAppContext.cs file and make the following highlighted changes.</span></span> <span data-ttu-id="f29be-169">要注意的重要變更包括：</span><span class="sxs-lookup"><span data-stu-id="f29be-169">The important changes to note are:</span></span>

- <span data-ttu-id="f29be-170">StoreAppCoNtext 類別會實 IStoreAppCoNtext 介面</span><span class="sxs-lookup"><span data-stu-id="f29be-170">StoreAppContext class implements IStoreAppContext interface</span></span>
- <span data-ttu-id="f29be-171">MarkAsModified 方法已實作為</span><span class="sxs-lookup"><span data-stu-id="f29be-171">MarkAsModified method is implemented</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

<span data-ttu-id="f29be-172">開啟 ProductController.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="f29be-172">Open the ProductController.cs file.</span></span> <span data-ttu-id="f29be-173">變更現有的程式碼，以符合反白顯示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f29be-173">Change the existing code to match the highlighted code.</span></span> <span data-ttu-id="f29be-174">這些變更會中斷對 StoreAppCoNtext 的相依性，並讓其他類別針對內容類別傳入不同的物件。</span><span class="sxs-lookup"><span data-stu-id="f29be-174">These changes break the dependency on StoreAppContext and enable other classes to pass in a different object for the context class.</span></span> <span data-ttu-id="f29be-175">這項變更可讓您在單元測試期間傳入測試內容。</span><span class="sxs-lookup"><span data-stu-id="f29be-175">This change will enable you to pass in a test context during unit tests.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

<span data-ttu-id="f29be-176">您必須在 ProductController 中進行一項變更。</span><span class="sxs-lookup"><span data-stu-id="f29be-176">There is one more change you must make in ProductController.</span></span> <span data-ttu-id="f29be-177">在**PutProduct**方法中，將設定實體狀態的程式程式碼取代為 MarkAsModified 方法的呼叫所修改的。</span><span class="sxs-lookup"><span data-stu-id="f29be-177">In the **PutProduct** method, replace the line that sets the entity state to modified with a call to the MarkAsModified method.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

<span data-ttu-id="f29be-178">建置方案。</span><span class="sxs-lookup"><span data-stu-id="f29be-178">Build the solution.</span></span>

<span data-ttu-id="f29be-179">您現在已準備好設定測試專案。</span><span class="sxs-lookup"><span data-stu-id="f29be-179">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="f29be-180">在測試專案中安裝 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="f29be-180">Install NuGet packages in test project</span></span>

<span data-ttu-id="f29be-181">當您使用空白範本來建立應用程式時，單元測試專案（StoreApp）不會包含任何已安裝的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="f29be-181">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="f29be-182">其他範本，例如 Web API 範本，則會在單元測試專案中包含一些 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="f29be-182">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="f29be-183">在本教學課程中，您必須將 Entity Framework 封裝和 Microsoft ASP.NET Web API 2 核心套件加入至測試專案。</span><span class="sxs-lookup"><span data-stu-id="f29be-183">For this tutorial, you must include the Entity Framework package and the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="f29be-184">以滑鼠右鍵按一下 [StoreApp] 專案，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="f29be-184">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="f29be-185">您必須選取 [StoreApp] 專案，才能將封裝加入至該專案。</span><span class="sxs-lookup"><span data-stu-id="f29be-185">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![管理封裝](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

<span data-ttu-id="f29be-187">從線上套件，尋找並安裝 EntityFramework 套件（6.0 版或更新版本）。</span><span class="sxs-lookup"><span data-stu-id="f29be-187">From the Online packages, find and install the EntityFramework package (version 6.0 or later).</span></span> <span data-ttu-id="f29be-188">如果已安裝 EntityFramework 封裝，您可能已選取 [StoreApp] 專案，而不是 [StoreApp] 專案。</span><span class="sxs-lookup"><span data-stu-id="f29be-188">If it appears that the EntityFramework package is already installed, you may have selected the StoreApp project instead of the StoreApp.Tests project.</span></span>

![新增 Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

<span data-ttu-id="f29be-190">尋找並安裝 Microsoft ASP.NET Web API 2 核心套件。</span><span class="sxs-lookup"><span data-stu-id="f29be-190">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![安裝 web api 核心套件](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

<span data-ttu-id="f29be-192">關閉 [管理 NuGet 封裝] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f29be-192">Close the Manage NuGet Packages window.</span></span>

<a id="testcontext"></a>
## <a name="create-test-context"></a><span data-ttu-id="f29be-193">建立測試內容</span><span class="sxs-lookup"><span data-stu-id="f29be-193">Create test context</span></span>

<span data-ttu-id="f29be-194">將名為**TestDbSet**的類別加入至測試專案。</span><span class="sxs-lookup"><span data-stu-id="f29be-194">Add a class named **TestDbSet** to the test project.</span></span> <span data-ttu-id="f29be-195">這個類別會作為測試資料集的基類。</span><span class="sxs-lookup"><span data-stu-id="f29be-195">This class serves as the base class for your test data set.</span></span> <span data-ttu-id="f29be-196">使用下列程式碼取代程式碼。</span><span class="sxs-lookup"><span data-stu-id="f29be-196">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

<span data-ttu-id="f29be-197">將名為**TestProductDbSet**的類別加入至包含下列程式碼的測試專案。</span><span class="sxs-lookup"><span data-stu-id="f29be-197">Add a class named **TestProductDbSet** to the test project which contains the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

<span data-ttu-id="f29be-198">新增名為**TestStoreAppCoNtext**的類別，並將現有的程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="f29be-198">Add a class named **TestStoreAppContext** and replace the existing code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="f29be-199">建立測試</span><span class="sxs-lookup"><span data-stu-id="f29be-199">Create tests</span></span>

<span data-ttu-id="f29be-200">根據預設，您的測試專案會包含名為**UnitTest1.cs**的空白測試檔案。</span><span class="sxs-lookup"><span data-stu-id="f29be-200">By default, your test project includes an empty test file named **UnitTest1.cs**.</span></span> <span data-ttu-id="f29be-201">此檔案會顯示您用來建立測試方法的屬性。</span><span class="sxs-lookup"><span data-stu-id="f29be-201">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="f29be-202">在本教學課程中，您可以刪除此檔案，因為您會加入新的測試類別。</span><span class="sxs-lookup"><span data-stu-id="f29be-202">For this tutorial, you can delete this file because you will add a new test class.</span></span>

<span data-ttu-id="f29be-203">將名為**TestProductController**的類別加入至測試專案。</span><span class="sxs-lookup"><span data-stu-id="f29be-203">Add a class named **TestProductController** to the test project.</span></span> <span data-ttu-id="f29be-204">使用下列程式碼取代程式碼。</span><span class="sxs-lookup"><span data-stu-id="f29be-204">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="f29be-205">執行測試</span><span class="sxs-lookup"><span data-stu-id="f29be-205">Run tests</span></span>

<span data-ttu-id="f29be-206">您現在已準備好執行測試。</span><span class="sxs-lookup"><span data-stu-id="f29be-206">You are now ready to run the tests.</span></span> <span data-ttu-id="f29be-207">所有以**TestMethod**屬性標記的方法都會進行測試。</span><span class="sxs-lookup"><span data-stu-id="f29be-207">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="f29be-208">從 [**測試**] 功能表項目執行測試。</span><span class="sxs-lookup"><span data-stu-id="f29be-208">From the **Test** menu item, run the tests.</span></span>

![執行測試](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

<span data-ttu-id="f29be-210">開啟 [**測試瀏覽器**] 視窗，並注意測試的結果。</span><span class="sxs-lookup"><span data-stu-id="f29be-210">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![測試結果](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
