---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 簡介（C#） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: e71275c93558c0b6ca087a145786e8c846b69721
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540667"
---
# <a name="intro-to-aspnet-mvc-3-c"></a><span data-ttu-id="5aea9-103">ASP.NET MVC 3 簡介 (C#)</span><span class="sxs-lookup"><span data-stu-id="5aea9-103">Intro to ASP.NET MVC 3 (C#)</span></span>

<span data-ttu-id="5aea9-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="5aea9-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="5aea9-105">本教學課程的更新版本可在[這裡](../../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="5aea9-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="5aea9-106">它更安全、更容易遵循，並示範更多功能。</span><span class="sxs-lookup"><span data-stu-id="5aea9-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="5aea9-107">本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。</span><span class="sxs-lookup"><span data-stu-id="5aea9-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="5aea9-108">開始之前，請先確定您已安裝下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="5aea9-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="5aea9-109">您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="5aea9-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="5aea9-110">或者，您可以使用下列連結個別安裝必要條件：</span><span class="sxs-lookup"><span data-stu-id="5aea9-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="5aea9-111">Visual Studio Web Developer Express SP1 必要條件</span><span class="sxs-lookup"><span data-stu-id="5aea9-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="5aea9-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="5aea9-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="5aea9-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）</span><span class="sxs-lookup"><span data-stu-id="5aea9-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="5aea9-114">如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="5aea9-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="5aea9-115">本主題提供具有C#原始程式碼的 Visual Web Developer 專案。</span><span class="sxs-lookup"><span data-stu-id="5aea9-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="5aea9-116">[下載C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="5aea9-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="5aea9-117">如果您偏好 Visual Basic，請切換到本教學課程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。</span><span class="sxs-lookup"><span data-stu-id="5aea9-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="5aea9-118">您要建置的內容</span><span class="sxs-lookup"><span data-stu-id="5aea9-118">What You'll Build</span></span>

<span data-ttu-id="5aea9-119">您將會執行簡單的電影清單應用程式，以支援從資料庫建立、編輯和列出電影。</span><span class="sxs-lookup"><span data-stu-id="5aea9-119">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="5aea9-120">以下是您將建立之應用程式的兩個螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="5aea9-120">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="5aea9-121">其中包含的頁面會顯示資料庫中的電影清單：</span><span class="sxs-lookup"><span data-stu-id="5aea9-121">It includes a page that displays a list of movies from a database:</span></span>

![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image1.png)

<span data-ttu-id="5aea9-123">應用程式也可讓您新增、編輯和刪除電影，以及查看個別資料的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5aea9-123">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="5aea9-124">所有的資料輸入案例都包含驗證，以確保資料庫中儲存的資料是正確的。</span><span class="sxs-lookup"><span data-stu-id="5aea9-124">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="5aea9-125">您要學習的技術</span><span class="sxs-lookup"><span data-stu-id="5aea9-125">Skills You'll Learn</span></span>

<span data-ttu-id="5aea9-126">以下是您要學習的內容：</span><span class="sxs-lookup"><span data-stu-id="5aea9-126">Here's what you'll learn:</span></span>

- <span data-ttu-id="5aea9-127">如何建立新的 ASP.NET MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="5aea9-127">How to create a new ASP.NET MVC project.</span></span>
- <span data-ttu-id="5aea9-128">如何建立 ASP.NET MVC 控制器和 views。</span><span class="sxs-lookup"><span data-stu-id="5aea9-128">How to create ASP.NET MVC controllers and views.</span></span>
- <span data-ttu-id="5aea9-129">如何使用 Entity Framework Code First 範例建立新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="5aea9-129">How to create a new database using the Entity Framework Code First paradigm.</span></span>
- <span data-ttu-id="5aea9-130">如何取出和顯示資料。</span><span class="sxs-lookup"><span data-stu-id="5aea9-130">How to retrieve and display data.</span></span>
- <span data-ttu-id="5aea9-131">如何編輯資料並啟用資料驗證。</span><span class="sxs-lookup"><span data-stu-id="5aea9-131">How to edit data and enable data validation.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5aea9-132">快速入門</span><span class="sxs-lookup"><span data-stu-id="5aea9-132">Getting Started</span></span>

<span data-ttu-id="5aea9-133">一開始先執行 Visual Web Developer 2010 Express （簡稱為「Visual Web Developer」），然後從 [**開始**] 頁面選取 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="5aea9-133">Start by running Visual Web Developer 2010 Express ("Visual Web Developer" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="5aea9-134">Visual Web Developer 是一個 IDE 或一個整合式開發環境。</span><span class="sxs-lookup"><span data-stu-id="5aea9-134">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="5aea9-135">就像您使用 Microsoft Word 來撰寫檔一樣，您將使用 IDE 來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="5aea9-135">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="5aea9-136">在 Visual Web Developer 中，有一個工具列沿著上方顯示各種可用的選項。</span><span class="sxs-lookup"><span data-stu-id="5aea9-136">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="5aea9-137">另外還有一個功能表，可提供另一種在 IDE 中執行工作的方式。</span><span class="sxs-lookup"><span data-stu-id="5aea9-137">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="5aea9-138">（例如，您可以使用功能表，然後選取 [檔案] &gt; [**新增專案**]，而不是從 [**開始**]**頁面選取 [** **新增專案**]。）</span><span class="sxs-lookup"><span data-stu-id="5aea9-138">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="5aea9-139">建立您的第一個應用程式</span><span class="sxs-lookup"><span data-stu-id="5aea9-139">Creating Your First Application</span></span>

<span data-ttu-id="5aea9-140">您可以使用 Visual Basic 或 Visual C#作為程式設計語言來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="5aea9-140">You can create applications using either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="5aea9-141">選取左側C#的 [視覺效果]，然後選取 [ **ASP.NET MVC 3 Web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="5aea9-141">Select Visual C# on the left and then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="5aea9-142">將專案命名為 "MvcMovie"，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="5aea9-142">Name your project "MvcMovie" and then click **OK**.</span></span> <span data-ttu-id="5aea9-143">（如果您偏好 Visual Basic，請切換至本教學課程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。）</span><span class="sxs-lookup"><span data-stu-id="5aea9-143">(If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.)</span></span>

![](intro-to-aspnet-mvc-3/_static/image5.png)

<span data-ttu-id="5aea9-144">在 [**新增 ASP.NET MVC 3 專案**] 對話方塊中，選取 [**網際網路應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="5aea9-144">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="5aea9-145">核取 [**使用 HTML5 標記**]，並保留**Razor**做為預設的 view engine。</span><span class="sxs-lookup"><span data-stu-id="5aea9-145">Check **Use HTML5 markup** and leave **Razor** as the default view engine.</span></span>

![](intro-to-aspnet-mvc-3/_static/image6.png)

<span data-ttu-id="5aea9-146">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5aea9-146">Click **OK**.</span></span> <span data-ttu-id="5aea9-147">Visual Web Developer 已針對您剛才建立的 ASP.NET MVC 專案使用預設範本，因此您現在有一個可運作的應用程式，而不需要執行任何動作！</span><span class="sxs-lookup"><span data-stu-id="5aea9-147">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="5aea9-148">這是簡單的「Hello World！」</span><span class="sxs-lookup"><span data-stu-id="5aea9-148">This is a simple "Hello World!"</span></span> <span data-ttu-id="5aea9-149">專案，這是啟動應用程式的好地方。</span><span class="sxs-lookup"><span data-stu-id="5aea9-149">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="5aea9-150">從 [偵錯] 功能表中，選取 [開始偵錯]。</span><span class="sxs-lookup"><span data-stu-id="5aea9-150">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="5aea9-151">請注意，啟動偵錯工具的鍵盤快速鍵是 F5。</span><span class="sxs-lookup"><span data-stu-id="5aea9-151">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="5aea9-152">F5 會使 Visual Web Developer 啟動開發 web 伺服器，並執行您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5aea9-152">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="5aea9-153">Visual Web Developer 接著會啟動瀏覽器，並開啟應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="5aea9-153">Visual Web Developer then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="5aea9-154">請注意，瀏覽器的網址列會顯示 `localhost`，而不是類似 `example.com`。</span><span class="sxs-lookup"><span data-stu-id="5aea9-154">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="5aea9-155">這是因為 `localhost` 一定會指向您自己的本機電腦，在此情況下，它會執行您剛建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5aea9-155">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="5aea9-156">當 Visual Web Developer 執行 Web 專案時，會針對網頁伺服器使用隨機埠。</span><span class="sxs-lookup"><span data-stu-id="5aea9-156">When Visual Web Developer runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="5aea9-157">在下圖中，隨機埠號碼為43246。</span><span class="sxs-lookup"><span data-stu-id="5aea9-157">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="5aea9-158">當您執行應用程式時，可能會看到不同的埠號碼。</span><span class="sxs-lookup"><span data-stu-id="5aea9-158">When you run the application, you'll probably see a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image10.png)

<span data-ttu-id="5aea9-159">現成的預設範本會提供您兩個要造訪的頁面和一個基本的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="5aea9-159">Right out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="5aea9-160">下一步是要變更此應用程式的運作方式，並稍微瞭解如何在進程中 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="5aea9-160">The next step is to change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="5aea9-161">關閉瀏覽器，讓我們變更一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="5aea9-161">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5aea9-162">下一個</span><span class="sxs-lookup"><span data-stu-id="5aea9-162">Next</span></span>](adding-a-controller.md)
