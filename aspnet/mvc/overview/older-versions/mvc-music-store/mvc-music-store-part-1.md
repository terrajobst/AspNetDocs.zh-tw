---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: 第1部分：總覽和檔案 > 新專案 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第1部分涵蓋總覽和檔案 > 的新專案。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 48428ff4ab5888253ed93ac41e79006eec823ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559980"
---
# <a name="part-1-overview-and-file-new-project"></a><span data-ttu-id="1d6ab-104">第1部分：總覽和檔案 > 的新專案</span><span class="sxs-lookup"><span data-stu-id="1d6ab-104">Part 1: Overview and File->New Project</span></span>

<span data-ttu-id="1d6ab-105">依[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="1d6ab-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="1d6ab-106">MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="1d6ab-107">MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="1d6ab-108">本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="1d6ab-109">第1部分涵蓋總覽和檔案&gt;的新專案。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-109">Part 1 covers Overview and File-&gt;New Project.</span></span>

## <a name="overview"></a><span data-ttu-id="1d6ab-110">概觀</span><span class="sxs-lookup"><span data-stu-id="1d6ab-110">Overview</span></span>

<span data-ttu-id="1d6ab-111">MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Web Developer 進行網頁程式開發的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-111">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Web Developer for web development.</span></span> <span data-ttu-id="1d6ab-112">我們會開始變慢，因此新手層級的 網頁程式開發體驗也沒關係。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="1d6ab-113">我們將建立的應用程式是簡單的音樂商店。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-113">The application we'll be building is a simple music store.</span></span> <span data-ttu-id="1d6ab-114">應用程式有三個主要部分： [購物]、[結帳] 和 [系統管理]。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-114">There are three main parts to the application: shopping, checkout, and administration.</span></span>

![](mvc-music-store-part-1/_static/image1.jpg)

<span data-ttu-id="1d6ab-115">訪客可以依內容類型流覽專輯：</span><span class="sxs-lookup"><span data-stu-id="1d6ab-115">Visitors can browse Albums by Genre:</span></span>

![](mvc-music-store-part-1/_static/image2.jpg)

<span data-ttu-id="1d6ab-116">他們可以查看單一專輯，並將其新增至購物車：</span><span class="sxs-lookup"><span data-stu-id="1d6ab-116">They can view a single album and add it to their cart:</span></span>

![](mvc-music-store-part-1/_static/image3.jpg)

<span data-ttu-id="1d6ab-117">他們可以審查其購物車，移除任何不再需要的專案：</span><span class="sxs-lookup"><span data-stu-id="1d6ab-117">They can review their cart, removing any items they no longer want:</span></span>

![](mvc-music-store-part-1/_static/image4.jpg)

<span data-ttu-id="1d6ab-118">繼續簽出將會提示他們登入或註冊使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-118">Proceeding to Checkout will prompt them to login or register for a user account.</span></span>

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

<span data-ttu-id="1d6ab-119">建立帳戶之後，他們可以填寫出貨和付款資訊來完成訂單。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-119">After creating an account, they can complete the order by filling out shipping and payment information.</span></span> <span data-ttu-id="1d6ab-120">為了簡單起見，我們會執行一項絕佳的促銷活動：如果您輸入促銷代碼「免費」，一切都免費！</span><span class="sxs-lookup"><span data-stu-id="1d6ab-120">To keep things simple, we're running an amazing promotion: everything's free if they enter promotion code "FREE"!</span></span>

![](mvc-music-store-part-1/_static/image5.jpg)

<span data-ttu-id="1d6ab-121">排序之後，他們會看到簡單的確認畫面：</span><span class="sxs-lookup"><span data-stu-id="1d6ab-121">After ordering, they see a simple confirmation screen:</span></span>

![](mvc-music-store-part-1/_static/image6.jpg)

<span data-ttu-id="1d6ab-122">除了客戶面向的頁面之外，我們也會建立 [系統管理員] 區段，其中會顯示系統管理員可以建立、編輯和刪除專輯的專輯清單：</span><span class="sxs-lookup"><span data-stu-id="1d6ab-122">In addition to customer-facing pages, we'll also build an administrator section that shows a list of albums from which Administrators can Create, Edit, and Delete albums:</span></span>

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a><span data-ttu-id="1d6ab-123">1. 檔案&gt; 的新專案</span><span class="sxs-lookup"><span data-stu-id="1d6ab-123">1. File -&gt; New Project</span></span>

### <a name="installing-the-software"></a><span data-ttu-id="1d6ab-124">安裝軟體</span><span class="sxs-lookup"><span data-stu-id="1d6ab-124">Installing the software</span></span>

<span data-ttu-id="1d6ab-125">本教學課程一開始會使用免費的 Visual Web Developer 2010 Express （這是免費的）來建立新的 ASP.NET MVC 3 專案，然後我們會以累加方式新增功能，以建立完整的運作中應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-125">This tutorial will begin by creating a new ASP.NET MVC 3 project using the free Visual Web Developer 2010 Express (which is free), and then we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="1d6ab-126">在此過程中，我們將討論資料庫存取、表單張貼案例、資料驗證、使用主版頁面進行一致的頁面配置、使用 AJAX 進行頁面更新和驗證、使用者登入等等。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-126">Along the way, we'll cover database access, form posting scenarios, data validation, using master pages for consistent page layout, using AJAX for page updates and validation, user login, and more.</span></span>

<span data-ttu-id="1d6ab-127">您可以依照步驟進行，也可以從[MVC-音樂存放區](https://github.com/evilDave/MVC-Music-Store)下載已完成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-127">You can follow along step by step, or you can download the completed application from [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="1d6ab-128">您可以使用 Visual Studio 2010 SP1 或 Visual Web Developer 2010 Express SP1 （免費版的 Visual Studio 2010）來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-128">You can use either Visual Studio 2010 SP1 or Visual Web Developer 2010 Express SP1 (a free version of Visual Studio 2010) to build the application.</span></span> <span data-ttu-id="1d6ab-129">我們將使用 SQL Server Compact （也免費）來裝載資料庫。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-129">We'll be using the SQL Server Compact (also free) to host the database.</span></span> <span data-ttu-id="1d6ab-130">開始之前，請先確定您已安裝下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-130">Before you start, make sure you've installed the prerequisites listed below.</span></span>

- <span data-ttu-id="1d6ab-131">[Visual Studio Web Developer Express SP1 必要條件]</span><span class="sxs-lookup"><span data-stu-id="1d6ab-131">[Visual Studio Web Developer Express SP1 prerequisites]</span></span>
- <span data-ttu-id="1d6ab-132">[ASP.NET MVC 3 工具更新]</span><span class="sxs-lookup"><span data-stu-id="1d6ab-132">[ASP.NET MVC 3 Tools Update]</span></span>
- <span data-ttu-id="1d6ab-133">[SQL Server Compact 4.0]-包含執行時間和工具支援</span><span class="sxs-lookup"><span data-stu-id="1d6ab-133">[SQL Server Compact 4.0] - including both runtime and tools support</span></span>

### <a name="creating-a-new-aspnet-mvc-3-project"></a><span data-ttu-id="1d6ab-134">建立新的 ASP.NET MVC 3 專案</span><span class="sxs-lookup"><span data-stu-id="1d6ab-134">Creating a new ASP.NET MVC 3 project</span></span>

<span data-ttu-id="1d6ab-135">我們會先從 Visual Web Developer 的 [檔案] 功能表中選取 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-135">We'll start by selecting "New Project" from the File menu in Visual Web Developer.</span></span> <span data-ttu-id="1d6ab-136">這會顯示 [新增專案] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-136">This brings up the New Project dialog.</span></span>

![](mvc-music-store-part-1/_static/image5.png)

<span data-ttu-id="1d6ab-137">我們將選取左側的C# [Visual&gt; Web Templates] 群組，然後選擇 [中間] 資料行中的 [ASP.NET MVC 3 Web 應用程式] 範本。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-137">We'll select the Visual C# -&gt; Web Templates group on the left, then choose the "ASP.NET MVC 3 Web Application" template in the center column.</span></span> <span data-ttu-id="1d6ab-138">將專案命名為 MvcMusicStore，然後按下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-138">Name your project MvcMusicStore and press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image8.jpg)

<span data-ttu-id="1d6ab-139">這會顯示次要對話，讓我們為專案進行一些 MVC 特定設定。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-139">This will display a secondary dialog which allows us to make some MVC specific settings for our project.</span></span> <span data-ttu-id="1d6ab-140">選取下列各項：</span><span class="sxs-lookup"><span data-stu-id="1d6ab-140">Select the following:</span></span>

<span data-ttu-id="1d6ab-141">專案範本-選取 [空白]</span><span class="sxs-lookup"><span data-stu-id="1d6ab-141">Project Template - select Empty</span></span>

<span data-ttu-id="1d6ab-142">視圖引擎-選取 Razor</span><span class="sxs-lookup"><span data-stu-id="1d6ab-142">View Engine - select Razor</span></span>

<span data-ttu-id="1d6ab-143">使用 HTML5 語義標記-已核取</span><span class="sxs-lookup"><span data-stu-id="1d6ab-143">Use HTML5 semantic markup - checked</span></span>

<span data-ttu-id="1d6ab-144">確認您的設定如下所示，然後按下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-144">Verify that your settings are as shown below, then press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image9.jpg)

<span data-ttu-id="1d6ab-145">這會建立我們的專案。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-145">This will create our project.</span></span> <span data-ttu-id="1d6ab-146">讓我們來看一下在右邊的方案總管中，已新增至應用程式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-146">Let's take a look at the folders that have been added to our application in the Solution Explorer on the right side.</span></span>

![](mvc-music-store-part-1/_static/image10.jpg)

<span data-ttu-id="1d6ab-147">空白 MVC 3 範本不是完全空白，它會新增基本資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="1d6ab-147">The Empty MVC 3 template isn't completely empty – it adds a basic folder structure:</span></span>

![](mvc-music-store-part-1/_static/image6.png)

<span data-ttu-id="1d6ab-148">ASP.NET MVC 會針對資料夾名稱使用一些基本的命名慣例：</span><span class="sxs-lookup"><span data-stu-id="1d6ab-148">ASP.NET MVC makes use of some basic naming conventions for folder names:</span></span>

| <span data-ttu-id="1d6ab-149">[資料夾]</span><span class="sxs-lookup"><span data-stu-id="1d6ab-149">**Folder**</span></span> | <span data-ttu-id="1d6ab-150">**目的**</span><span class="sxs-lookup"><span data-stu-id="1d6ab-150">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="1d6ab-151">**/Controllers**</span><span class="sxs-lookup"><span data-stu-id="1d6ab-151">**/Controllers**</span></span> | <span data-ttu-id="1d6ab-152">控制器會回應來自瀏覽器的輸入、決定該如何處理，以及將回應傳回給使用者。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-152">Controllers respond to input from the browser, decide what to do with it, and return response to the user.</span></span> |
| <span data-ttu-id="1d6ab-153">**/Views**</span><span class="sxs-lookup"><span data-stu-id="1d6ab-153">**/Views**</span></span> | <span data-ttu-id="1d6ab-154">Views 包含 UI 範本</span><span class="sxs-lookup"><span data-stu-id="1d6ab-154">Views hold our UI templates</span></span> |
| <span data-ttu-id="1d6ab-155">**/Models**</span><span class="sxs-lookup"><span data-stu-id="1d6ab-155">**/Models**</span></span> | <span data-ttu-id="1d6ab-156">模型保存和運算元據</span><span class="sxs-lookup"><span data-stu-id="1d6ab-156">Models hold and manipulate data</span></span> |
| <span data-ttu-id="1d6ab-157">**/Content**</span><span class="sxs-lookup"><span data-stu-id="1d6ab-157">**/Content**</span></span> | <span data-ttu-id="1d6ab-158">此資料夾包含我們的影像、CSS 和任何其他靜態內容</span><span class="sxs-lookup"><span data-stu-id="1d6ab-158">This folder holds our images, CSS, and any other static content</span></span> |
| <span data-ttu-id="1d6ab-159">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="1d6ab-159">**/Scripts**</span></span> | <span data-ttu-id="1d6ab-160">此資料夾包含我們的 JavaScript 檔案</span><span class="sxs-lookup"><span data-stu-id="1d6ab-160">This folder holds our JavaScript files</span></span> |

<span data-ttu-id="1d6ab-161">這些資料夾甚至會包含在空白的 ASP.NET MVC 應用程式中，因為 ASP.NET MVC 架構預設會使用「慣例 over 設定」方法，並根據資料夾命名慣例做出一些預設假設。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-161">These folders are included even in an Empty ASP.NET MVC application because the ASP.NET MVC framework by default uses a "convention over configuration" approach and makes some default assumptions based on folder naming conventions.</span></span> <span data-ttu-id="1d6ab-162">例如，控制器預設會在 [Views] 資料夾中尋找 views，而您不需要在程式碼中明確指定。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-162">For instance, controllers look for views in the Views folder by default without you having to explicitly specify this in your code.</span></span> <span data-ttu-id="1d6ab-163">堅持使用預設慣例可減少您需要撰寫的程式碼數量，也能讓其他開發人員更輕鬆地瞭解您的專案。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-163">Sticking with the default conventions reduces the amount of code you need to write, and can also make it easier for other developers to understand your project.</span></span> <span data-ttu-id="1d6ab-164">我們會在建立應用程式時，更清楚地說明這些慣例。</span><span class="sxs-lookup"><span data-stu-id="1d6ab-164">We'll explain these conventions more as we build our application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="1d6ab-165">下一個</span><span class="sxs-lookup"><span data-stu-id="1d6ab-165">Next</span></span>](mvc-music-store-part-2.md)
