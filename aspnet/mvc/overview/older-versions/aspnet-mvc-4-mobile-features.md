---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: ASP.NET MVC 4 行動功能 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程現在有一個 MVC 5 版本，其中包含在 Azure 網站上部署 ASP.NET MVC 5 行動 Web 應用程式中的程式碼範例。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: 9716def069ca9f7115af32e16381f41bd4d13342
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579986"
---
# <a name="aspnet-mvc-4-mobile-features"></a><span data-ttu-id="41c82-103">ASP.NET MVC 4 Mobile 功能</span><span class="sxs-lookup"><span data-stu-id="41c82-103">ASP.NET MVC 4 Mobile Features</span></span>

<span data-ttu-id="41c82-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="41c82-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="41c82-105">本教學課程現在有一個 MVC 5 版本，其中包含在[Azure 網站上部署 ASP.NET MVC 5 行動 Web 應用程式中](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="41c82-105">There is now an MVC 5 version of this tutorial with code samples at [Deploy an ASP.NET MVC 5 Mobile Web Application on Azure Web Sites](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/).</span></span>

<span data-ttu-id="41c82-106">本教學課程將告訴您如何在 ASP.NET MVC 4 Web 應用程式中使用行動功能的基本概念。</span><span class="sxs-lookup"><span data-stu-id="41c82-106">This tutorial will teach you the basics of how to work with mobile features in an ASP.NET MVC 4 Web application.</span></span> <span data-ttu-id="41c82-107">在本教學課程中，您可以使用[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)或 Visual web Developer 2010 Express Service Pack 1 （&quot;Visual web DEVELOPER 或 VWD&quot;）。</span><span class="sxs-lookup"><span data-stu-id="41c82-107">For this tutorial, you can use [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) or Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer or VWD&quot;).</span></span> <span data-ttu-id="41c82-108">如果您已經有，可以使用 professional 版本的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="41c82-108">You can use the professional version of Visual Studio if you already have that.</span></span>

<span data-ttu-id="41c82-109">開始之前，請先確定您已安裝下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="41c82-109">Before you start, make sure you've installed the prerequisites listed below.</span></span>

