---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: ASP.NET MVC 4 的新功能 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 是一種架構，用來建立可調整且以標準為基礎的 web 應用程式，並使用妥善建立的設計模式和 ASP.NET 的強大功能 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 4235f4fe666cdeb7d0821127a2b349f2ff30cd6e
ms.sourcegitcommit: 295cf898a4c87e264b0c35c7254b0fa4169f2278
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "74057035"
---
# <a name="whats-new-in-aspnet-mvc-4"></a><span data-ttu-id="5e9cb-103">ASP.NET MVC 4 的新功能</span><span class="sxs-lookup"><span data-stu-id="5e9cb-103">What's New in ASP.NET MVC 4</span></span>

<span data-ttu-id="5e9cb-104">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="5e9cb-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="5e9cb-105">下載 Web Camp 訓練套件</span><span class="sxs-lookup"><span data-stu-id="5e9cb-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="5e9cb-106">ASP.NET MVC 4 是一種架構，可讓您使用妥善建立的設計模式以及 ASP.NET 和 .NET framework 的強大功能，來建立可擴充且以標準為基礎的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-106">ASP.NET MVC 4 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of the ASP.NET and the .NET framework.</span></span> <span data-ttu-id="5e9cb-107">這個新的第四個版本的架構著重于讓行動 web 應用程式開發更輕鬆。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-107">This new, fourth version of the framework focuses on making mobile web application development easier.</span></span>

<span data-ttu-id="5e9cb-108">一開始，當您建立新的 ASP.NET MVC 4 專案時，現在有一個行動應用程式專案範本，可讓您用來建立專供行動裝置使用的獨立應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-108">To begin with, when you create a new ASP.NET MVC 4 project there is now a mobile application project template you can use to build a standalone app specifically for mobile devices.</span></span> <span data-ttu-id="5e9cb-109">此外，ASP.NET MVC 4 會透過 jQuery NuGet 套件與 jQuery Mobile 整合。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-109">Additionally, ASP.NET MVC 4 integrates with jQuery Mobile through a jQuery.Mobile.MVC NuGet package.</span></span> <span data-ttu-id="5e9cb-110">jQuery Mobile 是一種以 HTML5 為基礎的架構，用於開發與所有熱門行動裝置平臺（包括 Windows Phone、iPhone、Android 等等）相容的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-110">jQuery Mobile is an HTML5-based framework for developing web apps that are compatible with all popular mobile device platforms, including Windows Phone, iPhone, Android and so on.</span></span> <span data-ttu-id="5e9cb-111">不過，如果您需要特製化，ASP.NET MVC 4 也可讓您為不同的裝置提供不同的視圖，並提供裝置特定的優化。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-111">However, if you need specialization, ASP.NET MVC 4 also enables you to serve different views for different devices and provide device-specific optimizations.</span></span>

<span data-ttu-id="5e9cb-112">在這個實際操作實驗室中，您將從 ASP.NET MVC 4 &quot;Internet Application&quot; 專案範本開始，以建立相片圖庫應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-112">In this hands-on lab, you will start with the ASP.NET MVC 4 &quot;Internet Application&quot; project template to create a Photo Gallery application.</span></span> <span data-ttu-id="5e9cb-113">您將使用 jQuery Mobile 和 ASP.NET MVC 4 的新功能來逐步增強應用程式，使其與不同的行動裝置和桌上型電腦網頁瀏覽器相容。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-113">You will progressively enhance the app using jQuery Mobile and ASP.NET MVC 4's new features to make it compatible with different mobile devices and desktop web browsers.</span></span> <span data-ttu-id="5e9cb-114">您也將瞭解程式碼產生的新程式碼配方，以及 ASP.NET MVC 4 如何藉由支援 Task&lt;ActionResult&gt; 傳回型別，讓您更輕鬆地撰寫非同步動作方法。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-114">You will also learn about new code recipes for code generation and how ASP.NET MVC 4 makes it easier for you to write asynchronous action methods by supporting Task&lt;ActionResult&gt; return types.</span></span>

