---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: 在 ASP.NET Web Pages （Razor）網站中安裝 Helper |Microsoft Docs
author: Rick-Anderson
description: 本文說明如何在 ASP.NET Web Pages （Razor）網站中安裝協助程式。 協助程式是可重複使用的元件，其中包含程式碼和標記為每個 。
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 41e33c04a53a6ad257c3937cdadcec767e9217c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638583"
---
# <a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="c9462-104">在 ASP.NET Web Pages （Razor）網站中安裝 Helper</span><span class="sxs-lookup"><span data-stu-id="c9462-104">Installing a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="c9462-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c9462-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c9462-106">本文說明如何在 ASP.NET Web Pages （Razor）網站中安裝協助程式。</span><span class="sxs-lookup"><span data-stu-id="c9462-106">This article describes how to install a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="c9462-107">*Helper*是可重複使用的元件，其中包含程式碼和標記來執行可能單調乏味或複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="c9462-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="c9462-108">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="c9462-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="c9462-109">如何在使用 WebMatrix 3 建立的網站中安裝 helper。</span><span class="sxs-lookup"><span data-stu-id="c9462-109">How to install a helper in a website created using WebMatrix 3.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c9462-110">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="c9462-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c9462-111">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="c9462-111">WebMatrix 3</span></span>

## <a name="overview-of-helpers"></a><span data-ttu-id="c9462-112">協助程式總覽</span><span class="sxs-lookup"><span data-stu-id="c9462-112">Overview of Helpers</span></span>

<span data-ttu-id="c9462-113">人們通常會想要在網頁上執行的某些工作需要大量的程式碼，或需要額外的知識。</span><span class="sxs-lookup"><span data-stu-id="c9462-113">Some tasks that people often want to do on web pages require a lot of code or require extra knowledge.</span></span> <span data-ttu-id="c9462-114">範例包括顯示資料的圖表;在頁面上放置 Twitter 的 [跟隨] 按鈕;正在從您的網站傳送電子郵件;裁剪或調整影像大小;針對您的網站使用 PayPal。</span><span class="sxs-lookup"><span data-stu-id="c9462-114">Examples include displaying a chart for data; putting a Twitter "Follow" button on a page; sending email from your website; cropping or resizing images; using PayPal for your site.</span></span> <span data-ttu-id="c9462-115">為了讓您輕鬆執行這類工作，ASP.NET Web Pages 可讓*您使用協助*程式。</span><span class="sxs-lookup"><span data-stu-id="c9462-115">To make it easy to do these kinds of things, ASP.NET Web Pages lets you use *helpers*.</span></span> <span data-ttu-id="c9462-116">協助程式是您為網站安裝的元件，可讓您只使用一行或兩個 Razor 程式碼來執行一般工作。</span><span class="sxs-lookup"><span data-stu-id="c9462-116">Helpers are components that you install for a site and that let you perform typical tasks by using just a line or two of Razor code.</span></span>

<span data-ttu-id="c9462-117">ASP.NET Web Pages 內建了一些協助程式。</span><span class="sxs-lookup"><span data-stu-id="c9462-117">ASP.NET Web Pages has a few helpers built in.</span></span> <span data-ttu-id="c9462-118">不過，許多協助程式都可以在使用 NuGet 套件管理員所提供的封裝（增益集）中取得。</span><span class="sxs-lookup"><span data-stu-id="c9462-118">However, many helpers are available in packages (add-ins) that are provided using the NuGet package manager.</span></span> <span data-ttu-id="c9462-119">NuGet 可讓您選取要安裝的套件，然後負責安裝的所有詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c9462-119">NuGet lets you select a package to install and then it takes care of all the details of the installation.</span></span>

## <a name="installing-a-helper-in-webmatrix-3"></a><span data-ttu-id="c9462-120">在 WebMatrix 中安裝 Helper 3</span><span class="sxs-lookup"><span data-stu-id="c9462-120">Installing a Helper in WebMatrix 3</span></span>

1. <span data-ttu-id="c9462-121">在 WebMatrix 3 中，按一下 [ **NuGet** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c9462-121">In WebMatrix 3, click the **NuGet** button.</span></span>

    ![WebMatrix 中的 [NuGet 資源庫] 對話方塊](installing-helpers/_static/image1.png)
2. <span data-ttu-id="c9462-123">這會啟動 NuGet 套件管理員，並顯示可用的套件。</span><span class="sxs-lookup"><span data-stu-id="c9462-123">This launches the NuGet package manager and displays available packages.</span></span> <span data-ttu-id="c9462-124">在 [搜尋] 方塊中，為您要安裝的 helper 輸入關鍵字。</span><span class="sxs-lookup"><span data-stu-id="c9462-124">In the search box, enter a keyword for the helper you want to install.</span></span>

    ![WebMatrix 中的 [NuGet 資源庫] 對話方塊](installing-helpers/_static/image2.png)
3. <span data-ttu-id="c9462-126">選取套件，然後按一下 [**安裝**]。</span><span class="sxs-lookup"><span data-stu-id="c9462-126">Select the package and then click **Install**.</span></span> <span data-ttu-id="c9462-127">當系統詢問您是否要安裝套件，並指出您接受條款時，請按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="c9462-127">Click **Yes** when asked if you want to install the package and indicate that you accept the terms.</span></span>

     <span data-ttu-id="c9462-128">如果這是您第一次安裝 helper，NuGet 會針對組成協助程式的程式碼，在您的網站中建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="c9462-128">If this is the first time you've installed a helper, NuGet creates folders in your website for the code that makes up the helper.</span></span>
4. <span data-ttu-id="c9462-129">若要卸載協助程式，請按一下 [資源**庫**] 按鈕，按一下 [**已安裝**] 索引標籤，然後挑選您要卸載的套件。</span><span class="sxs-lookup"><span data-stu-id="c9462-129">To uninstall a helper, click the **Gallery** button, click the **Installed** tab, and pick the package you want to uninstall.</span></span>

## <a name="installing-the-twitter-helper"></a><span data-ttu-id="c9462-130">安裝 Twitter helper</span><span class="sxs-lookup"><span data-stu-id="c9462-130">Installing the Twitter helper</span></span>

<span data-ttu-id="c9462-131">Twitter API 的最新版本與您透過 NuGet 安裝的 Twitter helper 不相容。</span><span class="sxs-lookup"><span data-stu-id="c9462-131">The latest version of the Twitter API is not compatible with the Twitter helper you install through NuGet.</span></span> <span data-ttu-id="c9462-132">相反地，請參閱[Twitter helper With WebMatrix](twitter-helper.md)主題，以取得如何在專案中設定 Twitter 協助程式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c9462-132">Instead, see the [Twitter Helper with WebMatrix](twitter-helper.md) topic for information about how to set up the Twitter helper in your project.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="c9462-133">其他資源</span><span class="sxs-lookup"><span data-stu-id="c9462-133">Additional Resources</span></span>

[<span data-ttu-id="c9462-134">簡介 ASP.NET Web Pages 2-程式設計基本概念</span><span class="sxs-lookup"><span data-stu-id="c9462-134">Introducing ASP.NET Web Pages 2 - Programming Basics</span></span>](../getting-started/introducing-razor-syntax-c.md)

[<span data-ttu-id="c9462-135">Twitter Helper 與 WebMatrix</span><span class="sxs-lookup"><span data-stu-id="c9462-135">Twitter Helper with WebMatrix</span></span>](twitter-helper.md)