- <span data-ttu-id="41c82-110">[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) （建議）或 Visual Studio Web DEVELOPER Express SP1。</span><span class="sxs-lookup"><span data-stu-id="41c82-110">[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (recommended) or Visual Studio Web Developer Express SP1.</span></span> <span data-ttu-id="41c82-111">Visual Studio 2012 包含 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="41c82-111">Visual Studio 2012 contains ASP.NET MVC 4.</span></span> <span data-ttu-id="41c82-112">如果您使用的是 Visual Web Developer 2010，就必須安裝[ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)。</span><span class="sxs-lookup"><span data-stu-id="41c82-112">If you are using Visual Web Developer 2010, you must install [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392).</span></span>

<span data-ttu-id="41c82-113">您還需要一個行動瀏覽器模擬器。</span><span class="sxs-lookup"><span data-stu-id="41c82-113">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="41c82-114">下列任一項目都可使用：</span><span class="sxs-lookup"><span data-stu-id="41c82-114">Any of the following will work:</span></span>

- <span data-ttu-id="41c82-115">[Windows 7 Phone 模擬器](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)。</span><span class="sxs-lookup"><span data-stu-id="41c82-115">[Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span></span> <span data-ttu-id="41c82-116">（這是在本教學課程中大部分螢幕擷取畫面中使用的模擬器）。</span><span class="sxs-lookup"><span data-stu-id="41c82-116">(This is the emulator that's used in most of the screen shots in this tutorial.)</span></span>
- <span data-ttu-id="41c82-117">變更使用者代理程式字串以模擬 iPhone。</span><span class="sxs-lookup"><span data-stu-id="41c82-117">Change the user agent string to emulate an iPhone.</span></span> <span data-ttu-id="41c82-118">請參閱[此](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)blog 專案。</span><span class="sxs-lookup"><span data-stu-id="41c82-118">See [this](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) blog entry.</span></span>
- [<span data-ttu-id="41c82-119">Opera Mobile 模擬器</span><span class="sxs-lookup"><span data-stu-id="41c82-119">Opera Mobile Emulator</span></span>](http://www.opera.com/developer/tools/mobile/)
- <span data-ttu-id="41c82-120">將使用者代理程式設定為 iPhone 的[Apple Safari](http://www.apple.com/safari/download/) 。</span><span class="sxs-lookup"><span data-stu-id="41c82-120">[Apple Safari](http://www.apple.com/safari/download/) with the user agent set to iPhone.</span></span> <span data-ttu-id="41c82-121">如需有關如何將 Safari 中的使用者代理程式設定為「iPhone」的指示，請參閱[如何讓 safari](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html)在 David Alison 的 blog 上偽裝為 IE。</span><span class="sxs-lookup"><span data-stu-id="41c82-121">For instructions on how to set the user agent in Safari to "iPhone", see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) on David Alison's blog.</span></span>

<span data-ttu-id="41c82-122">此處提供具有 C\# 原始程式碼的 Visual Studio 專案來幫助您完成本主題：</span><span class="sxs-lookup"><span data-stu-id="41c82-122">Visual Studio projects with C# source code are available to accompany this topic:</span></span>

- [<span data-ttu-id="41c82-123">入門專案下載</span><span class="sxs-lookup"><span data-stu-id="41c82-123">Starter project download</span></span>](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [<span data-ttu-id="41c82-124">已完成專案下載</span><span class="sxs-lookup"><span data-stu-id="41c82-124">Completed project download</span></span>](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a><span data-ttu-id="41c82-125">您要建置的內容</span><span class="sxs-lookup"><span data-stu-id="41c82-125">What You'll Build</span></span>

<span data-ttu-id="41c82-126">在本教學課程中，您會將行動功能新增至[起始專案](https://go.microsoft.com/fwlink/?LinkId=228307)中提供的簡單會議清單應用程式。</span><span class="sxs-lookup"><span data-stu-id="41c82-126">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project](https://go.microsoft.com/fwlink/?LinkId=228307).</span></span> <span data-ttu-id="41c82-127">下列螢幕擷取畫面顯示已完成應用程式的 [標記] 頁面，如[Windows 7 Phone 模擬器](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)中所示。</span><span class="sxs-lookup"><span data-stu-id="41c82-127">The following screenshot shows the tags page of the completed application as seen in the [Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span></span> <span data-ttu-id="41c82-128">請參閱[Windows Phone 模擬器的鍵盤對應](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx)，以簡化鍵盤輸入。</span><span class="sxs-lookup"><span data-stu-id="41c82-128">See [Keyboard Mapping for Windows Phone Emulator](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) to simplify keyboard input.</span></span>

<span data-ttu-id="41c82-129">[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-129">[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)</span></span>

<span data-ttu-id="41c82-130">您可以藉由設定[使用者代理字串](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)，來使用 Internet Explorer 9 或10、FireFox 或 Chrome 來開發您的行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="41c82-130">You can use Internet Explorer version 9 or 10, FireFox or Chrome to develop your mobile application by setting the [user agent string](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/).</span></span> <span data-ttu-id="41c82-131">下圖顯示使用 Internet Explorer 模擬 iPhone 的已完成教學課程。</span><span class="sxs-lookup"><span data-stu-id="41c82-131">The following image shows the completed tutorial using Internet Explorer emulating an iPhone.</span></span> <span data-ttu-id="41c82-132">您可以使用 Internet Explorer F-12 開發人員工具和[Fiddler 工具](http://www.fiddler2.com/fiddler2/)，協助您進行應用程式的偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="41c82-132">You can use the Internet Explorer F-12 developer tools and the [Fiddler tool](http://www.fiddler2.com/fiddler2/) to help debug your application.</span></span>

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a><span data-ttu-id="41c82-133">您要學習的技術</span><span class="sxs-lookup"><span data-stu-id="41c82-133">Skills You'll Learn</span></span>

<span data-ttu-id="41c82-134">以下是您要學習的內容：</span><span class="sxs-lookup"><span data-stu-id="41c82-134">Here's what you'll learn:</span></span>

- <span data-ttu-id="41c82-135">ASP.NET MVC 4 範本如何使用 HTML5 `viewport` 屬性和適應性轉譯來改善行動裝置上的顯示。</span><span class="sxs-lookup"><span data-stu-id="41c82-135">How the ASP.NET MVC 4 templates use the HTML5 `viewport` attribute and adaptive rendering to improve display on mobile devices.</span></span>
- <span data-ttu-id="41c82-136">如何建立行動裝置特定的視圖。</span><span class="sxs-lookup"><span data-stu-id="41c82-136">How to create mobile-specific views.</span></span>
- <span data-ttu-id="41c82-137">如何建立可讓使用者在行動視圖和應用程式桌面視圖之間切換的視圖切換器。</span><span class="sxs-lookup"><span data-stu-id="41c82-137">How to create a view switcher that lets users toggle between a mobile view and a desktop view of the application.</span></span>

### <a name="getting-started"></a><span data-ttu-id="41c82-138">快速入門</span><span class="sxs-lookup"><span data-stu-id="41c82-138">Getting Started</span></span>

<span data-ttu-id="41c82-139">使用下列連結下載入門專案的會議清單應用程式：[下載](https://go.microsoft.com/fwlink/?LinkId=228307)。</span><span class="sxs-lookup"><span data-stu-id="41c82-139">Download the conference-listing application for the starter project using the following link: [Download](https://go.microsoft.com/fwlink/?LinkId=228307).</span></span> <span data-ttu-id="41c82-140">然後在 Windows Explorer 中，以滑鼠右鍵按一下 [ *MvcMobile* ] 檔案，然後選擇 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="41c82-140">Then in Windows Explorer, right-click the *MvcMobile.zip* file and choose **Properties**.</span></span> <span data-ttu-id="41c82-141">在 [ **MvcMobile 屬性**] 對話方塊中，選擇 [**解除封鎖**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="41c82-141">In the **MvcMobile.zip Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="41c82-142">(取消封鎖後，當您嘗試使用從網路下載的 .zip 檔案時，就不會出現安全性警告。)</span><span class="sxs-lookup"><span data-stu-id="41c82-142">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

<span data-ttu-id="41c82-144">以滑鼠右鍵按一下 [ *MvcMobile* ] 檔案，然後選取 [**解壓縮全部**] 以解壓縮檔案。</span><span class="sxs-lookup"><span data-stu-id="41c82-144">Right-click the *MvcMobile.zip* file and select **Extract All** to unzip the file.</span></span> <span data-ttu-id="41c82-145">在 Visual Studio 中，開啟 [ *MvcMobile* ] 檔案。</span><span class="sxs-lookup"><span data-stu-id="41c82-145">In Visual Studio, open the *MvcMobile.sln* file.</span></span>

<span data-ttu-id="41c82-146">按 CTRL + F5 執行應用程式，這會在您的桌面瀏覽器中顯示它。</span><span class="sxs-lookup"><span data-stu-id="41c82-146">Press CTRL+F5 to run the application, which will display it in your desktop browser.</span></span> <span data-ttu-id="41c82-147">啟動行動瀏覽器模擬器，將會議應用程式的 URL 複製到模擬器中，然後按一下 [**依標記流覽]** 連結。</span><span class="sxs-lookup"><span data-stu-id="41c82-147">Start your mobile browser emulator, copy the URL for the conference application into the emulator, and then click the **Browse by tag** link.</span></span> <span data-ttu-id="41c82-148">如果您使用 Windows Phone 模擬器，請按一下 URL 列，然後按下 [暫停] 鍵以取得鍵盤存取。</span><span class="sxs-lookup"><span data-stu-id="41c82-148">If you are using the Windows Phone Emulator, click in the URL bar and press the Pause key to get keyboard access.</span></span> <span data-ttu-id="41c82-149">下圖顯示 [ *AllTags* ] 視圖（從選擇 **[依標記流覽]** ）。</span><span class="sxs-lookup"><span data-stu-id="41c82-149">The image below shows the *AllTags* view (from choosing **Browse by tag**).</span></span>

<span data-ttu-id="41c82-150">[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-150">[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)</span></span>

<span data-ttu-id="41c82-151">該顯示內容在行動裝置上非常清楚易讀。</span><span class="sxs-lookup"><span data-stu-id="41c82-151">The display is very readable on a mobile device.</span></span> <span data-ttu-id="41c82-152">選擇 [ASP.NET] 連結。</span><span class="sxs-lookup"><span data-stu-id="41c82-152">Choose the ASP.NET link.</span></span>

<span data-ttu-id="41c82-153">[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-153">[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)</span></span>

<span data-ttu-id="41c82-154">ASP.NET 標記視圖非常雜亂。</span><span class="sxs-lookup"><span data-stu-id="41c82-154">The ASP.NET tag view is very cluttered.</span></span> <span data-ttu-id="41c82-155">例如，[**日期] 資料**行非常難以閱讀。</span><span class="sxs-lookup"><span data-stu-id="41c82-155">For example, the **Date** column is very difficult to read.</span></span> <span data-ttu-id="41c82-156">稍後在本教學課程中，您將會建立專為行動瀏覽器提供的*AllTags* view 版本，並讓顯示可讀取。</span><span class="sxs-lookup"><span data-stu-id="41c82-156">Later in the tutorial you'll create a version of the *AllTags* view that's specifically for mobile browsers and that will make the display readable.</span></span>

<span data-ttu-id="41c82-157">注意：行動快取引擎目前有一個 bug。</span><span class="sxs-lookup"><span data-stu-id="41c82-157">Note: Currently a bug exists in the mobile caching engine.</span></span> <span data-ttu-id="41c82-158">對於生產應用程式，您必須安裝[Fixed DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget 套件。</span><span class="sxs-lookup"><span data-stu-id="41c82-158">For production applications, you must install the [Fixed DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget package.</span></span> <span data-ttu-id="41c82-159">如需修正的詳細資訊，請參閱 < [ASP.NET MVC 4](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)行動快取錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="41c82-159">See [ASP.NET MVC 4 Mobile Caching Bug Fixed](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) for details on the fix.</span></span>

## <a name="css-media-queries"></a><span data-ttu-id="41c82-160">CSS 媒體查詢</span><span class="sxs-lookup"><span data-stu-id="41c82-160">CSS Media Queries</span></span>

<span data-ttu-id="41c82-161">[Css 媒體查詢](http://www.w3.org/TR/css3-mediaqueries/)是適用于媒體類型的 css 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="41c82-161">[CSS media queries](http://www.w3.org/TR/css3-mediaqueries/) are an extension to CSS for media types.</span></span> <span data-ttu-id="41c82-162">它們可讓您建立規則，以覆寫特定瀏覽器（使用者代理程式）的預設 CSS 規則。</span><span class="sxs-lookup"><span data-stu-id="41c82-162">They allow you to create rules that override the default CSS rules for specific browsers (user agents).</span></span> <span data-ttu-id="41c82-163">以行動瀏覽器為目標的 CSS 通用規則會定義最大螢幕大小。</span><span class="sxs-lookup"><span data-stu-id="41c82-163">A common rule for CSS that targets mobile browsers is defining the maximum screen size.</span></span> <span data-ttu-id="41c82-164">當您建立新的 ASP.NET MVC 4 網際網路專案時所建立的*Content\Site.css*檔案包含下列媒體查詢：</span><span class="sxs-lookup"><span data-stu-id="41c82-164">The *Content\Site.css* file that's created when you create a new ASP.NET MVC 4 Internet project contains the following media query:</span></span>

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

<span data-ttu-id="41c82-165">如果瀏覽器視窗寬或小於850圖元，則會使用此媒體區塊內的 CSS 規則。</span><span class="sxs-lookup"><span data-stu-id="41c82-165">If the browser window is 850 pixels wide or less, it will use the CSS rules inside this media block.</span></span> <span data-ttu-id="41c82-166">您可以使用像這樣的 CSS 媒體查詢，在小型瀏覽器（如行動瀏覽器）上提供更好的 HTML 內容顯示，而不是針對更廣泛的桌面瀏覽器顯示所設計的預設 CSS 規則。</span><span class="sxs-lookup"><span data-stu-id="41c82-166">You can use CSS media queries like this to provide a better display of HTML content on small browsers (like mobile browsers) than the default CSS rules that are designed for the wider displays of desktop browsers.</span></span>

## <a name="the-viewport-meta-tag"></a><span data-ttu-id="41c82-167">視口中繼標記</span><span class="sxs-lookup"><span data-stu-id="41c82-167">The Viewport Meta Tag</span></span>

<span data-ttu-id="41c82-168">大部分的行動瀏覽器定義的虛擬瀏覽器視窗寬度（*視口*）遠大於行動裝置的實際寬度。</span><span class="sxs-lookup"><span data-stu-id="41c82-168">Most mobile browsers define a virtual browser window width (the *viewport*) that's much larger than the actual width of the mobile device.</span></span> <span data-ttu-id="41c82-169">這可讓行動瀏覽器符合虛擬顯示器內的整個網頁。</span><span class="sxs-lookup"><span data-stu-id="41c82-169">This allows mobile browsers to fit the entire web page inside the virtual display.</span></span> <span data-ttu-id="41c82-170">然後，使用者可以放大感興趣的內容。</span><span class="sxs-lookup"><span data-stu-id="41c82-170">Users can then zoom in on interesting content.</span></span> <span data-ttu-id="41c82-171">不過，如果您將 [視口寬度] 設定為 [實際裝置寬度]，則不需要縮放，因為內容適合在行動瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="41c82-171">However, if you set the viewport width to the actual device width, no zooming is required, because the content fits in the mobile browser.</span></span>

<span data-ttu-id="41c82-172">ASP.NET MVC 4 配置檔案中的 [視口] `<meta>` 標記會將此視口設定為裝置寬度。</span><span class="sxs-lookup"><span data-stu-id="41c82-172">The viewport `<meta>` tag in the ASP.NET MVC 4 layout file sets the viewport to the device width.</span></span> <span data-ttu-id="41c82-173">下一行顯示 ASP.NET MVC 4 版面配置檔案中的 [視口] `<meta>` 標記。</span><span class="sxs-lookup"><span data-stu-id="41c82-173">The following line shows the viewport `<meta>` tag in the ASP.NET MVC 4 layout file.</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a><span data-ttu-id="41c82-174">檢查 CSS 媒體查詢和視口中繼標記的效果</span><span class="sxs-lookup"><span data-stu-id="41c82-174">Examining the Effect of CSS Media Queries and the Viewport Meta Tag</span></span>

<span data-ttu-id="41c82-175">在編輯器中開啟*Views\Shared\\_Layout. cshtml*檔案，並將 [視口] `<meta>` 標記批註。</span><span class="sxs-lookup"><span data-stu-id="41c82-175">Open the *Views\Shared\\_Layout.cshtml* file in the editor and comment out the viewport `<meta>` tag.</span></span> <span data-ttu-id="41c82-176">下列標記會顯示已加上批註的行。</span><span class="sxs-lookup"><span data-stu-id="41c82-176">The following markup shows the commented-out line.</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

<span data-ttu-id="41c82-177">在編輯器中開啟*MvcMobile\Content\Site.css*檔案，並將媒體查詢中的最大寬度變更為零圖元。</span><span class="sxs-lookup"><span data-stu-id="41c82-177">Open the *MvcMobile\Content\Site.css* file in the editor and change the maximum width in the media query to zero pixels.</span></span> <span data-ttu-id="41c82-178">這會讓 CSS 規則無法在行動瀏覽器中使用。</span><span class="sxs-lookup"><span data-stu-id="41c82-178">This will prevent the CSS rules from being used in mobile browsers.</span></span> <span data-ttu-id="41c82-179">下一行顯示已修改的媒體查詢：</span><span class="sxs-lookup"><span data-stu-id="41c82-179">The following line shows the modified media query:</span></span>

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

<span data-ttu-id="41c82-180">儲存您的變更，並在行動瀏覽器模擬器中流覽至會議應用程式。</span><span class="sxs-lookup"><span data-stu-id="41c82-180">Save your changes and browse to the Conference application in a mobile browser emulator.</span></span> <span data-ttu-id="41c82-181">下圖中的小型文字是移除 `<meta>` 標記的視口的結果。</span><span class="sxs-lookup"><span data-stu-id="41c82-181">The tiny text in the following image is the result of removing the viewport `<meta>` tag.</span></span> <span data-ttu-id="41c82-182">如果沒有 `<meta>` 標記的視口，瀏覽器會縮小為預設的視口寬度（850圖元或更寬，適用于大部分的行動瀏覽器）。</span><span class="sxs-lookup"><span data-stu-id="41c82-182">With no viewport `<meta>` tag, the browser is zooming out to the default viewport width (850 pixels or wider for most mobile browsers.)</span></span>

<span data-ttu-id="41c82-183">[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-183">[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)</span></span>

<span data-ttu-id="41c82-184">復原您的變更：將設定檔中的 `<meta>` 標記取消批註，並將媒體查詢還原至*網站 .css*檔案中的850圖元。</span><span class="sxs-lookup"><span data-stu-id="41c82-184">Undo your changes — uncomment the viewport `<meta>` tag in the layout file and restore the media query to 850 pixels in the *Site.css* file.</span></span> <span data-ttu-id="41c82-185">儲存您的變更並重新整理行動瀏覽器，以確認是否已還原行動方便的顯示器。</span><span class="sxs-lookup"><span data-stu-id="41c82-185">Save your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="41c82-186">[視口] `<meta>` 標記，而 CSS 媒體查詢不是 ASP.NET MVC 4 特有的，而且您可以在任何 web 應用程式中利用這些功能。</span><span class="sxs-lookup"><span data-stu-id="41c82-186">The viewport `<meta>` tag and the CSS media query are not specific to ASP.NET MVC 4, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="41c82-187">但是，這些檔案現在已內建在您建立新的 ASP.NET MVC 4 專案時所產生的檔案中。</span><span class="sxs-lookup"><span data-stu-id="41c82-187">But they are now built into the files that are generated when you create a new ASP.NET MVC 4 project.</span></span>

<span data-ttu-id="41c82-188">如需有關視口 `<meta>` 標記的詳細資訊，請參閱[兩個數據區的故事-第二部分](http://www.quirksmode.org/mobile/viewports2.html)。</span><span class="sxs-lookup"><span data-stu-id="41c82-188">For more information about the viewport `<meta>` tag, see [A tale of two viewports — part two](http://www.quirksmode.org/mobile/viewports2.html).</span></span>

<span data-ttu-id="41c82-189">您將在下一節看到如何提供行動瀏覽器專用的檢視。</span><span class="sxs-lookup"><span data-stu-id="41c82-189">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <a name="overriding-views-layouts-and-partial-views"></a><span data-ttu-id="41c82-190">覆寫視圖、版面配置和部分視圖</span><span class="sxs-lookup"><span data-stu-id="41c82-190">Overriding Views, Layouts, and Partial Views</span></span>

<span data-ttu-id="41c82-191">ASP.NET MVC 4 中的重要新功能是一種簡單的機制，可讓您針對一般行動瀏覽器、個別行動瀏覽器或任何特定瀏覽器，覆寫任何視圖（包括版面配置和部分觀點）。</span><span class="sxs-lookup"><span data-stu-id="41c82-191">A significant new feature in ASP.NET MVC 4 is a simple mechanism that lets you override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="41c82-192">若要提供行動裝置專屬的檢視，您可以複製檢視檔案並將 *.Mobile* 新增至檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="41c82-192">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="41c82-193">例如，若要建立行動*索引*視圖，請將*Views\Home\Index.cshtml*複製到*Views\Home\Index.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="41c82-193">For example, to create a mobile *Index* view, copy *Views\Home\Index.cshtml* to *Views\Home\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="41c82-194">本節將建立行動裝置專屬的配置檔案。</span><span class="sxs-lookup"><span data-stu-id="41c82-194">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="41c82-195">若要開始，請將*Views\Shared\\_Layout. cshtml*複製到*Views\Shared\\_Layout。*</span><span class="sxs-lookup"><span data-stu-id="41c82-195">To start, copy *Views\Shared\\_Layout.cshtml* to *Views\Shared\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="41c82-196">開啟 *\_Layout* ，並將標題從  **MVC4 會議** 變更為 **會議（** 行動裝置）。</span><span class="sxs-lookup"><span data-stu-id="41c82-196">Open *\_Layout.Mobile.cshtml* and change the title from **MVC4 Conference** to **Conference (Mobile)**.</span></span>

<span data-ttu-id="41c82-197">在每個 `Html.ActionLink` 呼叫中，移除每*個連結的*[流覽者]。</span><span class="sxs-lookup"><span data-stu-id="41c82-197">In each `Html.ActionLink` call, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="41c82-198">下列程式碼顯示行動配置檔案的已完成主體區段。</span><span class="sxs-lookup"><span data-stu-id="41c82-198">The following code shows the completed body section of the mobile layout file.</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

<span data-ttu-id="41c82-199">將*Views\Home\AllTags.cshtml*檔案複製到*Views\Home\AllTags.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="41c82-199">Copy the *Views\Home\AllTags.cshtml* file to *Views\Home\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="41c82-200">開啟新檔案並將 `<h2>` 元素從 "Tags" 變更為 "Tags (M)"：</span><span class="sxs-lookup"><span data-stu-id="41c82-200">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

<span data-ttu-id="41c82-201">使用桌面瀏覽器及行動瀏覽器模擬器，瀏覽至標籤頁面。</span><span class="sxs-lookup"><span data-stu-id="41c82-201">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="41c82-202">行動瀏覽器模擬器會顯示您所做的兩個變更。</span><span class="sxs-lookup"><span data-stu-id="41c82-202">The mobile browser emulator shows the two changes you made.</span></span>

<span data-ttu-id="41c82-203">[![p2m_layoutTags。 mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-203">[![p2m_layoutTags.mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)</span></span>

<span data-ttu-id="41c82-204">相較之下，桌面顯示器並未改變。</span><span class="sxs-lookup"><span data-stu-id="41c82-204">In contrast, the desktop display has not changed.</span></span>

<span data-ttu-id="41c82-205">[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-205">[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)</span></span>

## <a name="browser-specific-views"></a><span data-ttu-id="41c82-206">瀏覽器特定的視圖</span><span class="sxs-lookup"><span data-stu-id="41c82-206">Browser-Specific Views</span></span>

<span data-ttu-id="41c82-207">除了行動與桌面專用的檢視之外，您還可以為個別瀏覽器建立檢視。</span><span class="sxs-lookup"><span data-stu-id="41c82-207">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="41c82-208">例如，您可以建立專屬於 iPhone 瀏覽器的視圖。</span><span class="sxs-lookup"><span data-stu-id="41c82-208">For example, you can create views that are specifically for the iPhone browser.</span></span> <span data-ttu-id="41c82-209">在本節中，您要建立 iPhone 瀏覽器的配置，以及 iPhone 版的 *AllTags* 檢視。</span><span class="sxs-lookup"><span data-stu-id="41c82-209">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="41c82-210">開啟*global.asax*檔案，並將下列程式碼新增至 `Application_Start` 方法。</span><span class="sxs-lookup"><span data-stu-id="41c82-210">Open the *Global.asax* file and add the following code to the `Application_Start` method.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

<span data-ttu-id="41c82-211">此程式碼會定義要比對每個連入要求且名為 "iPhone" 的新顯示模式。</span><span class="sxs-lookup"><span data-stu-id="41c82-211">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="41c82-212">若連入的要求符合您定義的條件 (亦即使用者代理程式包含 "iPhone" 字串)，則 ASP.NET MVC 會尋找名稱包含 "iPhone" 字尾的檢視。</span><span class="sxs-lookup"><span data-stu-id="41c82-212">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

<span data-ttu-id="41c82-213">以滑鼠右鍵按一下程式碼的 `DefaultDisplayMode`，選擇 [解析]，然後選擇 `using System.Web.WebPages;`。</span><span class="sxs-lookup"><span data-stu-id="41c82-213">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="41c82-214">這麼做會將參考加入定義 `System.Web.WebPages` 和 `DisplayModes` 類型的 `DefaultDisplayMode` 命名空間。</span><span class="sxs-lookup"><span data-stu-id="41c82-214">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModes` and `DefaultDisplayMode` types are defined.</span></span>

<span data-ttu-id="41c82-215">[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-215">[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)</span></span>

<span data-ttu-id="41c82-216">或者，您可以手動將以下的行加入檔案的 `using` 區段即可。</span><span class="sxs-lookup"><span data-stu-id="41c82-216">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

<span data-ttu-id="41c82-217">*Global.asax*檔案的完整內容如下所示。</span><span class="sxs-lookup"><span data-stu-id="41c82-217">The complete contents of the *Global.asax* file is shown below.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

<span data-ttu-id="41c82-218">儲存變更。</span><span class="sxs-lookup"><span data-stu-id="41c82-218">Save the changes.</span></span> <span data-ttu-id="41c82-219">將*MvcMobile\Views\Shared\\_Layout.* *MvcMobile\Views\Shared\\_Layout. iPhone*。</span><span class="sxs-lookup"><span data-stu-id="41c82-219">Copy the *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file to *MvcMobile\Views\Shared\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="41c82-220">開啟新檔案，然後將 `h1` 標題從 `Conference (Mobile)` 變更為 [`Conference (iPhone)`]。</span><span class="sxs-lookup"><span data-stu-id="41c82-220">Open the new file and then change the `h1` heading from `Conference (Mobile)` to `Conference (iPhone)`.</span></span>

<span data-ttu-id="41c82-221">將*MvcMobile\Views\Home\AllTags.Mobile.cshtml*檔案複製到*MvcMobile\Views\Home\AllTags.iPhone.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="41c82-221">Copy the *MvcMobile\Views\Home\AllTags.Mobile.cshtml* file to *MvcMobile\Views\Home\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="41c82-222">在新檔案中，將 `<h2>` 元素從「Tags (M)」變更為「Tags (iPhone)」。</span><span class="sxs-lookup"><span data-stu-id="41c82-222">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="41c82-223">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="41c82-223">Run the application.</span></span> <span data-ttu-id="41c82-224">執行行動瀏覽器模擬器，請確認其使用者代理程式設為「iPhone」，然後瀏覽至 *AllTags* 檢視。</span><span class="sxs-lookup"><span data-stu-id="41c82-224">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="41c82-225">下列螢幕擷取畫面顯示在[Safari](http://www.apple.com/safari/download/)瀏覽器中呈現的*AllTags*視圖。</span><span class="sxs-lookup"><span data-stu-id="41c82-225">The following screenshot shows the *AllTags* view rendered in the [Safari](http://www.apple.com/safari/download/) browser.</span></span> <span data-ttu-id="41c82-226">您可以在[這裡](https://support.apple.com/kb/DL1531)下載適用于 Windows 的 Safari。</span><span class="sxs-lookup"><span data-stu-id="41c82-226">You can download Safari for Windows [here](https://support.apple.com/kb/DL1531).</span></span>

<span data-ttu-id="41c82-227">[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-227">[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)</span></span>

<span data-ttu-id="41c82-228">在本節中，我們已了解如何建立行動配置和檢視，以及如何為特定裝置 (例如 iPhone) 建立配置和檢視。</span><span class="sxs-lookup"><span data-stu-id="41c82-228">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span> <span data-ttu-id="41c82-229">在下一節中，您將瞭解如何運用 jQuery Mobile 來提供更吸引人的行動裝置。</span><span class="sxs-lookup"><span data-stu-id="41c82-229">In the next section you'll see how to leverage jQuery Mobile for more compelling mobile views.</span></span>

## <a name="using-jquery-mobile"></a><span data-ttu-id="41c82-230">使用 jQuery Mobile</span><span class="sxs-lookup"><span data-stu-id="41c82-230">Using jQuery Mobile</span></span>

<span data-ttu-id="41c82-231">[JQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html)程式庫提供一個可在所有主要行動瀏覽器上運作的使用者介面架構。</span><span class="sxs-lookup"><span data-stu-id="41c82-231">The [jQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) library provides a user interface framework that works on all the major mobile browsers.</span></span> <span data-ttu-id="41c82-232">jQuery Mobile 會對支援 CSS 和 JavaScript 的行動瀏覽器套用*漸進增強功能*。</span><span class="sxs-lookup"><span data-stu-id="41c82-232">jQuery Mobile applies *progressive enhancement* to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="41c82-233">漸進式增強功能可讓所有瀏覽器顯示網頁的基本內容，同時允許更強大的瀏覽器和裝置具有更豐富的顯示。</span><span class="sxs-lookup"><span data-stu-id="41c82-233">Progressive enhancement allows all browsers to display the basic content of a web page, while allowing more powerful browsers and devices to have a richer display.</span></span> <span data-ttu-id="41c82-234">JQuery Mobile 樣式的 JavaScript 和 CSS 檔案包含許多元素，以符合行動瀏覽器，而不會進行任何標記變更。</span><span class="sxs-lookup"><span data-stu-id="41c82-234">The JavaScript and CSS files that are included with jQuery Mobile style many elements to fit mobile browsers without making any markup changes.</span></span>

<span data-ttu-id="41c82-235">在本節中，您將安裝*Jquery MOBILE MVC* NuGet 封裝，它會安裝 jquery Mobile 和視圖切換器 widget。</span><span class="sxs-lookup"><span data-stu-id="41c82-235">In this section you'll install the *jQuery.Mobile.MVC* NuGet package, which installs jQuery Mobile and a view-switcher widget.</span></span>

<span data-ttu-id="41c82-236">若要開始，請先刪除您稍早建立的*共用\\_Layout.* 和*共用\\_Layout iPhone*檔案。</span><span class="sxs-lookup"><span data-stu-id="41c82-236">To start, delete the *Shared\\_Layout.Mobile.cshtml* and *Shared\\_Layout.iPhone.cshtml* files that you created earlier.</span></span>

<span data-ttu-id="41c82-237">將*Views\Home\AllTags.Mobile.cshtml*和*Views\Home\AllTags.iPhone.cshtml*檔案重新命名為*Views\Home\AllTags.iPhone.cshtml.hide*和*Views\Home\AllTags.Mobile.cshtml.hide*。</span><span class="sxs-lookup"><span data-stu-id="41c82-237">Rename *Views\Home\AllTags.Mobile.cshtml* and *Views\Home\AllTags.iPhone.cshtml* files to *Views\Home\AllTags.iPhone.cshtml.hide* and *Views\Home\AllTags.Mobile.cshtml.hide*.</span></span> <span data-ttu-id="41c82-238">因為檔案不再有 *. cshtml*副檔名，所以 ASP.NET MVC 執行時間不會使用這些檔案來轉譯*AllTags*視圖。</span><span class="sxs-lookup"><span data-stu-id="41c82-238">Because the files no longer have a *.cshtml* extension, they won't be used by the ASP.NET MVC runtime to render the *AllTags* view.</span></span>

<span data-ttu-id="41c82-239">執行下列動作以安裝*jQuery* NuGet 套件：</span><span class="sxs-lookup"><span data-stu-id="41c82-239">Install the *jQuery.Mobile.MVC* NuGet package by doing this:</span></span>

1. <span data-ttu-id="41c82-240">從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="41c82-240">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

    <span data-ttu-id="41c82-241">[![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-241">[![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)</span></span>
2. <span data-ttu-id="41c82-242">在 [**套件管理員主控台**] 中，輸入 `Install-Package jQuery.Mobile.MVC -version 1.0.0`</span><span class="sxs-lookup"><span data-stu-id="41c82-242">In the **Package Manager Console**, enter `Install-Package jQuery.Mobile.MVC -version 1.0.0`</span></span>

<span data-ttu-id="41c82-243">下圖顯示 NuGet jQuery. node.js 封裝新增和變更至 MvcMobile 專案的檔案。</span><span class="sxs-lookup"><span data-stu-id="41c82-243">The following image shows the files added and changed to the MvcMobile project by the NuGet jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="41c82-244">新增的檔案會在檔案名後面附加 [add]。</span><span class="sxs-lookup"><span data-stu-id="41c82-244">Files which are added have [add] appended after the file name.</span></span> <span data-ttu-id="41c82-245">影像不會顯示新增至*Content\images*資料夾的 GIF 和 PNG 檔案。</span><span class="sxs-lookup"><span data-stu-id="41c82-245">The image does not show the GIF and PNG files added to the *Content\images* folder.</span></span>

![](aspnet-mvc-4-mobile-features/_static/image21.png)

<span data-ttu-id="41c82-246">JQuery NuGet 套件會安裝下列各項：</span><span class="sxs-lookup"><span data-stu-id="41c82-246">The jQuery.Mobile.MVC NuGet package installs the following:</span></span>

- <span data-ttu-id="41c82-247">*應用程式\_Start\BundleMobileConfig.cs*檔，這是參考所新增之 jQuery JAVASCRIPT 和 CSS 檔案所需的檔案。</span><span class="sxs-lookup"><span data-stu-id="41c82-247">The *App\_Start\BundleMobileConfig.cs* file, which is needed to reference the jQuery JavaScript and CSS files added.</span></span> <span data-ttu-id="41c82-248">您必須遵循下列指示，並參考此檔案中定義的行動套件組合。</span><span class="sxs-lookup"><span data-stu-id="41c82-248">You must follow the instructions below and reference the mobile bundle defined in this file.</span></span>
- <span data-ttu-id="41c82-249">jQuery Mobile CSS 檔案。</span><span class="sxs-lookup"><span data-stu-id="41c82-249">jQuery Mobile CSS files.</span></span>
- <span data-ttu-id="41c82-250">`ViewSwitcher` 控制器 widget （*Controllers\ViewSwitcherController.cs*）。</span><span class="sxs-lookup"><span data-stu-id="41c82-250">A `ViewSwitcher` controller widget (*Controllers\ViewSwitcherController.cs*).</span></span>
- <span data-ttu-id="41c82-251">jQuery Mobile JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="41c82-251">jQuery Mobile JavaScript files.</span></span>
- <span data-ttu-id="41c82-252">JQuery Mobile 樣式配置檔案（*Views\Shared\\_Layout。*</span><span class="sxs-lookup"><span data-stu-id="41c82-252">A jQuery Mobile-styled layout file (*Views\Shared\\_Layout.Mobile.cshtml*).</span></span>
- <span data-ttu-id="41c82-253">「視圖-切換器部分視圖」 *（MvcMobile\Views\Shared\\_ViewSwitcher. cshtml*），可在每個頁面頂端提供連結，以從 [桌面] 視圖切換至 [mobile view]，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="41c82-253">A view-switcher partial view *(MvcMobile\Views\Shared\\_ViewSwitcher.cshtml*) that provides a link at the top of each page to switch from desktop view to mobile view and vice versa.</span></span>
- <span data-ttu-id="41c82-254"><em>Content\images</em>資料夾中有數個<em>.png</em>和<em>.gif</em>影像檔案。</span><span class="sxs-lookup"><span data-stu-id="41c82-254">Several<em>.png</em> and <em>.gif</em> image files in the <em>Content\images</em> folder.</span></span>

<span data-ttu-id="41c82-255">開啟*global.asax*檔案，並加入下列程式碼做為 `Application_Start` 方法的最後一行。</span><span class="sxs-lookup"><span data-stu-id="41c82-255">Open the *Global.asax* file and add the following code as the last line of the `Application_Start` method.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

<span data-ttu-id="41c82-256">下列程式碼顯示完整的*global.asax*檔案。</span><span class="sxs-lookup"><span data-stu-id="41c82-256">The following code shows the complete *Global.asax* file.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> <span data-ttu-id="41c82-257">如果您使用的是 Internet Explorer 9，但未在黃色醒目提示中看到 [`BundleMobileConfig`] 行，請按一下 IE 中![[相容性](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "[相容性檢視] 按鈕的圖片（關閉）")視圖] 按鈕的 [[相容性](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)視圖] 按鈕 [圖片]，讓圖示從![[相容性檢視] 按鈕（關閉）](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "[相容性檢視] 按鈕的圖片（關閉）")的大綱圖片變更為![[相容性檢視] 按鈕的純色圖片（開啟）](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "[相容性檢視] 按鈕的圖片（開啟）")。</span><span class="sxs-lookup"><span data-stu-id="41c82-257">If you are using Internet Explorer 9 and you don't see the `BundleMobileConfig` line above in yellow highlight, click the [Compatibility View button](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![Picture of the Compatibility View button (off)](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Picture of the Compatibility View button (off)") in IE to make the icon change from an outline ![Picture of the Compatibility View button (off)](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Picture of the Compatibility View button (off)") to a solid color ![Picture of the Compatibility View button (on)](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "Picture of the Compatibility View button (on)").</span></span> <span data-ttu-id="41c82-258">或者，您可以在 FireFox 或 Chrome 中觀看本教學課程。</span><span class="sxs-lookup"><span data-stu-id="41c82-258">Alternatively you can view this tutorial in FireFox or Chrome.</span></span>

<span data-ttu-id="41c82-259">開啟*MvcMobile\Views\Shared\\_Layout* ，然後在 `Html.Partial` 呼叫之後，直接新增下列標記：</span><span class="sxs-lookup"><span data-stu-id="41c82-259">Open the *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file and add the following markup directly after the `Html.Partial` call:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

<span data-ttu-id="41c82-260">完整的*MvcMobile\Views\Shared\\_Layout* ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="41c82-260">The complete *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file is shown below:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

<span data-ttu-id="41c82-261">建立應用程式，然後在您的行動瀏覽器模擬器中，流覽至 [ *AllTags* ] 視圖。</span><span class="sxs-lookup"><span data-stu-id="41c82-261">Build the application, and in your mobile browser emulator browse to the *AllTags* view.</span></span> <span data-ttu-id="41c82-262">這時會顯示下列項目：</span><span class="sxs-lookup"><span data-stu-id="41c82-262">You see the following:</span></span>

<span data-ttu-id="41c82-263">[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-263">[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)</span></span>

> [!NOTE]
> <span data-ttu-id="41c82-264">您可以藉由將 IE 或 Chrome[的使用者代理字串設定](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)為 iPhone，然後使用 F-12 開發人員工具，來對行動裝置的特定程式碼進行偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="41c82-264">You can debug the mobile specific code by [setting the user agent string](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) for IE or Chrome to iPhone and then using the F-12 developer tools.</span></span> <span data-ttu-id="41c82-265">如果您的行動瀏覽器未將 [**首頁**]、[**說話者**]、[**標記**] 和 [**日期**] 連結顯示為按鈕，則 jQuery mobile 腳本和 CSS 檔案的參考可能會不正確。</span><span class="sxs-lookup"><span data-stu-id="41c82-265">If your mobile browser doesn't display the **Home**, **Speaker**, **Tag**, and **Date** links as buttons, the references to jQuery Mobile scripts and CSS files are probably not correct.</span></span>

<span data-ttu-id="41c82-266">除了樣式變更之外，您還會看到 [ **mobile view** ] 和一個連結，可讓您從 [行動視圖] 切換到 [桌面視圖]。</span><span class="sxs-lookup"><span data-stu-id="41c82-266">In addition to the style changes, you see **Displaying mobile view** and a link that lets you switch from mobile view to desktop view.</span></span> <span data-ttu-id="41c82-267">選擇 [**桌面視圖**] 連結，隨即會顯示桌面視圖。</span><span class="sxs-lookup"><span data-stu-id="41c82-267">Choose the **Desktop view** link, and the desktop view is displayed.</span></span>

<span data-ttu-id="41c82-268">[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-268">[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)</span></span>

<span data-ttu-id="41c82-269">[桌面] 視圖無法直接流覽回到 [行動] 視圖。</span><span class="sxs-lookup"><span data-stu-id="41c82-269">The desktop view doesn't provide a way to directly navigate back to the mobile view.</span></span> <span data-ttu-id="41c82-270">您會立即修正此問題。</span><span class="sxs-lookup"><span data-stu-id="41c82-270">You'll fix that now.</span></span> <span data-ttu-id="41c82-271">開啟*Views\Shared\\_Layout. cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="41c82-271">Open the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="41c82-272">在 `body` 專案的頁面下，新增下列程式碼，以轉譯視圖切換器 widget：</span><span class="sxs-lookup"><span data-stu-id="41c82-272">Just under the page `body` element, add the following code, which renders the view-switcher widget:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

<span data-ttu-id="41c82-273">重新整理行動瀏覽器中的*AllTags*視圖。</span><span class="sxs-lookup"><span data-stu-id="41c82-273">Refresh the *AllTags* view in the mobile browser.</span></span> <span data-ttu-id="41c82-274">您現在可以在 [桌面] 和 [行動裝置] 視圖之間流覽。</span><span class="sxs-lookup"><span data-stu-id="41c82-274">You can now navigate between desktop and mobile views.</span></span>

<span data-ttu-id="41c82-275">[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-275">[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)</span></span>

> [!NOTE]
> <span data-ttu-id="41c82-276">Debug note：您可以將下列程式碼新增至 Views\Shared _ViewSwitcher\\的結尾，以在使用瀏覽器將使用者代理字串設定為行動裝置時，協助偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="41c82-276">Debug note: You can add the following code to the end of the Views\Shared\\_ViewSwitcher.cshtml to help debug views when using a browser the user agent string set to a mobile device.</span></span>
>
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
>
> <span data-ttu-id="41c82-277">並將下列標題新增至*Views\Shared\\_Layout. cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="41c82-277">and adding the following heading to the *Views\Shared\\_Layout.cshtml* file.</span></span>
>
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]

<span data-ttu-id="41c82-278">流覽至桌面瀏覽器中的 [ *AllTags* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="41c82-278">Browse to the *AllTags* page in a desktop browser.</span></span> <span data-ttu-id="41c82-279">「視圖切換器」 widget 不會顯示在桌面瀏覽器中，因為它只會新增至行動版面配置頁面。</span><span class="sxs-lookup"><span data-stu-id="41c82-279">The view-switcher widget is not displayed in a desktop browser because it's added only to the mobile layout page.</span></span> <span data-ttu-id="41c82-280">稍後在本教學課程中，您會看到如何將視圖切換器 widget 新增至桌面視圖。</span><span class="sxs-lookup"><span data-stu-id="41c82-280">Later in the tutorial you'll see how you can add the view-switcher widget to the desktop view.</span></span>

<span data-ttu-id="41c82-281">[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-281">[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)</span></span>

## <a name="improving-the-speakers-list"></a><span data-ttu-id="41c82-282">改善喇叭清單</span><span class="sxs-lookup"><span data-stu-id="41c82-282">Improving the Speakers List</span></span>

<span data-ttu-id="41c82-283">在行動瀏覽器中，選取 [演講者] 連結。</span><span class="sxs-lookup"><span data-stu-id="41c82-283">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="41c82-284">因為沒有 mobile view （*AllSpeakers*），所以會使用行動裝置版面配置視圖（ *\_layout*）來呈現預設的喇叭顯示（*AllSpeakers*）。</span><span class="sxs-lookup"><span data-stu-id="41c82-284">Because there's no mobile view(*AllSpeakers.Mobile.cshtml*), the default speakers display (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span>

<span data-ttu-id="41c82-285">[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-285">[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)</span></span>

<span data-ttu-id="41c82-286">您可以藉由將 `RequireConsistentDisplayMode` 設定為 [ *Views]\\_ViewStart. cshtml*檔案中的 `true`，將預設（非行動）視圖全域停用在行動配置內呈現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="41c82-286">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\_ViewStart.cshtml* file, like this:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

<span data-ttu-id="41c82-287">當 `RequireConsistentDisplayMode` 設定為 `true`時，行動裝置版面配置（<em>\_配置. cshtml</em>）只會用於行動裝置視圖。</span><span class="sxs-lookup"><span data-stu-id="41c82-287">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (<em>\_Layout.Mobile.cshtml</em>) is used only for mobile views.</span></span> <span data-ttu-id="41c82-288">（也就是說，視圖檔案的格式為<em>\* \* ViewName</em><em>。</em>`RequireConsistentDisplayMode`，如果您的行動配置不適用於您的非行動裝置的視圖，您可能會想要設定 `true`。</span><span class="sxs-lookup"><span data-stu-id="41c82-288">(That is, the view file is of the form <em>\*\*ViewName</em><em>.Mobile.cshtml</em>.) You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="41c82-289">下列螢幕擷取畫面顯示當 `RequireConsistentDisplayMode` 設定為 `true`時，<em>說話</em>者頁面的呈現方式。</span><span class="sxs-lookup"><span data-stu-id="41c82-289">The screenshot below shows how the <em>Speakers</em> page renders when `RequireConsistentDisplayMode` is set to `true`.</span></span>

<span data-ttu-id="41c82-290">[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-290">[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)</span></span>

<span data-ttu-id="41c82-291">您可以藉由將 `RequireConsistentDisplayMode` 設定為在視圖檔案中 `false`，停用一致的顯示模式。</span><span class="sxs-lookup"><span data-stu-id="41c82-291">You can disable consistent display mode in a view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="41c82-292">*Views\Home\AllSpeakers.cshtml*檔案中的下列標記會將 `RequireConsistentDisplayMode` 設定為 `false`：</span><span class="sxs-lookup"><span data-stu-id="41c82-292">The following markup in the *Views\Home\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a><span data-ttu-id="41c82-293">建立行動喇叭視圖</span><span class="sxs-lookup"><span data-stu-id="41c82-293">Creating a Mobile Speakers View</span></span>

<span data-ttu-id="41c82-294">如您適才所見，行動裝置上的 [ *演講者* ] 檢視已可讀取，但是連結卻非常微小而不容易點選。</span><span class="sxs-lookup"><span data-stu-id="41c82-294">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="41c82-295">在本節中，您將建立與新式行動應用程式類似的行動裝置特定*說話*者，它會顯示大型、易於分的連結，並包含搜尋方塊來快速尋找喇叭。</span><span class="sxs-lookup"><span data-stu-id="41c82-295">In this section, you'll create a mobile-specific *Speakers* view that looks like a modern mobile application — it displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="41c82-296">將*AllSpeakers*複製到*AllSpeakers*。</span><span class="sxs-lookup"><span data-stu-id="41c82-296">Copy *AllSpeakers.cshtml* to *AllSpeakers.Mobile.cshtml*.</span></span> <span data-ttu-id="41c82-297">開啟*AllSpeakers*檔案，並移除 `<h2>` 的標題元素。</span><span class="sxs-lookup"><span data-stu-id="41c82-297">Open the *AllSpeakers.Mobile.cshtml* file and remove the `<h2>` heading element.</span></span>

<span data-ttu-id="41c82-298">在 [`<ul>`] 標籤中，加入 `data-role` 屬性，並將其值設定為 [`listview`]。</span><span class="sxs-lookup"><span data-stu-id="41c82-298">In the `<ul>` tag, add the `data-role` attribute and set its value to `listview`.</span></span> <span data-ttu-id="41c82-299">就像其他[`data-*` 屬性](http://html5doctor.com/html5-custom-data-attributes/)一樣，`data-role="listview"` 讓大型清單專案變得更容易。</span><span class="sxs-lookup"><span data-stu-id="41c82-299">Like other [`data-*` attributes](http://html5doctor.com/html5-custom-data-attributes/), `data-role="listview"` makes the large list items easier to tap.</span></span> <span data-ttu-id="41c82-300">完成的標記如下所示：</span><span class="sxs-lookup"><span data-stu-id="41c82-300">This is what the completed markup looks like:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

<span data-ttu-id="41c82-301">重新整理行動瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="41c82-301">Refresh the mobile browser.</span></span> <span data-ttu-id="41c82-302">更新的檢視如下所示：</span><span class="sxs-lookup"><span data-stu-id="41c82-302">The updated view looks like this:</span></span>

<span data-ttu-id="41c82-303">[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-303">[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)</span></span>

<span data-ttu-id="41c82-304">雖然行動視圖已改良，但很難以流覽長的說話者清單。</span><span class="sxs-lookup"><span data-stu-id="41c82-304">Although the mobile view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="41c82-305">若要修正此問題，請在 `<ul>` 標記中加入 `data-filter` 屬性，並將它設定為 [`true`]。</span><span class="sxs-lookup"><span data-stu-id="41c82-305">To fix this, in the `<ul>` tag, add the `data-filter` attribute and set it to `true`.</span></span> <span data-ttu-id="41c82-306">下列程式碼顯示 `ul` 標記。</span><span class="sxs-lookup"><span data-stu-id="41c82-306">The code below shows the `ul` markup.</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

<span data-ttu-id="41c82-307">下圖顯示 `data-filter` 屬性所產生之頁面頂端的 [搜尋] 篩選方塊。</span><span class="sxs-lookup"><span data-stu-id="41c82-307">The following image shows the search filter box at the top of the page that results from the `data-filter` attribute.</span></span>

<span data-ttu-id="41c82-308">[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-308">[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)</span></span>

<span data-ttu-id="41c82-309">當您在 [搜尋] 方塊中輸入每個字母時，jQuery Mobile 會篩選顯示的清單，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="41c82-309">As you type each letter in the search box, jQuery Mobile filters the displayed list as shown in the image below.</span></span>

<span data-ttu-id="41c82-310">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-310">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)</span></span>

## <a name="improving-the-tags-list"></a><span data-ttu-id="41c82-311">改善標記清單</span><span class="sxs-lookup"><span data-stu-id="41c82-311">Improving the Tags List</span></span>

<span data-ttu-id="41c82-312">就像預設*說話*者的觀點一樣，*標記*視圖也是可讀取的，但連結很小，而且很容易在行動裝置上點擊。</span><span class="sxs-lookup"><span data-stu-id="41c82-312">Like the default *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="41c82-313">在本節中，您將以修正*喇叭*視圖的相同方式來修正*標記*的觀點。</span><span class="sxs-lookup"><span data-stu-id="41c82-313">In this section, you'll fix the *Tags* view the same way you fixed the *Speakers* view.</span></span>

<span data-ttu-id="41c82-314">移除 &quot;隱藏&quot; 尾碼至*Views\Home\AllTags.Mobile.cshtml.hide*檔案，使其名稱為*Views\Home\AllTags.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="41c82-314">Remove the &quot;hide&quot; suffix to the *Views\Home\AllTags.Mobile.cshtml.hide* file so the name is *Views\Home\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="41c82-315">開啟重新命名的檔案，並移除 `<h2>` 元素。</span><span class="sxs-lookup"><span data-stu-id="41c82-315">Open the renamed file and remove the `<h2>` element.</span></span>

<span data-ttu-id="41c82-316">將 `data-role` 和 `data-filter` 屬性新增至 `<ul>` 標記，如下所示：</span><span class="sxs-lookup"><span data-stu-id="41c82-316">Add the `data-role` and `data-filter` attributes to the `<ul>` tag, as shown here:</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

<span data-ttu-id="41c82-317">下圖顯示字母 `J`的標記頁面篩選。</span><span class="sxs-lookup"><span data-stu-id="41c82-317">The image below shows the tags page filtering on the letter `J`.</span></span>

<span data-ttu-id="41c82-318">[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-318">[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)</span></span>

## <a name="improving-the-dates-list"></a><span data-ttu-id="41c82-319">改善日期清單</span><span class="sxs-lookup"><span data-stu-id="41c82-319">Improving the Dates List</span></span>

<span data-ttu-id="41c82-320">您可以改善 [*說話*者 *] 和 [* 標籤] 視圖，讓您更輕鬆地在行動裝置上使用 [*日期*]。</span><span class="sxs-lookup"><span data-stu-id="41c82-320">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views, so that it's easier to use on a mobile device.</span></span>

<span data-ttu-id="41c82-321">將*Views\Home\AllDates.cshtml*檔案複製到*Views\Home\AllDates.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="41c82-321">Copy the *Views\Home\AllDates.cshtml* file to *Views\Home\AllDates.Mobile.cshtml*.</span></span> <span data-ttu-id="41c82-322">開啟新檔案，並移除 `<h2>` 元素。</span><span class="sxs-lookup"><span data-stu-id="41c82-322">Open the new file and remove the `<h2>` element.</span></span>

<span data-ttu-id="41c82-323">將 `data-role="listview"` 新增至 `<ul>` 標記，如下所示：</span><span class="sxs-lookup"><span data-stu-id="41c82-323">Add `data-role="listview"` to the `<ul>` tag, like this:</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

<span data-ttu-id="41c82-324">下圖顯示 [**日期**] 頁面在 [`data-role`] 屬性備妥的樣子。</span><span class="sxs-lookup"><span data-stu-id="41c82-324">The image below shows what the **Date** page looks like with the `data-role` attribute in place.</span></span>

<span data-ttu-id="41c82-325">[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png)使用下列程式碼取代*Views\Home\AllDates.Mobile.cshtml*檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="41c82-325">[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) Replace the contents of the *Views\Home\AllDates.Mobile.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

<span data-ttu-id="41c82-326">此程式碼會以天為單位來分組所有會話。</span><span class="sxs-lookup"><span data-stu-id="41c82-326">This code groups all sessions by days.</span></span> <span data-ttu-id="41c82-327">它會為每個新的日期建立清單分隔線，並列出分隔線下每一天的所有會話。</span><span class="sxs-lookup"><span data-stu-id="41c82-327">It creates a list divider for each new day, and it lists all the sessions for each day under a divider.</span></span> <span data-ttu-id="41c82-328">以下是此程式碼執行時的樣子：</span><span class="sxs-lookup"><span data-stu-id="41c82-328">Here's what it looks like when this code runs:</span></span>

<span data-ttu-id="41c82-329">[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-329">[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)</span></span>

## <a name="improving-the-sessionstable-view"></a><span data-ttu-id="41c82-330">改善 SessionsTable 視圖</span><span class="sxs-lookup"><span data-stu-id="41c82-330">Improving the SessionsTable View</span></span>

<span data-ttu-id="41c82-331">在本節中，您將建立會話的行動特定視圖。</span><span class="sxs-lookup"><span data-stu-id="41c82-331">In this section, you'll create a mobile-specific view of sessions.</span></span> <span data-ttu-id="41c82-332">我們所做的變更會比我們所建立的其他視圖更廣泛。</span><span class="sxs-lookup"><span data-stu-id="41c82-332">The changes we make will be more extensive than in other views we have created.</span></span>

<span data-ttu-id="41c82-333">在行動瀏覽器中，按一下 [**喇叭**] 按鈕，然後在搜尋方塊中輸入 `Sc`。</span><span class="sxs-lookup"><span data-stu-id="41c82-333">In the mobile browser, tap the **Speaker** button, then enter `Sc` in the search box.</span></span>

<span data-ttu-id="41c82-334">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-334">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)</span></span>

<span data-ttu-id="41c82-335">請按**Scott Hanselman**連結。</span><span class="sxs-lookup"><span data-stu-id="41c82-335">Tap the **Scott Hanselman** link.</span></span>

<span data-ttu-id="41c82-336">[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-336">[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)</span></span>

<span data-ttu-id="41c82-337">如您所見，在行動瀏覽器上顯示的畫面很容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="41c82-337">As you can see, the display is difficult to read on a mobile browser.</span></span> <span data-ttu-id="41c82-338">[日期] 資料行難以閱讀，而且 [標記] 資料行不在視圖中。</span><span class="sxs-lookup"><span data-stu-id="41c82-338">The date column is hard to read and the tags column is out of the view.</span></span> <span data-ttu-id="41c82-339">若要修正此問題，請將*Views\Home\SessionsTable.cshtml*複製到*Views\Home\SessionsTable.Mobile.cshtml*，然後將檔案的內容取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="41c82-339">To fix this, copy *Views\Home\SessionsTable.cshtml* to *Views\Home\SessionsTable.Mobile.cshtml*, and then replace the contents of the file with the following code:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

<span data-ttu-id="41c82-340">程式碼會移除 [會議室] 和 [標籤] 資料行，並以垂直方式格式化標題、說話者和日期，以便在行動瀏覽器上閱讀所有資訊。</span><span class="sxs-lookup"><span data-stu-id="41c82-340">The code removes the room and tags columns, and formats the title, speaker, and date vertically, so that all this information is readable on a mobile browser.</span></span> <span data-ttu-id="41c82-341">下圖反映了程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="41c82-341">The image below reflects the code changes.</span></span>

<span data-ttu-id="41c82-342">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-342">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)</span></span>

## <a name="improving-the-sessionbycode-view"></a><span data-ttu-id="41c82-343">改善 SessionByCode 視圖</span><span class="sxs-lookup"><span data-stu-id="41c82-343">Improving the SessionByCode View</span></span>

<span data-ttu-id="41c82-344">最後，您將建立*SessionByCode* view 的行動特定視圖。</span><span class="sxs-lookup"><span data-stu-id="41c82-344">Finally, you'll create a mobile-specific view of the *SessionByCode* view.</span></span> <span data-ttu-id="41c82-345">在行動瀏覽器中，按一下 [**喇叭**] 按鈕，然後在搜尋方塊中輸入 `Sc`。</span><span class="sxs-lookup"><span data-stu-id="41c82-345">In the mobile browser, tap the **Speaker** button, then enter `Sc` in the search box.</span></span>

<span data-ttu-id="41c82-346">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-346">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)</span></span>

<span data-ttu-id="41c82-347">請按**Scott Hanselman**連結。</span><span class="sxs-lookup"><span data-stu-id="41c82-347">Tap the **Scott Hanselman** link.</span></span> <span data-ttu-id="41c82-348">會顯示 Scott Hanselman 的會話。</span><span class="sxs-lookup"><span data-stu-id="41c82-348">Scott Hanselman's sessions are displayed.</span></span>

<span data-ttu-id="41c82-349">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-349">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)</span></span>

<span data-ttu-id="41c82-350">選擇 [ **MS Web Stack 的愛**] 連結的總覽。</span><span class="sxs-lookup"><span data-stu-id="41c82-350">Choose the **An Overview of the MS Web Stack of Love** link.</span></span>

<span data-ttu-id="41c82-351">[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-351">[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)</span></span>

<span data-ttu-id="41c82-352">預設桌面視圖是正常的，但您可以加以改善。</span><span class="sxs-lookup"><span data-stu-id="41c82-352">The default desktop view is fine, but you can improve it.</span></span>

<span data-ttu-id="41c82-353">將*Views\Home\SessionByCode.cshtml*複製到*Views\Home\SessionByCode.Mobile.cshtml* ，並以下列標記取代*Views\Home\SessionByCode.Mobile.cshtml*檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="41c82-353">Copy the *Views\Home\SessionByCode.cshtml* to *Views\Home\SessionByCode.Mobile.cshtml* and replace the contents of the *Views\Home\SessionByCode.Mobile.cshtml* file with the following markup:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

<span data-ttu-id="41c82-354">新的標記會使用 `data-role` 屬性來改善視圖的版面配置。</span><span class="sxs-lookup"><span data-stu-id="41c82-354">The new markup uses the `data-role` attribute to improve the layout of the view.</span></span>

<span data-ttu-id="41c82-355">重新整理行動瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="41c82-355">Refresh the mobile browser.</span></span> <span data-ttu-id="41c82-356">下圖反映您剛做的程式碼變更：</span><span class="sxs-lookup"><span data-stu-id="41c82-356">The following image reflects the code changes that you just made:</span></span>

<span data-ttu-id="41c82-357">[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)</span><span class="sxs-lookup"><span data-stu-id="41c82-357">[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)</span></span>

## <a name="wrapup-and-review"></a><span data-ttu-id="41c82-358">Wrapup 與審查</span><span class="sxs-lookup"><span data-stu-id="41c82-358">Wrapup and Review</span></span>

<span data-ttu-id="41c82-359">本教學課程引進了 ASP.NET MVC 4 Developer Preview 的新行動功能。</span><span class="sxs-lookup"><span data-stu-id="41c82-359">This tutorial has introduced the new mobile features of ASP.NET MVC 4 Developer Preview.</span></span> <span data-ttu-id="41c82-360">行動功能包括：</span><span class="sxs-lookup"><span data-stu-id="41c82-360">The mobile features include:</span></span>

- <span data-ttu-id="41c82-361">覆寫版面配置、視圖和部分視圖的能力，全域和個別視圖皆可。</span><span class="sxs-lookup"><span data-stu-id="41c82-361">The ability to override layout, views, and partial views, both globally and for an individual view.</span></span>
- <span data-ttu-id="41c82-362">使用 `RequireConsistentDisplayMode` 屬性來控制版面配置和部分覆寫的強制執行。</span><span class="sxs-lookup"><span data-stu-id="41c82-362">Control over layout and partial override enforcement using the `RequireConsistentDisplayMode` property.</span></span>
- <span data-ttu-id="41c82-363">行動裝置視圖的視圖切換器 widget 也可以在桌面視圖中顯示。</span><span class="sxs-lookup"><span data-stu-id="41c82-363">A view-switcher widget for mobile views than can also be displayed in desktop views.</span></span>
- <span data-ttu-id="41c82-364">支援支援特定的瀏覽器，例如 iPhone 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="41c82-364">Support for supporting specific browsers, such as the iPhone browser.</span></span>

## <a name="see-also"></a><span data-ttu-id="41c82-365">另請參閱</span><span class="sxs-lookup"><span data-stu-id="41c82-365">See Also</span></span>

- <span data-ttu-id="41c82-366">[JQuery mobile](http://jquerymobile.com)網站。</span><span class="sxs-lookup"><span data-stu-id="41c82-366">[jQuery Mobile](http://jquerymobile.com) site.</span></span>
- [<span data-ttu-id="41c82-367">jQuery Mobile 總覽</span><span class="sxs-lookup"><span data-stu-id="41c82-367">jQuery Mobile Overview</span></span>](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [<span data-ttu-id="41c82-368">W3C 推薦的行動 Web 應用程式最佳做法</span><span class="sxs-lookup"><span data-stu-id="41c82-368">W3C Recommendation Mobile Web Application Best Practices</span></span>](http://www.w3.org/TR/mwabp/)
- [<span data-ttu-id="41c82-369">W3C 針對媒體查詢的候選推薦做法</span><span class="sxs-lookup"><span data-stu-id="41c82-369">W3C Candidate Recommendation for media queries</span></span>](http://www.w3.org/TR/css3-mediaqueries/)
