---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
title: ASP.NET MVC 4 簡介 |Microsoft Docs
author: Rick-Anderson
description: 如果本教學課程可在此使用 Visual Studio 2013，則為更新版本。 新的教學課程使用 ASP.NET MVC 5，它提供了許多透過 t 的改良功能 。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: ed66530a-04d5-49eb-b76a-85be1f57c437
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 51709a9c6ddb39b8fcd1cd94cd08d530a595825a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599642"
---
# <a name="intro-to-aspnet-mvc-4"></a><span data-ttu-id="ed4ba-104">ASP.NET MVC 4 簡介</span><span class="sxs-lookup"><span data-stu-id="ed4ba-104">Intro to ASP.NET MVC 4</span></span>

<span data-ttu-id="ed4ba-105">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ed4ba-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="ed4ba-106">如果本教學[課程](../../getting-started/introduction/getting-started.md)可在此使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，則為更新版本。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="ed4ba-107">新的教學課程會使用 ASP.NET MVC 5，這在此教學課程中提供了許多改進功能。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
> <span data-ttu-id="ed4ba-108">本教學課程將告訴您使用 Microsoft [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)或 Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC 4 Web 應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-108">This tutorial will teach you the basics of building an ASP.NET MVC 4 Web application using Microsoft [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) or Visual Web Developer 2010 Express Service Pack 1.</span></span> <span data-ttu-id="ed4ba-109">建議使用 Visual Studio 2012，您不需要安裝任何專案，即可完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-109">Visual Studio 2012 is recommended, you won't need to install anything to complete the tutorial.</span></span> <span data-ttu-id="ed4ba-110">如果您使用 Visual Studio 2010，您必須安裝下列元件。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-110">If you are using Visual Studio 2010 you must install the components below.</span></span> <span data-ttu-id="ed4ba-111">您可以按一下下列連結來安裝所有這些專案：</span><span class="sxs-lookup"><span data-stu-id="ed4ba-111">You can install all of them by clicking the following links:</span></span>
>
> - [<span data-ttu-id="ed4ba-112">Visual Studio Web Developer Express SP1 必要條件</span><span class="sxs-lookup"><span data-stu-id="ed4ba-112">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="ed4ba-113">適用于 ASP.NET MVC 4 的 DOWNLOAD-WPI 安裝程式</span><span class="sxs-lookup"><span data-stu-id="ed4ba-113">WPI installer for ASP.NET MVC 4</span></span>](https://go.microsoft.com/fwlink/?LinkId=243392)
> - [<span data-ttu-id="ed4ba-114">LocalDB</span><span class="sxs-lookup"><span data-stu-id="ed4ba-114">LocalDB</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)
> - [<span data-ttu-id="ed4ba-115">SSDT</span><span class="sxs-lookup"><span data-stu-id="ed4ba-115">SSDT</span></span>](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)
>
> <span data-ttu-id="ed4ba-116">如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請安裝[適用于 ASP.NET MVC 4 的 download-wpi 安裝程式](https://go.microsoft.com/fwlink/?LinkId=243392)和： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)</span><span class="sxs-lookup"><span data-stu-id="ed4ba-116">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the [WPI installer for ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392) and the: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)</span></span>
>
> <span data-ttu-id="ed4ba-117">本主題提供具有C#原始程式碼的 Visual Web Developer 專案。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-117">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="ed4ba-118">[下載C#版本](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip)。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-118">[Download the C# version](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip).</span></span>
>
> <span data-ttu-id="ed4ba-119">在教學課程中，您會在 Visual Studio 中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-119">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="ed4ba-120">您也可以將應用程式部署至主機服務提供者，使其可透過網際網路使用。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-120">You can also make the application available over the Internet by deploying it to a hosting provider.</span></span> <span data-ttu-id="ed4ba-121">Microsoft 在[免費的 Windows Azure 試用帳戶](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)中，最多可為10個網站提供免費的 web 主機。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-121">Microsoft offers free web hosting for up to 10 web sites in a [free Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="ed4ba-122">如需如何將 Visual Studio Web 專案部署至 Windows Azure 網站的詳細資訊，請參閱[建立及部署 ASP.NET 網站，並使用 Visual Studio SQL Database](https://docs.microsoft.com/dotnet/azure/)。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-122">For information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create and deploy an ASP.NET web site and SQL Database with Visual Studio](https://docs.microsoft.com/dotnet/azure/).</span></span> <span data-ttu-id="ed4ba-123">該教學課程也會示範如何使用 Entity Framework Code First 移轉將您的 SQL Server 資料庫部署至 Windows Azure SQL Database （先前稱為 SQL Azure）。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-123">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Windows Azure SQL Database (formerly SQL Azure).</span></span>
>
> <span data-ttu-id="ed4ba-124">本教學課程是由 Rick Anderson （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）撰寫。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-124">This tutorial was written by Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ).</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="ed4ba-125">您要建置的內容</span><span class="sxs-lookup"><span data-stu-id="ed4ba-125">What You'll Build</span></span>

> [!NOTE]
> <span data-ttu-id="ed4ba-126">如果本教學[課程](../../getting-started/introduction/getting-started.md)可在此使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，則為更新版本。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-126">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="ed4ba-127">新的教學課程會使用 ASP.NET MVC 5，這在此教學課程中提供了許多改進功能。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-127">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>

<span data-ttu-id="ed4ba-128">您將會執行簡單的電影清單應用程式，以支援從資料庫建立、編輯、搜尋和列出電影。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-128">You'll implement a simple movie-listing application that supports creating, editing, searching and listing movies from a database.</span></span> <span data-ttu-id="ed4ba-129">以下是您將建立之應用程式的兩個螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-129">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="ed4ba-130">其中包含的頁面會顯示資料庫中的電影清單：</span><span class="sxs-lookup"><span data-stu-id="ed4ba-130">It includes a page that displays a list of movies from a database:</span></span>

![](intro-to-aspnet-mvc-4/_static/image1.png)

<span data-ttu-id="ed4ba-131">應用程式也可讓您新增、編輯和刪除電影，以及查看個別資料的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-131">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="ed4ba-132">所有的資料輸入案例都包含驗證，以確保資料庫中儲存的資料是正確的。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-132">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

![](intro-to-aspnet-mvc-4/_static/image2.png)

## <a name="getting-started"></a><span data-ttu-id="ed4ba-133">快速入門</span><span class="sxs-lookup"><span data-stu-id="ed4ba-133">Getting Started</span></span>

<span data-ttu-id="ed4ba-134">從執行 Visual Studio Express 2012 或 Visual Web Developer 2010 Express 開始。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-134">Start by running Visual Studio Express 2012 or Visual Web Developer 2010 Express.</span></span> <span data-ttu-id="ed4ba-135">此系列中的大部分螢幕擷取畫面都會使用 Visual Studio Express 2012，但您可以使用 Visual Studio 2010/SP1、Visual Studio 2012、Visual Studio Express 2012 或 Visual Web Developer 2010 Express 來完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-135">Most of the screen shots in this series use Visual Studio Express 2012, but you can complete this tutorial with Visual Studio 2010/SP1, Visual Studio 2012, Visual Studio Express 2012 or Visual Web Developer 2010 Express.</span></span> <span data-ttu-id="ed4ba-136">從 [**開始**] 頁面選取 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-136">Select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="ed4ba-137">Visual Studio 是 IDE 或整合式開發環境。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-137">Visual Studio is an IDE, or integrated development environment.</span></span> <span data-ttu-id="ed4ba-138">就像您使用 Microsoft Word 來撰寫檔一樣，您將使用 IDE 來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-138">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="ed4ba-139">在 Visual Studio 上方會有一個工具列，其中顯示您可以使用的各種選項。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-139">In Visual Studio there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="ed4ba-140">另外還有一個功能表，可提供另一種在 IDE 中執行工作的方式。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-140">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="ed4ba-141">（例如，您可以使用功能表，然後選取 [檔案] &gt; [**新增專案**]，而不是從 [**開始**]**頁面選取 [** **新增專案**]。）</span><span class="sxs-lookup"><span data-stu-id="ed4ba-141">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

![](intro-to-aspnet-mvc-4/_static/image3.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="ed4ba-142">建立您的第一個應用程式</span><span class="sxs-lookup"><span data-stu-id="ed4ba-142">Creating Your First Application</span></span>

<span data-ttu-id="ed4ba-143">您可以使用 Visual Basic 或 Visual C#作為程式設計語言來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-143">You can create applications using either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="ed4ba-144">選取左側C#的 [視覺效果]，然後選取 [ **ASP.NET MVC 4 Web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-144">Select Visual C# on the left and then select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="ed4ba-145">將專案命名為 &quot;MvcMovie&quot; 然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-145">Name your project &quot;MvcMovie&quot; and then click **OK**.</span></span>

![](intro-to-aspnet-mvc-4/_static/image4.png)

<span data-ttu-id="ed4ba-146">在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-146">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="ed4ba-147">保留**Razor**做為預設的 view engine。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-147">Leave **Razor** as the default view engine.</span></span>

![](intro-to-aspnet-mvc-4/_static/image5.png)

<span data-ttu-id="ed4ba-148">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-148">Click **OK**.</span></span> <span data-ttu-id="ed4ba-149">Visual Studio 使用您剛建立的 ASP.NET MVC 專案的預設範本，所以您現在有一個可運作的應用程式，而不需要執行任何動作！</span><span class="sxs-lookup"><span data-stu-id="ed4ba-149">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="ed4ba-150">這是簡單的 &quot;Hello World！&quot; 專案，這是啟動應用程式的好地方。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-150">This is a simple &quot;Hello World!&quot; project, and it's a good place to start your application.</span></span>

![](intro-to-aspnet-mvc-4/_static/image6.png)

<span data-ttu-id="ed4ba-151">從 [偵錯] 功能表中，選取 [開始偵錯]。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-151">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-4/_static/image7.png)

<span data-ttu-id="ed4ba-152">請注意，啟動偵錯工具的鍵盤快速鍵是 F5。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-152">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="ed4ba-153">F5 會使 Visual Studio 開始 IIS Express 並執行您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-153">F5 causes Visual Studio to start IIS Express and run your web application.</span></span> <span data-ttu-id="ed4ba-154">Visual Studio 接著會啟動瀏覽器，並開啟應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-154">Visual Studio then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="ed4ba-155">請注意，瀏覽器的網址列會顯示 `localhost`，而不是類似 `example.com`。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-155">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="ed4ba-156">這是因為 `localhost` 一定會指向您自己的本機電腦，在此情況下，它會執行您剛建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-156">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="ed4ba-157">當 Visual Studio 執行 Web 專案時，會針對網頁伺服器使用隨機埠。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-157">When Visual Studio runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="ed4ba-158">在下圖中，埠號碼為41788。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-158">In the image below, the port number is 41788.</span></span> <span data-ttu-id="ed4ba-159">當您執行應用程式時，可能會看到不同的埠號碼。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-159">When you run the application, you'll probably see a different port number.</span></span>

![](intro-to-aspnet-mvc-4/_static/image8.png)

<span data-ttu-id="ed4ba-160">現成的預設範本會提供您首頁、連絡人和頁面。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-160">Right out of the box this default template gives you Home, Contact and About pages.</span></span> <span data-ttu-id="ed4ba-161">它也提供註冊和登入的支援，以及 Facebook 和 Twitter 的連結。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-161">It also provides support to register and log in, and links to Facebook and Twitter.</span></span> <span data-ttu-id="ed4ba-162">下一步是變更此應用程式的運作方式，並稍微瞭解 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-162">The next step is to change how this application works and learn a little bit about ASP.NET MVC.</span></span> <span data-ttu-id="ed4ba-163">關閉瀏覽器，讓我們變更一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="ed4ba-163">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ed4ba-164">下一個</span><span class="sxs-lookup"><span data-stu-id="ed4ba-164">Next</span></span>](adding-a-controller.md)
