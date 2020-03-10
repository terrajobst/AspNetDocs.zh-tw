---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: 在 ASP.NET MVC 中使用 Page Inspector |Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 中的 Page Inspector 是具有整合式瀏覽器的 網頁程式開發工具。 在整合式瀏覽器中選取任何專案，然後 Page Inspector 。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5da3e142c52a770f59222c21d9f9a53cbbdbf498
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538014"
---
# <a name="using-page-inspector-in-aspnet-mvc"></a><span data-ttu-id="c69fa-104">在 ASP.NET MVC 中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="c69fa-104">Using Page Inspector in ASP.NET MVC</span></span>

<span data-ttu-id="c69fa-105">依 Tim Ammann</span><span class="sxs-lookup"><span data-stu-id="c69fa-105">by Tim Ammann</span></span>

> <span data-ttu-id="c69fa-106">Visual Studio 2012 中的 Page Inspector 是具有整合式瀏覽器的 網頁程式開發工具。</span><span class="sxs-lookup"><span data-stu-id="c69fa-106">Page Inspector in Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="c69fa-107">選取整合式瀏覽器中的任何元素，Page Inspector 立即反白顯示專案的來源和 CSS。</span><span class="sxs-lookup"><span data-stu-id="c69fa-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="c69fa-108">您可以流覽任何 MVC 視圖，快速尋找轉譯標記的來源，並直接在 Visual Studio 環境中使用瀏覽器工具。</span><span class="sxs-lookup"><span data-stu-id="c69fa-108">You can browse any MVC view, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> [<span data-ttu-id="c69fa-109">觀看影片</span><span class="sxs-lookup"><span data-stu-id="c69fa-109">Watch the Video</span></span>](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> <span data-ttu-id="c69fa-110">本教學課程示範如何啟用檢查模式，然後在您的 Web 專案中快速找出並編輯標記和 CSS。</span><span class="sxs-lookup"><span data-stu-id="c69fa-110">This tutorial shows how to enable Inspection Mode, and then quickly locate and edit markup and CSS within your web project.</span></span> <span data-ttu-id="c69fa-111">本教學課程使用 MVC 專案，但您也可以將 Page Inspector 用於[Web Forms](https://go.microsoft.com/?linkid=9802001)和其他 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c69fa-111">The tutorial uses an MVC Project, but you can also use Page Inspector for [Web Forms](https://go.microsoft.com/?linkid=9802001) and other ASP.NET applications.</span></span>
> 
> <span data-ttu-id="c69fa-112">本教學課程包含下列各節：</span><span class="sxs-lookup"><span data-stu-id="c69fa-112">The tutorial has the following sections:</span></span>
> 
> - [<span data-ttu-id="c69fa-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="c69fa-113">Prerequisites</span></span>](#_1_prerequisites)
> - [<span data-ttu-id="c69fa-114">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c69fa-114">Create a Web Application</span></span>](#_2_creating_a)
> - [<span data-ttu-id="c69fa-115">使用 Page Inspector 流覽至視圖</span><span class="sxs-lookup"><span data-stu-id="c69fa-115">Use Page Inspector to Browse to a View</span></span>](#_3_using_page)
> - [<span data-ttu-id="c69fa-116">啟用檢查模式</span><span class="sxs-lookup"><span data-stu-id="c69fa-116">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> - [<span data-ttu-id="c69fa-117">使用 Page Inspector 對標記進行變更</span><span class="sxs-lookup"><span data-stu-id="c69fa-117">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> - [<span data-ttu-id="c69fa-118">檢查模式和 HTML 視窗</span><span class="sxs-lookup"><span data-stu-id="c69fa-118">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> - <span data-ttu-id="c69fa-119">[[樣式] 視窗中的預覽 CSS 變更](#_7_previewing_css)</span><span class="sxs-lookup"><span data-stu-id="c69fa-119">[Preview CSS Changes in the Styles window](#_7_previewing_css)</span></span>
> - [<span data-ttu-id="c69fa-120">CSS 自動同步處理</span><span class="sxs-lookup"><span data-stu-id="c69fa-120">CSS Auto Sync</span></span>](#css_auto_sync)
> - [<span data-ttu-id="c69fa-121">使用 CSS 色彩選擇器</span><span class="sxs-lookup"><span data-stu-id="c69fa-121">Using the CSS Color Picker</span></span>](#css_color_picker)
> - [<span data-ttu-id="c69fa-122">將動態頁面元素對應至 JavaScript</span><span class="sxs-lookup"><span data-stu-id="c69fa-122">Mapping Dynamic Page Elements to JavaScript</span></span>](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="c69fa-123">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c69fa-123">Prerequisites</span></span>

- <span data-ttu-id="c69fa-124">[適用于 Web 的](https://www.microsoft.com/visualstudio/11/downloads#express-web) [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)或 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="c69fa-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="c69fa-125">若要取得最新版本的 Page Inspector，請使用[Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386)安裝適用于 .net 2.0 的 WINDOWS Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="c69fa-125">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Windows Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="c69fa-126">Page Inspector 與 Microsoft Web Developer Tools 配套。</span><span class="sxs-lookup"><span data-stu-id="c69fa-126">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="c69fa-127">最新版本是1.3。</span><span class="sxs-lookup"><span data-stu-id="c69fa-127">The latest version is 1.3.</span></span> <span data-ttu-id="c69fa-128">若要檢查您擁有哪個版本，請執行**Visual Studio，然後從 [說明**] 功能表中選取 [**關於 Microsoft Visual Studio** ]。</span><span class="sxs-lookup"><span data-stu-id="c69fa-128">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="c69fa-129">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c69fa-129">Create a Web Application</span></span>

<span data-ttu-id="c69fa-130">首先，建立您將搭配 Page Inspector 使用的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c69fa-130">First, create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="c69fa-131">在 Visual Studio 中，**選擇 [** 檔案] &gt; [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="c69fa-131">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="c69fa-132">在左側，展開 [**視覺C#效果**]，選取 [ **Web**]，然後選取 [ **ASP.NET MVC4 Web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="c69fa-132">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span>

![新增 ASP.NET MVC 應用程式](using-page-inspector-in-aspnet-mvc/_static/image2.png)

<span data-ttu-id="c69fa-134">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c69fa-134">Click **OK**.</span></span>

<span data-ttu-id="c69fa-135">在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="c69fa-135">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="c69fa-136">保留**Razor**做為預設的 view engine。</span><span class="sxs-lookup"><span data-stu-id="c69fa-136">Leave **Razor** as the default view engine.</span></span>

![新增 ASP.NET MVC 專案-網際網路應用程式](using-page-inspector-in-aspnet-mvc/_static/image4.png)

<span data-ttu-id="c69fa-138">應用程式會在**原始**檔視圖中開啟。</span><span class="sxs-lookup"><span data-stu-id="c69fa-138">The application opens in **Source** view.</span></span>

![來源視圖中的新 ASP.NET MVC 應用程式](using-page-inspector-in-aspnet-mvc/_static/image6.png)

<span data-ttu-id="c69fa-140">現在您已經有要使用的應用程式，您可以使用 Page Inspector 來檢查及修改它。</span><span class="sxs-lookup"><span data-stu-id="c69fa-140">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a><span data-ttu-id="c69fa-141">使用 Page Inspector 流覽至視圖</span><span class="sxs-lookup"><span data-stu-id="c69fa-141">Use Page Inspector to Browse to a View</span></span>

<span data-ttu-id="c69fa-142">在 Visual Studio 2012 中，您可以用滑鼠右鍵按一下專案中的任何視圖、選取  **Page Inspector 中**的 view，然後 Page Inspector 將會找出路線並顯示該頁面。</span><span class="sxs-lookup"><span data-stu-id="c69fa-142">In Visual Studio 2012, you can right-click any view in your project, select **View in Page Inspector**, and Page Inspector will figure out the route and display the page.</span></span>

<span data-ttu-id="c69fa-143">在**方案總管**中，依序展開 [ **Views** ] 資料夾和 [ **Home** ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c69fa-143">In **Solution Explorer**, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="c69fa-144">以滑鼠右鍵按一下索引. cshtml 檔案，然後選擇 [ **View in Page Inspector**]。</span><span class="sxs-lookup"><span data-stu-id="c69fa-144">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

![Page Inspector 中的 View Index. cshtml](using-page-inspector-in-aspnet-mvc/_static/image8.png)

<span data-ttu-id="c69fa-146">根據預設，Page Inspector 會停駐在 Visual Studio 環境左側的視窗中。</span><span class="sxs-lookup"><span data-stu-id="c69fa-146">By default, Page Inspector is docked as a window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="c69fa-147">如果您想要的話，可以將它停駐在別處，或停用視窗。</span><span class="sxs-lookup"><span data-stu-id="c69fa-147">If you prefer, you can dock it elsewhere, or undock the window.</span></span> <span data-ttu-id="c69fa-148">請參閱[如何：排列和停駐視窗](https://msdn.microsoft.com/library/z4y0hsax.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c69fa-148">See [How to: Arrange and Dock Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span></span>

<span data-ttu-id="c69fa-149">[Page Inspector] 視窗的上方窗格會在瀏覽器視窗中顯示目前的頁面。</span><span class="sxs-lookup"><span data-stu-id="c69fa-149">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="c69fa-150">下方窗格會顯示 HTML 標籤中的頁面，以及一些可讓您檢查頁面不同層面的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c69fa-150">The bottom pane shows the page in HTML markup, along with some tabs that let you inspect different aspects of the page.</span></span> <span data-ttu-id="c69fa-151">底部窗格類似 Internet Explorer 中的[F12 開發人員工具](https://msdn.microsoft.com/ie/aa740478)。</span><span class="sxs-lookup"><span data-stu-id="c69fa-151">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span>

![Page Inspector 中的 ASP.NET MVC 應用程式](using-page-inspector-in-aspnet-mvc/_static/image10.png)

<span data-ttu-id="c69fa-153">在本教學課程中，您將使用 [ **HTML** ] 和 [**樣式**] 索引標籤，快速流覽並對應用程式進行變更。</span><span class="sxs-lookup"><span data-stu-id="c69fa-153">In this tutorial, you will use the **HTML** and **Styles** tabs to navigate quickly and make changes to the application.</span></span>

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a><span data-ttu-id="c69fa-154">EnableInspection 模式</span><span class="sxs-lookup"><span data-stu-id="c69fa-154">EnableInspection Mode</span></span>

<span data-ttu-id="c69fa-155">若要將 Page Inspector 放入檢查模式，請按一下 [**檢查**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c69fa-155">To put Page Inspector into Inspection Mode, click the **Inspect** button.</span></span> <span data-ttu-id="c69fa-156">在檢查模式中，當您將滑鼠指標放在呈現頁面的任何部分上方時，對應的來源標記或程式碼會反白顯示。</span><span class="sxs-lookup"><span data-stu-id="c69fa-156">In Inspection Mode, when you hold the mouse pointer over any part of the rendered page, the corresponding source markup or code is highlighted.</span></span>

![切換檢查模式](using-page-inspector-in-aspnet-mvc/_static/image12.png)

<span data-ttu-id="c69fa-158">現在將您的滑鼠移到 Page Inspector 內不同的頁面部分。</span><span class="sxs-lookup"><span data-stu-id="c69fa-158">Now move your mouse over different parts of the page within Page Inspector.</span></span> <span data-ttu-id="c69fa-159">就像您一樣，滑鼠指標會變更為較大的加號，而下方的元素會反白顯示：</span><span class="sxs-lookup"><span data-stu-id="c69fa-159">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![將滑鼠停留在 div. 內容包裝函式](using-page-inspector-in-aspnet-mvc/_static/image14.png)

<span data-ttu-id="c69fa-161">當您移動滑鼠指標時，Visual Studio 會反白顯示原始檔案中對應的 Razor 語法。</span><span class="sxs-lookup"><span data-stu-id="c69fa-161">As you move the mouse pointer, Visual Studio highlights the corresponding Razor syntax in the source file.</span></span> <span data-ttu-id="c69fa-162">如果 HTML 元素來自另一個原始檔，Visual Studio 會自動開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="c69fa-162">If the HTML element comes from another source file, Visual Studio automatically opens the file.</span></span>

<span data-ttu-id="c69fa-163">在 Page Inspector 中，[ **html** ] 索引標籤會顯示從 Razor 語法產生的 html。</span><span class="sxs-lookup"><span data-stu-id="c69fa-163">In Page Inspector, the **HTML** tab shows the HTML that was generated from the Razor syntax.</span></span> <span data-ttu-id="c69fa-164">當您移動滑鼠指標時，HTML 元素會反白顯示。</span><span class="sxs-lookup"><span data-stu-id="c69fa-164">As you move the mouse pointer, the HTML elements are highlighted.</span></span> <span data-ttu-id="c69fa-165">[**樣式**] 索引標籤會顯示元素的 CSS 規則。</span><span class="sxs-lookup"><span data-stu-id="c69fa-165">The **Styles** tab shows the CSS rules for the element.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="c69fa-166">使用 Page Inspector 對標記進行變更</span><span class="sxs-lookup"><span data-stu-id="c69fa-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="c69fa-167">Page Inspector 可讓您尋找其位置可能不明顯的標記。</span><span class="sxs-lookup"><span data-stu-id="c69fa-167">Page Inspector lets you find markup whose location might not be obvious.</span></span> <span data-ttu-id="c69fa-168">然後您可以修改標記，並查看所產生的變更。</span><span class="sxs-lookup"><span data-stu-id="c69fa-168">Then you can modify the markup and see the resulting changes.</span></span>

<span data-ttu-id="c69fa-169">若要查看此功能，請按一下 [**檢查**]，然後在 [Page Inspector] 視窗中的頁面底部流覽。</span><span class="sxs-lookup"><span data-stu-id="c69fa-169">To see this, click **Inspect** and then scroll to the bottom of the page in the Page Inspector window.</span></span>

<span data-ttu-id="c69fa-170">當您將滑鼠指標移至頁尾區域時，Page Inspector 會開啟 \_配置 cshtml 檔案，並反白顯示您所選取之版面配置頁的區段。</span><span class="sxs-lookup"><span data-stu-id="c69fa-170">When you move the mouse pointer into the footer area, Page Inspector opens the \_Layout.cshtml file and highlights the section of the layout page that you have selected.</span></span> <span data-ttu-id="c69fa-171">如您所見，頁尾是定義在版面配置檔案中，而不是在 view 本身。</span><span class="sxs-lookup"><span data-stu-id="c69fa-171">As you can see, the footer are is defined in the layout file, and not the view itself.</span></span>

![頁尾](using-page-inspector-in-aspnet-mvc/_static/image16.png)

<span data-ttu-id="c69fa-173">現在，將滑鼠指標移到具有著作權<a id="a"></a>注意事項的那一行。</span><span class="sxs-lookup"><span data-stu-id="c69fa-173">Now move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span> <span data-ttu-id="c69fa-174">在 [\_配置. cshtml] 頁面中，會反白顯示對應的一行。</span><span class="sxs-lookup"><span data-stu-id="c69fa-174">In the \_Layout.cshtml page, the corresponding line is highlighted.</span></span>

![已反白顯示頁尾的著作權線](using-page-inspector-in-aspnet-mvc/_static/image18.png)

<span data-ttu-id="c69fa-176">將一些文字新增至 \_配置. cshtml 檔案中的行尾。</span><span class="sxs-lookup"><span data-stu-id="c69fa-176">Add some text to the end of the line in the \_Layout.cshtml file.</span></span>

<span data-ttu-id="c69fa-177">&lt;p&gt;&amp;複製;@DateTime.Now.Year-我的 ASP.NET MVC 應用程式 Rocks！&lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="c69fa-177">&lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET MVC Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="c69fa-178">現在，按下 Ctrl + Alt + Enter，或按一下更新列以在 [Page Inspector 瀏覽器] 視窗中查看結果。</span><span class="sxs-lookup"><span data-stu-id="c69fa-178">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![我的 ASP.NET 應用程式 Rocks！](using-page-inspector-in-aspnet-mvc/_static/image20.png)

<span data-ttu-id="c69fa-180">您可能認為頁尾中定義了頁尾，但它是在 \_配置. cshtml 中，而 Page Inspector 為您找到它。</span><span class="sxs-lookup"><span data-stu-id="c69fa-180">You might have thought that the footer defined in Index.cshtml, but it turned out to be in the \_Layout.cshtml, and Page Inspector found it for you.</span></span>

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="c69fa-181">檢查模式和 HTML 視窗</span><span class="sxs-lookup"><span data-stu-id="c69fa-181">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="c69fa-182">接下來，您將快速查看 [HTML] 視窗，以及它如何為您對應元素。</span><span class="sxs-lookup"><span data-stu-id="c69fa-182">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="c69fa-183">按一下 [**檢查**]，將 Page Inspector 放在檢查模式中。</span><span class="sxs-lookup"><span data-stu-id="c69fa-183">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="c69fa-184">按一下頁面的上半部，此處會顯示「您的標誌」。</span><span class="sxs-lookup"><span data-stu-id="c69fa-184">Click the top part of the page that says "Your logo here".</span></span> <span data-ttu-id="c69fa-185">您正以更詳細的方式檢查特定元素，因此當您移動滑鼠指標時，瀏覽器視窗中的顯示不會再變更。</span><span class="sxs-lookup"><span data-stu-id="c69fa-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="c69fa-186">現在，將滑鼠指標移至**HTML**視窗。</span><span class="sxs-lookup"><span data-stu-id="c69fa-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="c69fa-187">當您移動滑鼠指標時，Page Inspector 會在**HTML**視窗中概述元素，並在瀏覽器視窗中反白顯示對應的元素。</span><span class="sxs-lookup"><span data-stu-id="c69fa-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML 視窗](using-page-inspector-in-aspnet-mvc/_static/image22.png)

<span data-ttu-id="c69fa-189">如同之前一樣，Page Inspector 會在暫存索引標籤中開啟 \_的配置. cshtml 檔案。按一下 [\_配置] [暫存] 索引標籤，在 &lt;標頭&gt; 區段中會反白顯示對應的標記：</span><span class="sxs-lookup"><span data-stu-id="c69fa-189">As before, Page Inspector opens the \_Layout.cshtml file for you in a temporary tab. Click the \_Layout.cshtml temporary tab, and the corresponding markup will be highlighted in the &lt;header&gt; section for you:</span></span>

![反白顯示的標記](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="c69fa-191">[樣式] 視窗中的預覽 CSS 變更</span><span class="sxs-lookup"><span data-stu-id="c69fa-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="c69fa-192">接下來，您將使用 [Page Inspector**樣式**] 視窗，預覽 CSS 的變更。</span><span class="sxs-lookup"><span data-stu-id="c69fa-192">Next, you will use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="c69fa-193">按一下 [**檢查**]，將 Page Inspector 放在檢查模式中。</span><span class="sxs-lookup"><span data-stu-id="c69fa-193">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="c69fa-194">在 [Page Inspector 瀏覽器] 視窗中，將滑鼠指標移到 [首頁] 區段上，直到 [ **div. content-包裝函式**] 標籤出現為止。</span><span class="sxs-lookup"><span data-stu-id="c69fa-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![將滑鼠停留在 div. 內容包裝函式](using-page-inspector-in-aspnet-mvc/_static/image26.png)

<span data-ttu-id="c69fa-196">在 [div] [內容包裝函式] 區段中按一下一次，然後將滑鼠指標移至 [**樣式**] 視窗。</span><span class="sxs-lookup"><span data-stu-id="c69fa-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="c69fa-197">[**樣式**] 視窗會顯示此元素的所有 CSS 規則。</span><span class="sxs-lookup"><span data-stu-id="c69fa-197">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="c69fa-198">向下滾動以尋找 [精選] [內容包裝函式類別] 選取器。</span><span class="sxs-lookup"><span data-stu-id="c69fa-198">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="c69fa-199">現在清除 [背景色彩] 屬性的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="c69fa-199">Now clear the checkbox for the background-color property.</span></span>

![清除背景色彩](using-page-inspector-in-aspnet-mvc/_static/image28.png)

<span data-ttu-id="c69fa-201">請注意，[Page Inspector 瀏覽器] 視窗中的變更預覽會立即進行。</span><span class="sxs-lookup"><span data-stu-id="c69fa-201">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="c69fa-202">再次選取此核取方塊，然後按兩下屬性值並將它變更為紅色。</span><span class="sxs-lookup"><span data-stu-id="c69fa-202">Select the checkbox again, then double-click the property value and change it to red.</span></span> <span data-ttu-id="c69fa-203">變更會立即顯示：</span><span class="sxs-lookup"><span data-stu-id="c69fa-203">The change shows immediately:</span></span>

![紅色背景色彩](using-page-inspector-in-aspnet-mvc/_static/image30.png)

<span data-ttu-id="c69fa-205">[**樣式**] 視窗可讓您在認可樣式表單本身的變更之前，輕鬆地測試和預覽 CSS 變更。</span><span class="sxs-lookup"><span data-stu-id="c69fa-205">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="c69fa-206">CSS 自動同步處理</span><span class="sxs-lookup"><span data-stu-id="c69fa-206">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="c69fa-207">這項功能需要1.3 版的 Page Inspector。</span><span class="sxs-lookup"><span data-stu-id="c69fa-207">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="c69fa-208">CSS 自動同步處理功能可讓您直接編輯 CSS 檔案，並在 Page Inspector 瀏覽器中立即查看變更。</span><span class="sxs-lookup"><span data-stu-id="c69fa-208">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="c69fa-209">按一下 [**檢查**]，將 Page Inspector 放在檢查模式中。</span><span class="sxs-lookup"><span data-stu-id="c69fa-209">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="c69fa-210">在 Page Inspector 瀏覽器中，將滑鼠指標移到 [首頁] 區段上，直到 [ **div. content-包裝函式**] 標籤出現為止。</span><span class="sxs-lookup"><span data-stu-id="c69fa-210">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="c69fa-211">按一下 [一次] 以選取此元素。</span><span class="sxs-lookup"><span data-stu-id="c69fa-211">Click once to select this element.</span></span>

<span data-ttu-id="c69fa-212">[**樣式**] 視窗會顯示此元素的所有 CSS 規則。</span><span class="sxs-lookup"><span data-stu-id="c69fa-212">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="c69fa-213">向下滾動以尋找 [精選] [內容包裝函式類別] 選取器。</span><span class="sxs-lookup"><span data-stu-id="c69fa-213">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="c69fa-214">按一下 [. 功能內容-包裝函式]。</span><span class="sxs-lookup"><span data-stu-id="c69fa-214">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="c69fa-215">Page Inspector 會開啟定義此樣式（.css）的 CSS 檔案，並反白顯示對應的 CSS 樣式。</span><span class="sxs-lookup"><span data-stu-id="c69fa-215">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

<span data-ttu-id="c69fa-216">現在將 `background-color` 的值變更為「紅色」。</span><span class="sxs-lookup"><span data-stu-id="c69fa-216">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="c69fa-217">變更會立即出現在 Page Inspector 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="c69fa-217">The change appears immediately in the Page Inspector browser.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a><span data-ttu-id="c69fa-218">使用 CSS 色彩選擇器</span><span class="sxs-lookup"><span data-stu-id="c69fa-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="c69fa-219">Visual Studio 2012 中的 CSS 編輯器具有色彩選擇器，可讓您輕鬆地選擇和插入色彩。</span><span class="sxs-lookup"><span data-stu-id="c69fa-219">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="c69fa-220">色彩選擇器包含色彩的標準調色板、支援標準色彩名稱、雜湊碼、RGB、RGBA、HSL 和 HSLA 色彩，並維護您最近在檔中使用的色彩清單。</span><span class="sxs-lookup"><span data-stu-id="c69fa-220">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="c69fa-221">在上一節中，您已變更 `background-color` 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="c69fa-221">In the previous section, you changed the value of the `background-color` property.</span></span> <span data-ttu-id="c69fa-222">若要叫用色彩選擇器，請將插入點放在屬性名稱後面，然後輸入 **#** 或**rgb （** ）。</span><span class="sxs-lookup"><span data-stu-id="c69fa-222">To invoke the color picker, place the insertion point after the property name and type **#** or **rgb(**.</span></span>

![CSS 色彩選擇器列](using-page-inspector-in-aspnet-mvc/_static/image36.png)

<span data-ttu-id="c69fa-224">按一下色彩來選取它，或按向下鍵，然後使用向左鍵和向右鍵來流覽色彩。</span><span class="sxs-lookup"><span data-stu-id="c69fa-224">Click on a color to select it, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="c69fa-225">當您造訪色彩時，會預覽對應的十六進位值：</span><span class="sxs-lookup"><span data-stu-id="c69fa-225">When you visit a color, the corresponding hex value is previewed:</span></span>

![預覽的背景色彩屬性值](using-page-inspector-in-aspnet-mvc/_static/image38.png)

<span data-ttu-id="c69fa-227">如果色軸沒有您想要的色彩，您可以使用色彩選擇器快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="c69fa-227">If the color bar doesn't have the exact color you want, you can use the color picker pop-down.</span></span> <span data-ttu-id="c69fa-228">若要開啟它，請按一下色軸右端的雙燕號，或在鍵盤上按一次向下箭號或按兩次。</span><span class="sxs-lookup"><span data-stu-id="c69fa-228">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS 色彩選擇器快顯視窗](using-page-inspector-in-aspnet-mvc/_static/image40.png)

<span data-ttu-id="c69fa-230">按一下右側分隔號的色彩。</span><span class="sxs-lookup"><span data-stu-id="c69fa-230">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="c69fa-231">這會在主視窗中顯示該色彩的漸層。</span><span class="sxs-lookup"><span data-stu-id="c69fa-231">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="c69fa-232">按 Enter 鍵直接從分隔號中選擇色彩，或按一下主視窗中的任何點，選擇較高的精確度。</span><span class="sxs-lookup"><span data-stu-id="c69fa-232">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="c69fa-233">如果您的電腦畫面上有您想要使用的色彩（不一定要在 Visual Studio 使用者介面內），您可以使用右下方的 [滴管] 工具來捕捉其值。</span><span class="sxs-lookup"><span data-stu-id="c69fa-233">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="c69fa-234">您也可以移動色彩選擇器底部的滑杆來變更色彩的不透明度。</span><span class="sxs-lookup"><span data-stu-id="c69fa-234">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="c69fa-235">這麼做會將色彩值變更為 RGBA 值，因為 RGBA 格式可以代表不透明度。</span><span class="sxs-lookup"><span data-stu-id="c69fa-235">Doing so changes color values to RGBA values, because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="c69fa-236">選擇色彩之後，請按 Enter 鍵，然後輸入分號來完成*網站 .css*檔案中的背景色彩專案。</span><span class="sxs-lookup"><span data-stu-id="c69fa-236">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="c69fa-237">Page Inspector 更新列</span><span class="sxs-lookup"><span data-stu-id="c69fa-237">The Page Inspector Update Bar</span></span>

<span data-ttu-id="c69fa-238">Page Inspector 會立即偵測到*網站 .css*檔案的變更，並在更新列中顯示警示。</span><span class="sxs-lookup"><span data-stu-id="c69fa-238">Page Inspector immediately detects the change to the *Site.css* file and displays an alert in an update bar.</span></span>

![更新列](using-page-inspector-in-aspnet-mvc/_static/image42.png)

<span data-ttu-id="c69fa-240">若要儲存所有檔案並重新整理 Page Inspector 的瀏覽器，請按 Ctrl + Alt + Enter，或按一下更新列。</span><span class="sxs-lookup"><span data-stu-id="c69fa-240">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="c69fa-241">醒目提示色彩中的變更會出現在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="c69fa-241">The change in the highlight color appears in the browser.</span></span>

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a><span data-ttu-id="c69fa-242">將動態頁面元素對應至 JavaScript</span><span class="sxs-lookup"><span data-stu-id="c69fa-242">Mapping Dynamic Page Elements to JavaScript</span></span>

<span data-ttu-id="c69fa-243">在新式 web 應用程式中，頁面中的元素通常是使用 JavaScript 動態產生的。</span><span class="sxs-lookup"><span data-stu-id="c69fa-243">In modern web applications, elements in the page are often generated dynamically with JavaScript.</span></span> <span data-ttu-id="c69fa-244">這表示沒有對應至這些頁面元素的靜態標記（HTML 或 Razor）。</span><span class="sxs-lookup"><span data-stu-id="c69fa-244">That means there is no static markup (either HTML or Razor) that corresponds to these page elements.</span></span>

<span data-ttu-id="c69fa-245">使用1.3 版時，Page Inspector 現在可以將已動態新增至頁面的專案對應回相對應的 JavaScript 程式碼。</span><span class="sxs-lookup"><span data-stu-id="c69fa-245">With version 1.3, Page Inspector can now map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span> <span data-ttu-id="c69fa-246">為了示範這項功能，我們將使用[單一頁面應用程式（SPA）範本](../../../single-page-application/overview/introduction/knockoutjs-template.md)。</span><span class="sxs-lookup"><span data-stu-id="c69fa-246">To demonstrate this feature, we'll use the [Single Page Application (SPA) template](../../../single-page-application/overview/introduction/knockoutjs-template.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c69fa-247">SPA 範本需要[ASP.NET 和 Web 工具 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650)更新。</span><span class="sxs-lookup"><span data-stu-id="c69fa-247">The SPA template requires the [ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) update.</span></span>

<span data-ttu-id="c69fa-248">在 Visual Studio 中，**選擇 [** 檔案] &gt; [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="c69fa-248">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="c69fa-249">在左側，展開 [**視覺C#效果**]，選取 [ **Web**]，然後選取 [ **ASP.NET MVC4 Web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="c69fa-249">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span> <span data-ttu-id="c69fa-250">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c69fa-250">Click **OK**.</span></span>

<span data-ttu-id="c69fa-251">在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**單一頁面應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="c69fa-251">In the **New ASP.NET MVC 4 Project** dialog, select **Single Page Application**.</span></span>

<span data-ttu-id="c69fa-252">在方案總管中，依序展開 [ **Views** ] 資料夾和 [ **Home** ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c69fa-252">In Solution Explorer, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="c69fa-253">以滑鼠右鍵按一下索引. cshtml 檔案，然後選擇 [ **View in Page Inspector**]。</span><span class="sxs-lookup"><span data-stu-id="c69fa-253">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

<span data-ttu-id="c69fa-254">Page Inspector 瀏覽器中顯示的第一件事是登入頁面。</span><span class="sxs-lookup"><span data-stu-id="c69fa-254">The first thing that is displayed in the Page Inspector browser is a login page.</span></span> <span data-ttu-id="c69fa-255">按一下 [註冊]，然後建立使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="c69fa-255">Click "Sign Up" and create a user name and password.</span></span> <span data-ttu-id="c69fa-256">註冊之後，應用程式就會將您登入，並使用一些範例專案建立待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="c69fa-256">Once you sign up, the application logs you in and creates a to-do list with some sample items.</span></span>

<span data-ttu-id="c69fa-257">按一下 [**檢查**]，將 Page Inspector 放在檢查模式中。</span><span class="sxs-lookup"><span data-stu-id="c69fa-257">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span> <span data-ttu-id="c69fa-258">在 Page Inspector 瀏覽器中，按一下其中一個待辦事項專案。</span><span class="sxs-lookup"><span data-stu-id="c69fa-258">In the Page Inspector browser, click on one of the to-do items.</span></span> <span data-ttu-id="c69fa-259">請注意，不會以藍色反白顯示專案，而是以橙色反白顯示元素，並在專案名稱旁邊加上 "JS"。</span><span class="sxs-lookup"><span data-stu-id="c69fa-259">Notice that instead of being highlighted in blue, the element is highlighted in orange, with "JS" next to the element name.</span></span> <span data-ttu-id="c69fa-260">這表示已透過腳本動態建立元素。</span><span class="sxs-lookup"><span data-stu-id="c69fa-260">This indicates that the element was created dynamically through script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

<span data-ttu-id="c69fa-261">此外，[**呼叫堆疊**] 索引標籤上會顯示橙色底線。這表示 [**呼叫堆疊**] 窗格具有元素的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c69fa-261">In addition, an orange underline appears on the **Call Stack** tab. This indicates that the **Call Stack** pane has more information about the element.</span></span>

<span data-ttu-id="c69fa-262">按一下 [**呼叫堆疊**] 索引標籤。[**呼叫堆疊**] 窗格會顯示建立元素之 JavaScript 呼叫的呼叫堆疊。</span><span class="sxs-lookup"><span data-stu-id="c69fa-262">Click on the **Call Stack** tab. The **Call Stack** pane shows the call stack for the JavaScript call that created the element.</span></span> <span data-ttu-id="c69fa-263">對外部程式庫（例如 jQuery）的呼叫會折迭，讓您可以輕鬆地查看應用程式腳本的呼叫。</span><span class="sxs-lookup"><span data-stu-id="c69fa-263">Calls to external libraries such as jQuery are collapsed, so that you can easily see the calls to your application script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

<span data-ttu-id="c69fa-264">若要查看完整堆疊（包括對外部程式庫的呼叫），您可以展開標示為「外部程式庫」的節點：</span><span class="sxs-lookup"><span data-stu-id="c69fa-264">To see the full stack, including calls to external libraries, you can expand the nodes labeled "External Libraries":</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

<span data-ttu-id="c69fa-265">如果您按一下呼叫堆疊中的專案，Visual Studio 會開啟程式碼檔案，並反白顯示對應的腳本。</span><span class="sxs-lookup"><span data-stu-id="c69fa-265">If you click an item in the call stack, Visual Studio opens the code file and highlights the corresponding script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a><span data-ttu-id="c69fa-266">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c69fa-266">See Also</span></span>

<span data-ttu-id="c69fa-267">[使用 Visual Studio ASP.NET MVC 4 的簡介](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)（ASP.net 網站）</span><span class="sxs-lookup"><span data-stu-id="c69fa-267">[Intro to ASP.NET MVC 4 with Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net website)</span></span>

<span data-ttu-id="c69fa-268">[Page Inspector 簡介](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/)（Channel 9 影片）</span><span class="sxs-lookup"><span data-stu-id="c69fa-268">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 video)</span></span>

<span data-ttu-id="c69fa-269">[Page Inspector 錯誤訊息](https://go.microsoft.com/?linkid=9813062)（MSDN）</span><span class="sxs-lookup"><span data-stu-id="c69fa-269">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
