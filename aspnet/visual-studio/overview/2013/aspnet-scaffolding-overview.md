---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: Visual Studio 2013 中的 ASP.NET 架構 |Microsoft Docs
author: Rick-Anderson
description: ASP.NET 的樣板是包含在 Visual Studio 2013 中的新功能。
ms.author: riande
ms.date: 04/09/2014
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: cf4669b769cee28475e2dd6a6ddf07ea1434d04d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557978"
---
# <a name="aspnet-scaffolding-in-visual-studio-2013"></a><span data-ttu-id="0c5b7-103">Visual Studio 2013 中的 ASP.NET Scaffold</span><span class="sxs-lookup"><span data-stu-id="0c5b7-103">ASP.NET Scaffolding in Visual Studio 2013</span></span>

<span data-ttu-id="0c5b7-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="0c5b7-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0c5b7-105">ASP.NET 的樣板是包含在 Visual Studio 2013 中的新功能。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-105">ASP.NET Scaffolding is a new feature that is included in Visual Studio 2013.</span></span>

## <a name="overview"></a><span data-ttu-id="0c5b7-106">概觀</span><span class="sxs-lookup"><span data-stu-id="0c5b7-106">Overview</span></span>

<span data-ttu-id="0c5b7-107">ASP.NET 樣板是用於 ASP.NET Web 應用程式的程式碼產生架構。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-107">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="0c5b7-108">Visual Studio 2013 包括適用于 MVC 和 Web API 專案的預先安裝程式碼產生器。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-108">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="0c5b7-109">當您想要快速加入與資料模型互動的程式碼時，您可以將樣板加入至專案。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-109">You add scaffolding to your project when you want to quickly add code that interacts with data models.</span></span> <span data-ttu-id="0c5b7-110">使用樣板可以減少在專案中開發標準資料作業的時間量。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-110">Using scaffolding can reduce the amount of time to develop standard data operations in your project.</span></span>

<span data-ttu-id="0c5b7-111">根據預設，Visual Studio 2013 不支援產生 Web form 專案的程式碼，但您可以透過將 MVC 相依性新增至專案或安裝延伸模組，將樣板與 Web form 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-111">By default, Visual Studio 2013 does not support generating code for a Web Forms project, but you can use scaffolding with Web Forms by either adding MVC dependencies to the project or installing an extension.</span></span> <span data-ttu-id="0c5b7-112">這兩種方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-112">Both approaches are shown below.</span></span>

<span data-ttu-id="0c5b7-113">Visual Studio 2013 Update 2 （目前為 RC）可讓您擴充 ASP.NET 的架構，以符合您的案例需求。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-113">Visual Studio 2013 Update 2 (currently RC) provides the ability to extend ASP.NET Scaffolding to meet the requirements of your scenario.</span></span> <span data-ttu-id="0c5b7-114">透過這種功能，您可以建立自訂的樣板範本，並將其新增至 [加入新的 Scaffold] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-114">With this functionality, you can create a customized scaffolding template and add it to Add New Scaffold dialog.</span></span> <span data-ttu-id="0c5b7-115">在自訂範本內，您可以指定加入 scaffold 專案時所產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-115">Within the customized template, you specify the code that is generated when adding a scaffolded item.</span></span> <span data-ttu-id="0c5b7-116">如需詳細資訊，請參閱[建立 Visual Studio 的自訂 Scaffolder](https://go.microsoft.com/fwlink/p/?LinkId=395029)。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-116">For more information, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c5b7-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0c5b7-117">Prerequisites</span></span>

<span data-ttu-id="0c5b7-118">若要使用 ASP.NET 的架構，您必須具有：</span><span class="sxs-lookup"><span data-stu-id="0c5b7-118">To use ASP.NET Scaffolding, you must have:</span></span>

