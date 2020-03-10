---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: 第1部分：檔案 > 新專案 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第1部分涵蓋總覽和檔案/新增專案。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: 05a3ace3d8fef9c1f3593f7948e42b4725d70134
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636126"
---
# <a name="part-1-file--new-project"></a><span data-ttu-id="a2e37-104">第1部分：檔案 > 的新專案</span><span class="sxs-lookup"><span data-stu-id="a2e37-104">Part 1: File-> New Project</span></span>

<span data-ttu-id="a2e37-105">依[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="a2e37-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="a2e37-106">Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。</span><span class="sxs-lookup"><span data-stu-id="a2e37-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="a2e37-107">它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。</span><span class="sxs-lookup"><span data-stu-id="a2e37-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="a2e37-108">本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="a2e37-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="a2e37-109">第1部分涵蓋總覽和檔案/新增專案。</span><span class="sxs-lookup"><span data-stu-id="a2e37-109">Part 1 covers Overview and File/New Project.</span></span>

## <a id="_Toc260221666"></a><span data-ttu-id="a2e37-110">簡要</span><span class="sxs-lookup"><span data-stu-id="a2e37-110">Overview</span></span>

<span data-ttu-id="a2e37-111">本教學課程是 ASP.NET WebForms 的簡介。</span><span class="sxs-lookup"><span data-stu-id="a2e37-111">This tutorial is an introduction to ASP.NET WebForms.</span></span> <span data-ttu-id="a2e37-112">我們會開始變慢，因此新手層級的 網頁程式開發體驗也沒關係。</span><span class="sxs-lookup"><span data-stu-id="a2e37-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="a2e37-113">我們將建立的應用程式是簡單的線上商店。</span><span class="sxs-lookup"><span data-stu-id="a2e37-113">The application we'll be building is a simple on-line store.</span></span>

![](tailspin-spyworks-part-1/_static/image1.jpg)

<span data-ttu-id="a2e37-114">訪客可以依類別流覽產品：</span><span class="sxs-lookup"><span data-stu-id="a2e37-114">Visitors can browse Products by Category:</span></span>

![](tailspin-spyworks-part-1/_static/image2.jpg)

<span data-ttu-id="a2e37-115">他們可以查看單一產品，並將其新增至其購物車：</span><span class="sxs-lookup"><span data-stu-id="a2e37-115">They can view a single product and add it to their cart:</span></span>

![](tailspin-spyworks-part-1/_static/image3.jpg)

<span data-ttu-id="a2e37-116">他們可以審查其購物車，移除任何不再需要的專案：</span><span class="sxs-lookup"><span data-stu-id="a2e37-116">They can review their cart, removing any items they no longer want:</span></span>

![](tailspin-spyworks-part-1/_static/image4.jpg)

<span data-ttu-id="a2e37-117">繼續簽出將會提示他們</span><span class="sxs-lookup"><span data-stu-id="a2e37-117">Proceeding to Checkout will prompt them to</span></span>

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

<span data-ttu-id="a2e37-118">排序之後，他們會看到簡單的確認畫面：</span><span class="sxs-lookup"><span data-stu-id="a2e37-118">After ordering, they see a simple confirmation screen:</span></span>

![](tailspin-spyworks-part-1/_static/image7.jpg)

<span data-ttu-id="a2e37-119">我們將從在 Visual Studio 2010 中建立新的 ASP.NET WebForms 專案開始，並以累加方式新增功能，以建立完整的運作中應用程式。</span><span class="sxs-lookup"><span data-stu-id="a2e37-119">We'll begin by creating a new ASP.NET WebForms project in Visual Studio 2010, and we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="a2e37-120">在此過程中，我們將討論資料庫存取、清單和方格的觀點、資料更新頁面、資料驗證、使用主版頁面進行一致的頁面配置、AJAX、驗證、使用者成員資格等等。</span><span class="sxs-lookup"><span data-stu-id="a2e37-120">Along the way, we'll cover database access, list and grid views, data update pages, data validation, using master pages for consistent page layout, AJAX, validation, user membership, and more.</span></span>

<span data-ttu-id="a2e37-121">您可以依照步驟進行，也可以從[http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)下載已完成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a2e37-121">You can follow along step by step, or you can download the completed application from [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)</span></span>

<span data-ttu-id="a2e37-122">您可以從[https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/)使用 Visual Studio 2010 或免費的 Visual Web Developer 2010。</span><span class="sxs-lookup"><span data-stu-id="a2e37-122">You can use either Visual Studio 2010 or the free Visual Web Developer 2010 from [https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="a2e37-123">若要建立應用程式，您可以使用 SQL Server 或免費 SQL Server Express 來裝載資料庫。</span><span class="sxs-lookup"><span data-stu-id="a2e37-123">To build the application, you can use either SQL Server or the free SQL Server Express to host the database.</span></span>

## <a id="_Toc260221667"></a><span data-ttu-id="a2e37-124">檔案/新增專案</span><span class="sxs-lookup"><span data-stu-id="a2e37-124">File / New Project</span></span>

<span data-ttu-id="a2e37-125">我們會從 Visual Studio 的 [檔案] 功能表中選取新的專案開始。</span><span class="sxs-lookup"><span data-stu-id="a2e37-125">We'll start by selecting the New Project from the File menu in Visual Studio.</span></span> <span data-ttu-id="a2e37-126">這會顯示 [新增專案] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a2e37-126">This brings up the New Project dialog.</span></span>

![](tailspin-spyworks-part-1/_static/image8.jpg)

<span data-ttu-id="a2e37-127">我們將選取左側的C# [視覺效果/Web 範本] 群組，然後選擇 [中間] 資料行中的 [ASP.NET Web 應用程式] 範本。</span><span class="sxs-lookup"><span data-stu-id="a2e37-127">We'll select the Visual C# / Web Templates group on the left, and then choose the "ASP.NET Web Application" template in the center column.</span></span> <span data-ttu-id="a2e37-128">將專案命名為 TailspinSpyworks，然後按下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a2e37-128">Name your project TailspinSpyworks and press the OK button.</span></span>

![](tailspin-spyworks-part-1/_static/image9.jpg)

<span data-ttu-id="a2e37-129">這會建立我們的專案。</span><span class="sxs-lookup"><span data-stu-id="a2e37-129">This will create our project.</span></span> <span data-ttu-id="a2e37-130">讓我們來看看應用程式中包含在右側方案總管中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="a2e37-130">Let's take a look at the folders that are included in our application in the Solution Explorer on the right side.</span></span>

![](tailspin-spyworks-part-1/_static/image10.jpg)

<span data-ttu-id="a2e37-131">空白解決方案不完全空白–它會新增基本資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="a2e37-131">The Empty Solution isn't completely empty – it adds a basic folder structure:</span></span>

![](tailspin-spyworks-part-1/_static/image1.png)

<span data-ttu-id="a2e37-132">請注意 ASP.NET 4 預設專案範本所執行的慣例。</span><span class="sxs-lookup"><span data-stu-id="a2e37-132">Note the conventions implemented by the ASP.NET 4 default project template.</span></span>

- <span data-ttu-id="a2e37-133">「帳戶」資料夾會為 ASP 實行基本的使用者介面。NET 的成員資格子系統。</span><span class="sxs-lookup"><span data-stu-id="a2e37-133">The "Account" folder implements a basic user interface for ASP.NET's membership subsystem.</span></span>
- <span data-ttu-id="a2e37-134">「腳本」資料夾可作為用戶端 JavaScript 檔案的存放庫，而核心 jQuery .js 檔預設為可用。</span><span class="sxs-lookup"><span data-stu-id="a2e37-134">The "Scripts" folder serves as the repository for client side JavaScript files and the core jQuery .js files are made available by default.</span></span>
- <span data-ttu-id="a2e37-135">「樣式」資料夾是用來組織我們的網站視覺效果（CSS 樣式表單）</span><span class="sxs-lookup"><span data-stu-id="a2e37-135">The "Styles" folder is used to organize our web site visuals (CSS Style Sheets)</span></span>

<span data-ttu-id="a2e37-136">當我們按 F5 執行應用程式並轉譯 default.aspx 頁面時，我們會看到下列畫面。</span><span class="sxs-lookup"><span data-stu-id="a2e37-136">When we press F5 to run our application and render the default.aspx page we see the following.</span></span>

![](tailspin-spyworks-part-1/_static/image11.jpg)

<span data-ttu-id="a2e37-137">我們的第一個應用程式增強功能是將預設 WebForms 範本中的 Style .css 檔案取代成 CSS 類別和相關聯的影像檔案，這些檔案將會轉譯我們的 Tailspin Spyworks 應用程式所需的視覺效果 asthetics。</span><span class="sxs-lookup"><span data-stu-id="a2e37-137">Our first application enhancement will be to replace the Style.css file from the default WebForms template with the CSS classes and associated image files that will render the visual asthetics that we want for our Tailspin Spyworks application.</span></span>

<span data-ttu-id="a2e37-138">這麼做之後，default.aspx 頁面就會呈現如下。</span><span class="sxs-lookup"><span data-stu-id="a2e37-138">After doing so our default.aspx page renders like this.</span></span>

![](tailspin-spyworks-part-1/_static/image12.jpg)

<span data-ttu-id="a2e37-139">請注意頁面右上方的影像連結，以及已新增至主版頁面的功能表項目。</span><span class="sxs-lookup"><span data-stu-id="a2e37-139">Notice the image links at the top right of the page and the menu items that have been added to the master page.</span></span> <span data-ttu-id="a2e37-140">只有「登入」和「帳戶」連結會指向存在的頁面（由預設範本所產生），以及我們在建立應用程式時將會執行的其餘頁面。</span><span class="sxs-lookup"><span data-stu-id="a2e37-140">Only the "Sign In" and "Account" links point to pages that exist (generated by the default template) and the rest of the pages we will implement as we build our application.</span></span>

<span data-ttu-id="a2e37-141">我們也要將主版頁面重新放置到 [樣式] 目錄。</span><span class="sxs-lookup"><span data-stu-id="a2e37-141">We're also going to relocate the Master Page to the Styles directory.</span></span> <span data-ttu-id="a2e37-142">雖然這只是偏好的喜好設定，但如果我們決定讓我們的應用程式在未來「skinable」，則可能會變得更容易。</span><span class="sxs-lookup"><span data-stu-id="a2e37-142">Though this is only a preference it may make things a little easier if we decide to make our application "skinable" in the future.</span></span>

<span data-ttu-id="a2e37-143">這麼做之後，我們需要變更預設 ASP.NET WebForms 頁面所產生之所有 .aspx 檔案中的主版頁面參考。</span><span class="sxs-lookup"><span data-stu-id="a2e37-143">After doing this we'll need to change the master page references in all the .aspx files generated by the default ASP.NET WebForms pages.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a2e37-144">下一個</span><span class="sxs-lookup"><span data-stu-id="a2e37-144">Next</span></span>](tailspin-spyworks-part-2.md)
