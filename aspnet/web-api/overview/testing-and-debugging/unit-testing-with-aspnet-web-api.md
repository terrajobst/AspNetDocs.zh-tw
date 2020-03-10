---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: 單元測試 ASP.NET Web API 2 |Microsoft Docs
author: Rick-Anderson
description: 本指引和應用程式會示範如何為您的 Web API 2 應用程式建立簡單的單元測試。 本教學課程示範如何包含單元測試的 [proj] 。
ms.author: riande
ms.date: 06/05/2014
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f2d60b977475e048a3a74aabff4adc768ee22baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554968"
---
# <a name="unit-testing-aspnet-web-api-2"></a><span data-ttu-id="cd721-104">單元測試 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="cd721-104">Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="cd721-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="cd721-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="cd721-106">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="cd721-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="cd721-107">本指引和應用程式會示範如何為您的 Web API 2 應用程式建立簡單的單元測試。</span><span class="sxs-lookup"><span data-stu-id="cd721-107">This guidance and application demonstrate how to create simple unit tests for your Web API 2 application.</span></span> <span data-ttu-id="cd721-108">本教學課程會示範如何在您的方案中包含單元測試專案，以及撰寫可從控制器方法檢查傳回值的測試方法。</span><span class="sxs-lookup"><span data-stu-id="cd721-108">This tutorial shows how to include a unit test project in your solution, and write test methods that check the returned values from a controller method.</span></span>
>
> <span data-ttu-id="cd721-109">本教學課程假設您已熟悉 ASP.NET Web API 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="cd721-109">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="cd721-110">如需入門教學課程，請參閱[使用 ASP.NET Web API 2 的消費者入門](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="cd721-110">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> <span data-ttu-id="cd721-111">本主題中的單元測試會刻意限制為簡單的資料案例。</span><span class="sxs-lookup"><span data-stu-id="cd721-111">The unit tests in this topic are intentionally limited to simple data scenarios.</span></span> <span data-ttu-id="cd721-112">如需單元測試更先進的資料案例，請參閱[當單元測試 ASP.NET Web API 2 時的模擬 Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="cd721-112">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="cd721-113">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="cd721-113">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="cd721-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="cd721-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="cd721-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="cd721-115">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="cd721-116">本主題內容</span><span class="sxs-lookup"><span data-stu-id="cd721-116">In this topic</span></span>

<span data-ttu-id="cd721-117">本主題包含下列各節：</span><span class="sxs-lookup"><span data-stu-id="cd721-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="cd721-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="cd721-118">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="cd721-119">下載程式代碼</span><span class="sxs-lookup"><span data-stu-id="cd721-119">Download code</span></span>](#download)
- [<span data-ttu-id="cd721-120">使用單元測試專案建立應用程式</span><span class="sxs-lookup"><span data-stu-id="cd721-120">Create application with unit test project</span></span>](#appwithunittest)
    - [<span data-ttu-id="cd721-121">建立應用程式時加入單元測試專案</span><span class="sxs-lookup"><span data-stu-id="cd721-121">Add unit test project when creating the application</span></span>](#whencreate)
    - [<span data-ttu-id="cd721-122">將單元測試專案加入至現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="cd721-122">Add unit test project to an existing application</span></span>](#addtoexisting)
- [<span data-ttu-id="cd721-123">設定 Web API 2 應用程式</span><span class="sxs-lookup"><span data-stu-id="cd721-123">Set up the Web API 2 application</span></span>](#setupproject)
- [<span data-ttu-id="cd721-124">在測試專案中安裝 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="cd721-124">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="cd721-125">建立測試</span><span class="sxs-lookup"><span data-stu-id="cd721-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="cd721-126">執行測試</span><span class="sxs-lookup"><span data-stu-id="cd721-126">Run tests</span></span>](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="cd721-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cd721-127">Prerequisites</span></span>

<span data-ttu-id="cd721-128">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)社區、Professional 或 Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="cd721-128">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="cd721-129">下載程式碼</span><span class="sxs-lookup"><span data-stu-id="cd721-129">Download code</span></span>

<span data-ttu-id="cd721-130">下載[已完成的專案](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)。</span><span class="sxs-lookup"><span data-stu-id="cd721-130">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="cd721-131">可下載的專案包含本主題的單元測試程式碼，以及[單元測試 ASP.NET Web API 主題時的模擬 Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) 。</span><span class="sxs-lookup"><span data-stu-id="cd721-131">The downloadable project includes unit test code for this topic and for the [Mocking Entity Framework when Unit Testing ASP.NET Web API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="cd721-132">使用單元測試專案建立應用程式</span><span class="sxs-lookup"><span data-stu-id="cd721-132">Create application with unit test project</span></span>

<span data-ttu-id="cd721-133">建立應用程式或將單元測試專案加入至現有的應用程式時，您可以建立單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="cd721-133">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="cd721-134">本教學課程會顯示兩種建立單元測試專案的方法。</span><span class="sxs-lookup"><span data-stu-id="cd721-134">This tutorial shows both methods for creating a unit test project.</span></span> <span data-ttu-id="cd721-135">若要遵循本教學課程，您可以使用任一種方法。</span><span class="sxs-lookup"><span data-stu-id="cd721-135">To follow this tutorial, you can use either approach.</span></span>

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a><span data-ttu-id="cd721-136">建立應用程式時加入單元測試專案</span><span class="sxs-lookup"><span data-stu-id="cd721-136">Add unit test project when creating the application</span></span>

<span data-ttu-id="cd721-137">建立名為**StoreApp**的新 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd721-137">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

![建立專案](unit-testing-with-aspnet-web-api/_static/image1.png)

<span data-ttu-id="cd721-139">在 [新增 ASP.NET 專案] 視窗中，選取 [**空白**] 範本，並新增 Web API 的 [資料夾] 和 [核心參考]。</span><span class="sxs-lookup"><span data-stu-id="cd721-139">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="cd721-140">選取 [**加入單元測試**] 選項。</span><span class="sxs-lookup"><span data-stu-id="cd721-140">Select the **Add unit tests** option.</span></span> <span data-ttu-id="cd721-141">單元測試專案會自動命名為**StoreApp**。</span><span class="sxs-lookup"><span data-stu-id="cd721-141">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="cd721-142">您可以保留此名稱。</span><span class="sxs-lookup"><span data-stu-id="cd721-142">You can keep this name.</span></span>

![建立單元測試專案](unit-testing-with-aspnet-web-api/_static/image2.png)

<span data-ttu-id="cd721-144">建立應用程式之後，您會看到它包含兩個專案。</span><span class="sxs-lookup"><span data-stu-id="cd721-144">After creating the application, you will see it contains two projects.</span></span>

![兩個專案](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a><span data-ttu-id="cd721-146">將單元測試專案加入至現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="cd721-146">Add unit test project to an existing application</span></span>

<span data-ttu-id="cd721-147">如果您在建立應用程式時沒有建立單元測試專案，您可以隨時加入一個。</span><span class="sxs-lookup"><span data-stu-id="cd721-147">If you did not create the unit test project when you created your application, you can add one at any time.</span></span> <span data-ttu-id="cd721-148">例如，假設您已經有一個名為 StoreApp 的應用程式，而且您想要加入單元測試。</span><span class="sxs-lookup"><span data-stu-id="cd721-148">For example, suppose you already have an application named StoreApp, and you want to add unit tests.</span></span> <span data-ttu-id="cd721-149">若要加入單元測試專案，請以滑鼠右鍵按一下您的方案，然後選取 [**加入**] 和 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="cd721-149">To add a unit test project, right-click your solution and select **Add** and **New Project**.</span></span>

![將新專案新增至方案](unit-testing-with-aspnet-web-api/_static/image4.png)

<span data-ttu-id="cd721-151">在左窗格中選取 [**測試**]，然後選取專案類型的 [**單元測試專案**]。</span><span class="sxs-lookup"><span data-stu-id="cd721-151">Select **Test** in the left pane, and select **Unit Test Project** for the project type.</span></span> <span data-ttu-id="cd721-152">將專案命名為**StoreApp**。</span><span class="sxs-lookup"><span data-stu-id="cd721-152">Name the project **StoreApp.Tests**.</span></span>

![加入單元測試專案](unit-testing-with-aspnet-web-api/_static/image5.png)

<span data-ttu-id="cd721-154">您會在方案中看到單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="cd721-154">You will see the unit test project in your solution.</span></span>

<span data-ttu-id="cd721-155">在單元測試專案中，將專案參考加入至原始專案。</span><span class="sxs-lookup"><span data-stu-id="cd721-155">In the unit test project, add a project reference to the original project.</span></span>

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a><span data-ttu-id="cd721-156">設定 Web API 2 應用程式</span><span class="sxs-lookup"><span data-stu-id="cd721-156">Set up the Web API 2 application</span></span>

<span data-ttu-id="cd721-157">在您的 StoreApp 專案中，將類別檔案新增至名為**Product.cs**的 [**模型**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="cd721-157">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="cd721-158">以下列程式碼取代檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="cd721-158">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="cd721-159">建置方案。</span><span class="sxs-lookup"><span data-stu-id="cd721-159">Build the solution.</span></span>

<span data-ttu-id="cd721-160">以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [**加入**] 和 [**新增 scaffold 專案**]。</span><span class="sxs-lookup"><span data-stu-id="cd721-160">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="cd721-161">選取 [ **WEB API 2 控制器-空白**]。</span><span class="sxs-lookup"><span data-stu-id="cd721-161">Select **Web API 2 Controller - Empty**.</span></span>

![加入新的控制器](unit-testing-with-aspnet-web-api/_static/image6.png)

<span data-ttu-id="cd721-163">將控制器名稱設定為**SimpleProductController**，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="cd721-163">Set the controller name to **SimpleProductController**, and click **Add**.</span></span>

![指定控制器](unit-testing-with-aspnet-web-api/_static/image7.png)

<span data-ttu-id="cd721-165">將現有的程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="cd721-165">Replace the existing code with the following code.</span></span> <span data-ttu-id="cd721-166">為了簡化此範例，資料會儲存在清單中，而不是資料庫中。</span><span class="sxs-lookup"><span data-stu-id="cd721-166">To simplify this example, the data is stored in a list rather than a database.</span></span> <span data-ttu-id="cd721-167">此類別中定義的清單代表生產資料。</span><span class="sxs-lookup"><span data-stu-id="cd721-167">The list defined in this class represents the production data.</span></span> <span data-ttu-id="cd721-168">請注意，控制器包含一個可接受產品物件清單做為參數的函式。</span><span class="sxs-lookup"><span data-stu-id="cd721-168">Notice that the controller includes a constructor that takes as a parameter a list of Product objects.</span></span> <span data-ttu-id="cd721-169">這個函數可讓您在單元測試時傳遞測試資料。</span><span class="sxs-lookup"><span data-stu-id="cd721-169">This constructor enables you to pass test data when unit testing.</span></span> <span data-ttu-id="cd721-170">控制器也包含兩個**非同步**方法，以說明單元測試的非同步方法。</span><span class="sxs-lookup"><span data-stu-id="cd721-170">The controller also includes two **async** methods to illustrate unit testing asynchronous methods.</span></span> <span data-ttu-id="cd721-171">這些非同步方法的執行方式是呼叫**system.threading.tasks.task.fromresult**來將無關的程式碼降到最低，但通常方法會包含需要大量資源的作業。</span><span class="sxs-lookup"><span data-stu-id="cd721-171">These async methods were implemented by calling **Task.FromResult** to minimize extraneous code, but normally the methods would include resource-intensive operations.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="cd721-172">GetProduct 方法會傳回**應傳回 iHTTPactionresult**介面的實例。</span><span class="sxs-lookup"><span data-stu-id="cd721-172">The GetProduct method returns an instance of the **IHttpActionResult** interface.</span></span> <span data-ttu-id="cd721-173">應傳回 iHTTPactionresult 是 Web API 2 中的其中一項新功能，可簡化單元測試的開發。</span><span class="sxs-lookup"><span data-stu-id="cd721-173">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span> <span data-ttu-id="cd721-174">實應傳回 iHTTPactionresult 介面的類別可在[system.web. HTTP.sys](https://msdn.microsoft.com/library/system.web.http.results.aspx)命名空間中找到。</span><span class="sxs-lookup"><span data-stu-id="cd721-174">Classes that implement the IHttpActionResult interface are found in the [System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) namespace.</span></span> <span data-ttu-id="cd721-175">這些類別代表動作要求的可能回應，並對應至 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="cd721-175">These classes represent possible responses from an action request, and they correspond to HTTP status codes.</span></span>

<span data-ttu-id="cd721-176">建置方案。</span><span class="sxs-lookup"><span data-stu-id="cd721-176">Build the solution.</span></span>

<span data-ttu-id="cd721-177">您現在已準備好設定測試專案。</span><span class="sxs-lookup"><span data-stu-id="cd721-177">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="cd721-178">在測試專案中安裝 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="cd721-178">Install NuGet packages in test project</span></span>

<span data-ttu-id="cd721-179">當您使用空白範本來建立應用程式時，單元測試專案（StoreApp）不會包含任何已安裝的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="cd721-179">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="cd721-180">其他範本，例如 Web API 範本，則會在單元測試專案中包含一些 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="cd721-180">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="cd721-181">在本教學課程中，您必須在測試專案中包含 Microsoft ASP.NET Web API 2 核心套件。</span><span class="sxs-lookup"><span data-stu-id="cd721-181">For this tutorial, you must include the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="cd721-182">以滑鼠右鍵按一下 [StoreApp] 專案，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="cd721-182">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="cd721-183">您必須選取 [StoreApp] 專案，才能將封裝加入至該專案。</span><span class="sxs-lookup"><span data-stu-id="cd721-183">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![管理封裝](unit-testing-with-aspnet-web-api/_static/image8.png)

<span data-ttu-id="cd721-185">尋找並安裝 Microsoft ASP.NET Web API 2 核心套件。</span><span class="sxs-lookup"><span data-stu-id="cd721-185">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![安裝 web api 核心套件](unit-testing-with-aspnet-web-api/_static/image9.png)

<span data-ttu-id="cd721-187">關閉 [管理 NuGet 封裝] 視窗。</span><span class="sxs-lookup"><span data-stu-id="cd721-187">Close the Manage NuGet Packages window.</span></span>

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="cd721-188">建立測試</span><span class="sxs-lookup"><span data-stu-id="cd721-188">Create tests</span></span>

<span data-ttu-id="cd721-189">根據預設，您的測試專案會包含名為 UnitTest1.cs 的空白測試檔案。</span><span class="sxs-lookup"><span data-stu-id="cd721-189">By default, your test project includes an empty test file named UnitTest1.cs.</span></span> <span data-ttu-id="cd721-190">此檔案會顯示您用來建立測試方法的屬性。</span><span class="sxs-lookup"><span data-stu-id="cd721-190">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="cd721-191">針對單元測試，您可以使用此檔案，或建立您自己的檔案。</span><span class="sxs-lookup"><span data-stu-id="cd721-191">For your unit tests, you can either use this file or create your own file.</span></span>

![Unittest1.cpp](unit-testing-with-aspnet-web-api/_static/image10.png)

<span data-ttu-id="cd721-193">在本教學課程中，您將建立自己的測試類別。</span><span class="sxs-lookup"><span data-stu-id="cd721-193">For this tutorial, you will create your own test class.</span></span> <span data-ttu-id="cd721-194">您可以刪除 UnitTest1.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="cd721-194">You can delete the UnitTest1.cs file.</span></span> <span data-ttu-id="cd721-195">新增名為**TestSimpleProductController.cs**的類別，並將程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="cd721-195">Add a class named **TestSimpleProductController.cs**, and replace the code with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="cd721-196">執行測試</span><span class="sxs-lookup"><span data-stu-id="cd721-196">Run tests</span></span>

<span data-ttu-id="cd721-197">您現在已準備好執行測試。</span><span class="sxs-lookup"><span data-stu-id="cd721-197">You are now ready to run the tests.</span></span> <span data-ttu-id="cd721-198">所有以**TestMethod**屬性標記的方法都會進行測試。</span><span class="sxs-lookup"><span data-stu-id="cd721-198">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="cd721-199">從 [**測試**] 功能表項目執行測試。</span><span class="sxs-lookup"><span data-stu-id="cd721-199">From the **Test** menu item, run the tests.</span></span>

![執行測試](unit-testing-with-aspnet-web-api/_static/image11.png)

<span data-ttu-id="cd721-201">開啟 [**測試瀏覽器**] 視窗，並注意測試的結果。</span><span class="sxs-lookup"><span data-stu-id="cd721-201">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![測試結果](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a><span data-ttu-id="cd721-203">總結</span><span class="sxs-lookup"><span data-stu-id="cd721-203">Summary</span></span>

<span data-ttu-id="cd721-204">您已經完成此教學課程。</span><span class="sxs-lookup"><span data-stu-id="cd721-204">You have completed this tutorial.</span></span> <span data-ttu-id="cd721-205">本教學課程中的資料已刻意簡化，著重于單元測試條件。</span><span class="sxs-lookup"><span data-stu-id="cd721-205">The data in this tutorial was intentionally simplified to focus on unit testing conditions.</span></span> <span data-ttu-id="cd721-206">如需單元測試更先進的資料案例，請參閱[當單元測試 ASP.NET Web API 2 時的模擬 Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="cd721-206">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
