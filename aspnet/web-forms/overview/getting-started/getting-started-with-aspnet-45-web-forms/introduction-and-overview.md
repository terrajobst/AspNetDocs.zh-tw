---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: ASP.NET 4.7 Web Forms 和 Visual Studio 2017 的消費者入門 |Microsoft Docs
author: Erikre
description: 此逐步教學課程系列將教您使用 ASP.NET 4.7 和 Microsoft Visual Studio 建立 ASP.NET Web Forms 應用程式的基本概念
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 52d5eb7abe4520ebdf6667d299d055fc7619a635
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78568219"
---
# <a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a><span data-ttu-id="070b8-103">具有 ASP.NET 4.5 Web Forms 和 Visual Studio 2017 的消費者入門</span><span class="sxs-lookup"><span data-stu-id="070b8-103">Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2017</span></span>

<span data-ttu-id="070b8-104">[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="070b8-104">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

<span data-ttu-id="070b8-105">本教學課程系列會說明如何建立具有 ASP.NET 4.5 和 Microsoft Visual Studio 2017 的 ASP.NET Web form 應用程式。</span><span class="sxs-lookup"><span data-stu-id="070b8-105">This tutorial series shows you how to build an ASP.NET Web Forms application with ASP.NET 4.5 and Microsoft Visual Studio 2017.</span></span> 

## <a name="introduction"></a><span data-ttu-id="070b8-106">簡介</span><span class="sxs-lookup"><span data-stu-id="070b8-106">Introduction</span></span>

<span data-ttu-id="070b8-107">本教學課程系列會引導您使用 Visual Studio 2017 和 ASP.NET 4.5 來建立 ASP.NET Web Forms 應用程式。</span><span class="sxs-lookup"><span data-stu-id="070b8-107">This tutorial series guides you through creating an ASP.NET Web Forms application using Visual Studio 2017 and ASP.NET 4.5.</span></span> <span data-ttu-id="070b8-108">您將建立一個名為**Wingtip 玩具**的應用程式，這是一個簡化的店面網站，可在線上銷售專案。</span><span class="sxs-lookup"><span data-stu-id="070b8-108">You'll create an application named **Wingtip Toys** - a simplified storefront web site selling items online.</span></span> <span data-ttu-id="070b8-109">在此系列期間，會反白顯示新的 ASP.NET 4.5 功能。</span><span class="sxs-lookup"><span data-stu-id="070b8-109">During the series, new ASP.NET 4.5 features are highlighted.</span></span>

### <a name="target-audience"></a><span data-ttu-id="070b8-110">目標對象</span><span class="sxs-lookup"><span data-stu-id="070b8-110">Target audience</span></span>

<span data-ttu-id="070b8-111">ASP.NET Web form 的新開發人員是本教學課程系列的目標物件。</span><span class="sxs-lookup"><span data-stu-id="070b8-111">Developers new to ASP.NET Web Forms are the target audience for this tutorial series.</span></span>

<span data-ttu-id="070b8-112">在下列領域中，您應該有一些知識：</span><span class="sxs-lookup"><span data-stu-id="070b8-112">You should have some knowledge in the following areas:</span></span>

- <span data-ttu-id="070b8-113">物件導向程式設計（OOP）和語言</span><span class="sxs-lookup"><span data-stu-id="070b8-113">Object-oriented programming (OOP) and languages</span></span>
- <span data-ttu-id="070b8-114">Web 開發（HTML、CSS、JavaScript）</span><span class="sxs-lookup"><span data-stu-id="070b8-114">Web development (HTML, CSS, JavaScript)</span></span>
- <span data-ttu-id="070b8-115">關聯式資料庫</span><span class="sxs-lookup"><span data-stu-id="070b8-115">Relational databases</span></span>
- <span data-ttu-id="070b8-116">多層式架構</span><span class="sxs-lookup"><span data-stu-id="070b8-116">N-tier architecture</span></span>

<span data-ttu-id="070b8-117">若要查看這些區域，請考慮研究下列內容：</span><span class="sxs-lookup"><span data-stu-id="070b8-117">To review these areas, consider studying the following content:</span></span>

- [<span data-ttu-id="070b8-118">使用視覺效果消費者入門C#</span><span class="sxs-lookup"><span data-stu-id="070b8-118">Getting Started with Visual C#</span></span>](https://msdn.microsoft.com/library/a72418yk.aspx)
- <span data-ttu-id="070b8-119">[Web 開發](https://msdn.microsoft.com/beginner/bb308760.aspx)、 [HTML、CSS、JavaScript、SQL、PHP、JQuery](http://w3schools.com/)</span><span class="sxs-lookup"><span data-stu-id="070b8-119">[Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span></span>
- [<span data-ttu-id="070b8-120">關係資料庫</span><span class="sxs-lookup"><span data-stu-id="070b8-120">Relational database</span></span>](http://en.wikipedia.org/wiki/Relational_database)
- [<span data-ttu-id="070b8-121">多層式架構</span><span class="sxs-lookup"><span data-stu-id="070b8-121">Multitier architecture</span></span>](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a><span data-ttu-id="070b8-122">應用程式功能</span><span class="sxs-lookup"><span data-stu-id="070b8-122">Application features</span></span>

<span data-ttu-id="070b8-123">本系列提供的 ASP.NET Web Form 功能包括：</span><span class="sxs-lookup"><span data-stu-id="070b8-123">The ASP.NET Web Form features presented in this series include:</span></span>

- <span data-ttu-id="070b8-124">Web 應用程式專案（而非網站專案）</span><span class="sxs-lookup"><span data-stu-id="070b8-124">The Web Application Project (not Web Site Project)</span></span>
- <span data-ttu-id="070b8-125">Web Form</span><span class="sxs-lookup"><span data-stu-id="070b8-125">Web Forms</span></span>
- <span data-ttu-id="070b8-126">主版頁面，設定</span><span class="sxs-lookup"><span data-stu-id="070b8-126">Master Pages, Configuration</span></span>
- <span data-ttu-id="070b8-127">從中</span><span class="sxs-lookup"><span data-stu-id="070b8-127">Bootstrap</span></span>
- <span data-ttu-id="070b8-128">Entity Framework Code First、LocalDB</span><span class="sxs-lookup"><span data-stu-id="070b8-128">Entity Framework Code First, LocalDB</span></span>
- <span data-ttu-id="070b8-129">要求驗證</span><span class="sxs-lookup"><span data-stu-id="070b8-129">Request Validation</span></span>
- <span data-ttu-id="070b8-130">強型別資料控制</span><span class="sxs-lookup"><span data-stu-id="070b8-130">Strongly-typed Data Controls</span></span>
- <span data-ttu-id="070b8-131">模型繫結</span><span class="sxs-lookup"><span data-stu-id="070b8-131">Model Binding</span></span>
- <span data-ttu-id="070b8-132">資料註釋</span><span class="sxs-lookup"><span data-stu-id="070b8-132">Data Annotations</span></span>
- <span data-ttu-id="070b8-133">值提供者</span><span class="sxs-lookup"><span data-stu-id="070b8-133">Value Providers</span></span>
- <span data-ttu-id="070b8-134">SSL 和 OAuth</span><span class="sxs-lookup"><span data-stu-id="070b8-134">SSL and OAuth</span></span>
- <span data-ttu-id="070b8-135">ASP.NET Identity、設定和授權</span><span class="sxs-lookup"><span data-stu-id="070b8-135">ASP.NET Identity, Configuration, and Authorization</span></span>
- <span data-ttu-id="070b8-136">不顯眼的驗證</span><span class="sxs-lookup"><span data-stu-id="070b8-136">Unobtrusive Validation</span></span>
- <span data-ttu-id="070b8-137">路由</span><span class="sxs-lookup"><span data-stu-id="070b8-137">Routing</span></span>
- <span data-ttu-id="070b8-138">ASP.NET 錯誤處理</span><span class="sxs-lookup"><span data-stu-id="070b8-138">ASP.NET Error Handling</span></span>

### <a name="application-scenarios-and-tasks"></a><span data-ttu-id="070b8-139">應用程式案例和工作</span><span class="sxs-lookup"><span data-stu-id="070b8-139">Application scenarios and tasks</span></span>

<span data-ttu-id="070b8-140">教學課程系列工作包括：</span><span class="sxs-lookup"><span data-stu-id="070b8-140">Tutorial series tasks include:</span></span>

- <span data-ttu-id="070b8-141">建立、查看和執行新專案</span><span class="sxs-lookup"><span data-stu-id="070b8-141">Creating, reviewing, and running a new project</span></span>
- <span data-ttu-id="070b8-142">建立資料庫結構</span><span class="sxs-lookup"><span data-stu-id="070b8-142">Creating a database structure</span></span>
- <span data-ttu-id="070b8-143">初始化和植入資料庫</span><span class="sxs-lookup"><span data-stu-id="070b8-143">Initializing and seeding a database</span></span>
- <span data-ttu-id="070b8-144">使用樣式、圖形和主版頁面自訂 UI</span><span class="sxs-lookup"><span data-stu-id="070b8-144">Customizing the UI with styles, graphics, and a master page</span></span>
- <span data-ttu-id="070b8-145">加入頁面和導覽</span><span class="sxs-lookup"><span data-stu-id="070b8-145">Adding pages and navigation</span></span>
- <span data-ttu-id="070b8-146">顯示功能表細節和產品資料</span><span class="sxs-lookup"><span data-stu-id="070b8-146">Displaying menu details and product data</span></span>
- <span data-ttu-id="070b8-147">建立購物車</span><span class="sxs-lookup"><span data-stu-id="070b8-147">Creating a shopping cart</span></span>
- <span data-ttu-id="070b8-148">新增 SSL 和 OAuth 支援</span><span class="sxs-lookup"><span data-stu-id="070b8-148">Adding SSL and OAuth support</span></span>
- <span data-ttu-id="070b8-149">新增付款條件</span><span class="sxs-lookup"><span data-stu-id="070b8-149">Adding a payment method</span></span>
- <span data-ttu-id="070b8-150">包含系統管理員角色和使用者至應用程式</span><span class="sxs-lookup"><span data-stu-id="070b8-150">Including an administrator role and a user to the application</span></span>
- <span data-ttu-id="070b8-151">限制對特定頁面和資料夾的存取</span><span class="sxs-lookup"><span data-stu-id="070b8-151">Restricting access to specific pages and folder</span></span>
- <span data-ttu-id="070b8-152">將檔案上傳至 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="070b8-152">Uploading a file to the web application</span></span>
- <span data-ttu-id="070b8-153">執行輸入驗證</span><span class="sxs-lookup"><span data-stu-id="070b8-153">Implementing input validation</span></span>
- <span data-ttu-id="070b8-154">註冊 web 應用程式的路由</span><span class="sxs-lookup"><span data-stu-id="070b8-154">Registering routes for the web application</span></span>
- <span data-ttu-id="070b8-155">執行錯誤處理和錯誤記錄</span><span class="sxs-lookup"><span data-stu-id="070b8-155">Implementing error handling and error logging</span></span>

## <a name="overview"></a><span data-ttu-id="070b8-156">概觀</span><span class="sxs-lookup"><span data-stu-id="070b8-156">Overview</span></span>

<span data-ttu-id="070b8-157">本教學課程系列適用于熟悉程式設計概念的人，但 ASP.NET Web form 的新手。</span><span class="sxs-lookup"><span data-stu-id="070b8-157">This tutorial series is intended for someone familiar with programming concepts, but new to ASP.NET Web Forms.</span></span> <span data-ttu-id="070b8-158">如果您已經熟悉 ASP.NET Web form，此系列仍然可以協助您瞭解新的 ASP.NET 4.5 功能。</span><span class="sxs-lookup"><span data-stu-id="070b8-158">If you're already familiar with ASP.NET Web Forms, this series can still help you learn about new ASP.NET 4.5 features.</span></span> <span data-ttu-id="070b8-159">對於不熟悉程式設計概念和 ASP.NET Web form 的讀者，請參閱 ASP.NET 網站上[消費者入門](../../../index.md)一節中提供的其他 Web form 教學課程。</span><span class="sxs-lookup"><span data-stu-id="070b8-159">For readers unfamiliar with programming concepts and ASP.NET Web Forms, see the additional Web Forms tutorials provided in the [Getting Started](../../../index.md) section on the ASP.NET Web site.</span></span>

<span data-ttu-id="070b8-160">本教學課程系列中提供的 ASP.NET 4.5 包含下列功能：</span><span class="sxs-lookup"><span data-stu-id="070b8-160">The ASP.NET 4.5 provided in this tutorial series includes the following features:</span></span>

- <span data-ttu-id="070b8-161">用於建立專案的簡單 UI，可提供[許多 ASP.NET](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add)架構（web FORM、MVC 和 web API）的支援。</span><span class="sxs-lookup"><span data-stu-id="070b8-161">A simple UI for creating projects that offers [support for many ASP.NET frameworks](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC, and Web API).</span></span>
- <span data-ttu-id="070b8-162">[啟動](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)程式、版面配置、主題和回應式設計架構。</span><span class="sxs-lookup"><span data-stu-id="070b8-162">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), a layout, theming, and responsive design framework.</span></span>
- <span data-ttu-id="070b8-163">[ASP.NET Identity](../../../../identity/index.md)，這是一個新的 ASP.NET 成員資格系統，在所有 ASP.NET 架構中的運作方式都相同，並可與 IIS 以外的 web 主控軟體搭配運作。</span><span class="sxs-lookup"><span data-stu-id="070b8-163">[ASP.NET Identity](../../../../identity/index.md), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
- [<span data-ttu-id="070b8-164">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="070b8-164">Entity Framework 6</span></span>](https://msdn.microsoft.com/data/ef.aspx)

  <span data-ttu-id="070b8-165">Entity Framework 的更新可讓您：</span><span class="sxs-lookup"><span data-stu-id="070b8-165">An update to the Entity Framework enabling you to:</span></span>
  - <span data-ttu-id="070b8-166">以強型別物件的形式抓取和運算元據</span><span class="sxs-lookup"><span data-stu-id="070b8-166">Retrieve and manipulate data as strongly-typed objects</span></span>
  - <span data-ttu-id="070b8-167">以非同步方式存取資料</span><span class="sxs-lookup"><span data-stu-id="070b8-167">Access data asynchronously</span></span>
  - <span data-ttu-id="070b8-168">處理暫時性連接錯誤</span><span class="sxs-lookup"><span data-stu-id="070b8-168">Handle transient connection faults</span></span>
  - <span data-ttu-id="070b8-169">記錄 SQL 語句</span><span class="sxs-lookup"><span data-stu-id="070b8-169">Log SQL statements</span></span>

<span data-ttu-id="070b8-170">如需完整的 ASP.NET 4.5 功能清單，請參閱[Visual Studio 2013 版本資訊的 ASP.NET 和 Web 工具](../../../../visual-studio/overview/2013/release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="070b8-170">For a complete ASP.NET 4.5 feature list, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span>

### <a name="the-wingtip-toys-sample-application"></a><span data-ttu-id="070b8-171">Wingtip 玩具範例應用程式</span><span class="sxs-lookup"><span data-stu-id="070b8-171">The Wingtip Toys sample application</span></span>

<span data-ttu-id="070b8-172">下列螢幕擷取畫面是來自您在本教學課程系列中建立的 ASP.NET Web Forms 應用程式。</span><span class="sxs-lookup"><span data-stu-id="070b8-172">The following screenshots are from the ASP.NET Web Forms application that you create in this tutorial series.</span></span> <span data-ttu-id="070b8-173">當您在 Visual Studio 中執行應用程式時，會出現下列 web 首頁。</span><span class="sxs-lookup"><span data-stu-id="070b8-173">When you run the application in Visual Studio, the following web Home page appears.</span></span>

![Wingtip 玩具-預設頁面](introduction-and-overview/_static/image1.png)

<span data-ttu-id="070b8-175">您可以註冊為新的使用者，或以現有的使用者身分登入。</span><span class="sxs-lookup"><span data-stu-id="070b8-175">You can register as a new user, or sign in as an existing user.</span></span> <span data-ttu-id="070b8-176">頂端導覽具有從資料庫到產品類別目錄及其產品的連結。</span><span class="sxs-lookup"><span data-stu-id="070b8-176">The top navigation has links to product categories and their products from the database.</span></span>

<span data-ttu-id="070b8-177">如果您選取 [**產品**]，則會顯示所有可用的產品。</span><span class="sxs-lookup"><span data-stu-id="070b8-177">If you select **Products**, all available products are displayed.</span></span> 

![Wingtip 玩具-產品](introduction-and-overview/_static/image2.png)

<span data-ttu-id="070b8-179">如果您選取特定產品，則會顯示產品詳細資料。</span><span class="sxs-lookup"><span data-stu-id="070b8-179">If you select a specific product, product details are displayed.</span></span>

![Wingtip 玩具-產品詳細資料](introduction-and-overview/_static/image3.png)

<span data-ttu-id="070b8-181">身為使用者，您可以使用 Web Forms 範本預設功能進行註冊和登入。</span><span class="sxs-lookup"><span data-stu-id="070b8-181">As a user, you can register and sign in with Web Forms template default functionality.</span></span> <span data-ttu-id="070b8-182">本教學課程也會說明如何使用現有的 Gmail 帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="070b8-182">This tutorial also explains how to sign in using an existing Gmail account.</span></span> <span data-ttu-id="070b8-183">此外，您可以用系統管理員身分登入，以便在資料庫中新增和移除產品。</span><span class="sxs-lookup"><span data-stu-id="070b8-183">Additionally, you can sign in as the administrator to add and remove products from the database.</span></span>

![Wingtip 玩具-登入](introduction-and-overview/_static/image4.png)

<span data-ttu-id="070b8-185">以使用者身分登入之後，您可以將產品新增至購物車，並簽出 PayPal。</span><span class="sxs-lookup"><span data-stu-id="070b8-185">Once you've signed in as a user, you can add products to the shopping cart and checkout with PayPal.</span></span> <span data-ttu-id="070b8-186">範例應用程式是設計來在 PayPal 的開發人員沙箱中工作。</span><span class="sxs-lookup"><span data-stu-id="070b8-186">The sample application is designed to work in PayPal's developer sandbox.</span></span> <span data-ttu-id="070b8-187">不會發生實際的 money 交易。</span><span class="sxs-lookup"><span data-stu-id="070b8-187">No actual money transaction takes place.</span></span>

![Wingtip 玩具-購物車](introduction-and-overview/_static/image5.png)

<span data-ttu-id="070b8-189">PayPal 會確認您的帳戶、訂購和付款資訊。</span><span class="sxs-lookup"><span data-stu-id="070b8-189">PayPal confirms your account, order, and payment information.</span></span>

![Wingtip 玩具-PayPal](introduction-and-overview/_static/image6.png)

<span data-ttu-id="070b8-191">從 PayPal 傳回之後，您可以檢查並完成您的訂單。</span><span class="sxs-lookup"><span data-stu-id="070b8-191">After returning from PayPal, you can review and complete your order.</span></span>

![Wingtip 玩具-訂購評論](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a><span data-ttu-id="070b8-193">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="070b8-193">Prerequisites</span></span>

<span data-ttu-id="070b8-194">開始之前，請確定您的電腦上已安裝下列軟體：</span><span class="sxs-lookup"><span data-stu-id="070b8-194">Before you start, make sure the following software is installed on your computer:</span></span>

- <span data-ttu-id="070b8-195">[Microsoft Visual Studio 2017 或 Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="070b8-195">[Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).</span></span>

<span data-ttu-id="070b8-196">.NET Framework 會自動安裝。</span><span class="sxs-lookup"><span data-stu-id="070b8-196">The .NET Framework is installed automatically.</span></span>

<span data-ttu-id="070b8-197">本教學課程系列使用 Microsoft Visual Studio Community 2017。</span><span class="sxs-lookup"><span data-stu-id="070b8-197">This tutorial series uses Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="070b8-198">您可以使用該方法或 Microsoft Visual Studio 2017 來完成此教學課程系列。</span><span class="sxs-lookup"><span data-stu-id="070b8-198">You can use either that or Microsoft Visual Studio 2017 to complete this tutorial series.</span></span>

<span data-ttu-id="070b8-199">請注意下列關於 Visual Studio 的事項：</span><span class="sxs-lookup"><span data-stu-id="070b8-199">Note the following about Visual Studio:</span></span>

* <span data-ttu-id="070b8-200">Microsoft Visual Studio 2017 和 Microsoft Visual Studio Community 2017 在本教學課程系列中稱為*Visual Studio* 。</span><span class="sxs-lookup"><span data-stu-id="070b8-200">Microsoft Visual Studio 2017 and Microsoft Visual Studio Community 2017 are referred to as *Visual Studio* throughout this tutorial series.</span></span>

* <span data-ttu-id="070b8-201">Visual Studio 2017 會安裝在已安裝的任何舊版本旁邊。</span><span class="sxs-lookup"><span data-stu-id="070b8-201">Visual Studio 2017 is installed next to any older versions already installed.</span></span> <span data-ttu-id="070b8-202">在舊版中建立的網站可以在 Visual Studio 2017 中開啟，並繼續在舊版中開啟。</span><span class="sxs-lookup"><span data-stu-id="070b8-202">Sites created in earlier versions can be opened in Visual Studio 2017 and continue to open in previous versions.</span></span>

* <span data-ttu-id="070b8-203">第一次開始 Visual Studio 時，會假設您已選取 [ *Web 開發*] 設定。</span><span class="sxs-lookup"><span data-stu-id="070b8-203">The first time you started Visual Studio, it is assumed you selected the *Web Development* settings.</span></span> <span data-ttu-id="070b8-204">如需詳細資訊，請參閱[如何：選取 Web 開發環境設定](https://msdn.microsoft.com/library/ff521558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="070b8-204">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

<span data-ttu-id="070b8-205">安裝必要條件之後，您就可以開始建立本教學課程系列中所提供的 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="070b8-205">After installing the prerequisites, you're ready to begin creating the Web project presented in this tutorial series.</span></span>

## <a name="download-the-sample-application"></a><span data-ttu-id="070b8-206">下載範例應用程式</span><span class="sxs-lookup"><span data-stu-id="070b8-206">Download the sample application</span></span>

 <span data-ttu-id="070b8-207">您可以隨時從 MSDN 範例網站下載完整的範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="070b8-207">You can download the completed sample application at anytime from the MSDN Samples site:</span></span>

<span data-ttu-id="070b8-208">[使用 ASP.NET 4.5 Web Forms 和 Visual Studio 2013 Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)（C#）的消費者入門</span><span class="sxs-lookup"><span data-stu-id="070b8-208">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span> 

 <span data-ttu-id="070b8-209">此下載包含下列專案：</span><span class="sxs-lookup"><span data-stu-id="070b8-209">This download has the following items:</span></span>

- <span data-ttu-id="070b8-210">*WingtipToys*資料夾中的範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="070b8-210">The sample application in the *WingtipToys* folder.</span></span>
- <span data-ttu-id="070b8-211">用來在 [ *WingtipToys* ] 資料夾的 [ *WingtipToys-資產*] 資料夾中建立範例應用程式的資源。</span><span class="sxs-lookup"><span data-stu-id="070b8-211">The resources used to create the sample application in the *WingtipToys-Assets* folder in the *WingtipToys* folder.</span></span>

<span data-ttu-id="070b8-212">下載為 *.zip*檔案。</span><span class="sxs-lookup"><span data-stu-id="070b8-212">The download is a *.zip* file.</span></span> <span data-ttu-id="070b8-213">若要查看此教學課程系列所建立的已完成專案，請*C#* 尋找並選取 .zip 檔案中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="070b8-213">To see the completed project that this tutorial series creates, find and select the *C#* folder in the .zip file.</span></span> <span data-ttu-id="070b8-214">將C#資料夾儲存至您用來處理 Visual Studio 專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="070b8-214">Save the C# folder to the folder you use to work with Visual Studio projects.</span></span> <span data-ttu-id="070b8-215">根據預設，Visual Studio 2017 projects 資料夾為：</span><span class="sxs-lookup"><span data-stu-id="070b8-215">By default, the Visual Studio 2017 projects folder is:</span></span>

<span data-ttu-id="070b8-216"><strong>C:\Users&#92;</strong>  <strong><em>&lt;username&gt;</em></strong> <strong>\source\repos</strong></span><span class="sxs-lookup"><span data-stu-id="070b8-216"><strong>C:\Users&#92;</strong><strong><em>&lt;username&gt;</em></strong><strong>\source\repos</strong></span></span>

<span data-ttu-id="070b8-217">將***C#*** 資料夾重新命名為***WingtipToys***。</span><span class="sxs-lookup"><span data-stu-id="070b8-217">Rename the ***C#*** folder to ***WingtipToys***.</span></span>

> [!NOTE]
> <span data-ttu-id="070b8-218">如果您的 [專案] 資料夾中已經有名為*WingtipToys*的資料夾，請在將*C#* 資料夾重新命名為*WingtipToys*之前，暫時將該現有資料夾重新命名。</span><span class="sxs-lookup"><span data-stu-id="070b8-218">If you already have a folder named *WingtipToys* in your Projects folder, temporarily rename that existing folder before renaming the *C#* folder to *WingtipToys*.</span></span>

<span data-ttu-id="070b8-219">若要執行已完成的專案，請開啟 [ *WingtipToys* ] 資料夾，然後按兩下 [ *WingtipToys* ] 檔案。</span><span class="sxs-lookup"><span data-stu-id="070b8-219">To run the completed project, open the *WingtipToys* folder and double-click the *WingtipToys.sln* file.</span></span> <span data-ttu-id="070b8-220">Visual Studio 2017 會開啟專案。</span><span class="sxs-lookup"><span data-stu-id="070b8-220">Visual Studio 2017 opens the project.</span></span> <span data-ttu-id="070b8-221">接下來，在**方案總管**中的*default.aspx*檔案上按一下滑鼠右鍵，然後**在瀏覽器中**選取 [View]。</span><span class="sxs-lookup"><span data-stu-id="070b8-221">Next, right-click the *Default.aspx* file in **Solution Explorer** and select **View In Browser**.</span></span>

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a><span data-ttu-id="070b8-222">參加 ASP.NET Web Forms 測驗以審查內容</span><span class="sxs-lookup"><span data-stu-id="070b8-222">Take a ASP.NET Web Forms quiz to review content</span></span>

<span data-ttu-id="070b8-223">完成本教學課程系列之後，請進行測驗來測試您的知識並強化重要概念。</span><span class="sxs-lookup"><span data-stu-id="070b8-223">After completing the tutorial series, take a quiz to test your knowledge and reinforce key concepts.</span></span> <span data-ttu-id="070b8-224">每個問題都提供其他指引的說明和連結。</span><span class="sxs-lookup"><span data-stu-id="070b8-224">Each question provides an explanation and links to additional guidance.</span></span>

* [<span data-ttu-id="070b8-225">ASP.NET Web Forms 測驗</span><span class="sxs-lookup"><span data-stu-id="070b8-225">ASP.NET Web Forms Quiz</span></span>](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a><span data-ttu-id="070b8-226">教學課程支援和批註</span><span class="sxs-lookup"><span data-stu-id="070b8-226">Tutorial support and comments</span></span>

<span data-ttu-id="070b8-227">如有問題和意見，請使用[ASP.NET 4.5 Web Forms 和 Visual Studio 2013 Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)（C#）範例頁面上包含的消費者入門的 Q 和 A 區段。</span><span class="sxs-lookup"><span data-stu-id="070b8-227">For questions and comments, use the Q and A section included on the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span>

<span data-ttu-id="070b8-228">歡迎使用此教學課程系列的批註。</span><span class="sxs-lookup"><span data-stu-id="070b8-228">Comments on this tutorial series are welcome.</span></span> <span data-ttu-id="070b8-229">當此教學課程系列更新時，每次致力於考慮改善的更正或建議。</span><span class="sxs-lookup"><span data-stu-id="070b8-229">When this tutorial series is updated, every effort is made to consider corrections or suggestions for improvements.</span></span>

<span data-ttu-id="070b8-230">如果發生錯誤，對應的錯誤訊息可能會造成混淆，而不會有如何修正此問題的絕佳說明。</span><span class="sxs-lookup"><span data-stu-id="070b8-230">If an error occurs, the corresponding error messages could be confusing, with no good explanation on how to fix it.</span></span> <span data-ttu-id="070b8-231">如需協助，您可以查看[ASP.NET 論壇](https://forums.asp.net/)。</span><span class="sxs-lookup"><span data-stu-id="070b8-231">For help, you can check the [ASP.NET forums](https://forums.asp.net/).</span></span> <span data-ttu-id="070b8-232">另一個不錯的來源是消費者入門中的 Q 和一節[與 ASP.NET 4.5 Web Forms 和 Visual Studio 2013 Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)（C#）範例頁面。</span><span class="sxs-lookup"><span data-stu-id="070b8-232">Another good source is the Q and A section in the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="070b8-233">下一個</span><span class="sxs-lookup"><span data-stu-id="070b8-233">Next</span></span>](create-the-project.md)
