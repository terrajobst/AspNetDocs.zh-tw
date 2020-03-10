---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC 簡介 |Microsoft Docs
author: shanselman
description: 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 建立可從資料庫讀取和寫入的簡單 web 應用程式。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581582"
---
# <a name="intro-to-aspnet-mvc"></a><span data-ttu-id="a42ba-104">ASP.NET MVC 簡介</span><span class="sxs-lookup"><span data-stu-id="a42ba-104">Intro to ASP.NET MVC</span></span>

<span data-ttu-id="a42ba-105">由[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="a42ba-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="a42ba-106">如果本教學[課程](../../getting-started/introduction/getting-started.md)可在此使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，則為更新版本。</span><span class="sxs-lookup"><span data-stu-id="a42ba-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="a42ba-107">新的教學課程會使用 ASP.NET MVC 5，這在此教學課程中提供了許多改進功能。</span><span class="sxs-lookup"><span data-stu-id="a42ba-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="a42ba-108">這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="a42ba-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="a42ba-109">您將建立可從資料庫讀取和寫入的簡單 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a42ba-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="a42ba-110">請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。</span><span class="sxs-lookup"><span data-stu-id="a42ba-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="a42ba-111">讓我們使用[Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)來製作第一個 ASP.NET MVC Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a42ba-111">Let's make our first ASP.NET MVC Web Application using [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="a42ba-112">我們將製作一個小電影清單的應用程式，讓我們建立和列出電影。</span><span class="sxs-lookup"><span data-stu-id="a42ba-112">We'll make a little Movie list application that will let us create and list movies.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="a42ba-113">您要建置的內容</span><span class="sxs-lookup"><span data-stu-id="a42ba-113">What You'll Build</span></span>

<span data-ttu-id="a42ba-114">以下是您將建立之應用程式的兩個螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="a42ba-114">Here are two screenshots of the application you'll build.</span></span> <span data-ttu-id="a42ba-115">您將會有一個具有各種資料行的簡單電影資料表。</span><span class="sxs-lookup"><span data-stu-id="a42ba-115">You will have a simple table of movies with various columns.</span></span>

<span data-ttu-id="a42ba-116">[![電影清單-Windows Internet Explorer （12）](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a42ba-116">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span></span>

<span data-ttu-id="a42ba-117">您將會有一個建立表單，讓我們可以將電影加入清單中。</span><span class="sxs-lookup"><span data-stu-id="a42ba-117">And you'll have a Create Form so we can add movies to the list.</span></span>

<span data-ttu-id="a42ba-118">[![建立電影-Windows Internet Explorer （2）](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="a42ba-118">[![Create a Movie - Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="a42ba-119">您要學習的技術</span><span class="sxs-lookup"><span data-stu-id="a42ba-119">Skills You'll Learn</span></span>

<span data-ttu-id="a42ba-120">本教學課程將告訴您使用 Visual Studio 建立 ASP.NET MVC Web 應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="a42ba-120">This tutorial will teach you the basics of building an ASP.NET MVC Web Application using Visual Studio.</span></span> <span data-ttu-id="a42ba-121">您將了解：</span><span class="sxs-lookup"><span data-stu-id="a42ba-121">You'll learn:</span></span>

- <span data-ttu-id="a42ba-122">如何建立新的 ASP.NET MVC 專案</span><span class="sxs-lookup"><span data-stu-id="a42ba-122">How to create a new ASP.NET MVC Project</span></span>
- <span data-ttu-id="a42ba-123">如何使用 SQL Server 建立新的資料庫</span><span class="sxs-lookup"><span data-stu-id="a42ba-123">How to create a new Database with SQL Server</span></span>
- <span data-ttu-id="a42ba-124">如何建立 ASP.NET MVC 控制器和 Views</span><span class="sxs-lookup"><span data-stu-id="a42ba-124">How to create ASP.NET MVC Controllers and Views</span></span>
- <span data-ttu-id="a42ba-125">如何取出和顯示資料</span><span class="sxs-lookup"><span data-stu-id="a42ba-125">How to retrieve and display data</span></span>
- <span data-ttu-id="a42ba-126">如何編輯資料並啟用資料驗證</span><span class="sxs-lookup"><span data-stu-id="a42ba-126">How to edit data and enable data validation</span></span>
- <span data-ttu-id="a42ba-127">如何更新資料庫架構</span><span class="sxs-lookup"><span data-stu-id="a42ba-127">How to update the database schema</span></span>

## <a name="get-started"></a><span data-ttu-id="a42ba-128">開始使用</span><span class="sxs-lookup"><span data-stu-id="a42ba-128">Get Started</span></span>

<span data-ttu-id="a42ba-129">一開始先執行 Visual Web Developer 2010 Express （我會從現在稱為「VWD」），然後從 [開始] 畫面選取 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="a42ba-129">Start by running Visual Web Developer 2010 Express (I'll call it "VWD" from now on) and select New Project from the Start Screen.</span></span>

<span data-ttu-id="a42ba-130">Visual Web Developer 是一個 IDE，也是整合式開發人員環境。</span><span class="sxs-lookup"><span data-stu-id="a42ba-130">Visual Web Developer is an IDE, or Integrated Developer Environment.</span></span> <span data-ttu-id="a42ba-131">就像您使用 Microsoft Word 來撰寫檔一樣，您將使用 IDE 來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="a42ba-131">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="a42ba-132">頂端還有一個工具列，其中顯示您可以使用的各種選項，以及您也可以用來選取檔案的功能表 |新增專案。</span><span class="sxs-lookup"><span data-stu-id="a42ba-132">There's a toolbar along the top showing various options available to you, as well as the menu you could also have used to Select File | New project.</span></span>

<span data-ttu-id="a42ba-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="a42ba-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span></span>

## <a name="creating-your-first-application"></a><span data-ttu-id="a42ba-134">建立您的第一個應用程式</span><span class="sxs-lookup"><span data-stu-id="a42ba-134">Creating Your First Application</span></span>

<span data-ttu-id="a42ba-135">您可以使用 Visual Basic 或視覺效果C#來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="a42ba-135">You can create applications using Visual Basic or Visual C#.</span></span> <span data-ttu-id="a42ba-136">現在，選取左側的C# [視覺效果]，然後挑選 [ASP.NET MVC 2 Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a42ba-136">For now, Select Visual C# on the left, then pick "ASP.NET MVC 2 Web Application."</span></span> <span data-ttu-id="a42ba-137">將您的專案命名為「電影」，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a42ba-137">Name your project "Movies" and click OK.</span></span>

<span data-ttu-id="a42ba-138">[![新增專案](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="a42ba-138">[![New Project](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span></span>

<span data-ttu-id="a42ba-139">右側是顯示應用程式中所有檔案和資料夾的方案總管。</span><span class="sxs-lookup"><span data-stu-id="a42ba-139">On the right-hand side is the Solution Explorer showing all the files and folders in your application.</span></span> <span data-ttu-id="a42ba-140">中間的大視窗是您編輯程式碼，並花費大多數時間的地方。</span><span class="sxs-lookup"><span data-stu-id="a42ba-140">The big window in the middle is where you edit your code and spend most of your time.</span></span> <span data-ttu-id="a42ba-141">Visual Studio 使用您剛建立的 ASP.NET MVC 專案的預設範本，所以您現在有一個可運作的應用程式，而不需要執行任何動作！</span><span class="sxs-lookup"><span data-stu-id="a42ba-141">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="a42ba-142">這是簡單的「Hello World！</span><span class="sxs-lookup"><span data-stu-id="a42ba-142">This is a simple "Hello World!</span></span> <span data-ttu-id="a42ba-143">專案，這是我們應用程式的好起點。</span><span class="sxs-lookup"><span data-stu-id="a42ba-143">project, and it is a good place to start for our application.</span></span>

<span data-ttu-id="a42ba-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="a42ba-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span></span>

<span data-ttu-id="a42ba-145">選取工具列上的 [播放] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a42ba-145">Select the "play" button to the toolbar.</span></span>

![[偵錯]](getting-started-with-mvc-part1/_static/image11.png)

<span data-ttu-id="a42ba-147">它是指向右側的綠色箭號，它會編譯您的程式，並在網頁瀏覽器中啟動您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a42ba-147">It's a green arrow pointing to the right that will compile your program and start your application in a web browser.</span></span>

<span data-ttu-id="a42ba-148">*注意：您可以改為在鍵盤上按 F5，或從 [Debug] 功能表中選取 [Debug-&gt;開始偵錯工具]。*</span><span class="sxs-lookup"><span data-stu-id="a42ba-148">*NOTE: You can instead press F5 on your keyboard, or select Debug-&gt;Start Debugging from the "Debug" menu.*</span></span>

<span data-ttu-id="a42ba-149">這會導致 Visual Web Developer 啟動開發 web 伺服器，並執行 web 應用程式（不需要進行任何設定或手動步驟即可啟用）。</span><span class="sxs-lookup"><span data-stu-id="a42ba-149">This will cause Visual Web Developer to start a development web-server and run our web application (there are no configuration or manual steps required to enable this).</span></span> <span data-ttu-id="a42ba-150">接著，它會啟動瀏覽器，並將它設定為流覽應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="a42ba-150">It will then launch a browser and configure it to browse the application's home-page.</span></span> <span data-ttu-id="a42ba-151">請注意，瀏覽器的網址列會顯示 "localhost"，而不是類似 example.com 的專案。</span><span class="sxs-lookup"><span data-stu-id="a42ba-151">Notice below that the address bar of the browser says "localhost", and not something like example.com.</span></span> <span data-ttu-id="a42ba-152">這是因為 localhost 一律會指向您自己的本機電腦，在此情況下，會執行我們剛才建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a42ba-152">That's because localhost always points to your own local computer - which in this case is running the application we just built.</span></span>

<span data-ttu-id="a42ba-153">[![首頁](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="a42ba-153">[![Home Page](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span></span>

<span data-ttu-id="a42ba-154">現成的預設範本會提供您兩個要造訪的頁面和一個基本的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="a42ba-154">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="a42ba-155">讓我們來變更此應用程式的運作方式，並稍微瞭解如何在進程中 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="a42ba-155">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="a42ba-156">關閉您的瀏覽器，並讓變更一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="a42ba-156">Close your browser and lets change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a42ba-157">下一個</span><span class="sxs-lookup"><span data-stu-id="a42ba-157">Next</span></span>](getting-started-with-mvc-part2.md)