- <span data-ttu-id="0c5b7-119">Microsoft Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="0c5b7-119">Microsoft Visual Studio 2013</span></span>
- <span data-ttu-id="0c5b7-120">Web 開發人員工具（預設 Visual Studio 2013 安裝的一部分）</span><span class="sxs-lookup"><span data-stu-id="0c5b7-120">Web Developer Tools (part of default Visual Studio 2013 installation)</span></span>
- <span data-ttu-id="0c5b7-121">ASP.NET Web 架構和工具2013（預設 Visual Studio 2013 安裝的一部分）</span><span class="sxs-lookup"><span data-stu-id="0c5b7-121">ASP.NET Web Frameworks and Tools 2013 (part of default Visual Studio 2013 installation)</span></span>

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a><span data-ttu-id="0c5b7-122">將 scaffold 專案新增至 MVC 或 Web API</span><span class="sxs-lookup"><span data-stu-id="0c5b7-122">Add a scaffolded item to MVC or Web API</span></span>

<span data-ttu-id="0c5b7-123">若要加入 scaffold，請以滑鼠右鍵按一下專案中的專案或資料夾，**然後選取 [** 新增]-[**新的 scaffold 專案**]，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-123">To add a scaffold, right-click either the project or a folder within the project, and select **Add** – **New Scaffolded Item**, as shown in the following image.</span></span>

![新增 scaffold 專案](aspnet-scaffolding-overview/_static/image1.png)

<span data-ttu-id="0c5b7-125">從 [**新增 Scaffold** ] 視窗中，選取要新增的 Scaffold 類型。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-125">From the **Add Scaffold** window, select the type of scaffold to add.</span></span>

![選取 scaffold 類型](aspnet-scaffolding-overview/_static/image2.png)

<span data-ttu-id="0c5b7-127">[**新增控制器**] 視窗可讓您選擇產生控制器的選項，包括是否要使用 Entity Framework 6 的新異步功能。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-127">The **Add Controller** window gives you the opportunity to select options for generating the controller, including whether you want to use the new async features from Entity Framework 6.</span></span>

![新增控制器](aspnet-scaffolding-overview/_static/image3.png)

<span data-ttu-id="0c5b7-129">系統會為您的案例建立相關的類別和頁面。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-129">The relevant classes and pages are created for your scenario.</span></span> <span data-ttu-id="0c5b7-130">例如，下圖顯示透過名為「電影」之模型類別的樣板所建立的 MVC 控制器和 views。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-130">For example, the following image shows the MVC controller and views that were created through scaffolding for a model class named Movies.</span></span>

