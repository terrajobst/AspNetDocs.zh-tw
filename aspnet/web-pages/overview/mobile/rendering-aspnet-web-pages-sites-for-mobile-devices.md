---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: 行動裝置的轉譯 ASP.NET Web Pages （Razor）網站 |Microsoft Docs
author: Rick-Anderson
description: 本文說明如何在 ASP.NET Web Pages （Razor）網站中建立會在行動裝置上適當呈現的頁面。 您將瞭解的內容：如何 。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: c012348d65e48a275cb0e4808fef2a7f31e5fb33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563564"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a><span data-ttu-id="e1047-104">行動裝置的轉譯 ASP.NET Web Pages （Razor）網站</span><span class="sxs-lookup"><span data-stu-id="e1047-104">Rendering ASP.NET Web Pages (Razor) Sites for Mobile Devices</span></span>

<span data-ttu-id="e1047-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="e1047-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="e1047-106">本文說明如何在 ASP.NET Web Pages （Razor）網站中建立會在行動裝置上適當呈現的頁面。</span><span class="sxs-lookup"><span data-stu-id="e1047-106">This article describes how to create pages in an ASP.NET Web Pages (Razor) site that will render appropriately on mobile devices.</span></span>
> 
> <span data-ttu-id="e1047-107">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="e1047-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="e1047-108">如何使用命名慣例來指定頁面專為行動裝置所設計。</span><span class="sxs-lookup"><span data-stu-id="e1047-108">How to use a naming convention to specify that a page is designed specifically for mobile devices.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e1047-109">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="e1047-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="e1047-110">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="e1047-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="e1047-111">本教學課程也適用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="e1047-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="e1047-112">ASP.NET Web Pages 可讓您建立自訂顯示，以在行動裝置或其他裝置上呈現內容。</span><span class="sxs-lookup"><span data-stu-id="e1047-112">ASP.NET Web Pages lets you create custom displays for rendering content on mobile or other devices.</span></span>

<span data-ttu-id="e1047-113">在 ASP.NET Web Pages 網站中建立裝置特定頁面的最簡單方式，就是使用檔案命名模式，如下所示： *FileName.* . #。</span><span class="sxs-lookup"><span data-stu-id="e1047-113">The simplest way to create device-specific page in an ASP.NET Web Pages site is by using a file-naming pattern like this: *FileName.Mobile.cshtml*.</span></span> <span data-ttu-id="e1047-114">您可以建立兩個版本的網頁（例如，一個名稱為*myfile.txt* ，另一個名為*myfile.txt*）。</span><span class="sxs-lookup"><span data-stu-id="e1047-114">You can create two versions of a page (for example, one named *MyFile.cshtml* and one named *MyFile.Mobile.cshtml*).</span></span> <span data-ttu-id="e1047-115">在執行時間，當行動裝置要求*myfile.txt*時，ASP.NET 會從*myfile.txt*呈現內容。</span><span class="sxs-lookup"><span data-stu-id="e1047-115">At run time, when a mobile device requests *MyFile.cshtml*, ASP.NET renders the content from *MyFile.Mobile.cshtml*.</span></span> <span data-ttu-id="e1047-116">否則，會呈現*myfile.txt* 。</span><span class="sxs-lookup"><span data-stu-id="e1047-116">Otherwise, *MyFile.cshtml* is rendered.</span></span>

<span data-ttu-id="e1047-117">下列範例顯示如何藉由新增行動裝置的內容頁面來啟用行動轉譯。</span><span class="sxs-lookup"><span data-stu-id="e1047-117">The following example shows how to enable mobile rendering by adding a content page for mobile devices.</span></span> <span data-ttu-id="e1047-118">*Page1. cshtml*包含內容以及導覽提要欄位。</span><span class="sxs-lookup"><span data-stu-id="e1047-118">*Page1.cshtml* contains content plus a navigation sidebar.</span></span> <span data-ttu-id="e1047-119">*Page1*包含相同的內容，但省略提要欄位。</span><span class="sxs-lookup"><span data-stu-id="e1047-119">*Page1.Mobile.cshtml* contains the same content, but omits the sidebar.</span></span>

1. <span data-ttu-id="e1047-120">在 ASP.NET Web Pages 網站中，建立名為*Page1. cshtml*的檔案，並以下列標記取代目前的內容。</span><span class="sxs-lookup"><span data-stu-id="e1047-120">In an ASP.NET Web Pages site, create a file named *Page1.cshtml* and replace the current content with following markup.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. <span data-ttu-id="e1047-121">建立名為*Page1*的檔案，並以下列標記取代現有的內容。</span><span class="sxs-lookup"><span data-stu-id="e1047-121">Create a file named *Page1.Mobile.cshtml* and replace the existing content with the following markup.</span></span> <span data-ttu-id="e1047-122">請注意，行動版的頁面會省略流覽區段，以便在較小的螢幕上進行更佳的轉譯。</span><span class="sxs-lookup"><span data-stu-id="e1047-122">Notice that the mobile version of the page omits the navigation section for better rendering on a smaller screen.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. <span data-ttu-id="e1047-123">執行桌面瀏覽器並流覽至*Page1. cshtml*。</span><span class="sxs-lookup"><span data-stu-id="e1047-123">Run a desktop browser and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="e1047-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e1047-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span></span>
4. <span data-ttu-id="e1047-125">執行行動瀏覽器（或行動裝置模擬器）並流覽至*Page1. cshtml*。</span><span class="sxs-lookup"><span data-stu-id="e1047-125">Run a mobile browser (or a mobile device emulator) and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="e1047-126">（請注意，您不會包含*mobile* 。</span><span class="sxs-lookup"><span data-stu-id="e1047-126">(Notice that you do not include *.mobile.*</span></span> <span data-ttu-id="e1047-127">作為 URL 的一部分）。即使要求是*page1. cshtml*，ASP.NET 還是會呈現*page1*。</span><span class="sxs-lookup"><span data-stu-id="e1047-127">as part of the URL.) Even though the request is to *Page1.cshtml*, ASP.NET renders *Page1.Mobile.cshtml*.</span></span>

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="e1047-129">若要測試行動頁面，您可以使用在桌上型電腦上執行的行動裝置模擬器。</span><span class="sxs-lookup"><span data-stu-id="e1047-129">To test mobile pages, you can use a mobile device simulator that runs on a desktop computer.</span></span> <span data-ttu-id="e1047-130">這項工具可讓您測試網頁在行動裝置上的外觀（也就是，通常會有更小的顯示區域）。</span><span class="sxs-lookup"><span data-stu-id="e1047-130">This tool lets you test web pages as they would look on mobile devices (that is, typically with a much smaller display area).</span></span> <span data-ttu-id="e1047-131">其中一個模擬器範例是 Mozilla Firefox 的[使用者代理程式切換器附加](http://addons.mozilla.org/firefox/addon/user-agent-switcher/)元件，可讓您從桌上出版本的 firefox 模擬各種行動瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="e1047-131">One example of a simulator is the [User Agent Switcher add-on](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) for Mozilla Firefox, which lets you emulate various mobile browsers from a desktop version of Firefox.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="e1047-132">其他資源</span><span class="sxs-lookup"><span data-stu-id="e1047-132">Additional Resources</span></span>

<span data-ttu-id="e1047-133">[Windows Phone 模擬器](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span><span class="sxs-lookup"><span data-stu-id="e1047-133">[Windows Phone Emulator](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span></span>
