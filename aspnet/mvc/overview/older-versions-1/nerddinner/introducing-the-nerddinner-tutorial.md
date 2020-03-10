---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: NerdDinner 教學課程簡介 |Microsoft Docs
author: shanselman
description: 學習新架構的最佳方式是使用它來建立一些專案。 本教學課程逐步解說如何使用 ASP.NE 建立一個小型但完整的應用程式 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580574"
---
# <a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="f734f-104">NerdDinner 教學課程簡介</span><span class="sxs-lookup"><span data-stu-id="f734f-104">Introducing the NerdDinner Tutorial</span></span>

<span data-ttu-id="f734f-105">由[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="f734f-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

[<span data-ttu-id="f734f-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="f734f-106">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="f734f-107">學習新架構的最佳方式是使用它來建立一些專案。</span><span class="sxs-lookup"><span data-stu-id="f734f-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="f734f-108">本教學課程逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的應用程式，並介紹其背後的一些核心概念。</span><span class="sxs-lookup"><span data-stu-id="f734f-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="f734f-109">如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="f734f-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-tutorial"></a><span data-ttu-id="f734f-110">NerdDinner 教學課程</span><span class="sxs-lookup"><span data-stu-id="f734f-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="f734f-111">學習新架構的最佳方式是使用它來建立一些專案。</span><span class="sxs-lookup"><span data-stu-id="f734f-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="f734f-112">本教學課程逐步解說如何使用 ASP.NET MVC 建立一個小型但完整的應用程式，並介紹其背後的一些核心概念。</span><span class="sxs-lookup"><span data-stu-id="f734f-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="f734f-113">我們即將建立的應用程式稱為「NerdDinner」。</span><span class="sxs-lookup"><span data-stu-id="f734f-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="f734f-114">NerdDinner 提供一種簡單的方式，讓人們能夠在線上尋找和組織 dinners：</span><span class="sxs-lookup"><span data-stu-id="f734f-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="f734f-115">NerdDinner 可讓已註冊的使用者建立、編輯和刪除 dinners。</span><span class="sxs-lookup"><span data-stu-id="f734f-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="f734f-116">它會在整個應用程式中強制執行一組一致的驗證和商務規則：</span><span class="sxs-lookup"><span data-stu-id="f734f-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="f734f-117">訪客可以使用以 AJAX 為基礎的對應來搜尋即將保留的 dinners：</span><span class="sxs-lookup"><span data-stu-id="f734f-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="f734f-118">按一下晚餐會將他們帶到詳細資料頁面，讓他們深入瞭解：</span><span class="sxs-lookup"><span data-stu-id="f734f-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="f734f-119">如果他們有興趣參加晚餐，他們可以在網站上登入或註冊：</span><span class="sxs-lookup"><span data-stu-id="f734f-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="f734f-120">他們可以按一下以 AJAX 為基礎的 RSVP 連結來參加活動：</span><span class="sxs-lookup"><span data-stu-id="f734f-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="f734f-121">執行 NerdDinner</span><span class="sxs-lookup"><span data-stu-id="f734f-121">Implementing NerdDinner</span></span>

<span data-ttu-id="f734f-122">我們即將開始我們的 NerdDinner 應用程式，方法是使用 Visual Studio 內的檔案&gt;[新增專案] 命令，建立全新的 ASP.NET MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="f734f-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="f734f-123">然後，我們會以累加方式新增功能和功能。</span><span class="sxs-lookup"><span data-stu-id="f734f-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="f734f-124">在本文中，我們將討論：</span><span class="sxs-lookup"><span data-stu-id="f734f-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="f734f-125">如何建立新的 ASP.NET MVC 專案</span><span class="sxs-lookup"><span data-stu-id="f734f-125">How to create a new ASP.NET MVC Project</span></span>](create-a-new-aspnet-mvc-project.md)
2. [<span data-ttu-id="f734f-126">如何建立資料庫</span><span class="sxs-lookup"><span data-stu-id="f734f-126">How to create a database</span></span>](create-a-database.md)
3. [<span data-ttu-id="f734f-127">如何使用商務規則驗證來建立模型</span><span class="sxs-lookup"><span data-stu-id="f734f-127">How to build a model with business rule validations</span></span>](build-a-model-with-business-rule-validations.md)
4. [<span data-ttu-id="f734f-128">如何使用控制器和 views 來執行清單/詳細資料 UI</span><span class="sxs-lookup"><span data-stu-id="f734f-128">How to use controllers and views to implement a listing/details UI</span></span>](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [<span data-ttu-id="f734f-129">如何提供 CRUD （建立、讀取、更新、刪除）資料表單專案支援</span><span class="sxs-lookup"><span data-stu-id="f734f-129">How to provide CRUD (create, read, update, delete) data form entry support</span></span>](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [<span data-ttu-id="f734f-130">如何使用 ViewData 和執行 ViewModel 類別</span><span class="sxs-lookup"><span data-stu-id="f734f-130">How to use ViewData and implement ViewModel classes</span></span>](use-viewdata-and-implement-viewmodel-classes.md)
7. [<span data-ttu-id="f734f-131">如何使用主版頁面和部分重新使用 UI</span><span class="sxs-lookup"><span data-stu-id="f734f-131">How to re-use UI using master pages and partials</span></span>](re-use-ui-using-master-pages-and-partials.md)
8. [<span data-ttu-id="f734f-132">如何實行有效率的資料分頁</span><span class="sxs-lookup"><span data-stu-id="f734f-132">How to implement efficient data paging</span></span>](implement-efficient-data-paging.md)
9. [<span data-ttu-id="f734f-133">如何使用驗證和授權保護應用程式</span><span class="sxs-lookup"><span data-stu-id="f734f-133">How to secure applications using authentication and authorization</span></span>](secure-applications-using-authentication-and-authorization.md)
10. [<span data-ttu-id="f734f-134">如何使用 AJAX 傳遞動態更新</span><span class="sxs-lookup"><span data-stu-id="f734f-134">How to use AJAX to deliver dynamic updates</span></span>](use-ajax-to-deliver-dynamic-updates.md)
11. [<span data-ttu-id="f734f-135">如何使用 AJAX 來執行對應案例</span><span class="sxs-lookup"><span data-stu-id="f734f-135">How to use AJAX to implement mapping scenarios</span></span>](use-ajax-to-implement-mapping-scenarios.md)
12. [<span data-ttu-id="f734f-136">如何啟用自動化單元測試</span><span class="sxs-lookup"><span data-stu-id="f734f-136">How to enable automated unit testing</span></span>](enable-automated-unit-testing.md)

<span data-ttu-id="f734f-137">您可以完成本章節逐步解說的每個步驟，從頭建立自己的 NerdDinner 複本。</span><span class="sxs-lookup"><span data-stu-id="f734f-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="f734f-138">或者，您可以在這裡下載原始程式碼的完整版本： [GitHub 上的 NerdDinner](https://github.com/AspNetMVPSamples/NerdDinner)。</span><span class="sxs-lookup"><span data-stu-id="f734f-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="f734f-139">如果您想要離線閱讀本教學課程，您也可以選擇性地[下載本教學課程的免費 PDF 版本](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)。</span><span class="sxs-lookup"><span data-stu-id="f734f-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="f734f-140">您可以使用 Visual Studio 2008 或免費的 Visual Web Developer 2008 Express 來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="f734f-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="f734f-141">您可以使用 SQL Server 或資料庫的免費 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="f734f-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="f734f-142">您可以使用[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)的 V2 安裝 ASP.NET MVC、Visual Web Developer 2008 Express 和 SQL Server Express （所有免費）</span><span class="sxs-lookup"><span data-stu-id="f734f-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="f734f-143">現在讓我們開始吧 。</span><span class="sxs-lookup"><span data-stu-id="f734f-143">Now let's get started....</span></span>

<span data-ttu-id="f734f-144">既然我們已經討論過什麼 NerdDinner，讓我們來匯總卷起袖子並撰寫一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="f734f-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="f734f-145">我們會先使用 Visual Studio 中的檔案&gt;新專案來建立 NerdDinner 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f734f-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f734f-146">下一個</span><span class="sxs-lookup"><span data-stu-id="f734f-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)