![建立的檔案](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a><span data-ttu-id="0c5b7-132">將 scaffold 專案新增至 Web Forms</span><span class="sxs-lookup"><span data-stu-id="0c5b7-132">Add a scaffolded item to Web Forms</span></span>

<span data-ttu-id="0c5b7-133">若要加入產生 Web form 程式碼的樣板，您必須安裝延伸模組以 Visual Studio 或加入 MVC 相依性。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-133">To add scaffolding that generates Web Forms code, you must either install an extension to Visual Studio or add MVC dependencies.</span></span> <span data-ttu-id="0c5b7-134">這兩種方法如下所示，但您只需要執行其中一種方法。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-134">Both approaches are shown below, but you only need to do one of these approaches.</span></span>

### <a name="web-forms-scaffolding-extension"></a><span data-ttu-id="0c5b7-135">Web Forms 樣板延伸模組</span><span class="sxs-lookup"><span data-stu-id="0c5b7-135">Web Forms Scaffolding Extension</span></span>

<span data-ttu-id="0c5b7-136">您可以安裝 Visual Studio 延伸模組，讓您使用具有 Web form 專案的樣板。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-136">You can install a Visual Studio extension that enable you to use scaffolding with a Web Forms project.</span></span> <span data-ttu-id="0c5b7-137">在 Visual Studio 中，依序選取 [**工具**] 和 [**擴充功能和更新**]。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-137">In Visual Studio, select **Tools** and then **Extensions and Updates**.</span></span> <span data-ttu-id="0c5b7-138">從這個對話方塊中，搜尋**Web**form 樣板的 Visual Studio 資源庫。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-138">From this dialog search the Visual Studio Gallery for **Web Forms Scaffolding**.</span></span>

![安裝 web forms 樣板](aspnet-scaffolding-overview/_static/image5.png)

<span data-ttu-id="0c5b7-140">如需詳細資訊，請參閱[Web Forms](https://go.microsoft.com/fwlink/p/?LinkId=396478)樣板。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-140">For more information, see [Web Forms Scaffolding](https://go.microsoft.com/fwlink/p/?LinkId=396478).</span></span>

### <a name="mvc-dependencies"></a><span data-ttu-id="0c5b7-141">MVC 相依性</span><span class="sxs-lookup"><span data-stu-id="0c5b7-141">MVC Dependencies</span></span>

<span data-ttu-id="0c5b7-142">若**要新增 MVC**相依性，請選取 [新增 - 新的**scaffold 專案**]。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-142">To add MVC dependencies, select **Add** - **New Scaffolded Item**.</span></span> <span data-ttu-id="0c5b7-143">在 [新增 Scaffold] 視窗中，選取 [ **MVC**相依性]，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-143">In the Add Scaffold window, select **MVC Dependencies**, as shown below.</span></span>

![新增 MVC 相依性](aspnet-scaffolding-overview/_static/image6.png)

<span data-ttu-id="0c5b7-145">有兩個適用于樣板 MVC 的選項;最小和完整。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-145">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="0c5b7-146">如果您選取 [最低]，則只會將 ASP.NET MVC 的 NuGet 套件和參考新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-146">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="0c5b7-147">如果您選取 [完整] 選項，則會加入最少的相依性，以及 MVC 專案所需的內容檔案。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-147">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span> <span data-ttu-id="0c5b7-148">若要輕鬆使用樣板，請選取 [完整相依性]。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-148">To easily use scaffolding, select Full dependencies.</span></span>

![選取 [完整相依性]](aspnet-scaffolding-overview/_static/image7.png)

<span data-ttu-id="0c5b7-150">新增相依性之後，您會**看到 readme.txt 檔案**。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-150">After adding the dependencies, you will see a **readme.txt** file.</span></span> <span data-ttu-id="0c5b7-151">請仔細遵循此檔案中的指示，以確保您的專案能正常運作。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-151">Carefully follow the instructions in this file to ensure that your project works correctly.</span></span>

<span data-ttu-id="0c5b7-152">當您完成了 readme.txt 檔案中的步驟時，您可以新增 scaffold 專案，如上一節中的 MVC 和 Web API 所示。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-152">When you have completed the steps in the readme.txt file, you can add a new scaffolded item as shown in the previous section about MVC and Web API.</span></span> <span data-ttu-id="0c5b7-153">自動產生的視圖和控制器將會在您的專案中正常運作。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-153">The automatically-generated views and controller will function correctly within your project.</span></span>

## <a name="tutorials"></a><span data-ttu-id="0c5b7-154">教學課程</span><span class="sxs-lookup"><span data-stu-id="0c5b7-154">Tutorials</span></span>

<span data-ttu-id="0c5b7-155">若要建立自訂 scaffolder，請參閱[建立 Visual Studio 的自訂 scaffolder](https://go.microsoft.com/fwlink/p/?LinkId=395029)。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-155">To create a customized scaffolder, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

<span data-ttu-id="0c5b7-156">若要自訂產生的檔案，請參閱[如何從新的 Scaffold 專案自訂產生的檔案對話方塊](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-156">To customize the generated files, see [How to customize the generated files from the New Scaffolded Item dialog](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx).</span></span>

<span data-ttu-id="0c5b7-157">如需搭配**Database First 開發**使用架構的範例，請參閱[使用 ASP.NET MVC 的 EF Database First](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md)。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-157">For an example of using scaffolding with **Database First development**, see [EF Database First with ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md).</span></span>

<span data-ttu-id="0c5b7-158">如需在**mvc**專案中使用樣板的範例，請參閱[使用 ASP.NET mvc 5 的消費者入門](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-158">For an example of using scaffolding in an **MVC** project, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="0c5b7-159">如需在**WEB api**專案中使用樣板的範例，請參閱使用[web api 2 中的屬性路由建立 REST API](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="0c5b7-159">For an example of using scaffolding in a **Web API** project, see [Create a REST API with Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).</span></span>