> [!NOTE]
> <span data-ttu-id="5e9cb-115">所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[Microsoft web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)取得。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-115">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="5e9cb-116">此實驗室的特定專案可在[ASP.NET 4.5 中 Web Forms 的新功能](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)中取得。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-116">The project specific to this lab is available at [What's New in Web Forms in ASP.NET 4.5](https://github.com/Microsoft-Web/HOL-ASPNETWebForms).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="5e9cb-117">目標</span><span class="sxs-lookup"><span data-stu-id="5e9cb-117">Objectives</span></span>

<span data-ttu-id="5e9cb-118">在此實際操作實驗室中，您將瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="5e9cb-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="5e9cb-119">利用 ASP.NET MVC 專案範本的增強功能，包括新的行動應用程式專案範本</span><span class="sxs-lookup"><span data-stu-id="5e9cb-119">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="5e9cb-120">使用 HTML5 視口屬性和 CSS 媒體查詢來改善行動裝置上的顯示</span><span class="sxs-lookup"><span data-stu-id="5e9cb-120">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="5e9cb-121">使用 jQuery Mobile 進行漸進式增強，以及建立觸控式優化的 web UI</span><span class="sxs-lookup"><span data-stu-id="5e9cb-121">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="5e9cb-122">建立行動裝置特定的視圖</span><span class="sxs-lookup"><span data-stu-id="5e9cb-122">Create mobile-specific views</span></span>
- <span data-ttu-id="5e9cb-123">使用視圖切換器元件，在應用程式中的行動和桌面視圖之間切換</span><span class="sxs-lookup"><span data-stu-id="5e9cb-123">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="5e9cb-124">使用工作支援建立異步控制器</span><span class="sxs-lookup"><span data-stu-id="5e9cb-124">Create asynchronous controllers using task support</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="5e9cb-125">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5e9cb-125">Prerequisites</span></span>

<span data-ttu-id="5e9cb-126">您必須具有下列專案，才能完成此實驗室：</span><span class="sxs-lookup"><span data-stu-id="5e9cb-126">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="5e9cb-127">適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需如何安裝的指示，請參閱[附錄 B](#AppendixB) ）。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-127">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>
- <span data-ttu-id="5e9cb-128">[ASP.NET MVC 4](../../../mvc4.md) （包含在 Microsoft Visual Studio 2012 安裝中）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-128">[ASP.NET MVC 4](../../../mvc4.md) (included in the Microsoft Visual Studio 2012 installation)</span></span>
- <span data-ttu-id="5e9cb-129">Windows Phone 模擬器（隨附于[Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233)）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-129">Windows Phone Emulator (included in the [Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233))</span></span>
- <span data-ttu-id="5e9cb-130">選擇性- [WebMatrix 2](https://www.microsoft.com/web/webmatrix/)搭配**電動梅紅 iPhone**模擬器延伸模組（僅適用于使用 iPhone 模擬器流覽 Web 應用程式的練習3）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-130">Optional - [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) with **Electric Plum iPhone Simulator** extension (only for Exercise 3 used to browse the web application with an iPhone simulator)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="5e9cb-131">安裝程式</span><span class="sxs-lookup"><span data-stu-id="5e9cb-131">Setup</span></span>

<span data-ttu-id="5e9cb-132">在整個實驗室檔中，系統會指示您插入程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-132">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="5e9cb-133">為了方便起見，大部分的程式碼都是以 Visual Studio Code 程式碼片段的形式提供，您可以從 Visual Studio 內使用它來避免手動新增。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-133">For your convenience, most of that code is provided as Visual Studio Code Snippets, which you can use from within Visual Studio to avoid having to add it manually.</span></span>

<span data-ttu-id="5e9cb-134">若要安裝程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="5e9cb-134">To install the code snippets:</span></span>

1. <span data-ttu-id="5e9cb-135">開啟 Windows Explorer 視窗，並流覽至實驗室的 [ **Source\Setup** ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-135">Open a Windows Explorer window and browse to the lab's **Source\Setup** folder.</span></span>
2. <span data-ttu-id="5e9cb-136">按兩下此資料夾中的**Setup .cmd**檔案，安裝 Visual Studio 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-136">Double-click the **Setup.cmd** file in this folder to install the Visual Studio code snippets.</span></span>

<span data-ttu-id="5e9cb-137">如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 A：使用程式碼片段](#AppendixA)&quot;。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="5e9cb-138">練習</span><span class="sxs-lookup"><span data-stu-id="5e9cb-138">Exercises</span></span>

<span data-ttu-id="5e9cb-139">這個實際操作實驗室包含下列練習：</span><span class="sxs-lookup"><span data-stu-id="5e9cb-139">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="5e9cb-140">新的 ASP.NET MVC 4 專案範本</span><span class="sxs-lookup"><span data-stu-id="5e9cb-140">New ASP.NET MVC 4 Project Templates</span></span>](#Exercise1)
2. [<span data-ttu-id="5e9cb-141">建立相片圖庫 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5e9cb-141">Creating the Photo Gallery Web Application</span></span>](#Exercise2)
3. [<span data-ttu-id="5e9cb-142">新增行動裝置的支援</span><span class="sxs-lookup"><span data-stu-id="5e9cb-142">Adding Support for Mobile Devices</span></span>](#Exercise3)
4. [<span data-ttu-id="5e9cb-143">使用非同步控制器</span><span class="sxs-lookup"><span data-stu-id="5e9cb-143">Using Asynchronous Controllers</span></span>](#Exercise4)

> [!NOTE]
> <span data-ttu-id="5e9cb-144">每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-144">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="5e9cb-145">如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-145">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="5e9cb-146">完成此實驗室的預估時間： **60 分鐘**。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-146">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a><span data-ttu-id="5e9cb-147">練習1：新增 ASP.NET MVC 4 專案範本</span><span class="sxs-lookup"><span data-stu-id="5e9cb-147">Exercise 1: New ASP.NET MVC 4 Project Templates</span></span>

<span data-ttu-id="5e9cb-148">在此練習中，您將探索 ASP.NET MVC 4 專案範本中的增強功能。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-148">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 Project templates.</span></span> <span data-ttu-id="5e9cb-149">除了網際網路應用程式範本，已存在於 MVC 3 中，此版本現在還包含適用于行動應用程式的個別範本。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-149">In addition to the Internet Application template, already present in MVC 3, this version now includes a separate template for Mobile applications.</span></span> <span data-ttu-id="5e9cb-150">首先，您將會看到每個範本的相關功能。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-150">First, you will look at some relevant features of each of the templates.</span></span> <span data-ttu-id="5e9cb-151">然後，您可以使用正確的方法，在不同的平臺上正確呈現您的頁面。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-151">Then, you will work on rendering your page properly on the different platforms by using the right approach.</span></span>

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a><span data-ttu-id="5e9cb-152">工作 1-探索網際網路應用程式範本</span><span class="sxs-lookup"><span data-stu-id="5e9cb-152">Task 1 - Exploring the Internet Application Template</span></span>

1. <span data-ttu-id="5e9cb-153">開啟**Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-153">Open **Visual Studio**.</span></span>
2. <span data-ttu-id="5e9cb-154">選取檔案 **|新增 |[專案**] 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-154">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="5e9cb-155">在 [**新增專案**] 對話方塊中，**選取C#視覺效果 |** 在左窗格樹狀結構上，選擇 [ **ASP.NET MVC 4 Web 應用程式]。**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-155">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="5e9cb-156">將專案命名為**PhotoGallery**，選取位置（或保留預設值），然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-156">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e9cb-157">您稍後會自訂您目前建立的 PhotoGallery ASP.NET MVC 4 解決方案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-157">You will later customize the PhotoGallery ASP.NET MVC 4 solution you are now creating.</span></span>

    <span data-ttu-id="5e9cb-158">![建立新專案](whats-new-in-aspnet-mvc-4/_static/image1.png "建立新專案")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-158">![Creating a new project](whats-new-in-aspnet-mvc-4/_static/image1.png "Creating a new project")</span></span>

    <span data-ttu-id="5e9cb-159">*建立新專案*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-159">*Creating a new project*</span></span>
3. <span data-ttu-id="5e9cb-160">在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**] 專案範本，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-160">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="5e9cb-161">請確定您已選取 Razor 做為 view engine。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-161">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="5e9cb-162">![建立新的 ASP.NET MVC 4 網際網路應用程式](whats-new-in-aspnet-mvc-4/_static/image2.png "建立新的 ASP.NET MVC 4 網際網路應用程式")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-162">![Creating a new ASP.NET MVC 4 Internet Application](whats-new-in-aspnet-mvc-4/_static/image2.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="5e9cb-163">*建立新的 ASP.NET MVC 4 網際網路應用程式*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-163">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e9cb-164">Razor 語法已在 ASP.NET MVC 3 中引進。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-164">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="5e9cb-165">其目標是要將檔案中所需的字元和按鍵數目降至最低，以啟用快速且流暢的程式碼撰寫工作流程。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-165">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="5e9cb-166">Razor 利用現有C# /VB （或其他）語言技能，並提供範本標記語法來啟用絕佳的 HTML 結構工作流程。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-166">Razor leverages existing C# / VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="5e9cb-167">按**F5**執行方案，並查看已更新的範本。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-167">Press **F5** to run the solution and see the renewed templates.</span></span> <span data-ttu-id="5e9cb-168">您可以查看下列功能：</span><span class="sxs-lookup"><span data-stu-id="5e9cb-168">You can check out the following features:</span></span>

    <span data-ttu-id="5e9cb-169">**現代化樣式範本**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-169">**Modern-style templates**</span></span>

    <span data-ttu-id="5e9cb-170">這些範本已更新，提供更現代化的樣式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-170">The templates have been renewed, providing more modern-looking styles.</span></span>

    <span data-ttu-id="5e9cb-171">![ASP.NET MVC 4 風貌範本](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 風貌範本")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-171">![ASP.NET MVC 4 restyled templates](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 restyled templates")</span></span>

    <span data-ttu-id="5e9cb-172">*ASP.NET MVC 4 風貌範本*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-172">*ASP.NET MVC 4 restyled templates*</span></span>

    <span data-ttu-id="5e9cb-173">![新增連絡人頁面](whats-new-in-aspnet-mvc-4/_static/image4.png "新增連絡人頁面")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-173">![New Contact page](whats-new-in-aspnet-mvc-4/_static/image4.png "New Contact page")</span></span>

    <span data-ttu-id="5e9cb-174">*新增連絡人頁面*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-174">*New Contact page*</span></span>

    <span data-ttu-id="5e9cb-175">**適應性呈現**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-175">**Adaptive Rendering**</span></span>

    <span data-ttu-id="5e9cb-176">查看調整瀏覽器視窗的大小，並注意頁面配置如何動態適應新的視窗大小。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-176">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="5e9cb-177">這些範本會使用自動調整轉譯技術，在桌上型電腦和行動平臺中正確轉譯，而不需要任何自訂。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-177">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

    <span data-ttu-id="5e9cb-178">![不同瀏覽器大小的 ASP.NET MVC 4 專案範本](whats-new-in-aspnet-mvc-4/_static/image5.png "不同瀏覽器大小的 ASP.NET MVC 4 專案範本")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-178">![ASP.NET MVC 4 project template in different browser sizes](whats-new-in-aspnet-mvc-4/_static/image5.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

    <span data-ttu-id="5e9cb-179">*不同瀏覽器大小的 ASP.NET MVC 4 專案範本*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-179">*ASP.NET MVC 4 project template in different browser sizes*</span></span>

    <span data-ttu-id="5e9cb-180">**使用 JavaScript 的更豐富 UI**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-180">**Richer UI with JavaScript**</span></span>

    <span data-ttu-id="5e9cb-181">預設專案範本的另一個增強功能是使用 JavaScript 來提供更互動式的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-181">Another enhancement to default project templates is the use of JavaScript to provide a more interactive JavaScript.</span></span> <span data-ttu-id="5e9cb-182">在範本中使用的登入和註冊連結範例說明點如何使用 jQuery 驗證來驗證用戶端的輸入欄位。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-182">The Login and Register links used in the template exemplify how to use the jQuery Validations to validate the input fields from client-side.</span></span>

    ![jQuery 驗證](whats-new-in-aspnet-mvc-4/_static/image6.png)

    <span data-ttu-id="5e9cb-184">*jQuery 驗證*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-184">*jQuery Validation*</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e9cb-185">請注意兩個登入區段，您可以在第一節中，使用已註冊的帳戶從網站登入，在第二個區段中，您也可以使用其他驗證服務（如 google）登入（預設為停用）。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-185">Notice the two log in sections, in the first section you can log in using a registered account from the site and in the second section you can alternatively log in using another authentication service like google (disabled by default).</span></span>
5. <span data-ttu-id="5e9cb-186">關閉瀏覽器以停止偵錯工具，並返回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-186">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="5e9cb-187">開啟位於**應用程式\_[開始**] 資料夾底下的檔案**AuthConfig.cs** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-187">Open the file **AuthConfig.cs** located under the **App\_Start** folder.</span></span>
7. <span data-ttu-id="5e9cb-188">從最後一行移除批註，以註冊 Google 用戶端進行*OAuth*驗證。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-188">Remove the comment from the last line to register Google client for *OAuth* authentication.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > <span data-ttu-id="5e9cb-189">請注意，您可以輕鬆地使用任何 OpenID 或 OAuth 服務（例如 Facebook、Twitter、Microsoft 等）來啟用驗證。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-189">Notice you can easily enable authentication using any OpenID or OAuth service like Facebook, Twitter, Microsoft, etc.</span></span>
8. <span data-ttu-id="5e9cb-190">按**F5**執行方案，並流覽至登入頁面。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-190">Press **F5** to run the solution and navigate to the login page.</span></span>
9. <span data-ttu-id="5e9cb-191">選取 [ **Google**服務] 以登入。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-191">Select **Google** service to log in.</span></span>

    ![選取登入服務](whats-new-in-aspnet-mvc-4/_static/image7.png)

    <span data-ttu-id="5e9cb-193">*選取登入服務*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-193">*Selecting the log in service*</span></span>
10. <span data-ttu-id="5e9cb-194">使用您的 Google 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-194">Log in using your Google account.</span></span>
11. <span data-ttu-id="5e9cb-195">允許網站（localhost）從 Google 帳戶取出資訊。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-195">Allow the site (localhost) to retrieve information from Google account.</span></span>
12. <span data-ttu-id="5e9cb-196">最後，您將必須在網站中註冊，才能建立 Google 帳戶的關聯。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-196">Finally, you will have to register in the site to associate the Google account.</span></span>

   ![建立 Google 帳戶的關聯](whats-new-in-aspnet-mvc-4/_static/image8.png)

   <span data-ttu-id="5e9cb-198">*建立 Google 帳戶的關聯*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-198">*Associating your Google account*</span></span>
13. <span data-ttu-id="5e9cb-199">關閉瀏覽器以停止偵錯工具，並返回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-199">Close the browser to stop the debugger and return to Visual Studio.</span></span>
14. <span data-ttu-id="5e9cb-200">現在請探索解決方案，以查看專案範本中 ASP.NET MVC 4 所引進的一些新功能。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-200">Now explore the solution to check out some other new features introduced by ASP.NET MVC 4 in the project template.</span></span>

   <span data-ttu-id="5e9cb-201">![ASP.NET MVC 4 網際網路應用程式專案範本](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 網際網路應用程式專案範本")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-201">![The ASP.NET MVC 4 Internet Application Project Template](whats-new-in-aspnet-mvc-4/_static/image9.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

   <span data-ttu-id="5e9cb-202">*ASP.NET MVC 4 網際網路應用程式專案範本*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-202">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

    - <span data-ttu-id="5e9cb-203">**HTML 5 標記**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-203">**HTML 5 Markup**</span></span>

       <span data-ttu-id="5e9cb-204">流覽範本視圖以找出新的主題標記。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-204">Browse template views to find out the new theme markup.</span></span>

       <span data-ttu-id="5e9cb-205">![新範本，使用 Razor 和 HTML5 標記關於 cshtml。](whats-new-in-aspnet-mvc-4/_static/image10.png "新範本，使用 Razor 和 HTML5 標記關於 cshtml。")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-205">![New template, using Razor and HTML5 markup About.cshtml.](whats-new-in-aspnet-mvc-4/_static/image10.png "New template, using Razor and HTML5 markup About.cshtml.")</span></span>

       <span data-ttu-id="5e9cb-206">*使用 Razor 和 HTML5 標記的新範本（關於. cshtml）。*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-206">*New template, using Razor and HTML5 markup (About.cshtml).*</span></span>
    - <span data-ttu-id="5e9cb-207">**已更新 JavaScript 程式庫**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-207">**Updated JavaScript libraries**</span></span>

       <span data-ttu-id="5e9cb-208">ASP.NET MVC 4 預設範本現在包含 KnockoutJS，這是一種 JavaScript MVVM 架構，可讓您使用 JavaScript 和 HTML 建立豐富且回應速度高的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-208">The ASP.NET MVC 4 default template now includes KnockoutJS, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="5e9cb-209">如同在 MVC3 中，jQuery 和 jQuery UI 程式庫也包含在 ASP.NET MVC 4 中。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-209">Like in MVC3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

     > [!NOTE]
     > <span data-ttu-id="5e9cb-210">您可以在此連結中取得 KnockOutJS 程式庫的詳細資訊： [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/)。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-210">You can get more information about KnockOutJS library in this link: [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/).</span></span> <span data-ttu-id="5e9cb-211">此外，您可以在[[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)中瞭解 jQuery 和 jquery UI。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-211">Additionally, you can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a><span data-ttu-id="5e9cb-212">工作 2-探索行動應用程式範本</span><span class="sxs-lookup"><span data-stu-id="5e9cb-212">Task 2 - Exploring the Mobile Application Template</span></span>

<span data-ttu-id="5e9cb-213">ASP.NET MVC 4 有助於開發行動和平板電腦瀏覽器的網站。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-213">ASP.NET MVC 4 facilitates the development of websites for mobile and tablet browsers.</span></span> <span data-ttu-id="5e9cb-214">此範本具有與網際網路應用程式範本相同的應用程式結構（請注意，控制器程式碼幾乎完全相同），但其樣式已修改為在觸控式行動裝置中正確轉譯。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-214">This template has the same application structure as the Internet Application template (notice that the controller code is practically identical), but its style was modified to render properly in touch-based mobile devices.</span></span>

1. <span data-ttu-id="5e9cb-215">選取檔案 **|新增 |[專案**] 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-215">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="5e9cb-216">在 [**新增專案**] 對話方塊中，**選取C#視覺效果 |Web**範本：在左窗格樹狀結構上，選擇 [ **ASP.NET MVC 4 Web 應用程式]。**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-216">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="5e9cb-217">將專案命名為**PhotoGallery**，選取位置（或保留預設值），選取 [&quot;新增至方案]&quot; 然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-217">Name the project **PhotoGallery.Mobile**, select a location (or leave the default), select &quot;Add to solution&quot; and click **OK**.</span></span>
2. <span data-ttu-id="5e9cb-218">在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [行動**應用程式**] 專案範本，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-218">In the **New ASP.NET MVC 4 Project** dialog, select the **Mobile Application** project template and click **OK**.</span></span> <span data-ttu-id="5e9cb-219">請確定您已選取 Razor 做為 view engine。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-219">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="5e9cb-220">![建立新的 ASP.NET MVC 4 行動應用程式](whats-new-in-aspnet-mvc-4/_static/image11.png "建立新的 ASP.NET MVC 4 行動應用程式")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-220">![Creating a new ASP.NET MVC 4 Mobile Application](whats-new-in-aspnet-mvc-4/_static/image11.png "Creating a new ASP.NET MVC 4 Mobile Application")</span></span>

    <span data-ttu-id="5e9cb-221">*建立新的 ASP.NET MVC 4 行動應用程式*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-221">*Creating a new ASP.NET MVC 4 Mobile Application*</span></span>
3. <span data-ttu-id="5e9cb-222">現在您可以流覽解決方案，並查看適用于 mobile 的 ASP.NET MVC 4 解決方案範本所引進的一些新功能：</span><span class="sxs-lookup"><span data-stu-id="5e9cb-222">Now you are able to explore the solution and check out some of the new features introduced by the ASP.NET MVC 4 solution template for mobile:</span></span>

    - <span data-ttu-id="5e9cb-223">**jQuery Mobile 程式庫**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-223">**jQuery Mobile Library**</span></span>

        <span data-ttu-id="5e9cb-224">行動應用程式專案範本包含 jQuery Mobile library，這是行動瀏覽器相容性的開放原始碼程式庫。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-224">The Mobile Application project template includes the jQuery Mobile library, which is an open source library for mobile browser compatibility.</span></span> <span data-ttu-id="5e9cb-225">jQuery Mobile 會對支援 CSS 和 JavaScript 的行動瀏覽器套用漸進增強功能。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-225">jQuery Mobile applies progressive enhancement to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="5e9cb-226">漸進式增強功能可讓所有瀏覽器顯示網頁的基本內容，而只會啟用最強大的瀏覽器來顯示豐富的內容。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-226">Progressive enhancement enables all browsers to display the basic content of a web page, while it only enables the most powerful browsers to display the rich content.</span></span> <span data-ttu-id="5e9cb-227">包含在 jQuery Mobile 樣式中的 JavaScript 和 CSS 檔案，可協助行動瀏覽器符合畫面中的內容，而不會在頁面標記中進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-227">The JavaScript and CSS files, included in the jQuery Mobile style, help mobile browsers to fit the content in the screen without making any change in the page markup.</span></span>

        ![jQuery-行動庫-內含-範本](whats-new-in-aspnet-mvc-4/_static/image12.png)

        <span data-ttu-id="5e9cb-229">*範本中包含的 jQuery mobile library*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-229">*jQuery mobile library included in the template*</span></span>
    - <span data-ttu-id="5e9cb-230">**以 HTML5 為基礎的標記**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-230">**HTML5 based markup**</span></span>

        ![Mobile-應用程式-範本-使用-HTML5-標記](whats-new-in-aspnet-mvc-4/_static/image13.png)

        <span data-ttu-id="5e9cb-232">*使用 HTML5 標記的行動應用程式範本（Login. cshtml 和 index. cshtml）*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-232">*Mobile application template using HTML5 markup, (Login.cshtml and index.cshtml)*</span></span>
4. <span data-ttu-id="5e9cb-233">按**F5**執行方案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-233">Press **F5** to run the solution.</span></span>
5. <span data-ttu-id="5e9cb-234">開啟**Windows Phone 7 模擬器**。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-234">Open the **Windows Phone 7 Emulator**.</span></span>
6. <span data-ttu-id="5e9cb-235">在手機的 [開始] 畫面中，開啟 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-235">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="5e9cb-236">查看桌面應用程式啟動的 URL，並從電話流覽至該 URL （例如 `http://localhost:[PortNumber]/`）。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-236">Check out the URL where the desktop application started and browse to that URL from the phone (e.g. `http://localhost:[PortNumber]/`).</span></span>
7. <span data-ttu-id="5e9cb-237">現在您可以進入登入頁面，或查看 [關於] 頁面。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-237">Now you are able to enter the login page or check out the about page.</span></span> <span data-ttu-id="5e9cb-238">請注意，網站的樣式是以適用于 mobile 的新 Metro 應用程式為基礎。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-238">Notice that the style of the website is based on the new Metro app for mobile.</span></span> <span data-ttu-id="5e9cb-239">ASP.NET MVC 4 專案範本會正確地顯示在行動裝置上，確定頁面的所有元素都是可見的，並且已啟用。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-239">The ASP.NET MVC 4 project template is correctly displayed on mobile devices, making sure all the elements of the page are visible and enabled.</span></span> <span data-ttu-id="5e9cb-240">請注意，標頭上的連結夠大，可供按一下或點擊。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-240">Notice that the links on the header are big enough to be clicked or tapped.</span></span>

    <span data-ttu-id="5e9cb-241">![行動裝置中的專案範本頁面](whats-new-in-aspnet-mvc-4/_static/image14.png "行動裝置中的專案範本頁面")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-241">![Project template pages in a mobile device](whats-new-in-aspnet-mvc-4/_static/image14.png "Project template pages in a mobile device")</span></span>

    <span data-ttu-id="5e9cb-242">*行動裝置中的專案範本頁面*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-242">*Project template pages in a mobile device*</span></span>
8. <span data-ttu-id="5e9cb-243">新範本也會使用「**視口中繼」標記**。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-243">The new template also uses the **Viewport meta tag**.</span></span> <span data-ttu-id="5e9cb-244">大部分的行動瀏覽器都會定義虛擬瀏覽器視窗或 &quot;區&quot;的寬度，這大於行動裝置的實際寬度。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-244">Most mobile browsers define a width for a virtual browser window or &quot;viewport&quot;, which is larger than the actual width of the mobile device.</span></span> <span data-ttu-id="5e9cb-245">這可讓行動瀏覽器在虛擬顯示器內部顯示整個網頁。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-245">This enables mobile browsers to display the entire web page inside the virtual display.</span></span> <span data-ttu-id="5e9cb-246">「**視口中繼標記**」可讓 網頁程式開發人員在行動裝置上設定瀏覽器區域的寬度、高度和規模 **。**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-246">The **Viewport meta tag** allows web developers to set the width, height and scale of the browser area on mobile devices **.**</span></span> <span data-ttu-id="5e9cb-247">適用于行動應用程式的 ASP.NET MVC 4 範本會將此視口設定為版面配置範本（*Views\Shared\_layout*）中的裝置寬度（&quot;寬度 = 裝置寬度&quot;），讓所有頁面都將其視口設定為裝置螢幕寬度。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-247">The ASP.NET MVC 4 template for Mobile Applications sets the viewport to the device width (&quot;width=device-width&quot;) in the layout template (*Views\Shared\_Layout.cshtml*), so that all the pages will have their viewport set to the device screen width.</span></span> <span data-ttu-id="5e9cb-248">請注意，[視口] 中繼標記不會變更預設瀏覽器視圖。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-248">Notice that the Viewport meta tag will not change the default browser view.</span></span>
9. <span data-ttu-id="5e9cb-249">開啟 **\_Layout**，位於**Views |共用**資料夾，並批註「視口」中繼標記。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-249">Open **\_Layout.cshtml**, located in the **Views | Shared** folder, and comment the Viewport meta tag.</span></span> <span data-ttu-id="5e9cb-250">執行應用程式（如果尚未開啟），並查看差異。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-250">Run the application, if not already opened, and check out the differences.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

<span data-ttu-id="5e9cb-251">![批註區中繼標記之後的網站](whats-new-in-aspnet-mvc-4/_static/image15.png "批註區中繼標記之後的網站")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-251">![The site after commenting the viewport meta tag](whats-new-in-aspnet-mvc-4/_static/image15.png "The site after commenting the viewport meta tag")</span></span>

<span data-ttu-id="5e9cb-252">*批註區中繼標記之後的網站*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-252">*The site after commenting the viewport meta tag*</span></span>
10. <span data-ttu-id="5e9cb-253">在 Visual Studio 中，按**SHIFT** + **F5**停止對應用程式的偵測。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-253">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
11. <span data-ttu-id="5e9cb-254">取消批註視口中繼標記。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-254">Uncomment the viewport meta tag.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a><span data-ttu-id="5e9cb-255">工作 3-使用適應性呈現</span><span class="sxs-lookup"><span data-stu-id="5e9cb-255">Task 3 - Using Adaptive Rendering</span></span>

<span data-ttu-id="5e9cb-256">在這項工作中，您將學習另一種在行動裝置和網頁瀏覽器上正確呈現網頁的方法，而不需要任何自訂。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-256">In this task, you will learn another method to render a Web page correctly on mobile devices and Web browsers at the same time without any customization.</span></span> <span data-ttu-id="5e9cb-257">您已經使用了類似用途的「視口中繼」標記。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-257">You have already used Viewport meta tag with a similar purpose.</span></span> <span data-ttu-id="5e9cb-258">現在您會符合另一個強大的*方法：彈性*轉譯。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-258">Now you will meet another powerful method: *adaptive rendering*.</span></span>

<span data-ttu-id="5e9cb-259">適應性轉譯是一種技術，使用**CSS3 媒體查詢**來自訂套用至頁面的樣式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-259">Adaptive rendering is a technique that uses **CSS3 media queries** to customize the style applied to a page.</span></span> <span data-ttu-id="5e9cb-260">媒體查詢會定義樣式表單內的條件，並在特定條件下將 CSS 樣式分組。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-260">Media queries define conditions inside a style sheet, grouping CSS styles under a certain condition.</span></span> <span data-ttu-id="5e9cb-261">只有當條件為 true 時，樣式才會套用至已宣告的物件。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-261">Only when the condition is true, the style is applied to the declared objects.</span></span>

<span data-ttu-id="5e9cb-262">調適型轉譯技術所提供的彈性可讓您在不同裝置上顯示網站的任何自訂專案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-262">The flexibility provided by the adaptive rendering technique enables any customization for displaying the site on different devices.</span></span> <span data-ttu-id="5e9cb-263">您可以在單一樣式表單上定義任意數目的樣式，而不需要撰寫邏輯程式碼來選擇樣式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-263">You can define as many styles as you want on a single style sheet without writing logic code to choose the style.</span></span> <span data-ttu-id="5e9cb-264">因此，它是調整頁面樣式的一種非常棒的方式，因為它會減少重複使用的程式碼和邏輯數量。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-264">Therefore, it is a very neat way of adapting page styles, as it reduces the amount of duplicated code and logic for rendering purposes.</span></span> <span data-ttu-id="5e9cb-265">另一方面，頻寬耗用量會增加，因為 CSS 檔案的大小可能會逐漸成長。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-265">On the other hand, bandwidth consumption would increase, as the size of your CSS files could grow marginally.</span></span>

<span data-ttu-id="5e9cb-266">藉由使用調適型呈現技術，不論瀏覽器為何，您的網站都將會**正確顯示。**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-266">By using the adaptive rendering technique, your site will be **displayed properly, regardless of the browser.**</span></span> <span data-ttu-id="5e9cb-267">不過，您應該考慮頻寬額外負載是否有問題。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-267">However, you should consider if the bandwidth extra load is a concern.</span></span>

> [!NOTE]
> <span data-ttu-id="5e9cb-268">媒體查詢的基本格式為： @media \[範圍：全部 |掌上 |列印 |投射 |螢幕\] （[屬性：值] 和 。[屬性：值]）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-268">The basic format of a media query is: @media \[Scope: all | handheld | print | projection | screen\] ([property:value] and ... [property:value])</span></span>

<span data-ttu-id="5e9cb-269">媒體查詢的範例： &gt; **@media 全部和（最大寬度：1000px）和（最小寬度：700px） {}：** 適用于700px 與1000px 之間的所有解析度。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-269">Examples of media queries: &gt;**@media all and (max-width: 1000px) and (min-width: 700px) {}:** For all the resolutions between 700px and 1000px.</span></span>

> <span data-ttu-id="5e9cb-270">**@media 螢幕和（最小寬度：400px）和（最大寬度：700px） {...}：** 僅適用于螢幕。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-270">**@media screen and (min-width: 400px) and (max-width: 700px) { ... }:** Only for screens.</span></span> <span data-ttu-id="5e9cb-271">解決方式必須介於400和700px 之間。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-271">The resolution must be between 400 and 700px.</span></span>
> 
> <span data-ttu-id="5e9cb-272">**@media 掌上型和（最小寬度：20em）、螢幕和（最小寬度：20em） {...}：** 適用于掌上型電腦（行動裝置和裝置）和螢幕。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-272">**@media handheld and (min-width: 20em), screen and (min-width: 20em) { ... }:** For handhelds(mobile and devices) and screens.</span></span> <span data-ttu-id="5e9cb-273">寬度下限必須大於20em。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-273">The minimum width must be greater than 20em.</span></span>
> 
> <span data-ttu-id="5e9cb-274">您可以在[W3C 網站](http://www.w3.org/TR/css3-mediaqueries/)上找到更多有關此的資訊。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-274">You can find more information about this on the [W3C site](http://www.w3.org/TR/css3-mediaqueries/).</span></span>

<span data-ttu-id="5e9cb-275">您現在將探索彈性轉譯的運作方式，改善 ASP.NET MVC 4 預設網站範本的可讀性。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-275">You will now explore how the adaptive rendering works, improving the readability of the ASP.NET MVC 4 default website template.</span></span>

1. <span data-ttu-id="5e9cb-276">開啟您在工作1建立的 [ **PhotoGallery** ] 方案，然後選取 [ **PhotoGallery** ] 專案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-276">Open the **PhotoGallery.sln** solution you have created at Task 1 and select the **PhotoGallery** project.</span></span> <span data-ttu-id="5e9cb-277">按**F5**執行方案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-277">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="5e9cb-278">調整瀏覽器寬度的大小，將視窗設定為一半或小於其原始大小的一季。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-278">Resize the browser's width, setting the windows to half or to less than a quarter of its original size.</span></span> <span data-ttu-id="5e9cb-279">請注意標頭中的專案會發生什麼情況：部分元素不會出現在標頭的可見區域中。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-279">Notice what happens with the items in the header: Some elements will not appear in the visible area of the header.</span></span>
3. <span data-ttu-id="5e9cb-280">從位於 [**內容**] 專案資料夾中的 Visual Studio 方案瀏覽器開啟 [**網站 .css**檔案]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-280">Open **Site.css** file from the Visual Studio Solution explorer, located in **Content** project folder.</span></span> <span data-ttu-id="5e9cb-281">按**CTRL + F**以開啟 Visual Studio 整合式搜尋，然後撰寫 `@media` 以尋找**CSS 媒體查詢**。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-281">Press **CTRL + F** to open Visual Studio integrated search, and write `@media` to locate the **CSS media query**.</span></span>

    <span data-ttu-id="5e9cb-282">此範本中定義的媒體查詢準則會以這種方式運作：當瀏覽器的視窗大小低於**850 Px**時，所套用的 CSS 規則就是在此媒體區塊內定義的樣式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-282">The media query condition defined in this template works in this way: When the browser's window size is below **850 px**, the CSS rules applied are the ones defined inside this media block.</span></span>

    <span data-ttu-id="5e9cb-283">![尋找媒體查詢](whats-new-in-aspnet-mvc-4/_static/image16.png "尋找媒體查詢")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-283">![Locating the media query](whats-new-in-aspnet-mvc-4/_static/image16.png "Locating the media query")</span></span>

    <span data-ttu-id="5e9cb-284">*尋找媒體查詢*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-284">*Locating the media query*</span></span>
4. <span data-ttu-id="5e9cb-285">將 850 px 中設定的最大寬度屬性值取代為**10px**，以停用自動調整轉譯，然後按**CTRL + S**儲存變更。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-285">Replace the max-width attribute value set in 850 px with **10px**, in order to disable the adaptive rendering, and press **CTRL + S** to save the changes.</span></span> <span data-ttu-id="5e9cb-286">返回瀏覽器，然後按下**CTRL + F5** ，使用您所做的變更來重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-286">Return to the browser and press **CTRL + F5** to refresh the page with the changes you have made.</span></span> <span data-ttu-id="5e9cb-287">在調整視窗的寬度時，請注意這兩個頁面的差異。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-287">Notice the differences in both pages when adjusting the width of the window.</span></span>

    <span data-ttu-id="5e9cb-288">![在左側，頁面會套用 @media 樣式，在右邊，會省略樣式](whats-new-in-aspnet-mvc-4/_static/image17.png "在左側，頁面會套用 @media 樣式，在右邊，會省略樣式")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-288">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image17.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="5e9cb-289">*在左側，頁面會套用 @media 樣式，在右邊，會省略樣式*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-289">*In the left, the page is applying the @media style, in the right, the style is omitted*</span></span>

    <span data-ttu-id="5e9cb-290">現在，讓我們來看看行動裝置會發生什麼事：</span><span class="sxs-lookup"><span data-stu-id="5e9cb-290">Now, let's check out what happens on mobile devices:</span></span>

    <span data-ttu-id="5e9cb-291">![在左側，頁面會套用 @media 樣式，在右邊，會省略樣式](whats-new-in-aspnet-mvc-4/_static/image18.png "在左側，頁面會套用 @media 樣式，在右邊，會省略樣式")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-291">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image18.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="5e9cb-292">*在左側，頁面會套用 @media 樣式，在右邊，會省略樣式*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-292">*In the left, the page is applying the @media style, in the right, the style is omitted*</span></span>

    <span data-ttu-id="5e9cb-293">雖然您會注意到網頁在網頁瀏覽器中呈現時的變更並不重要，但在使用行動裝置時，差異變得更明顯。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-293">Although you will notice that the changes when the page is rendered in a Web browser are not very significant, when using a mobile device the differences become more obvious.</span></span> <span data-ttu-id="5e9cb-294">在影像的左邊，我們可以看到自訂樣式已改善可讀性。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-294">On the left side of the image, we can see that the custom style improved the readability.</span></span>

    <span data-ttu-id="5e9cb-295">彈性轉譯可以在許多案例中使用，讓您更輕鬆地將條件式樣式套用至網站，並使用整齊的方法解決常見的樣式問題。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-295">Adaptive rendering can be used in many more scenarios, making it easier to apply conditional styling to a Web site and solving common style issues with a neat approach.</span></span>

    <span data-ttu-id="5e9cb-296">「視口」中繼標記和 CSS 媒體查詢不是 ASP.NET MVC 4 特有的，因此您可以在任何 web 應用程式中利用這些功能。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-296">The Viewport meta tag and CSS media queries are not specific to ASP.NET MVC 4, so you can take advantage of these features in any web application.</span></span>
5. <span data-ttu-id="5e9cb-297">在 Visual Studio 中，按**SHIFT** + **F5**停止對應用程式的偵測。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-297">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a><span data-ttu-id="5e9cb-298">練習2：建立相片圖庫 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5e9cb-298">Exercise 2: Creating the Photo Gallery Web Application</span></span>

<span data-ttu-id="5e9cb-299">在此練習中，您將使用相片圖庫應用程式來顯示相片。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-299">In this exercise, you will work on a Photo Gallery application to display photos.</span></span> <span data-ttu-id="5e9cb-300">您將從 ASP.NET MVC 4 專案範本開始，然後新增功能以從服務抓取相片，並將其顯示在首頁中。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-300">You will start with the ASP.NET MVC 4 project template, and then you will add a feature to retrieve photos from a service and display them in the home page.</span></span>

<span data-ttu-id="5e9cb-301">在下列練習中，您將更新此解決方案，以增強其在行動裝置上的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-301">In the following exercise, you will update this solution to enhance the way it is displayed on mobile devices.</span></span>

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a><span data-ttu-id="5e9cb-302">工作 1-建立 Mock 相片服務</span><span class="sxs-lookup"><span data-stu-id="5e9cb-302">Task 1 - Creating a Mock Photo Service</span></span>

<span data-ttu-id="5e9cb-303">在這項工作中，您將建立相片服務的 mock，以抓取將顯示在資源庫中的內容。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-303">In this task, you will create a mock of the photo service to retrieve the content that will be displayed in the gallery.</span></span> <span data-ttu-id="5e9cb-304">若要這麼做，您將加入新的控制器，只會傳回包含每張相片資料的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-304">To do this, you will add a new controller that will simply return a JSON file with the data of each photo.</span></span>

1. <span data-ttu-id="5e9cb-305">開啟**Visual Studio** （如果尚未開啟）。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-305">Open **Visual Studio** if not already opened.</span></span>
2. <span data-ttu-id="5e9cb-306">選取檔案 **|新增 |[專案**] 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-306">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="5e9cb-307">在 [**新增專案**] 對話方塊中，**選取C#視覺效果 |** 在左窗格樹狀結構上，選擇 [ **ASP.NET MVC 4 Web 應用程式]。**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-307">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="5e9cb-308">將專案命名為**PhotoGallery**，選取位置（或保留預設值），然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-308">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span> <span data-ttu-id="5e9cb-309">或者，您可以繼續使用**練習 1**中現有的 ASP.NET MVC 4**網際網路應用程式**解決方案，並略過下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-309">Alternatively, you can continue working from your existing ASP.NET MVC 4 **Internet Application** solution from **Exercise 1** and skip the next step.</span></span>
3. <span data-ttu-id="5e9cb-310">在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**] 專案範本，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-310">In the **New ASP.NET MVC 4 Project** dialog box, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="5e9cb-311">請確定您已選取 Razor 做為 View Engine。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-311">Make sure you have Razor selected as the View Engine.</span></span>
4. <span data-ttu-id="5e9cb-312">在 **方案總管**中，以滑鼠右鍵按一下專案的**應用程式\_Data**  資料夾，然後選取 **新增 |現有的專案**。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-312">In the **Solution Explorer**, right-click the **App\_Data** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="5e9cb-313">流覽至此實驗室的**Source\Assets\App\_Data**資料夾，並新增**相片. json**檔案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-313">Browse to the **Source\Assets\App\_Data** folder of this lab and add the **Photos.json** file.</span></span>
5. <span data-ttu-id="5e9cb-314">建立名為**PhotoController**的新控制器。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-314">Create a new controller with the name **PhotoController**.</span></span> <span data-ttu-id="5e9cb-315">若要這麼做，請在 [**控制器**] 資料夾上按一下滑鼠右鍵，移至 [**新增**]，然後選取 [**控制器]。**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-315">To do this, right-click on the **Controllers** folder, go to **Add** and select **Controller.**</span></span> <span data-ttu-id="5e9cb-316">完成 [控制器名稱]，保留**空白的 [MVC 控制器**] 範本，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-316">Complete the controller name, leave the **Empty MVC controller** template and click **Add**.</span></span>

    <span data-ttu-id="5e9cb-317">![新增 PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "新增 PhotoController")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-317">![Adding the PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "Adding the PhotoController")</span></span>

    <span data-ttu-id="5e9cb-318">*新增 PhotoController*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-318">*Adding the PhotoController*</span></span>
6. <span data-ttu-id="5e9cb-319">以下列元件**庫**動作取代**Index**方法，並從您最近新增至專案的 JSON 檔案傳回內容。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-319">Replace the **Index** method with the following **Gallery** action, and return the content from the JSON file you have recently added to the project.</span></span>

    <span data-ttu-id="5e9cb-320">（程式碼片段- *ASP.NET MVC 4 Lab-Ex02-圖庫動作*）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-320">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Gallery Action*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. <span data-ttu-id="5e9cb-321">按**F5**執行解決方案，然後流覽至下列 URL，以測試模擬相片服務： `http://localhost:[port]/photo/gallery` （[埠] 值取決於啟動應用程式的目前埠）。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-321">Press **F5** to run the solution, and then browse to the following URL in order to test the mocked photo service: `http://localhost:[port]/photo/gallery` (the [port] value depends on the current port where the application was launched).</span></span> <span data-ttu-id="5e9cb-322">此 URL 的要求應該會抓取**相片. json**檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-322">The request to this URL should retrieve the content of the **Photos.json** file.</span></span>

    <span data-ttu-id="5e9cb-323">![測試模擬相片服務](whats-new-in-aspnet-mvc-4/_static/image20.png "測試模擬相片服務")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-323">![Testing the mocked photo service](whats-new-in-aspnet-mvc-4/_static/image20.png "Testing the mocked photo service")</span></span>

    <span data-ttu-id="5e9cb-324">*測試模擬相片服務*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-324">*Testing the mocked photo service*</span></span>

<span data-ttu-id="5e9cb-325">在實際的執行中，您可以使用[ASP.NET Web API](../../../../web-api/index.md)來執行相片圖庫服務。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-325">In a real implementation you could use [ASP.NET Web API](../../../../web-api/index.md) to implement the Photo Gallery service.</span></span> <span data-ttu-id="5e9cb-326">ASP.NET Web API 是一種架構，可讓您輕鬆地建立可觸及各種用戶端（包括瀏覽器和行動裝置）的 HTTP 服務。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-326">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="5e9cb-327">ASP.NET Web 應用程式開發介面是在 .NET Framework 上建置 RESTful 應用程式的理想平台。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-327">ASP.NET Web API is an ideal platform for building RESTful applications on the .NET Framework.</span></span>

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a><span data-ttu-id="5e9cb-328">工作 2-顯示相片圖庫</span><span class="sxs-lookup"><span data-stu-id="5e9cb-328">Task 2 - Displaying the Photo Gallery</span></span>

<span data-ttu-id="5e9cb-329">在這項工作中，您將使用在本練習的第一個工作中建立的模擬服務，更新首頁以顯示相片圖庫。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-329">In this task, you will update the Home page to show the photo gallery by using the mocked service you created in the first task of this exercise.</span></span> <span data-ttu-id="5e9cb-330">您將會新增模型檔案，並更新資源庫視圖。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-330">You will add model files and update the gallery views.</span></span>

1. <span data-ttu-id="5e9cb-331">在 Visual Studio 中，按**SHIFT** + **F5**停止對應用程式的偵測。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-331">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="5e9cb-332">在 [**模型**] 資料夾中建立**相片**類別。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-332">Create the **Photo** class in the **Models** folder.</span></span> <span data-ttu-id="5e9cb-333">若要這麼做，請在 [**模型**] 資料夾上按一下滑鼠右鍵，選取 [**新增**]，然後按一下 [**類別**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-333">To do this, right-click on the **Models** folder, select **Add** and click **Class**.</span></span> <span data-ttu-id="5e9cb-334">然後，將名稱設定為**Photo.cs** ，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-334">Then, set the name to **Photo.cs** and click **Add**.</span></span>
3. <span data-ttu-id="5e9cb-335">將下列成員新增至**Photo**類別。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-335">Add the following members to the **Photo** class.</span></span>

    <span data-ttu-id="5e9cb-336">（程式碼片段- *ASP.NET MVC 4 Lab-Ex02-相片 model*）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-336">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo model*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. <span data-ttu-id="5e9cb-337">從 **Controllers** 資料夾中，開啟 **HomeController.cs** 檔案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-337">Open the **HomeController.cs** file from the **Controllers** folder.</span></span>
5. <span data-ttu-id="5e9cb-338">使用陳述式加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-338">Add the following using statements.</span></span>

    <span data-ttu-id="5e9cb-339">（程式碼片段- *ASP.NET MVC 4 Lab-Ex02-HomeController using*）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-339">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - HomeController Usings*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. <span data-ttu-id="5e9cb-340">更新 [**索引**] 動作，以使用**HttpClient**來抓取圖庫資料，然後使用**JavaScriptSerializer**將它還原序列化為視圖模型。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-340">Update the **Index** action to use **HttpClient** to retrieve the gallery data, and then use the **JavaScriptSerializer** to deserialize it to the view model.</span></span>

    <span data-ttu-id="5e9cb-341">（程式碼片段- *ASP.NET MVC 4 實驗室-Ex02-索引動作*）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-341">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Index Action*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. <span data-ttu-id="5e9cb-342">開啟位於**Views\Home**資料夾底下的**Index. cshtml**檔案，並以下列程式碼取代所有內容。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-342">Open the **Index.cshtml** file located under the **Views\Home** folder and replace all the content with the following code.</span></span>

    <span data-ttu-id="5e9cb-343">此程式碼會在所有從服務中取出的相片上執行迴圈，並將其顯示為未排序清單。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-343">This code loops through all the photos retrieved from the service and displays them into an unordered list.</span></span>

    <span data-ttu-id="5e9cb-344">（程式碼片段- *ASP.NET MVC 4 實驗室-Ex02-相片清單*）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-344">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo List*)</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. <span data-ttu-id="5e9cb-345">在 **方案總管**中，以滑鼠右鍵按一下專案的 **內容** 資料夾，然後選取 **新增 |現有的專案**。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-345">In the **Solution Explorer**, right-click the **Content** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="5e9cb-346">流覽至此實驗室的 [ **Source\Assets\Content** ] 資料夾，然後新增 [**網站 .css** ] 檔案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-346">Browse to the **Source\Assets\Content** folder of this lab and add the **Site.css** file.</span></span> <span data-ttu-id="5e9cb-347">您將必須確認其取代。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-347">You will have to confirm its replacement.</span></span> <span data-ttu-id="5e9cb-348">如果您已開啟**網站 .css**檔案，就必須確認是否也要重載檔案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-348">If you have the **Site.css** file open, you will have to confirm to reload the file also.</span></span>
9. <span data-ttu-id="5e9cb-349">開啟 [檔案瀏覽器]，然後將位於此實驗室的 [ **Source\Assets** ] 資料夾底下的整個**相片**資料夾，複製到方案總管中專案的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-349">Open File Explorer and copy the entire **Photos** folder located under the **Source\Assets** folder of this lab to the root folder of your project in Solution Explorer.</span></span>
10. <span data-ttu-id="5e9cb-350">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-350">Run the application.</span></span> <span data-ttu-id="5e9cb-351">您現在應該會在圖庫中看到顯示相片的首頁。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-351">You should now see the home page displaying the photos in the gallery.</span></span>

    <span data-ttu-id="5e9cb-352">![相片圖庫](whats-new-in-aspnet-mvc-4/_static/image21.png "相片圖庫")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-352">![Photo Gallery](whats-new-in-aspnet-mvc-4/_static/image21.png "Photo Gallery")</span></span>

    <span data-ttu-id="5e9cb-353">*相片圖庫*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-353">*Photo Gallery*</span></span>
11. <span data-ttu-id="5e9cb-354">在 Visual Studio 中，按**SHIFT** + **F5**停止對應用程式的偵測。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-354">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a><span data-ttu-id="5e9cb-355">練習3：新增行動裝置的支援</span><span class="sxs-lookup"><span data-stu-id="5e9cb-355">Exercise 3: Adding support for mobile devices</span></span>

<span data-ttu-id="5e9cb-356">ASP.NET MVC 4 中的其中一個重要更新是行動裝置開發的支援。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-356">One of the key updates in ASP.NET MVC 4 is the support for mobile development.</span></span> <span data-ttu-id="5e9cb-357">在此練習中，您將藉由擴充您在上一個練習中建立的 PhotoGallery 解決方案，探索行動應用程式的 ASP.NET MVC 4 新功能。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-357">In this exercise, you will explore ASP.NET MVC 4 new features for mobile applications by extending the PhotoGallery solution you have created in the previous exercise.</span></span>

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a><span data-ttu-id="5e9cb-358">工作 1-在 ASP.NET MVC 4 應用程式中安裝 jQuery Mobile</span><span class="sxs-lookup"><span data-stu-id="5e9cb-358">Task 1 - Installing jQuery Mobile in an ASP.NET MVC 4 Application</span></span>

1. <span data-ttu-id="5e9cb-359">開啟位於**來源/Ex3-MobileSupport/開始/** 資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-359">Open the **Begin** solution located at **Source/Ex3-MobileSupport/Begin/** folder.</span></span> <span data-ttu-id="5e9cb-360">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-360">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="5e9cb-361">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-361">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="5e9cb-362">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-362">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="5e9cb-363">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-363">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="5e9cb-364">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-364">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="5e9cb-365">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-365">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="5e9cb-366">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-366">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="5e9cb-367">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-367">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="5e9cb-368">按一下 **工具** >  **NuGet 套件管理員** > **套件管理員主控台** 功能表選項，以開啟 **套件管理員主控台**。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-368">Open the **Package Manager Console** by clicking the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu option.</span></span>

    <span data-ttu-id="5e9cb-369">![開啟 NuGet 套件管理員主控台](whats-new-in-aspnet-mvc-4/_static/image22.png "開啟 NuGet 套件管理員主控台")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-369">![Opening the NuGet Package Manager Console](whats-new-in-aspnet-mvc-4/_static/image22.png "Opening the NuGet Package Manager Console")</span></span>

    <span data-ttu-id="5e9cb-370">*開啟 NuGet 套件管理員主控台*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-370">*Opening the NuGet Package Manager Console*</span></span>
3. <span data-ttu-id="5e9cb-371">在 [套件管理員主控台] 中，執行下列命令以安裝**jQuery.** node.js 封裝。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-371">In the Package Manager Console run the following command to install the **jQuery.Mobile.MVC** package.</span></span>

    <span data-ttu-id="5e9cb-372">jQuery Mobile 是一種開放原始碼程式庫，可用於建立觸控式優化的 web UI。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-372">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="5e9cb-373">JQuery NuGet 套件包含協助程式搭配 ASP.NET MVC 4 應用程式使用 jQuery Mobile。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-373">The jQuery.Mobile.MVC NuGet package includes helpers to use jQuery Mobile with an ASP.NET MVC 4 application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e9cb-374">藉由執行下列命令，您將會從 Nuget 下載 jQuery. MVC 程式庫。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-374">By running the following command, you will be downloading the jQuery.Mobile.MVC library from Nuget.</span></span>

    <span data-ttu-id="5e9cb-375">PM</span><span class="sxs-lookup"><span data-stu-id="5e9cb-375">PM</span></span>

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    <span data-ttu-id="5e9cb-376">此命令會安裝 jQuery Mobile 和一些 helper 檔案，包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="5e9cb-376">This command installs jQuery Mobile and some helper files, including the following:</span></span>

    - <span data-ttu-id="5e9cb-377">**Views/Shared/\_Layout**：是以 jQuery mobile 為基礎的版面配置，針對較小的螢幕進行優化。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-377">**Views/Shared/\_Layout.Mobile.cshtml**: is a jQuery Mobile-based layout optimized for a smaller screen.</span></span> <span data-ttu-id="5e9cb-378">當網站從行動瀏覽器收到要求時，會將原始配置（\_Layout）取代為此配置。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-378">When the website receives a request from a mobile browser, it will replace the original layout (\_Layout.cshtml) with this one.</span></span>
    - <span data-ttu-id="5e9cb-379">View-切換器元件：由**Views/Shared/\_ViewSwitcher**部分視圖和**ViewSwitcherController.cs**控制器所組成。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-379">A view-switcher component: consists of the **Views/Shared/\_ViewSwitcher.cshtml** partial view and the **ViewSwitcherController.cs** controller.</span></span> <span data-ttu-id="5e9cb-380">此元件會在行動瀏覽器上顯示連結，讓使用者切換到桌上出版本的頁面。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-380">This component will show a link on mobile browsers to enable users to switch to the desktop version of the page.</span></span>  
        <span data-ttu-id="5e9cb-381">![具有行動支援的相片圖庫專案](whats-new-in-aspnet-mvc-4/_static/image23.png "Ph具有行動支援的 oto 資源庫專案 "）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-381">![Photo Gallery project with mobile support](whats-new-in-aspnet-mvc-4/_static/image23.png "Photo Gallery project with mobile support")</span></span>

        <span data-ttu-id="5e9cb-382">*具有行動支援的相片圖庫專案*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-382">*Photo Gallery project with mobile support*</span></span>
4. <span data-ttu-id="5e9cb-383">註冊行動套件組合。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-383">Register the Mobile bundles.</span></span> <span data-ttu-id="5e9cb-384">若要這麼做，請開啟**Global.asax.cs**檔案，並新增下列這一行。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-384">To do this, open the **Global.asax.cs** file and add the following line.</span></span>

    <span data-ttu-id="5e9cb-385">（程式碼片段- *ASP.NET MVC 4 Lab-Ex03-註冊*行動套件組合）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-385">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - Register Mobile Bundles*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. <span data-ttu-id="5e9cb-386">使用桌面 web 瀏覽器執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-386">Run the application using a desktop web browser.</span></span>
6. <span data-ttu-id="5e9cb-387">開啟位於 [開始] 功能表中的 [ **Windows Phone 7 模擬器**] **|所有程式 |Windows Phone SDK 7.1 |Windows Phone 模擬器。**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-387">Open the **Windows Phone 7 Emulator,** located in **Start Menu | All Programs | Windows Phone SDK 7.1 | Windows Phone Emulator.**</span></span>
7. <span data-ttu-id="5e9cb-388">在手機的 [開始] 畫面中，開啟 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-388">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="5e9cb-389">查看應用程式啟動的 URL，並使用電話瀏覽器流覽至該 URL （例如 `http://localhost:[PortNumber]/`）。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-389">Check out the URL where the application started and browse to that URL with the phone browser (e.g. `http://localhost:[PortNumber]/`).</span></span>

    <span data-ttu-id="5e9cb-390">您會注意到，在 Windows Phone 模擬器中，您的應用程式看起來會不同，因為 jQuery 會在專案中建立新的資產，以顯示針對行動裝置優化的視圖。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-390">You will notice that your application will look different in the Windows Phone emulator, as the jQuery.Mobile.MVC has created new assets in your project that show views optimized for mobile devices.</span></span>

    <span data-ttu-id="5e9cb-391">請注意電話頂端的訊息，其中會顯示切換到桌面視圖的連結。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-391">Notice the message at the top of the phone, showing the link that switches to the Desktop view.</span></span> <span data-ttu-id="5e9cb-392">此外，您已安裝之封裝所建立的 **\_配置。** 在應用程式中包含不同的版面配置。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-392">Additionally, the **\_Layout.Mobile.cshtml** layout that was created by the package you have installed is including a different layout in the application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e9cb-393">到目前為止，沒有可回到 mobile view 的連結。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-393">So far, there is no link to get back to mobile view.</span></span> <span data-ttu-id="5e9cb-394">這會包含在較新的版本中。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-394">It will be included in later versions.</span></span>

    <span data-ttu-id="5e9cb-395">![[相片圖庫] 首頁的 [移動流覽]](whats-new-in-aspnet-mvc-4/_static/image24.png "[相片圖庫] 首頁的 [移動流覽]")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-395">![Mobile view of the Photo Gallery Home page](whats-new-in-aspnet-mvc-4/_static/image24.png "Mobile view of the Photo Gallery Home page")</span></span>

    <span data-ttu-id="5e9cb-396">*[相片圖庫] 首頁的 [移動流覽]*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-396">*Mobile view of the Photo Gallery Home page*</span></span>
8. <span data-ttu-id="5e9cb-397">在 Visual Studio 中，按**SHIFT** + **F5**停止對應用程式的偵測。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-397">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a><span data-ttu-id="5e9cb-398">工作 2-建立行動裝置視圖</span><span class="sxs-lookup"><span data-stu-id="5e9cb-398">Task 2 - Creating Mobile Views</span></span>

<span data-ttu-id="5e9cb-399">在這項工作中，您將建立索引視圖的行動版，並將內容調整為可在行動裝置中更佳的外觀。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-399">In this task, you will create a mobile version of the index view with content adapted for better appearance in mobile devices.</span></span>

1. <span data-ttu-id="5e9cb-400">複製 [ **Views\Home\Index.cshtml** ] 視圖並貼上以建立複本，並將新檔案重新**命名為 [.]** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-400">Copy the **Views\Home\Index.cshtml** view and paste it to create a copy, rename the new file to **Index.Mobile.cshtml**.</span></span>
2. <span data-ttu-id="5e9cb-401">開啟新建立的 [node.js **] 視圖，** 並使用此程式碼取代現有的 &lt;ul&gt; 標記。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-401">Open the new created **Index.Mobile.cshtml** view and replace the existing &lt;ul&gt; tag with this code.</span></span> <span data-ttu-id="5e9cb-402">如此一來，您將會使用 jQuery Mobile 資料批註來更新 &lt;ul&gt; 標記，以使用 jQuery 中的行動主題。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-402">By doing this, you will be updating the &lt;ul&gt; tag with jQuery Mobile data annotations to use the mobile themes from jQuery.</span></span>

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > <span data-ttu-id="5e9cb-403">請注意：</span><span class="sxs-lookup"><span data-stu-id="5e9cb-403">Notice that:</span></span>
    > 
    > - <span data-ttu-id="5e9cb-404">設定為**listview**的**資料角色**屬性會使用 listview 樣式來轉譯清單。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-404">The **data-role** attribute set to **listview** will render the list using the listview styles.</span></span>
    > 
    > - <span data-ttu-id="5e9cb-405">**資料-內陷**屬性設為 true 時，會顯示具有圓角框線和邊界的清單。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-405">The **data-inset** attribute set to true will show the list with rounded border and margin.</span></span>
    > 
    > - <span data-ttu-id="5e9cb-406">設定為**true**的**資料篩選**屬性會產生搜尋方塊。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-406">The **data-filter** attribute set to **true** will generate a search box.</span></span>
    > 
    > <span data-ttu-id="5e9cb-407">您可以在專案檔案中深入瞭解 jQuery Mobile 慣例： [ [http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span><span class="sxs-lookup"><span data-stu-id="5e9cb-407">You can learn more about jQuery Mobile conventions in the project documentation: [[http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span></span>
3. <span data-ttu-id="5e9cb-408">按**CTRL + S**儲存變更。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-408">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="5e9cb-409">切換至**Windows Phone 模擬器**並重新整理網站。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-409">Switch to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="5e9cb-410">請注意，圖庫清單的新外觀與風格，以及位於頂端的新搜尋方塊。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-410">Notice the new look and feel of the gallery list, as well as the new search box located on the top.</span></span> <span data-ttu-id="5e9cb-411">然後在 [搜尋] 方塊中輸入一個字（例如， **Tulips**），以在相片圖庫中開始搜尋。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-411">Then, type a word in the search box (for instance, **Tulips**) to start a search in the photo gallery.</span></span>

    <span data-ttu-id="5e9cb-412">![使用 listview 樣式搭配篩選的資源庫](whats-new-in-aspnet-mvc-4/_static/image25.png "使用 listview 樣式搭配篩選的資源庫")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-412">![Gallery using listview style with filtering](whats-new-in-aspnet-mvc-4/_static/image25.png "Gallery using listview style with filtering")</span></span>

    <span data-ttu-id="5e9cb-413">*使用 listview 樣式搭配篩選的資源庫*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-413">*Gallery using listview style with filtering*</span></span>

    <span data-ttu-id="5e9cb-414">總而言之，您已使用 View Mobilizer 配方，以 &quot;mobile&quot; 尾碼來建立索引視圖的複本。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-414">To summarize, you have used the View Mobilizer recipe to create a copy of the Index view with the &quot;mobile&quot; suffix.</span></span> <span data-ttu-id="5e9cb-415">這個尾碼表示 ASP.NET MVC 4，從行動裝置產生的每個要求都會使用此索引複本。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-415">This suffix indicates to ASP.NET MVC 4 that every request generated from a mobile device will use this copy of the index.</span></span> <span data-ttu-id="5e9cb-416">此外，您已更新索引視圖的行動版，以使用 jQuery Mobile 來增強行動裝置中的網站外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-416">Additionally, you have updated the mobile version of the Index view to use jQuery Mobile for enhancing the site look and feel in mobile devices.</span></span>
5. <span data-ttu-id="5e9cb-417">返回 Visual Studio**並開啟位於** **Content**資料夾底下的 node.js。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-417">Go back to Visual Studio and open **Site.Mobile.css** located under the **Content** folder.</span></span>
6. <span data-ttu-id="5e9cb-418">修正相片標題的位置，使其顯示在影像的右側。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-418">Fix the positioning of the photo title to make it show at the right side of the image.</span></span> <span data-ttu-id="5e9cb-419">若要這麼做，請將下列程式碼新增至 node.js**檔案。**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-419">To do this, add the following code to the **Site.Mobile.css** file.</span></span>

    <span data-ttu-id="5e9cb-420">CSS</span><span class="sxs-lookup"><span data-stu-id="5e9cb-420">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. <span data-ttu-id="5e9cb-421">按**CTRL + S**儲存變更。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-421">Press **CTRL + S** to save the changes.</span></span>
8. <span data-ttu-id="5e9cb-422">切換回**Windows Phone 模擬器**並重新整理網站。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-422">Switch back to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="5e9cb-423">請注意，相片標題現在已正確定位。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-423">Notice the photo title is properly positioned now.</span></span>

    <span data-ttu-id="5e9cb-424">![標題位於影像右邊](whats-new-in-aspnet-mvc-4/_static/image26.png "標題位於影像右邊")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-424">![Title positioned on the right side of the image](whats-new-in-aspnet-mvc-4/_static/image26.png "Title positioned on the right side of the image")</span></span>

    <span data-ttu-id="5e9cb-425">*標題位於影像右邊*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-425">*Title positioned on the right side of the image*</span></span>

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a><span data-ttu-id="5e9cb-426">工作 3-jQuery Mobile 主題</span><span class="sxs-lookup"><span data-stu-id="5e9cb-426">Task 3 - jQuery Mobile Themes</span></span>

<span data-ttu-id="5e9cb-427">JQuery Mobile 中的每個版面配置和小工具都是針對新的物件導向 CSS 架構所設計，可讓您將完整的統一視覺效果設計主題套用至網站和應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-427">Every layout and widget in jQuery Mobile is designed around a new object-oriented CSS framework that makes it possible to apply a complete unified visual design theme to sites and applications.</span></span>

<span data-ttu-id="5e9cb-428">jQuery Mobile 的預設主題包含5個以字母（a、b、c、d、e）提供的色板，以供快速參考。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-428">jQuery Mobile's default Theme includes 5 swatches that are given letters (a, b, c, d, e) for quick reference.</span></span>

<span data-ttu-id="5e9cb-429">在這項工作中，您將更新行動配置，以使用與預設不同的主題。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-429">In this task, you will update the mobile layout to use a different theme than the default.</span></span>

1. <span data-ttu-id="5e9cb-430">切換回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-430">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="5e9cb-431">開啟位於**Views\Shared**的 **\_Layout**檔案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-431">Open the **\_Layout.Mobile.cshtml** file located in **Views\Shared**.</span></span>
3. <span data-ttu-id="5e9cb-432">尋找 資料-角色 設定為 &quot; 頁面上的 div 元素&quot; 並將**資料主題**更新為 &quot;**e**&quot;。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-432">Find the div element with the data-role set to &quot;page&quot; and update the **data-theme** to &quot;**e**&quot;.</span></span>

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. <span data-ttu-id="5e9cb-433">按**CTRL + S**儲存變更。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-433">Press **CTRL + S** to save the changes.</span></span>
5. <span data-ttu-id="5e9cb-434">重新整理**Windows Phone 模擬器**中的網站，並注意新的色彩配置。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-434">Refresh the site in the **Windows Phone Emulator** and notice the new colors scheme.</span></span>

    <span data-ttu-id="5e9cb-435">![使用不同色彩配置的行動裝置版面配置](whats-new-in-aspnet-mvc-4/_static/image27.png "使用不同色彩配置的行動裝置版面配置")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-435">![Mobile layout with a different color scheme](whats-new-in-aspnet-mvc-4/_static/image27.png "Mobile layout with a different color scheme")</span></span>

    <span data-ttu-id="5e9cb-436">*使用不同色彩配置的行動裝置版面配置*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-436">*Mobile layout with a different color scheme*</span></span>

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a><span data-ttu-id="5e9cb-437">工作 4-使用視圖切換器元件和瀏覽器覆寫功能</span><span class="sxs-lookup"><span data-stu-id="5e9cb-437">Task 4 - Using the View-Switcher Component and the Browser Overriding Features</span></span>

<span data-ttu-id="5e9cb-438">行動優化網頁的慣例是加入一個連結，其文字類似于桌面視圖或完整網站模式，可讓使用者切換至桌上出版本的頁面。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-438">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="5e9cb-439">JQuery 封裝包含用於 **\_** 配置中的這個用途的範例**視圖切換**器元件。請參閱。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-439">The jQuery.Mobile.MVC package includes a sample **view-switcher** component for this purpose used in the **\_Layout.Mobile.cshtml** view.</span></span>

<span data-ttu-id="5e9cb-440">![切換至桌面視圖的連結](whats-new-in-aspnet-mvc-4/_static/image28.png "切換至桌面視圖的連結")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-440">![Link to switch to Desktop View](whats-new-in-aspnet-mvc-4/_static/image28.png "Link to switch to Desktop View")</span></span>

<span data-ttu-id="5e9cb-441">*切換至桌面視圖的連結*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-441">*Link to switch to Desktop View*</span></span>

<span data-ttu-id="5e9cb-442">「視圖切換器」會使用稱為「**瀏覽器覆寫**」的新功能。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-442">The view switcher uses a new feature called **Browser Overriding**.</span></span> <span data-ttu-id="5e9cb-443">這項功能可讓您的應用程式將要求視為來自不同的瀏覽器（使用者代理程式），而不是實際的來源。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-443">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they are actually coming from.</span></span>

<span data-ttu-id="5e9cb-444">在這項工作中，您將探索 jQuery 所新增之視圖切換器的範例執行，以及覆寫 ASP.NET MVC 4 中功能的新瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-444">In this task, you will explore the sample implementation of a view-switcher added by jQuery.Mobile.MVC and the new browser overriding features in ASP.NET MVC 4.</span></span>

1. <span data-ttu-id="5e9cb-445">切換回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-445">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="5e9cb-446">開啟位於 [ **Views\Shared** ] 資料夾底下的 [ **\_** 配置]，並注意被參考為部分視圖的視圖切換器元件。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-446">Open the **\_Layout.Mobile.cshtml** view located under the **Views\Shared** folder and notice the view-switcher component being referenced as a partial view.</span></span>

    <span data-ttu-id="5e9cb-447">![使用視圖切換器元件的行動版面配置](whats-new-in-aspnet-mvc-4/_static/image29.png "使用視圖切換器元件的行動版面配置")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-447">![Mobile layout using View-Switcher component](whats-new-in-aspnet-mvc-4/_static/image29.png "Mobile layout using View-Switcher component")</span></span>

    <span data-ttu-id="5e9cb-448">*使用視圖切換器元件的行動版面配置*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-448">*Mobile layout using View-Switcher component*</span></span>
3. <span data-ttu-id="5e9cb-449">開啟 [ **\_ViewSwitcher** ] [部分視圖]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-449">Open the **\_ViewSwitcher.cshtml** partial view.</span></span>

    <span data-ttu-id="5e9cb-450">部分視圖會使用 ViewCoNtext 的新方法**GetOverriddenBrowser （）** 來判斷 web 要求的來源，並顯示對應的連結以切換到桌面或行動裝置的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-450">The partial view uses the new method **ViewContext.HttpContext.GetOverriddenBrowser()** to determine the origin of the web request and show the corresponding link to switch either to the Desktop or Mobile views.</span></span>

    <span data-ttu-id="5e9cb-451">**GetOverriddenBrowser**方法會傳回**HttpBrowserCapabilitiesBase**實例，其對應至目前針對要求所設定的使用者代理程式（實際或已覆寫）。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-451">The **GetOverriddenBrowser** method returns an **HttpBrowserCapabilitiesBase** instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="5e9cb-452">您可以使用這個值來取得**IsMobileDevice**之類的屬性。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-452">You can use this value to get properties such as **IsMobileDevice**.</span></span>

    <span data-ttu-id="5e9cb-453">![ViewSwitcher 部分視圖](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher 部分視圖")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-453">![ViewSwitcher partial view](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher partial view")</span></span>

    <span data-ttu-id="5e9cb-454">*ViewSwitcher 部分視圖*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-454">*ViewSwitcher partial view*</span></span>
4. <span data-ttu-id="5e9cb-455">開啟位於 [**控制器**] 資料夾中的**ViewSwitcherController.cs**類別。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-455">Open the **ViewSwitcherController.cs** class located in the **Controllers** folder.</span></span> <span data-ttu-id="5e9cb-456">查看 ViewSwitcher 元件中的連結所呼叫的 SwitchView 動作，並注意新的 HttpCoNtext 方法。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-456">Check out that SwitchView action is called by the link in the ViewSwitcher component, and notice the new HttpContext methods.</span></span>

    - <span data-ttu-id="5e9cb-457">**ClearOverriddenBrowser （）** 方法會移除目前要求的任何已覆寫使用者代理程式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-457">The **HttpContext.ClearOverriddenBrowser()** method removes any overridden user agent for the current request.</span></span>
    - <span data-ttu-id="5e9cb-458">**SetOverriddenBrowser （）** 方法會使用指定的使用者代理程式，覆寫要求的實際使用者代理程式值。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-458">The **HttpContext.SetOverriddenBrowser()** method overrides the request's actual user agent value using the specified user agent.</span></span>  
        <span data-ttu-id="5e9cb-459">![ViewSwitcher 控制器](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher 控制器」）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-459">![ViewSwitcher Controller](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher Controller")</span></span>  
<span data-ttu-id="5e9cb-460">*ViewSwitcher 控制器*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-460">*ViewSwitcher Controller*</span></span>

        <span data-ttu-id="5e9cb-461">瀏覽器覆寫是 ASP.NET MVC 4 的核心功能，即使您未安裝 jQuery. node.js 封裝也可以使用。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-461">Browser Overriding is a core feature of ASP.NET MVC 4, which is also available even if you do not install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="5e9cb-462">不過，這項功能只會影響視圖、版面配置和部分查看，而且不會影響任何相依于要求的功能。 Browser 物件。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-462">However, this feature affects only view, layout, and partial-view, and it does not affect any of the features that depend on the Request.Browser object.</span></span>

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a><span data-ttu-id="5e9cb-463">工作 5-在桌面視圖中新增視圖切換器</span><span class="sxs-lookup"><span data-stu-id="5e9cb-463">Task 5 - Adding the View-Switcher in the Desktop View</span></span>

<span data-ttu-id="5e9cb-464">在這項工作中，您將更新桌上出版面配置以包含視圖切換器。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-464">In this task, you will update the desktop layout to include the view-switcher.</span></span> <span data-ttu-id="5e9cb-465">這可讓行動使用者在流覽桌面視圖時回到行動視圖。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-465">This will allow mobile users to go back to the mobile view when browsing the desktop view.</span></span>

1. <span data-ttu-id="5e9cb-466">重新整理**Windows Phone 模擬器**中的網站。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-466">Refresh the site in the **Windows Phone Emulator**.</span></span>
2. <span data-ttu-id="5e9cb-467">按一下資源庫頂端的 [**桌面視圖**] 連結。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-467">Click on the **Desktop view** link at the top of the gallery.</span></span> <span data-ttu-id="5e9cb-468">請注意，桌上型電腦視圖中沒有任何視圖切換器可讓您返回行動裝置視圖。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-468">Notice there is no view-switcher in the desktop view to allow you return to the mobile view.</span></span>
3. <span data-ttu-id="5e9cb-469">返回 Visual Studio，然後開啟 [ **\_Layout** ] 視圖。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-469">Go back to Visual Studio and open the **\_Layout.cshtml** view.</span></span>
4. <span data-ttu-id="5e9cb-470">尋找 [登入] 區段，然後插入呼叫，將 **\_ViewSwitcher**部分視圖轉譯 **\_LogOnPartial**部分視圖底下。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-470">Find the login section and insert a call to render the **\_ViewSwitcher** partial view below the **\_LogOnPartial** partial view.</span></span> <span data-ttu-id="5e9cb-471">然後，按**CTRL + S**儲存變更。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-471">Then, press **CTRL + S** to save the changes.</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. <span data-ttu-id="5e9cb-472">按**CTRL + S**儲存變更。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-472">Press **CTRL + S** to save the changes.</span></span>
6. <span data-ttu-id="5e9cb-473">重新整理 Windows Phone 模擬器中的頁面，然後按兩下畫面以放大。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-473">Refresh the page in the Windows Phone Emulator and double-click the screen to zoom in.</span></span> <span data-ttu-id="5e9cb-474">請注意，[首頁] 頁面現在會顯示從 [行動裝置] 切換到 [桌面] 視圖的 [**移動流覽**] 連結。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-474">Notice that the home page now shows the **Mobile view** link that switches from mobile to desktop view.</span></span>

    <span data-ttu-id="5e9cb-475">![桌面視圖中呈現的視圖切換器](whats-new-in-aspnet-mvc-4/_static/image32.png "桌面視圖中呈現的視圖切換器")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-475">![View Switcher rendered in desktop view](whats-new-in-aspnet-mvc-4/_static/image32.png "View Switcher rendered in desktop view")</span></span>

    <span data-ttu-id="5e9cb-476">*桌面視圖中呈現的視圖切換器*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-476">*View Switcher rendered in desktop view*</span></span>
7. <span data-ttu-id="5e9cb-477">再次切換到行動裝置視圖，然後流覽至 [**關於**] 頁面（ http://localhost [埠]/Home/About）。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-477">Switch to the Mobile view again and browse to **About** page (http://localhost[port]/Home/About).</span></span> <span data-ttu-id="5e9cb-478">請注意，即使您尚未建立 About. # view 視圖，[About] 頁面還是會使用行動配置（\_Layout）來顯示。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-478">Notice that, even if you haven't created an About.Mobile.cshtml view, the About page is displayed using the mobile layout (\_Layout.Mobile.cshtml).</span></span>

    <span data-ttu-id="5e9cb-479">![關於頁面](whats-new-in-aspnet-mvc-4/_static/image33.png "About 頁面")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-479">![About page](whats-new-in-aspnet-mvc-4/_static/image33.png "About page")</span></span>

    <span data-ttu-id="5e9cb-480">*關於頁面*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-480">*About page*</span></span>
8. <span data-ttu-id="5e9cb-481">最後，在桌面網頁瀏覽器中開啟網站。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-481">Finally, open the site in a desktop Web browser.</span></span> <span data-ttu-id="5e9cb-482">請注意，先前的更新都不會影響到桌面視圖。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-482">Notice that none of the previous updates has affected the desktop view.</span></span>

    <span data-ttu-id="5e9cb-483">![PhotoGallery 桌面視圖](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery 桌面視圖")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-483">![PhotoGallery desktop view](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery desktop view")</span></span>

    <span data-ttu-id="5e9cb-484">*PhotoGallery 桌面視圖*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-484">*PhotoGallery desktop view*</span></span>

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a><span data-ttu-id="5e9cb-485">工作 6-建立新的顯示模式</span><span class="sxs-lookup"><span data-stu-id="5e9cb-485">Task 6 - Creating New Display Modes</span></span>

<span data-ttu-id="5e9cb-486">新的顯示模式功能可讓應用程式根據產生要求的瀏覽器選取 views。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-486">The new display modes feature lets an application select views depending on the browser that is generating the request.</span></span> <span data-ttu-id="5e9cb-487">例如，如果桌面瀏覽器要求首頁，應用程式將會傳回**Views\Home\Index.cshtml**範本。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-487">For example, if a desktop browser requests the Home page, the application will return the **Views\Home\Index.cshtml** template.</span></span> <span data-ttu-id="5e9cb-488">然後，如果行動瀏覽器要求首頁，應用程式將會傳回**Views\Home\Index.mobile.cshtml**範本。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-488">Then, if a mobile browser requests the Home page, the application will return the **Views\Home\Index.mobile.cshtml** template.</span></span>

<span data-ttu-id="5e9cb-489">在這項工作中，您將建立 iPhone 裝置的自訂版面配置，而且您必須模擬 iPhone 裝置的要求。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-489">In this task, you will create a customized layout for iPhone devices, and you will have to simulate requests from iPhone devices.</span></span> <span data-ttu-id="5e9cb-490">若要執行這項操作，您可以使用 iPhone 模擬器/模擬器（例如[電動](http://www.electricplum.com/)行動模擬器）或具有修改使用者代理程式之附加元件的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-490">To do this, you can use either an iPhone emulator/simulator (like [Electric Mobile Simulator](http://www.electricplum.com/)) or a browser with add-ons that modify the user agent.</span></span> <span data-ttu-id="5e9cb-491">如需如何在 Safari 瀏覽器中設定使用者代理程式字串以模擬 iPhone 的指示，請參閱[如何讓 safari](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html)在 David Alison 的 blog 中偽裝成 IE。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-491">For instructions on how to set the user agent string in an Safari browser to emulate an iPhone, see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) in David Alison's blog.</span></span>

<span data-ttu-id="5e9cb-492">**請注意，這項工作是選擇性的，您可以在整個實驗室中繼續進行，而不需要執行它。**</span><span class="sxs-lookup"><span data-stu-id="5e9cb-492">**Notice that this task is optional and you can continue throughout the lab without executing it.**</span></span>

1. <span data-ttu-id="5e9cb-493">在 Visual Studio 中，按**SHIFT** + **F5**停止對應用程式的偵測。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-493">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="5e9cb-494">開啟**Global.asax.cs** ，並加入下列 using 語句。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-494">Open **Global.asax.cs** and add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. <span data-ttu-id="5e9cb-495">將下列反白顯示的程式碼新增至應用程式\_Start 方法。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-495">Add the following highlighted code into the Application\_Start method.</span></span>

    <span data-ttu-id="5e9cb-496">（程式碼片段- *ASP.NET MVC 4 Lab-Ex03-IPhone DisplayMode*）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-496">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - iPhone DisplayMode*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

<span data-ttu-id="5e9cb-497">您已在靜態**DisplayModeProvider**中註冊**名為 &quot;iPhone&quot;** 的新 DefaultDisplayMode，其將會針對每個連入要求進行比對。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-497">You have registered a new **DefaultDisplayMode named &quot;iPhone&quot;**, within the static **DisplayModeProvider.Instance.Modes** static list, that will be matched against each incoming request.</span></span> <span data-ttu-id="5e9cb-498">如果傳入要求包含 iPhone&quot;&quot;的字串，ASP.NET MVC 會尋找其名稱包含 &quot;iPhone&quot; 尾碼的視圖。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-498">If the incoming request contains the string &quot;iPhone&quot;, ASP.NET MVC will find the views whose name contain the &quot;iPhone&quot; suffix.</span></span> <span data-ttu-id="5e9cb-499">0參數表示新模式的特定方式。比方說，此視圖比一般 &quot;更明確。行動&quot; 規則符合來自行動裝置的要求。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-499">The 0 parameter indicates how specific is the new mode; for instance, this view is more specific than the general &quot;.mobile&quot; rule that matches requests from mobile devices.</span></span>

<span data-ttu-id="5e9cb-500">在此程式碼執行之後，當 iPhone 瀏覽器產生要求時，您的應用程式將會使用 Views\Shared\\您將在後續步驟中建立的 **_Layout. iPhone. cshtml**配置。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-500">After this code runs, when an iPhone browser generates a request, your application will use the **Views\Shared\\_Layout.iPhone.cshtml** layout you will create in the next steps.</span></span>

> [!NOTE]
> <span data-ttu-id="5e9cb-501">這種測試 iPhone 要求的方式已經簡化，以供示範之用，而且可能無法依每個 iPhone 使用者代理程式字串（例如測試區分大小寫）的預期運作。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-501">This way of testing the request for iPhone has been simplified for demo purposes and might not work as expected for every iPhone user agent string (for example test is case sensitive).</span></span>

4. <span data-ttu-id="5e9cb-502">在**Views\Shared**資料夾中建立 **\_Layout**檔案的複本，並將複本重新命名為 &quot; **\_Layout. cshtml**&quot;。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-502">Create a copy of the **\_Layout.Mobile.cshtml** file in the **Views\Shared** folder and rename the copy to &quot;**\_Layout.iPhone.cshtml**&quot;.</span></span>
5. <span data-ttu-id="5e9cb-503">開啟您在上一個步驟中建立的 **\_Layout. cshtml** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-503">Open **\_Layout.iPhone.cshtml** you created in the previous step.</span></span>
6. <span data-ttu-id="5e9cb-504">尋找 [資料-角色] 屬性設定為 [**頁面**] 的 div 元素，然後將 [**資料主題**] 屬性變更**為 &quot;&quot;** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-504">Find the div element with the data-role attribute set to **page** and change the **data-theme** attribute to &quot;**a**&quot;.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

<span data-ttu-id="5e9cb-505">您的 ASP.NET MVC 4 應用程式現在有3個版面配置：</span><span class="sxs-lookup"><span data-stu-id="5e9cb-505">Now you have 3 layouts in your ASP.NET MVC 4 application:</span></span>

1. <span data-ttu-id="5e9cb-506">**\_配置. cshtml**：用於桌面瀏覽器的預設版面配置。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-506">**\_Layout.cshtml**: default layout used for desktop browsers.</span></span>
2. <span data-ttu-id="5e9cb-507">**\_layout**：用於行動裝置的預設配置。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-507">**\_Layout.mobile.cshtml**: default layout used for mobile devices.</span></span>
3. <span data-ttu-id="5e9cb-508">**\_layout**： iphone 裝置的特定版面配置，使用不同的色彩配置來區別 \_的 layout。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-508">**\_Layout.iPhone.cshtml**: specific layout for iPhone devices, using a different color scheme to differentiate from \_Layout.mobile.cshtml.</span></span>
7. <span data-ttu-id="5e9cb-509">按**F5**以執行應用程式，並在**Windows Phone 模擬器**中流覽網站。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-509">Press **F5** to run the application and browse the site in the **Windows Phone Emulator**.</span></span>
8. <span data-ttu-id="5e9cb-510">開啟**iPhone**模擬器（如需有關如何安裝和設定 iPhone 模擬器的指示，請參閱[附錄 C](#AppendixC) ），並流覽至網站。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-510">Open an **iPhone simulator** (see [Appendix C](#AppendixC) for instructions on how to install and configure an iPhone simulator), and browse to the site too.</span></span> <span data-ttu-id="5e9cb-511">請注意，每個電話都會使用特定的範本。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-511">Notice that each phone is using the specific template.</span></span>

    ![使用-不同-views-每個 device2](whats-new-in-aspnet-mvc-4/_static/image35.png)

    <span data-ttu-id="5e9cb-513">*針對每個行動裝置使用不同的視圖*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-513">*Using different views for each mobile device*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a><span data-ttu-id="5e9cb-514">練習4：使用非同步控制器</span><span class="sxs-lookup"><span data-stu-id="5e9cb-514">Exercise 4: Using Asynchronous Controllers</span></span>

<span data-ttu-id="5e9cb-515">Microsoft .NET Framework 4.5 引進和 Visual Basic 中C#的新語言功能，以在 .net 程式設計中提供非同步新基礎。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-515">Microsoft .NET Framework 4.5 introduces new language features in C# and Visual Basic to provide a new foundation for asynchrony in .NET programming.</span></span> <span data-ttu-id="5e9cb-516">這個新的基礎使非同步程式設計類似-，而且與同步程式設計一樣簡單。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-516">This new foundation makes asynchronous programming similar to - and about as straightforward as - synchronous programming.</span></span> <span data-ttu-id="5e9cb-517">您現在可以使用**AsyncController**類別，在 ASP.NET MVC 4 中撰寫非同步動作方法。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-517">You are now able to write asynchronous action methods in ASP.NET MVC 4 by using the **AsyncController** class.</span></span> <span data-ttu-id="5e9cb-518">您可以針對長時間執行的非 CPU 系結要求使用非同步動作方法。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-518">You can use asynchronous action methods for long-running, non-CPU bound requests.</span></span> <span data-ttu-id="5e9cb-519">這可避免在處理要求時，阻止 Web 服務器執行工作。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-519">This avoids blocking the Web server from performing work while the request is being processed.</span></span> <span data-ttu-id="5e9cb-520">AsyncController 類別通常用於長時間執行的 Web 服務呼叫。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-520">The AsyncController class is typically used for long-running Web service calls.</span></span>

<span data-ttu-id="5e9cb-521">此練習說明 ASP.NET MVC 4 中非同步作業的基本概念。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-521">This exercise explains the basics of asynchronous operation in ASP.NET MVC 4.</span></span> <span data-ttu-id="5e9cb-522">如果您想要深入瞭解，您可以參閱下列文章： [ [https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="5e9cb-522">If you want a deeper dive, you can check out the following article: [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span></span>

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a><span data-ttu-id="5e9cb-523">工作 1-執行非同步控制器</span><span class="sxs-lookup"><span data-stu-id="5e9cb-523">Task 1 - Implementing an Asynchronous Controller</span></span>

1. <span data-ttu-id="5e9cb-524">開啟位於 [**來源/Ex4-非同步/開始/** 資料夾] 的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-524">Open the **Begin** solution located at **Source/Ex4-Async/Begin/** folder.</span></span> <span data-ttu-id="5e9cb-525">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-525">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="5e9cb-526">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-526">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="5e9cb-527">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-527">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="5e9cb-528">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-528">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="5e9cb-529">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-529">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="5e9cb-530">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-530">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="5e9cb-531">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-531">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="5e9cb-532">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-532">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="5e9cb-533">從 [**控制器**] 資料夾開啟**HomeController.cs**類別。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-533">Open the **HomeController.cs** class from the **Controllers** folder.</span></span>
3. <span data-ttu-id="5e9cb-534">新增下列 using 語句。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-534">Add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. <span data-ttu-id="5e9cb-535">更新**HomeController**類別以繼承自**AsyncController**。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-535">Update the **HomeController** class to inherit from **AsyncController**.</span></span> <span data-ttu-id="5e9cb-536">衍生自 AsyncController 的控制器可讓 ASP.NET 處理非同步要求，而且仍然可以服務同步動作方法。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-536">Controllers that derive from AsyncController enable ASP.NET to process asynchronous requests, and they can still service synchronous action methods.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. <span data-ttu-id="5e9cb-537">將**async**關鍵字新增至**Index**方法，使其傳回類型工作 **&lt;ActionResult&gt;** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-537">Add the **async** keyword to the **Index** method and make it return the type **Task&lt;ActionResult&gt;**.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > <span data-ttu-id="5e9cb-538">**Async**關鍵字是 .NET Framework 4.5 提供的其中一個新關鍵字;它會告知編譯器此方法包含非同步程式碼。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-538">The **async** keyword is one of the new keywords the .NET Framework 4.5 provides; it tells the compiler that this method contains asynchronous code.</span></span> <span data-ttu-id="5e9cb-539">**Task**物件代表可能在未來某個時間點完成的非同步作業。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-539">A **Task** object represents an asynchronous operation that may complete at some point in the future.</span></span>
6. <span data-ttu-id="5e9cb-540">取代**用戶端。** 使用 await 關鍵字以完整非同步版本呼叫 GetAsync （），如下所示。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-540">Replace the **client.GetAsync()** call with the full async version using await keyword as shown below.</span></span>

    <span data-ttu-id="5e9cb-541">（程式碼片段- *ASP.NET MVC 4 Lab-Ex04-GetAsync*）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-541">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - GetAsync*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="5e9cb-542">在先前的版本中，您使用**工作物件的** **Result**屬性來封鎖執行緒，直到傳回結果為止（同步處理版本）。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-542">In the previous version, you were using the **Result** property from the **Task** object to block the thread until the result is returned (sync version).</span></span>
    > 
    > <span data-ttu-id="5e9cb-543">新增**await**關鍵字會指示編譯器以非同步方式等候方法呼叫所傳回的工作。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-543">Adding the **await** keyword tells the compiler to asynchronously wait for the task returned from the method call.</span></span> <span data-ttu-id="5e9cb-544">這表示程式碼的其餘部分只會在等候的方法完成之後，以回呼的形式執行。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-544">This means that the rest of the code will be executed as a callback only after the awaited method completes.</span></span> <span data-ttu-id="5e9cb-545">另一個要注意的是，您不需要變更您的 try-catch 區塊來進行這項工作：在背景或前景中所發生的例外狀況仍會被攔截，而不需要使用架構所提供的處理常式進行任何額外的工作。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-545">Another thing to notice is that you do not need to change your try-catch block in order to make this work: the exceptions that happen in background or in foreground will still be caught without any extra work using a handler provided by the framework.</span></span>
7. <span data-ttu-id="5e9cb-546">將程式碼取代為新的程式碼，如下所示，藉以變更程式碼以繼續進行非同步執行</span><span class="sxs-lookup"><span data-stu-id="5e9cb-546">Change the code to continue with the asynchronous implementation by replacing the lines with the new code as shown below</span></span>

    <span data-ttu-id="5e9cb-547">（程式碼片段- *ASP.NET MVC 4 Lab-Ex04-ReadAsStringAsync*）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-547">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - ReadAsStringAsync*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. <span data-ttu-id="5e9cb-548">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-548">Run the application.</span></span> <span data-ttu-id="5e9cb-549">您會注意到沒有重大變更，但您的程式碼不會封鎖執行緒集區中的執行緒，讓伺服器資源的使用更好，並提升效能。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-549">You will notice no major changes, but your code will not block a thread from the thread pool making a better usage of the server resources and improving performance.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e9cb-550">您可以深入瞭解實驗室中新的非同步程式設計功能 &quot; **.net 4.5 中的非同步程式設計C# ，以及**Visual Studio 訓練套件中包含的 Visual Basic&quot;。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-550">You can learn more about the new asynchronous programming features in the lab &quot;**Asynchronous Programming in .NET 4.5 with C# and Visual Basic**&quot; included in the Visual Studio Training Kit.</span></span>

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a><span data-ttu-id="5e9cb-551">工作 2-使用解除標記處理超時</span><span class="sxs-lookup"><span data-stu-id="5e9cb-551">Task 2 - Handling Time-Outs with Cancellation Tokens</span></span>

<span data-ttu-id="5e9cb-552">傳回工作實例的非同步動作方法也可以支援超時。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-552">Asynchronous action methods that return Task instances can also support time-outs.</span></span> <span data-ttu-id="5e9cb-553">在這項工作中，您將會更新索引方法程式碼，以使用解除標記來處理超時案例。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-553">In this task, you will update the Index method code to handle a time-out scenario using a cancellation token.</span></span>

1. <span data-ttu-id="5e9cb-554">返回 Visual Studio，然後按**SHIFT + F5**停止調試。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-554">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>
2. <span data-ttu-id="5e9cb-555">將下列 using 語句新增至**HomeController.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-555">Add the following using statement to the **HomeController.cs** file.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. <span data-ttu-id="5e9cb-556">更新索引動作以接收**CancellationToken**引數。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-556">Update the Index action to receive a **CancellationToken** argument.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. <span data-ttu-id="5e9cb-557">更新**GetAsync**呼叫以傳遞解除標記。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-557">Update the **GetAsync** call to pass the cancellation token.</span></span>

    <span data-ttu-id="5e9cb-558">（程式碼片段- *ASP.NET MVC 4 Lab-Ex04-SendAsync With CancellationToken*）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-558">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - SendAsync with CancellationToken*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. <span data-ttu-id="5e9cb-559">將**AsyncTimeout**屬性設為500毫秒，並將**HandleError**屬性設定為藉由重新導向至**TimedOut**視圖來處理**TaskCanceledException** ，以裝飾*索引*方法。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-559">Decorate the *Index* method with an **AsyncTimeout** attribute set to 500 milliseconds and a **HandleError** attribute configured to handle **TaskCanceledException** by redirecting to a **TimedOut** view.</span></span>

    <span data-ttu-id="5e9cb-560">（程式碼片段- *ASP.NET MVC 4 實驗室-Ex04-屬性*）</span><span class="sxs-lookup"><span data-stu-id="5e9cb-560">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - Attributes*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. <span data-ttu-id="5e9cb-561">開啟**PhotoController**類別並更新資源**庫**方法，以順延強制1000毫秒（1秒）來模擬長時間執行的工作。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-561">Open the **PhotoController** class and update the **Gallery** method to delay the execution 1000 milliseconds (1 second) to simulate a long running task.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. <span data-ttu-id="5e9cb-562">開啟 web.config**檔案**，並藉由新增下列元素來啟用自訂錯誤。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-562">Open the **Web.config** file and enable custom errors by adding the following element.</span></span>

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. <span data-ttu-id="5e9cb-563">在**Views\Shared**中建立名為**TimedOut**的新視圖，並使用預設版面配置。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-563">Create a new view in **Views\Shared** named **TimedOut** and use the default layout.</span></span> <span data-ttu-id="5e9cb-564">在 方案總管中，以滑鼠右鍵按一下  **Views\Shared**  資料夾，然後選取 **新增 |View**。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-564">In the Solution Explorer, right-click the **Views\Shared** folder and select **Add | View**.</span></span>

    <span data-ttu-id="5e9cb-565">![針對每個行動裝置使用不同的視圖](whats-new-in-aspnet-mvc-4/_static/image36.png "針對每個行動裝置使用不同的視圖")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-565">![Using different views for each mobile device](whats-new-in-aspnet-mvc-4/_static/image36.png "Using different views for each mobile device")</span></span>

    <span data-ttu-id="5e9cb-566">*針對每個行動裝置使用不同的視圖*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-566">*Using different views for each mobile device*</span></span>
9. <span data-ttu-id="5e9cb-567">更新**TimedOut** view 內容，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-567">Update the **TimedOut** view content as shown below.</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. <span data-ttu-id="5e9cb-568">執行應用程式，並流覽至根 URL。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-568">Run the application and navigate to the root URL.</span></span> <span data-ttu-id="5e9cb-569">當您已新增執行緒時，就會出現一段時間1000毫秒的**睡眠**，您將會收到逾時錯誤，由**AsyncTimeout**屬性產生並由**HandleError**屬性攔截。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-569">As you have added a **Thread.Sleep** of 1000 milliseconds, you will get a time-out error, generated by the **AsyncTimeout** attribute and catch by the **HandleError** attribute.</span></span>

    <span data-ttu-id="5e9cb-570">![已處理超時例外狀況](whats-new-in-aspnet-mvc-4/_static/image37.png "已處理超時例外狀況")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-570">![Time-out exception handled](whats-new-in-aspnet-mvc-4/_static/image37.png "Time-out exception handled")</span></span>

    <span data-ttu-id="5e9cb-571">*已處理超時例外狀況*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-571">*Time-out exception handled*</span></span>

> [!NOTE]
> <span data-ttu-id="5e9cb-572">此外，您可以遵循[附錄 D：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式](#AppendixD)，將此應用程式部署到 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-572">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixD).</span></span>

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="5e9cb-573">總結</span><span class="sxs-lookup"><span data-stu-id="5e9cb-573">Summary</span></span>

<span data-ttu-id="5e9cb-574">在這個實際操作實驗室中，您已觀察到 ASP.NET MVC 4 中的一些新功能。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-574">In this hands-on-lab, you've observed some of the new features resident in ASP.NET MVC 4.</span></span> <span data-ttu-id="5e9cb-575">已討論過下列概念：</span><span class="sxs-lookup"><span data-stu-id="5e9cb-575">The following concepts have been discussed:</span></span>

- <span data-ttu-id="5e9cb-576">利用 ASP.NET MVC 專案範本的增強功能，包括新的行動應用程式專案範本</span><span class="sxs-lookup"><span data-stu-id="5e9cb-576">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="5e9cb-577">使用 HTML5 視口屬性和 CSS 媒體查詢來改善行動裝置上的顯示</span><span class="sxs-lookup"><span data-stu-id="5e9cb-577">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="5e9cb-578">使用 jQuery Mobile 進行漸進式增強，以及建立觸控式優化的 web UI</span><span class="sxs-lookup"><span data-stu-id="5e9cb-578">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="5e9cb-579">建立行動裝置特定的視圖</span><span class="sxs-lookup"><span data-stu-id="5e9cb-579">Create mobile-specific views</span></span>
- <span data-ttu-id="5e9cb-580">使用視圖切換器元件，在應用程式中的行動和桌面視圖之間切換</span><span class="sxs-lookup"><span data-stu-id="5e9cb-580">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="5e9cb-581">使用工作支援建立異步控制器</span><span class="sxs-lookup"><span data-stu-id="5e9cb-581">Create asynchronous controllers using task support</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="5e9cb-582">附錄 A：使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="5e9cb-582">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="5e9cb-583">有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-583">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="5e9cb-584">實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-584">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="5e9cb-585">![使用 Visual Studio 程式碼片段將程式碼插入您的專案](whats-new-in-aspnet-mvc-4/_static/image38.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-585">![Using Visual Studio code snippets to insert code into your project](whats-new-in-aspnet-mvc-4/_static/image38.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="5e9cb-586">*使用 Visual Studio 程式碼片段將程式碼插入您的專案*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-586">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="5e9cb-587">***若要使用鍵盤新增程式碼片段（C#僅限）***</span><span class="sxs-lookup"><span data-stu-id="5e9cb-587">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="5e9cb-588">將游標放在您想要插入程式碼的位置。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-588">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="5e9cb-589">開始鍵入程式碼片段名稱（不含空格或連字號）。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-589">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="5e9cb-590">監看 IntelliSense 會顯示相符的程式碼片段名稱。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-590">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="5e9cb-591">選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-591">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="5e9cb-592">按兩次 Tab 鍵，在游標位置插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-592">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="5e9cb-593">![開始鍵入程式碼片段名稱](whats-new-in-aspnet-mvc-4/_static/image39.png "開始鍵入程式碼片段名稱")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-593">![Start typing the snippet name](whats-new-in-aspnet-mvc-4/_static/image39.png "Start typing the snippet name")</span></span>

<span data-ttu-id="5e9cb-594">*開始鍵入程式碼片段名稱*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-594">*Start typing the snippet name*</span></span>

<span data-ttu-id="5e9cb-595">![按 Tab 鍵以選取反白顯示的程式碼片段](whats-new-in-aspnet-mvc-4/_static/image40.png "按 Tab 鍵以選取反白顯示的程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-595">![Press Tab to select the highlighted snippet](whats-new-in-aspnet-mvc-4/_static/image40.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="5e9cb-596">*按 Tab 鍵以選取反白顯示的程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-596">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="5e9cb-597">![再按一次 Tab 鍵，將會展開程式碼片段](whats-new-in-aspnet-mvc-4/_static/image41.png "再按一次 Tab 鍵，將會展開程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-597">![Press Tab again and the snippet will expand](whats-new-in-aspnet-mvc-4/_static/image41.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="5e9cb-598">*再按一次 Tab 鍵，將會展開程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-598">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="5e9cb-599">***若要使用滑鼠（C#、VISUAL BASIC 和 XML）加入程式碼片段***</span><span class="sxs-lookup"><span data-stu-id="5e9cb-599">***To add a code snippet using the mouse (C#, Visual Basic and XML)***</span></span>

1. <span data-ttu-id="5e9cb-600">以滑鼠右鍵按一下您要插入程式碼片段的位置。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-600">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="5e9cb-601">選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-601">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="5e9cb-602">按一下清單中的相關程式碼片段，即可加以選取。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-602">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="5e9cb-603">![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](whats-new-in-aspnet-mvc-4/_static/image42.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-603">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-aspnet-mvc-4/_static/image42.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="5e9cb-604">*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-604">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="5e9cb-605">![按一下清單中的相關程式碼片段，即可加以選取](whats-new-in-aspnet-mvc-4/_static/image43.png "按一下清單中的相關程式碼片段，即可加以選取")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-605">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-aspnet-mvc-4/_static/image43.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="5e9cb-606">*按一下清單中的相關程式碼片段，即可加以選取*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-606">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="5e9cb-607">附錄 B：安裝 Web 的 Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="5e9cb-607">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="5e9cb-608">您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-608">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="5e9cb-609">下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-609">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="5e9cb-610">移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-610">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="5e9cb-611">或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;*Visual Studio Express 2012 For Web* 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-611">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="5e9cb-612">按一下 [**立即安裝**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-612">Click on **Install Now**.</span></span> <span data-ttu-id="5e9cb-613">如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-613">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="5e9cb-614">開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-614">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="5e9cb-615">![安裝 Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "安裝 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-615">![Install Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="5e9cb-616">*安裝 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-616">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="5e9cb-617">閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-617">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受授權條款](whats-new-in-aspnet-mvc-4/_static/image45.png)

    <span data-ttu-id="5e9cb-619">*接受授權條款*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-619">*Accepting the license terms*</span></span>
5. <span data-ttu-id="5e9cb-620">等到下載和安裝程式完成為止。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-620">Wait until the downloading and installation process completes.</span></span>

    ![安裝進度](whats-new-in-aspnet-mvc-4/_static/image46.png)

    <span data-ttu-id="5e9cb-622">*安裝進度*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-622">*Installation progress*</span></span>
6. <span data-ttu-id="5e9cb-623">當安裝完成時，按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-623">When the installation completes, click **Finish**.</span></span>

    ![安裝已完成](whats-new-in-aspnet-mvc-4/_static/image47.png)

    <span data-ttu-id="5e9cb-625">*安裝已完成*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-625">*Installation completed*</span></span>
7. <span data-ttu-id="5e9cb-626">按一下 **[** 結束] 以關閉 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-626">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="5e9cb-627">若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-627">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磚](whats-new-in-aspnet-mvc-4/_static/image48.png)

    <span data-ttu-id="5e9cb-629">*VS Express for Web 磚*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-629">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a><span data-ttu-id="5e9cb-630">附錄 C：安裝 WebMatrix 2 和 iPhone 模擬器</span><span class="sxs-lookup"><span data-stu-id="5e9cb-630">Appendix C: Installing WebMatrix 2 and iPhone Simulator</span></span>

<span data-ttu-id="5e9cb-631">若要在模擬的 iPhone 裝置中執行您的網站，您可以使用 WebMatrix 擴充功能 &quot;適用于 iPhone&quot;的電子行動模擬器。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-631">To run your site in a simulated iPhone device you can use the WebMatrix extension &quot;Electric Mobile Simulator for the iPhone&quot;.</span></span> <span data-ttu-id="5e9cb-632">此外，您可以設定相同的延伸模組，以從 Visual Studio 2012 執行模擬器。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-632">Also, you can configure the same extension to run the simulator from Visual Studio 2012.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a><span data-ttu-id="5e9cb-633">工作 1-安裝 WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="5e9cb-633">Task 1 - Installing WebMatrix 2</span></span>

1. <span data-ttu-id="5e9cb-634">移至[[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-634">Go to [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="5e9cb-635">或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後搜尋產品 &quot;*WebMatrix 2*&quot;。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-635">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*WebMatrix 2*&quot;.</span></span>
2. <span data-ttu-id="5e9cb-636">按一下 [**立即安裝**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-636">Click on **Install Now**.</span></span> <span data-ttu-id="5e9cb-637">如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-637">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="5e9cb-638">開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-638">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="5e9cb-639">![安裝 WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "安裝 WebMatrix 2")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-639">![Install WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "Install WebMatrix 2")</span></span>

    <span data-ttu-id="5e9cb-640">*安裝 WebMatrix 2*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-640">*Install WebMatrix 2*</span></span>
4. <span data-ttu-id="5e9cb-641">閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-641">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    <span data-ttu-id="5e9cb-642">![接受授權條款](whats-new-in-aspnet-mvc-4/_static/image50.png "接受授權條款")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-642">![Accepting the license terms](whats-new-in-aspnet-mvc-4/_static/image50.png "Accepting the license terms")</span></span>

    <span data-ttu-id="5e9cb-643">*接受授權條款*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-643">*Accepting the license terms*</span></span>
5. <span data-ttu-id="5e9cb-644">等到下載和安裝程式完成為止。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-644">Wait until the downloading and installation process completes.</span></span>

    <span data-ttu-id="5e9cb-645">![安裝進度](whats-new-in-aspnet-mvc-4/_static/image51.png "安裝進度")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-645">![Installation progress](whats-new-in-aspnet-mvc-4/_static/image51.png "Installation progress")</span></span>

    <span data-ttu-id="5e9cb-646">*安裝進度*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-646">*Installation progress*</span></span>
6. <span data-ttu-id="5e9cb-647">當安裝完成時，按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-647">When the installation completes, click **Finish**.</span></span>

    <span data-ttu-id="5e9cb-648">![安裝已完成](whats-new-in-aspnet-mvc-4/_static/image52.png "安裝已完成")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-648">![Installation completed](whats-new-in-aspnet-mvc-4/_static/image52.png "Installation completed")</span></span>

    <span data-ttu-id="5e9cb-649">*安裝已完成*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-649">*Installation completed*</span></span>
7. <span data-ttu-id="5e9cb-650">按一下 **[** 結束] 以關閉 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-650">Click **Exit** to close Web Platform Installer.</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a><span data-ttu-id="5e9cb-651">工作 2-安裝 iPhone 模擬器擴充功能</span><span class="sxs-lookup"><span data-stu-id="5e9cb-651">Task 2 - Installing the iPhone Simulator Extension</span></span>

1. <span data-ttu-id="5e9cb-652">執行**WebMatrix**並開啟任何現有的網站或建立新的網站。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-652">Run **WebMatrix** and open any existing Web site or create a new one.</span></span>
2. <span data-ttu-id="5e9cb-653">從 [**首頁**] 功能區按一下 [**執行**] 按鈕，然後選取 [**加入新**的]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-653">Click the **Run** button from the **Home** ribbon and select **Add new**.</span></span>

    <span data-ttu-id="5e9cb-654">![正在新增 WebMatrix 擴充功能](whats-new-in-aspnet-mvc-4/_static/image53.png "正在新增 WebMatrix 擴充功能")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-654">![Adding new WebMatrix extension](whats-new-in-aspnet-mvc-4/_static/image53.png "Adding new WebMatrix extension")</span></span>

    <span data-ttu-id="5e9cb-655">*正在新增 WebMatrix 擴充功能*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-655">*Adding new WebMatrix extension*</span></span>
3. <span data-ttu-id="5e9cb-656">選取 [ **iPhone**模擬器]，然後按一下 [**安裝**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-656">Select **iPhone Simulator** and click **Install**.</span></span>

    <span data-ttu-id="5e9cb-657">![流覽 WebMatrix 擴充功能](whats-new-in-aspnet-mvc-4/_static/image54.png "流覽 WebMatrix 擴充功能")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-657">![Browsing WebMatrix extensions](whats-new-in-aspnet-mvc-4/_static/image54.png "Browsing WebMatrix extensions")</span></span>

    <span data-ttu-id="5e9cb-658">*流覽 WebMatrix 擴充功能*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-658">*Browsing WebMatrix extensions*</span></span>
4. <span data-ttu-id="5e9cb-659">在套件詳細資料中，按一下 [**安裝**] 以繼續安裝延伸模組。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-659">In the package details, click **Install** to continue with the extension installation.</span></span>

    <span data-ttu-id="5e9cb-660">![iPhone 模擬器擴充功能](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone 模擬器擴充功能")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-660">![iPhone Simulator extension](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone Simulator extension")</span></span>

    <span data-ttu-id="5e9cb-661">*iPhone 模擬器擴充功能*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-661">*iPhone Simulator extension*</span></span>
5. <span data-ttu-id="5e9cb-662">閱讀並接受延伸模組 EULA。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-662">Read and accept the extension EULA.</span></span>

    <span data-ttu-id="5e9cb-663">![WebMatrix 延伸模組 EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix 延伸模組 EULA")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-663">![WebMatrix extension EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix extension EULA")</span></span>

    <span data-ttu-id="5e9cb-664">*WebMatrix 延伸模組 EULA*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-664">*WebMatrix extension EULA*</span></span>
6. <span data-ttu-id="5e9cb-665">現在，您可以使用 iPhone 模擬器選項，從 WebMatrix 執行您的網站。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-665">Now, you can run your Web site from WebMatrix using the iPhone Simulator option.</span></span>

    <span data-ttu-id="5e9cb-666">![使用 iPhone 執行](whats-new-in-aspnet-mvc-4/_static/image57.png "使用 iPhone 執行")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-666">![Run using iPhone](whats-new-in-aspnet-mvc-4/_static/image57.png "Run using iPhone")</span></span>

    <span data-ttu-id="5e9cb-667">*使用 iPhone 執行*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-667">*Run using iPhone*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a><span data-ttu-id="5e9cb-668">工作 3-設定 Visual Studio 2012 來執行 iPhone 模擬器</span><span class="sxs-lookup"><span data-stu-id="5e9cb-668">Task 3 - Configuring Visual Studio 2012 to run iPhone Simulator</span></span>

1. <span data-ttu-id="5e9cb-669">開啟**Visual Studio 2012**並開啟任何網站，或建立新的專案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-669">Open **Visual Studio 2012** and open any Web site or create a new project.</span></span>
2. <span data-ttu-id="5e9cb-670">按一下 [執行] 按鈕上的向下箭號，然後選取 **[流覽方式]** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-670">Click the down arrow from the Run button and select **Browse with**.</span></span>

    <span data-ttu-id="5e9cb-671">![流覽方式](whats-new-in-aspnet-mvc-4/_static/image58.png "流覽方式")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-671">![Browse with](whats-new-in-aspnet-mvc-4/_static/image58.png "Browse with")</span></span>

    <span data-ttu-id="5e9cb-672">*流覽方式*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-672">*Browse with*</span></span>
3. <span data-ttu-id="5e9cb-673">在 [&quot;流覽&quot;] 對話方塊中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-673">In the &quot;Browse With&quot; dialog, click **Add**.</span></span>
4. <span data-ttu-id="5e9cb-674">在 [&quot;新增程式&quot;] 對話方塊中，使用下列值：</span><span class="sxs-lookup"><span data-stu-id="5e9cb-674">In the &quot;Add Program&quot; dialog, use the following values:</span></span>

   - <span data-ttu-id="5e9cb-675">**程式**： C:\Users\*{CurrentUser} \* \AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *（據以更新路徑）*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-675">**Program**: C:\Users\*{CurrentUser}\*\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(update the path accordingly)*</span></span>
   - <span data-ttu-id="5e9cb-676">**引數**： &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="5e9cb-676">**Arguments**: &quot;1&quot;</span></span>
   - <span data-ttu-id="5e9cb-677">**易記名稱**： iPhone 模擬器</span><span class="sxs-lookup"><span data-stu-id="5e9cb-677">**Friendly name**: iPhone Simulator</span></span>

     <span data-ttu-id="5e9cb-678">![新增程式](whats-new-in-aspnet-mvc-4/_static/image59.png "新增程式")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-678">![Add program](whats-new-in-aspnet-mvc-4/_static/image59.png "Add program")</span></span>

     <span data-ttu-id="5e9cb-679">*新增要流覽的程式*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-679">*Add program to browse with*</span></span>
5. <span data-ttu-id="5e9cb-680">按一下 **[確定]** 並關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-680">Click **OK** and close the dialogs.</span></span>
6. <span data-ttu-id="5e9cb-681">現在您可以從 Visual Studio 2012，在 iPhone 模擬器中執行您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-681">Now you are able to run your Web applications in the iPhone simulator from Visual Studio 2012.</span></span>

    <span data-ttu-id="5e9cb-682">![使用 iPhone 模擬器流覽](whats-new-in-aspnet-mvc-4/_static/image60.png "使用 iPhone 模擬器流覽")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-682">![Browse with iPhone Simulator](whats-new-in-aspnet-mvc-4/_static/image60.png "Browse with iPhone Simulator")</span></span>

    <span data-ttu-id="5e9cb-683">*使用 iPhone 模擬器流覽*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-683">*Browse with iPhone Simulator*</span></span>

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="5e9cb-684">附錄 D：使用 Web Deploy 發行 ASP.NET MVC 4 應用程式</span><span class="sxs-lookup"><span data-stu-id="5e9cb-684">Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="5e9cb-685">本附錄將告訴您如何從 Windows Azure 管理入口網站建立新的網站，以及如何發佈您在實驗室之後取得的應用程式，利用 Windows Azure 提供的 Web Deploy 發行功能。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-685">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="5e9cb-686">工作 1-從 Windows Azure 入口網站建立新的網站</span><span class="sxs-lookup"><span data-stu-id="5e9cb-686">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="5e9cb-687">移至[Windows Azure 管理入口網站](https://manage.windowsazure.com/)並使用與您的訂用帳戶相關聯的 Microsoft 認證登入。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-687">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e9cb-688">有了 Windows Azure，您可以免費裝載10個 ASP.NET 網站，然後隨著流量的成長而調整。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-688">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="5e9cb-689">您可以在[這裡](https://aka.ms/aspnet-hol-azure)註冊。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-689">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="5e9cb-690">![登入 Windows Azure 入口網站](whats-new-in-aspnet-mvc-4/_static/image61.png "登入 Windows Azure 入口網站")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-690">![Log on to Windows Azure portal](whats-new-in-aspnet-mvc-4/_static/image61.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="5e9cb-691">*登入 Windows Azure 管理入口網站*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-691">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="5e9cb-692">按一下命令列上的 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-692">Click **New** on the command bar.</span></span>

    <span data-ttu-id="5e9cb-693">![建立新網站](whats-new-in-aspnet-mvc-4/_static/image62.png "建立新網站")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-693">![Creating a new Web Site](whats-new-in-aspnet-mvc-4/_static/image62.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="5e9cb-694">*建立新網站*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-694">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="5e9cb-695">按一下 [**計算** | 的**網站**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-695">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="5e9cb-696">然後選取 [**快速建立**] 選項。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-696">Then select **Quick Create** option.</span></span> <span data-ttu-id="5e9cb-697">提供新網站的可用 URL，然後按一下 [**建立網站**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-697">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e9cb-698">Windows Azure 網站是在雲端中執行之 Web 應用程式的主機，您可以控制和管理。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-698">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="5e9cb-699">[快速建立] 選項可讓您從入口網站外部，將已完成的 web 應用程式部署至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-699">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="5e9cb-700">它不包含設定資料庫的步驟。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-700">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="5e9cb-701">![使用 [快速建立] 建立新的網站](whats-new-in-aspnet-mvc-4/_static/image63.png "使用 [快速建立] 建立新的網站")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-701">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-mvc-4/_static/image63.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="5e9cb-702">*使用 [快速建立] 建立新的網站*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-702">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="5e9cb-703">等到新**網站**建立完畢。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-703">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="5e9cb-704">建立網站之後，請按一下 [ **URL** ] 資料行下方的連結。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-704">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="5e9cb-705">檢查新網站是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-705">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="5e9cb-706">![流覽至新網站](whats-new-in-aspnet-mvc-4/_static/image64.png "流覽至新網站")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-706">![Browsing to the new web site](whats-new-in-aspnet-mvc-4/_static/image64.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="5e9cb-707">*流覽至新網站*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-707">*Browsing to the new web site*</span></span>

    <span data-ttu-id="5e9cb-708">![網站正在執行](whats-new-in-aspnet-mvc-4/_static/image65.png "網站正在執行")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-708">![Web site running](whats-new-in-aspnet-mvc-4/_static/image65.png "Web site running")</span></span>

    <span data-ttu-id="5e9cb-709">*網站正在執行*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-709">*Web site running*</span></span>
6. <span data-ttu-id="5e9cb-710">返回入口網站，然後按一下 [**名稱**] 欄底下的網站名稱，以顯示管理頁面。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-710">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="5e9cb-711">![開啟網站管理頁面](whats-new-in-aspnet-mvc-4/_static/image66.png "開啟網站管理頁面")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-711">![Opening the web site management pages](whats-new-in-aspnet-mvc-4/_static/image66.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="5e9cb-712">*開啟網站管理頁面*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-712">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="5e9cb-713">在 [**儀表板**] 頁面的 [**快速概覽**] 區段下，按一下 [**下載發行設定檔**] 連結。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-713">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e9cb-714">*發行設定檔*包含將 web 應用程式發佈至 Windows Azure 網站所需的所有資訊，以供每個已啟用的發行方法使用。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-714">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="5e9cb-715">發行設定檔包含 Url、使用者認證和資料庫字串，這些都是連接到已啟用發行方法的每個端點並進行驗證所需的。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-715">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="5e9cb-716">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支援讀取發行設定檔，以將這些程式的設定自動化，以將 Web 應用程式發佈至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-716">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="5e9cb-717">![正在下載網站發行設定檔](whats-new-in-aspnet-mvc-4/_static/image67.png "正在下載網站發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-717">![Downloading the web site publish profile](whats-new-in-aspnet-mvc-4/_static/image67.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="5e9cb-718">*正在下載網站發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-718">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="5e9cb-719">將發行設定檔下載到已知的位置。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-719">Download the publish profile file to a known location.</span></span> <span data-ttu-id="5e9cb-720">在此練習中，您將瞭解如何使用此檔案，將 web 應用程式從 Visual Studio 發行至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-720">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="5e9cb-721">![儲存發行設定檔](whats-new-in-aspnet-mvc-4/_static/image68.png "正在儲存發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-721">![Saving the publish profile file](whats-new-in-aspnet-mvc-4/_static/image68.png "Saving the publish profile")</span></span>

    <span data-ttu-id="5e9cb-722">*儲存發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-722">*Saving the publish profile file*</span></span>

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="5e9cb-723">工作 2-設定資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="5e9cb-723">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="5e9cb-724">如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-724">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="5e9cb-725">如果您想要部署不使用 SQL Server 的簡單應用程式，您可能會略過這項工作。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-725">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="5e9cb-726">您將需要 SQL Database 伺服器來儲存應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-726">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="5e9cb-727">您可以在 Windows Azure 管理入口網站的  **SQL 資料庫** | **伺服器** | **伺服器的儀表板**上，從您的訂用帳戶中查看 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-727">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="5e9cb-728">如果您沒有建立伺服器，可以使用命令列上的 [**新增**] 按鈕建立一個。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-728">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="5e9cb-729">記下 [**伺服器名稱] 和 [URL]、[系統管理員登入名稱] 和 [密碼**]，因為您將在後續工作中使用它們。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-729">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="5e9cb-730">請不要建立資料庫，因為它會在稍後的階段中建立。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-730">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="5e9cb-731">![SQL Database Server 儀表板](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database Server 儀表板")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-731">![SQL Database Server Dashboard](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="5e9cb-732">*SQL Database Server 儀表板*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-732">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="5e9cb-733">在下一項工作中，您將會從 Visual Studio 測試資料庫連線，因此您必須在伺服器的**允許 IP 位址**清單中包含本機 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-733">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="5e9cb-734">若要這麼做，請按一下 **設定**，從**目前的用戶端 IP 位址**中選取 IP 位址，並將它貼入 **起始 Ip 位址**] 和 [**結束 ip 位址**] 文字方塊，然後按一下 [![新增-用戶端-IP-位址-確定 按鈕](whats-new-in-aspnet-mvc-4/_static/image70.png) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-734">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png) button.</span></span>

    ![正在新增用戶端 IP 位址](whats-new-in-aspnet-mvc-4/_static/image71.png)

    <span data-ttu-id="5e9cb-736">*正在新增用戶端 IP 位址*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-736">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="5e9cb-737">將**用戶端 Ip 位址**新增至 [允許的 ip 位址] 清單之後，按一下 [**儲存**] 以確認變更。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-737">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![確認變更](whats-new-in-aspnet-mvc-4/_static/image72.png)

    <span data-ttu-id="5e9cb-739">*確認變更*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-739">*Confirm Changes*</span></span>

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="5e9cb-740">工作 3-使用 Web Deploy 發行 ASP.NET MVC 4 應用程式</span><span class="sxs-lookup"><span data-stu-id="5e9cb-740">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="5e9cb-741">返回 ASP.NET MVC 4 解決方案。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-741">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="5e9cb-742">在 **方案總管**中，以滑鼠右鍵按一下 網站 專案，然後選取 **發佈**。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-742">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="5e9cb-743">![發行應用程式](whats-new-in-aspnet-mvc-4/_static/image73.png "發行應用程式")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-743">![Publishing the Application](whats-new-in-aspnet-mvc-4/_static/image73.png "Publishing the Application")</span></span>

    <span data-ttu-id="5e9cb-744">*發行網站*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-744">*Publishing the web site*</span></span>
2. <span data-ttu-id="5e9cb-745">匯入您在第一個工作中儲存的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-745">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="5e9cb-746">![匯入發行設定檔](whats-new-in-aspnet-mvc-4/_static/image74.png "匯入發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-746">![Importing the publish profile](whats-new-in-aspnet-mvc-4/_static/image74.png "Importing the publish profile")</span></span>

    <span data-ttu-id="5e9cb-747">*正在匯入發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-747">*Importing publish profile*</span></span>
3. <span data-ttu-id="5e9cb-748">按一下 [**驗證連接**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-748">Click **Validate Connection**.</span></span> <span data-ttu-id="5e9cb-749">驗證完成後，按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-749">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e9cb-750">當您看到 [驗證連線] 按鈕旁出現綠色核取記號時，驗證就會完成。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-750">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="5e9cb-751">![正在驗證連接](whats-new-in-aspnet-mvc-4/_static/image75.png "正在驗證連接")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-751">![Validating connection](whats-new-in-aspnet-mvc-4/_static/image75.png "Validating connection")</span></span>

    <span data-ttu-id="5e9cb-752">*正在驗證連接*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-752">*Validating connection*</span></span>
4. <span data-ttu-id="5e9cb-753">在 [**設定**] 頁面的 [**資料庫**] 區段底下，按一下資料庫連接的文字方塊旁邊的按鈕（也就是**DefaultConnection**）。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-753">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="5e9cb-754">![Web deploy 設定](whats-new-in-aspnet-mvc-4/_static/image76.png "Web deploy 設定")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-754">![Web deploy configuration](whats-new-in-aspnet-mvc-4/_static/image76.png "Web deploy configuration")</span></span>

    <span data-ttu-id="5e9cb-755">*Web deploy 設定*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-755">*Web deploy configuration*</span></span>
5. <span data-ttu-id="5e9cb-756">設定資料庫連接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5e9cb-756">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="5e9cb-757">在 [**伺服器名稱**] 中，使用*tcp：* prefix 輸入您的 SQL Database 伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-757">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="5e9cb-758">在 [**使用者名稱**] 中，輸入您的伺服器管理員登入名稱。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-758">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="5e9cb-759">在 [**密碼**] 中輸入您的伺服器管理員登入密碼。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-759">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="5e9cb-760">輸入新的資料庫名稱，例如： *MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-760">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="5e9cb-761">![正在設定目的地連接字串](whats-new-in-aspnet-mvc-4/_static/image77.png "正在設定目的地連接字串")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-761">![Configuring destination connection string](whats-new-in-aspnet-mvc-4/_static/image77.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="5e9cb-762">*正在設定目的地連接字串*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-762">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="5e9cb-763">然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-763">Then click **OK**.</span></span> <span data-ttu-id="5e9cb-764">當系統提示您建立資料庫時，請按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-764">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="5e9cb-765">![建立資料庫](whats-new-in-aspnet-mvc-4/_static/image78.png "建立資料庫字串")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-765">![Creating the database](whats-new-in-aspnet-mvc-4/_static/image78.png "Creating the database string")</span></span>

    <span data-ttu-id="5e9cb-766">*建立資料庫*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-766">*Creating the database*</span></span>
7. <span data-ttu-id="5e9cb-767">您將用來連接到 Windows Azure 中 SQL Database 的連接字串會顯示在 [預設連接] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-767">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="5e9cb-768">然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-768">Then click **Next**.</span></span>

    <span data-ttu-id="5e9cb-769">![指向 SQL Database 的連接字串](whats-new-in-aspnet-mvc-4/_static/image79.png "指向 SQL Database 的連接字串")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-769">![Connection string pointing to SQL Database](whats-new-in-aspnet-mvc-4/_static/image79.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="5e9cb-770">*指向 SQL Database 的連接字串*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-770">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="5e9cb-771">在 [**預覽**] 頁面中，按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-771">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="5e9cb-772">![發行 web 應用程式](whats-new-in-aspnet-mvc-4/_static/image80.png "發行 web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-772">![Publishing the web application](whats-new-in-aspnet-mvc-4/_static/image80.png "Publishing the web application")</span></span>

    <span data-ttu-id="5e9cb-773">*發行 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-773">*Publishing the web application*</span></span>
9. <span data-ttu-id="5e9cb-774">發佈程式完成後，您的預設瀏覽器會開啟已發行的網站。</span><span class="sxs-lookup"><span data-stu-id="5e9cb-774">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="5e9cb-775">![發行至 Windows Azure 的應用程式](whats-new-in-aspnet-mvc-4/_static/image81.png "發行至 Windows Azure 的應用程式")</span><span class="sxs-lookup"><span data-stu-id="5e9cb-775">![Application published to Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="5e9cb-776">*發行至 Windows Azure 的應用程式*</span><span class="sxs-lookup"><span data-stu-id="5e9cb-776">*Application published to Windows Azure*</span></span>
