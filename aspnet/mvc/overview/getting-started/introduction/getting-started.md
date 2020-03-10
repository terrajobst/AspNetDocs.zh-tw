---
uid: mvc/overview/getting-started/introduction/getting-started
title: ASP.NET MVC 5 的消費者入門 |Microsoft Docs
author: Rick-Anderson
ms.author: riande
ms.date: 10/04/2018
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ca39bc37c757c0452cf56624c8e37c04df4b41f2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78602764"
---
# <a name="getting-started-with-aspnet-mvc-5"></a><span data-ttu-id="e4447-102">開始使用 ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="e4447-102">Getting started with ASP.NET MVC 5</span></span>

<span data-ttu-id="e4447-103">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="e4447-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](../../../../includes/razor.md)]

<span data-ttu-id="e4447-104">本教學課程會教您使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)建立 ASP.NET MVC 5 web 應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="e4447-104">This tutorial teaches you the basics of building an ASP.NET MVC 5 web app using [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span> <span data-ttu-id="e4447-105">本教學課程的最終原始程式碼位於[GitHub](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)。</span><span class="sxs-lookup"><span data-stu-id="e4447-105">The final source code for the tutorial is located on [GitHub](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie).</span></span>

<span data-ttu-id="e4447-106">本教學課程是由[Scott Guthrie](https://weblogs.asp.net/scottgu/) （twitter[@scottgu](https://twitter.com/scottgu) ）、 [scott Hanselman](http://www.hanselman.com/blog/) （Twitter： [@shanselman](https://twitter.com/shanselman) ）和[Rick Anderson](https://twitter.com/RickAndMSFT) （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）所撰寫</span><span class="sxs-lookup"><span data-stu-id="e4447-106">This tutorial was written by [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[@scottgu](https://twitter.com/scottgu) ), [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](https://twitter.com/shanselman) ), and [Rick Anderson](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )</span></span>

<span data-ttu-id="e4447-107">您需要 Azure 帳戶，才能將此應用程式部署至 Azure：</span><span class="sxs-lookup"><span data-stu-id="e4447-107">You need an Azure account to deploy this app to Azure:</span></span>

- <span data-ttu-id="e4447-108">您可以[免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-您將取得可試用付費 azure 服務的額度，且即使在用完後，您仍可保留帳戶，並使用免費的 azure 服務。</span><span class="sxs-lookup"><span data-stu-id="e4447-108">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="e4447-109">您可以 [啟用 MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - 您的 MSDN 訂閱每月會提供您額度，您可以用在 Azure 付費服務。</span><span class="sxs-lookup"><span data-stu-id="e4447-109">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="get-started"></a><span data-ttu-id="e4447-110">開始使用</span><span class="sxs-lookup"><span data-stu-id="e4447-110">Get started</span></span>

<span data-ttu-id="e4447-111">一開始請先[安裝 Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="e4447-111">Start by [installing Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span> <span data-ttu-id="e4447-112">然後，開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e4447-112">Then, open Visual Studio.</span></span>

<span data-ttu-id="e4447-113">Visual Studio 是 IDE 或整合式開發環境。</span><span class="sxs-lookup"><span data-stu-id="e4447-113">Visual Studio is an IDE, or integrated development environment.</span></span> <span data-ttu-id="e4447-114">就像您使用 Microsoft Word 來撰寫檔一樣，您將使用 IDE 來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4447-114">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="e4447-115">在 Visual Studio 中，底部會有一個清單，顯示您可以使用的各種選項。</span><span class="sxs-lookup"><span data-stu-id="e4447-115">In Visual Studio, there's a list along the bottom showing various options available to you.</span></span> <span data-ttu-id="e4447-116">另外還有一個功能表，可提供另一種在 IDE 中執行工作的方式。</span><span class="sxs-lookup"><span data-stu-id="e4447-116">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="e4447-117">例如，您可以使用功能表列，然後選取 [檔案] > [**新增專案**]，而不**是選取 [** **開始] 頁面**上的 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="e4447-117">For example, instead of selecting **New Project** on the **Start page**, you can use the menu bar and select **File** > **New Project**.</span></span>

![](getting-started/_static/image1.png)

## <a name="create-your-first-app"></a><span data-ttu-id="e4447-118">建立您的第一個應用程式</span><span class="sxs-lookup"><span data-stu-id="e4447-118">Create your first app</span></span>

<span data-ttu-id="e4447-119">在 [**開始] 頁面**上，選取 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="e4447-119">On the **Start page**, select **New Project**.</span></span> <span data-ttu-id="e4447-120">在 [**新增專案**] 對話方塊中，依序選取左側的 [**視覺效果C#**  ] 類別目錄和 [ **web**]，然後選取 [ **ASP.NET Web 應用程式（.NET Framework）** ] 專案範本。</span><span class="sxs-lookup"><span data-stu-id="e4447-120">In the **New project** dialog box, select the **Visual C#** category on the left, then **Web**, and then select the **ASP.NET Web Application (.NET Framework)** project template.</span></span> <span data-ttu-id="e4447-121">將專案命名為 "MvcMovie"，然後選擇 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="e4447-121">Name your project "MvcMovie" and then choose **OK**.</span></span>

![](getting-started/_static/image2.png)

<span data-ttu-id="e4447-122">在 [**新增 ASP.NET Web 應用程式**] 對話方塊中，選擇 [ **MVC** ]，然後選擇 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="e4447-122">In the **New ASP.NET Web Application** dialog, choose **MVC** and then choose **OK**.</span></span>

![](getting-started/_static/image3.png)

<span data-ttu-id="e4447-123">Visual Studio 使用您剛建立的 ASP.NET MVC 專案的預設範本，所以您現在有一個可運作的應用程式，而不需要執行任何動作！</span><span class="sxs-lookup"><span data-stu-id="e4447-123">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="e4447-124">這是簡單的「Hello World！」</span><span class="sxs-lookup"><span data-stu-id="e4447-124">This is a simple "Hello World!"</span></span> <span data-ttu-id="e4447-125">專案，這是啟動應用程式的好地方。</span><span class="sxs-lookup"><span data-stu-id="e4447-125">project, and it's a good place to start your application.</span></span>

![](getting-started/_static/image4.png)

<span data-ttu-id="e4447-126">按 **F5** 開始偵錯作業。</span><span class="sxs-lookup"><span data-stu-id="e4447-126">Press **F5** to start debugging.</span></span> <span data-ttu-id="e4447-127">當您按下**F5**時，Visual Studio 會開始[IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)並執行您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4447-127">When you press **F5**, Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your web app.</span></span> <span data-ttu-id="e4447-128">Visual Studio 接著會啟動瀏覽器，並開啟應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="e4447-128">Visual Studio then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="e4447-129">請注意，瀏覽器的網址列會顯示 `localhost:port#`，而不是類似 `example.com`。</span><span class="sxs-lookup"><span data-stu-id="e4447-129">Notice that the address bar of the browser says `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="e4447-130">這是因為 `localhost` 一定會指向您自己的本機電腦，在此情況下，它會執行您剛建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4447-130">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="e4447-131">當 Visual Studio 執行 Web 專案時，會針對網頁伺服器使用隨機埠。</span><span class="sxs-lookup"><span data-stu-id="e4447-131">When Visual Studio runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="e4447-132">在下圖中，埠號碼為1234。</span><span class="sxs-lookup"><span data-stu-id="e4447-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="e4447-133">當您執行應用程式時，您會看到不同的埠號碼。</span><span class="sxs-lookup"><span data-stu-id="e4447-133">When you run the application, you'll see a different port number.</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="e4447-134">現成的預設範本會提供您 `Home`、`Contact`和 `About` 頁面的許可權。</span><span class="sxs-lookup"><span data-stu-id="e4447-134">Right out of the box this default template gives you `Home`, `Contact`, and `About` pages.</span></span> <span data-ttu-id="e4447-135">下圖不會顯示 [**首頁**]、[**關於**] 和 [**連絡人**] 連結。</span><span class="sxs-lookup"><span data-stu-id="e4447-135">The image below doesn't show the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="e4447-136">視瀏覽器視窗的大小而定，您可能需要按一下流覽圖示才能看到這些連結。</span><span class="sxs-lookup"><span data-stu-id="e4447-136">Depending on the size of your browser window, you might need to click the navigation icon to see these links.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="e4447-137">應用程式也會提供註冊和登入的支援。</span><span class="sxs-lookup"><span data-stu-id="e4447-137">The application also provides support to register and log in.</span></span> <span data-ttu-id="e4447-138">下一步是變更此應用程式的運作方式，並稍微瞭解 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="e4447-138">The next step is to change how this application works and learn a little bit about ASP.NET MVC.</span></span> <span data-ttu-id="e4447-139">關閉 ASP.NET MVC 應用程式，讓我們變更一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="e4447-139">Close the ASP.NET MVC application and let's change some code.</span></span>

<span data-ttu-id="e4447-140">如需目前教學課程的清單，請參閱[MVC 建議的文章](../mvc-learning-sequence.md)。</span><span class="sxs-lookup"><span data-stu-id="e4447-140">For a list of current tutorials, see [MVC recommended articles](../mvc-learning-sequence.md).</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="e4447-141">請參閱此應用程式在 Azure 上執行</span><span class="sxs-lookup"><span data-stu-id="e4447-141">See this app running on Azure</span></span>

<span data-ttu-id="e4447-142">您是否想要查看已完成的網站以即時 web 應用程式的形式執行？</span><span class="sxs-lookup"><span data-stu-id="e4447-142">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="e4447-143">只要按一下下列按鈕，您就可以將應用程式的完整版本部署至您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4447-143">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

<span data-ttu-id="e4447-144">您需要 Azure 帳戶，才能將此解決方案部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="e4447-144">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="e4447-145">如果您還沒有帳戶，請使用下列其中一個選項建立一個：</span><span class="sxs-lookup"><span data-stu-id="e4447-145">If you don't already have an account, use one of the following options to create one:</span></span>

- <span data-ttu-id="e4447-146">[免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-您將取得可試用付費 azure 服務的額度，且即使在用完後，您仍可保留帳戶，並使用免費的 azure 服務。</span><span class="sxs-lookup"><span data-stu-id="e4447-146">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="e4447-147">[啟用 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers)-您的 Visual Studio 訂用帳戶每月會提供您額度，供您用於付費 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="e4447-147">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e4447-148">下一個</span><span class="sxs-lookup"><span data-stu-id="e4447-148">Next</span></span>](adding-a-controller.md)
