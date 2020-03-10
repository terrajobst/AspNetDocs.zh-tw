---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: 在 ASP.NET Web Forms 中使用適用于 Visual Studio 2012 的 Page Inspector |Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 的 Page Inspector 是具有整合式瀏覽器的 網頁程式開發工具。 選取整合式瀏覽器中的任何元素，然後 Page Inspector 。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: c165bbea505b4cb8eae1312cdd587f4ed36541a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575919"
---
# <a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a><span data-ttu-id="a87ba-104">在 ASP.NET Web Forms 中使用 Page Inspector for Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="a87ba-104">Using Page Inspector for Visual Studio 2012 in ASP.NET Web Forms</span></span>

<span data-ttu-id="a87ba-105">依 Tim Ammann</span><span class="sxs-lookup"><span data-stu-id="a87ba-105">by Tim Ammann</span></span>

> <span data-ttu-id="a87ba-106">Visual Studio 2012 的 Page Inspector 是具有整合式瀏覽器的 網頁程式開發工具。</span><span class="sxs-lookup"><span data-stu-id="a87ba-106">Page Inspector for Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="a87ba-107">選取整合式瀏覽器中的任何元素，Page Inspector 立即反白顯示專案的來源和 CSS。</span><span class="sxs-lookup"><span data-stu-id="a87ba-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="a87ba-108">您可以流覽應用程式中的任何頁面，快速尋找轉譯標記的來源，並直接在 Visual Studio 環境中使用瀏覽器工具。</span><span class="sxs-lookup"><span data-stu-id="a87ba-108">You can browse any page in your application, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> <span data-ttu-id="a87ba-109">本教學課程示範如何啟用檢查模式，然後在您的 Web 專案中快速找出並編輯 CSS 規則和文字。</span><span class="sxs-lookup"><span data-stu-id="a87ba-109">This tutorial shows how to enable Inspection Mode and then quickly locate and edit CSS rules and text within your web project.</span></span> <span data-ttu-id="a87ba-110">本教學課程使用 Web Forms 應用程式專案，但您也可以使用網站專案和[MVC](https://go.microsoft.com/?linkid=9802002)應用程式的 Page Inspector。</span><span class="sxs-lookup"><span data-stu-id="a87ba-110">The tutorial uses a Web Forms Application Project, but you can also use Page Inspector for Web Site projects and [MVC](https://go.microsoft.com/?linkid=9802002) applications.</span></span>
> 
> <span data-ttu-id="a87ba-111">本教學課程包含下列各節：</span><span class="sxs-lookup"><span data-stu-id="a87ba-111">The tutorial has the following sections:</span></span>
> 
> [<span data-ttu-id="a87ba-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="a87ba-112">Prerequisites</span></span>](#_1_prerequisites)
> 
> [<span data-ttu-id="a87ba-113">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a87ba-113">Create a Web Application</span></span>](#_2_creating_a)
> 
> [<span data-ttu-id="a87ba-114">使用 Page Inspector 來查看應用程式</span><span class="sxs-lookup"><span data-stu-id="a87ba-114">Use Page Inspector to View the Application</span></span>](#_3_using_page)
> 
> [<span data-ttu-id="a87ba-115">啟用檢查模式</span><span class="sxs-lookup"><span data-stu-id="a87ba-115">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> 
> [<span data-ttu-id="a87ba-116">使用 Page Inspector 對標記進行變更</span><span class="sxs-lookup"><span data-stu-id="a87ba-116">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> 
> [<span data-ttu-id="a87ba-117">檢查模式和 HTML 視窗</span><span class="sxs-lookup"><span data-stu-id="a87ba-117">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> 
> <span data-ttu-id="a87ba-118">[[樣式] 視窗中的預覽 CSS 變更](#_7_previewing_css)</span><span class="sxs-lookup"><span data-stu-id="a87ba-118">[Preview CSS Changes in the Styles Window](#_7_previewing_css)</span></span>
> 
> [<span data-ttu-id="a87ba-119">CSS 自動同步處理</span><span class="sxs-lookup"><span data-stu-id="a87ba-119">CSS Auto Sync</span></span>](#css_auto_sync)
> 
> [<span data-ttu-id="a87ba-120">使用 CSS 色彩選擇器</span><span class="sxs-lookup"><span data-stu-id="a87ba-120">Using the CSS Color Picker</span></span>](#css_color_picker)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="a87ba-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a87ba-121">Prerequisites</span></span>

- <span data-ttu-id="a87ba-122">[適用于 Web 的](https://www.microsoft.com/visualstudio/11/downloads#express-web) [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)或 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="a87ba-122">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="a87ba-123">若要取得最新版本的 Page Inspector，請使用[Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386)來安裝 Azure SDK for .net 2.0。</span><span class="sxs-lookup"><span data-stu-id="a87ba-123">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="a87ba-124">Page Inspector 與 Microsoft Web Developer Tools 配套。</span><span class="sxs-lookup"><span data-stu-id="a87ba-124">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="a87ba-125">最新版本是1.3。</span><span class="sxs-lookup"><span data-stu-id="a87ba-125">The latest version is 1.3.</span></span> <span data-ttu-id="a87ba-126">若要檢查您擁有哪個版本，請執行**Visual Studio，然後從 [說明**] 功能表中選取 [**關於 Microsoft Visual Studio** ]。</span><span class="sxs-lookup"><span data-stu-id="a87ba-126">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="a87ba-127">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a87ba-127">Create a Web Application</span></span>

<span data-ttu-id="a87ba-128">首先，您將建立要搭配 Page Inspector 使用的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a87ba-128">First, you will create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="a87ba-129">在 Visual Studio 中，**選擇 [** 檔案] &gt; [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="a87ba-129">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="a87ba-130">在左側，展開 [**視覺C#效果**]，選取 [ **Web**]，然後選取 [ **ASP.NET Web Forms 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="a87ba-130">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET Web Forms Application**.</span></span>

![新的 Web Forms 應用程式](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

<span data-ttu-id="a87ba-132">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a87ba-132">Click **OK**.</span></span>

<span data-ttu-id="a87ba-133">應用程式會在**原始**檔視圖中開啟。</span><span class="sxs-lookup"><span data-stu-id="a87ba-133">The application opens in **Source** view.</span></span>

![來源視圖中的新 Web Forms 應用程式](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

<span data-ttu-id="a87ba-135">現在您已經有要使用的應用程式，您可以使用 Page Inspector 來檢查及修改它。</span><span class="sxs-lookup"><span data-stu-id="a87ba-135">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a><span data-ttu-id="a87ba-136">使用 Page Inspector 來查看應用程式</span><span class="sxs-lookup"><span data-stu-id="a87ba-136">Use Page Inspector to View the Application</span></span>

<span data-ttu-id="a87ba-137">接下來，您將使用 Page Inspector 來觀看應用程式。</span><span class="sxs-lookup"><span data-stu-id="a87ba-137">Next, you will view the application with Page Inspector.</span></span> <span data-ttu-id="a87ba-138">在**方案總管**中，以滑鼠右鍵按一下專案，然後選擇 [**在 Page Inspector 中顯示**]。</span><span class="sxs-lookup"><span data-stu-id="a87ba-138">In **Solution Explorer**, right click the project, and then choose **View in Page Inspector**.</span></span>

![在 Page Inspector 中檢視](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

<span data-ttu-id="a87ba-140">根據預設，當 Page Inspector 第一次啟動時，它會停駐在 Visual Studio 環境左側的縮小視窗。</span><span class="sxs-lookup"><span data-stu-id="a87ba-140">By default, when Page Inspector launches for the first time, it is docked as a narrow window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="a87ba-141">將它停駐在左側，並將它設為您慣用的寬度，或將它固定在頂端、底部或右邊的其中一個工具區域中：</span><span class="sxs-lookup"><span data-stu-id="a87ba-141">Leave it docked on the left side and set it to a width that is comfortable for you, or dock it in one of the tool areas on the top, bottom, or right:</span></span>

![Page Inspector 銜接位置](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

<span data-ttu-id="a87ba-143">如果您停用 [Page Inspector] 視窗，則可以將它放在 Visual Studio 之外，甚至是在第二個監視器上（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="a87ba-143">If you undock the Page Inspector window, you can place it outside Visual Studio, or even on a second monitor if you have one.</span></span> <span data-ttu-id="a87ba-144">不過，若要在 Page Inspector 視窗停駐時，Page Inspector 和 Visual Studio 之間進行 ALT + TAB，請移至 **工具**&gt;**選項** &gt;**環境**&gt; 索引標籤**和 視窗**，然後在 索引標籤 底下，清除名為 **浮動工具視窗** 的核取方塊： 一律保留</span><span class="sxs-lookup"><span data-stu-id="a87ba-144">However, in order to ALT+TAB between Page Inspector and Visual Studio when the Page Inspector window is undocked, go to **Tools** &gt; **Options** &gt; **Environment** &gt; **Tabs and Windows**, and under **Tab Well**, clear the check box called **Floating tool windows always stay on top of the main window**:</span></span>

![清除 [浮動工具視窗] 核取方塊，以在 Visual Studio 和停駐的 Page Inspector 視窗之間進行 ALT + TAB](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

<span data-ttu-id="a87ba-146">[Page Inspector] 視窗的上方窗格會在瀏覽器視窗中顯示目前的頁面。</span><span class="sxs-lookup"><span data-stu-id="a87ba-146">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="a87ba-147">底部窗格會在左側顯示 HTML 標籤中的頁面，以及右邊的一些索引標籤，可讓您檢查頁面的不同層面。</span><span class="sxs-lookup"><span data-stu-id="a87ba-147">The bottom pane shows the page in HTML markup on the left, and some tabs on the right that let you inspect different aspects of the page.</span></span> <span data-ttu-id="a87ba-148">底部窗格類似 Internet Explorer 中的[F12 開發人員工具](https://msdn.microsoft.com/ie/aa740478)。</span><span class="sxs-lookup"><span data-stu-id="a87ba-148">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span> <span data-ttu-id="a87ba-149">（不過，與開發人員工具不同的是，您可以直接在 Visual Studio 中使用 Page Inspector）。</span><span class="sxs-lookup"><span data-stu-id="a87ba-149">(However, unlike the developer tools, you can use Page Inspector right within Visual Studio.)</span></span>

![Page Inspector](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

<span data-ttu-id="a87ba-151">在本教學課程中，您將使用 [Page Inspector 瀏覽器] 窗格，以及 [ **HTML** ] 和 [**樣式**] 索引標籤，協助您快速流覽並變更應用程式。</span><span class="sxs-lookup"><span data-stu-id="a87ba-151">In this tutorial, you will use the Page Inspector browser pane, and the **HTML** and **Styles** tabs to help you rapidly navigate and make changes to the application.</span></span>

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a><span data-ttu-id="a87ba-152">啟用檢查模式</span><span class="sxs-lookup"><span data-stu-id="a87ba-152">Enable Inspection Mode</span></span>

<span data-ttu-id="a87ba-153">接下來，您會看到 Page Inspector 的檢查模式運作方式。</span><span class="sxs-lookup"><span data-stu-id="a87ba-153">Next, you will see how Page Inspector's Inspection Mode works.</span></span> <span data-ttu-id="a87ba-154">在 [Page Inspector] 視窗中，按一下 [**檢查**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a87ba-154">In the Page Inspector window, click the **Inspect** button.</span></span>

![檢查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

<span data-ttu-id="a87ba-156">若要查看作用中的檢查模式，請將滑鼠移至 [Page Inspector 瀏覽器] 視窗中頁面的不同部分。</span><span class="sxs-lookup"><span data-stu-id="a87ba-156">To see inspection mode in action, move your mouse over different parts of the page within the Page Inspector browser window.</span></span> <span data-ttu-id="a87ba-157">就像您一樣，滑鼠指標會變更為較大的加號，而下方的元素會反白顯示：</span><span class="sxs-lookup"><span data-stu-id="a87ba-157">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![將滑鼠停留在 div. 內容包裝函式](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

<span data-ttu-id="a87ba-159">當您移動滑鼠指標時，請注意</span><span class="sxs-lookup"><span data-stu-id="a87ba-159">As you move the mouse pointer, note that</span></span>

- <span data-ttu-id="a87ba-160">**來源**視圖中的內容會變更，以顯示與頁面上所選項目對應的標記。</span><span class="sxs-lookup"><span data-stu-id="a87ba-160">The content in **Source** view changes to show the markup corresponding to the selected element on the page.</span></span> <span data-ttu-id="a87ba-161">相關的標記會反白顯示。</span><span class="sxs-lookup"><span data-stu-id="a87ba-161">The relevant markup is highlighted.</span></span> <span data-ttu-id="a87ba-162">如果來源位於另一個檔案中，則會在原始檔中開啟該檔案，並反白顯示相關的標記。</span><span class="sxs-lookup"><span data-stu-id="a87ba-162">If the source is in another file, that file is opened in Source view with the relevant markup highlighted.</span></span>

- <span data-ttu-id="a87ba-163">在 Page Inspector 的 [ **HTML** ] 索引標籤中顯示的標記也會變更，以對應至頁面上所選取的元素。</span><span class="sxs-lookup"><span data-stu-id="a87ba-163">The markup displayed in the **HTML** tab in Page Inspector also changes to correspond to the selected element on the page.</span></span> <span data-ttu-id="a87ba-164">在 [ **HTML** ] 索引標籤中，會列出相關的標記。</span><span class="sxs-lookup"><span data-stu-id="a87ba-164">In the **HTML** tab, the relevant markup is outlined.</span></span>

- <span data-ttu-id="a87ba-165">[**樣式**] 索引標籤會顯示與目前選取專案相關的 CSS 規則。</span><span class="sxs-lookup"><span data-stu-id="a87ba-165">The **Styles** tab shows the CSS rules relevant to the current selection.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="a87ba-166">使用 Page Inspector 對標記進行變更</span><span class="sxs-lookup"><span data-stu-id="a87ba-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="a87ba-167">現在您將瞭解如何使用 Page Inspector 來尋找和變更位置可能不會立即明顯的標記或文字。</span><span class="sxs-lookup"><span data-stu-id="a87ba-167">Now you will see how you can use Page Inspector to find and make changes to markup or text whose location might not be immediately obvious.</span></span>

<span data-ttu-id="a87ba-168">將 Page Inspector 放在檢查模式中，然後在首頁的底部進行滾動。</span><span class="sxs-lookup"><span data-stu-id="a87ba-168">Put Page Inspector in Inspection Mode and then scroll to the bottom of the home page.</span></span>

<span data-ttu-id="a87ba-169">一旦您輸入頁尾區域，Page Inspector 會在 [**來源**視圖] 中，于 [其他] 索引標籤右邊的暫時索引標籤中開啟 [*網站*] 設定檔案，並反白顯示您所選取之主版頁面的區段。</span><span class="sxs-lookup"><span data-stu-id="a87ba-169">As soon as you enter the footer area, Page Inspector opens the *Site.Master* layout file in **Source** view in a temporary tab to the right of the other tabs and highlights the section of the master page that you have selected.</span></span> <span data-ttu-id="a87ba-170">這會向您示範 Page Inspector 如何在頁面上尋找和顯示內容，而這可能實際上來自于您原本開啟的檔案。</span><span class="sxs-lookup"><span data-stu-id="a87ba-170">This shows you how Page Inspector can find and display content on a page that might actually come from a different file than the one you originally opened.</span></span>

![檢查模式中的頁尾醒目提示](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

<span data-ttu-id="a87ba-172">在 [Page Inspector 瀏覽器] 視窗中，將滑鼠指標移到具有著作權<a id="a"></a>注意事項的那一行。</span><span class="sxs-lookup"><span data-stu-id="a87ba-172">In the Page Inspector browser window, move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span>

<span data-ttu-id="a87ba-173">在 [*網站*] 頁面中，會反白顯示對應的一行。</span><span class="sxs-lookup"><span data-stu-id="a87ba-173">In the *Site.Master* page, the corresponding line is highlighted.</span></span>

![已反白顯示頁尾的著作權線](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

<span data-ttu-id="a87ba-175">將一些文字加入至*網站*結尾檔案中的行尾。</span><span class="sxs-lookup"><span data-stu-id="a87ba-175">Add some text to the end of the line in the *Site.Master* file.</span></span>

<span data-ttu-id="a87ba-176">&lt;p&gt;&amp;複製;&lt;%： DateTime。現在. 年%&gt;-我的 ASP.NET 應用程式 Rocks！&lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="a87ba-176">&lt;p&gt;&amp;copy; &lt;%: DateTime.Now.Year %&gt; - My ASP.NET Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="a87ba-177">現在，按下 Ctrl + Alt + Enter，或按一下更新列以在 [Page Inspector 瀏覽器] 視窗中查看結果。</span><span class="sxs-lookup"><span data-stu-id="a87ba-177">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![我的 ASP.NET 應用程式 Rocks！](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

<span data-ttu-id="a87ba-179">您可能已經認為頁尾是在*default.aspx*頁面上，但是它已經放在主要版面配置頁面中，Page Inspector 找到它。</span><span class="sxs-lookup"><span data-stu-id="a87ba-179">You might have thought that the footer was on the *Default.aspx* page, but it turned out to be in the master layout page, and Page Inspector found it for you.</span></span>

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="a87ba-180">檢查模式和 HTML 視窗</span><span class="sxs-lookup"><span data-stu-id="a87ba-180">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="a87ba-181">接下來，您將快速查看 [HTML] 視窗，以及它如何為您對應元素。</span><span class="sxs-lookup"><span data-stu-id="a87ba-181">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="a87ba-182">將 Page Inspector 放在檢查模式中。</span><span class="sxs-lookup"><span data-stu-id="a87ba-182">Put Page Inspector in Inspection Mode.</span></span>

![檢查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

<span data-ttu-id="a87ba-184">按一下頁面的上半部，此處會顯示「您的標誌」。</span><span class="sxs-lookup"><span data-stu-id="a87ba-184">Click the top part of the page that says "your logo here".</span></span> <span data-ttu-id="a87ba-185">您正以更詳細的方式檢查特定元素，因此當您移動滑鼠指標時，瀏覽器視窗中的顯示不會再變更。</span><span class="sxs-lookup"><span data-stu-id="a87ba-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="a87ba-186">現在，將滑鼠指標移至**HTML**視窗。</span><span class="sxs-lookup"><span data-stu-id="a87ba-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="a87ba-187">當您移動滑鼠指標時，Page Inspector 會在**HTML**視窗中概述元素，並在瀏覽器視窗中反白顯示對應的元素。</span><span class="sxs-lookup"><span data-stu-id="a87ba-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML 視窗](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

<span data-ttu-id="a87ba-189">如同之前一樣，Page Inspector 會在暫存索引標籤中開啟*網站*檔案。按一下 [網站] 索引標籤，即可在 [&lt;標題]&gt; 區段中反白顯示對應的標記：</span><span class="sxs-lookup"><span data-stu-id="a87ba-189">As before, Page Inspector opens the *Site.Master* file for you in a temporary tab. Click the Site.Master tab, and the corresponding markup is highlighted in the &lt;header&gt; section:</span></span>

![反白顯示的標記](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="a87ba-191">[樣式] 視窗中的預覽 CSS 變更</span><span class="sxs-lookup"><span data-stu-id="a87ba-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="a87ba-192">接下來，您將瞭解如何使用 [Page Inspector**樣式**] 視窗，預覽 CSS 的變更。</span><span class="sxs-lookup"><span data-stu-id="a87ba-192">Next, you will see how you can use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="a87ba-193">按一下 [**檢查**] 按鈕，將 Page Inspector 放在檢查模式中。</span><span class="sxs-lookup"><span data-stu-id="a87ba-193">Click the **Inspect** button to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="a87ba-194">在 [Page Inspector 瀏覽器] 視窗中，將滑鼠指標移到 [首頁] 區段上，直到 [ **div. content-包裝函式**] 標籤出現為止。</span><span class="sxs-lookup"><span data-stu-id="a87ba-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![將滑鼠停留在元素上](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

<span data-ttu-id="a87ba-196">在 [div] [內容包裝函式] 區段中按一下一次，然後將滑鼠指標移至 [**樣式**] 視窗。</span><span class="sxs-lookup"><span data-stu-id="a87ba-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="a87ba-197">在 [專題-包裝函式類別] 選取器底下，清除並選取 [背景色彩] 屬性的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a87ba-197">Under the .featured .content-wrapper class selector, clear and select the checkbox for the background-color property.</span></span>

![清除背景色彩](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

<span data-ttu-id="a87ba-199">請注意，[Page Inspector 瀏覽器] 視窗中的變更預覽會立即進行。</span><span class="sxs-lookup"><span data-stu-id="a87ba-199">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="a87ba-200">再次選取此核取方塊，然後按兩下屬性值並將它變更為 `red`。</span><span class="sxs-lookup"><span data-stu-id="a87ba-200">Select the checkbox again, then double-click the property value and change it to `red`.</span></span> <span data-ttu-id="a87ba-201">變更會立即顯示：</span><span class="sxs-lookup"><span data-stu-id="a87ba-201">The change shows immediately:</span></span>

![紅色背景色彩](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

<span data-ttu-id="a87ba-203">[**樣式**] 視窗可讓您在認可樣式表單本身的變更之前，輕鬆地測試和預覽 CSS 變更。</span><span class="sxs-lookup"><span data-stu-id="a87ba-203">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="a87ba-204">CSS 自動同步處理</span><span class="sxs-lookup"><span data-stu-id="a87ba-204">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="a87ba-205">這項功能需要1.3 版的 Page Inspector。</span><span class="sxs-lookup"><span data-stu-id="a87ba-205">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="a87ba-206">CSS 自動同步處理功能可讓您直接編輯 CSS 檔案，並在 Page Inspector 瀏覽器中立即查看變更。</span><span class="sxs-lookup"><span data-stu-id="a87ba-206">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="a87ba-207">按一下 [**檢查**]，將 Page Inspector 放在檢查模式中。</span><span class="sxs-lookup"><span data-stu-id="a87ba-207">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="a87ba-208">在 Page Inspector 瀏覽器中，將滑鼠指標移到 [首頁] 區段上，直到 [ **div. content-包裝函式**] 標籤出現為止。</span><span class="sxs-lookup"><span data-stu-id="a87ba-208">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="a87ba-209">按一下 [一次] 以選取此元素。</span><span class="sxs-lookup"><span data-stu-id="a87ba-209">Click once to select this element.</span></span>

<span data-ttu-id="a87ba-210">[**樣式**] 視窗會顯示此元素的所有 CSS 規則。</span><span class="sxs-lookup"><span data-stu-id="a87ba-210">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="a87ba-211">向下滾動以尋找 [精選] [內容包裝函式類別] 選取器。</span><span class="sxs-lookup"><span data-stu-id="a87ba-211">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="a87ba-212">按一下 [. 功能內容-包裝函式]。</span><span class="sxs-lookup"><span data-stu-id="a87ba-212">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="a87ba-213">Page Inspector 會開啟定義此樣式（.css）的 CSS 檔案，並反白顯示對應的 CSS 樣式。</span><span class="sxs-lookup"><span data-stu-id="a87ba-213">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![CSS 檔案](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

<span data-ttu-id="a87ba-215">現在將 `background-color` 的值變更為「紅色」。</span><span class="sxs-lookup"><span data-stu-id="a87ba-215">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="a87ba-216">變更會立即出現在 Page Inspector 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="a87ba-216">The change appears immediately in the Page Inspector browser.</span></span>

![Page Inspector 瀏覽器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a><span data-ttu-id="a87ba-218">使用 CSS 色彩選擇器</span><span class="sxs-lookup"><span data-stu-id="a87ba-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="a87ba-219">接下來，您將瞭解如何使用 Page Inspector 來快速尋找並變更預設應用程式中反白顯示文字的 CSS。</span><span class="sxs-lookup"><span data-stu-id="a87ba-219">Next, you'll learn how to use Page Inspector to quickly find and change the CSS for highlighted text in the default application.</span></span> <span data-ttu-id="a87ba-220">在此範例中，您已決定不喜歡藍色反白顯示，而且想要將它變更為另一個色彩。</span><span class="sxs-lookup"><span data-stu-id="a87ba-220">In this example, you've decided that you don't like the blue highlighting and want to change it to another color.</span></span>

<span data-ttu-id="a87ba-221">按一下 [**檢查**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a87ba-221">Click the **Inspect** button.</span></span>

![檢查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

<span data-ttu-id="a87ba-223">在 [Page Inspector 瀏覽器] 視窗中，將滑鼠指標移至反白顯示的 [影片、教學課程和範例] 文字上方，以顯示 CSS "mark" 標籤。</span><span class="sxs-lookup"><span data-stu-id="a87ba-223">In the Page Inspector browser window, move the mouse pointer over the highlighted "videos, tutorials, and samples" text so that the CSS "mark" label appears.</span></span>

![將滑鼠停留在 mark 元素上方](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

<span data-ttu-id="a87ba-225">按一下以選取文字。</span><span class="sxs-lookup"><span data-stu-id="a87ba-225">Click the text to select it.</span></span> <span data-ttu-id="a87ba-226">對應的 CSS 標記選取器會出現在 [**樣式**] 視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="a87ba-226">The corresponding CSS mark selector appears at the bottom of the **Styles** window.</span></span>

![[樣式] 視窗中的標記選取器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

<span data-ttu-id="a87ba-228">按一下標記選取器。</span><span class="sxs-lookup"><span data-stu-id="a87ba-228">Click the mark selector.</span></span> <span data-ttu-id="a87ba-229">這會開啟 web 應用程式的*網站 .css*檔案。</span><span class="sxs-lookup"><span data-stu-id="a87ba-229">This opens the *Site.css* file for the web application.</span></span> <span data-ttu-id="a87ba-230">按一下 [網站 .css] 索引標籤，就會反白顯示選取器的對應 CSS：</span><span class="sxs-lookup"><span data-stu-id="a87ba-230">Click the Site.css tab, and the corresponding CSS for the selector is highlighted:</span></span>

![在樣式表單中標記選取器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

<span data-ttu-id="a87ba-232">選取並移除具有背景色彩屬性的行。</span><span class="sxs-lookup"><span data-stu-id="a87ba-232">Select and remove the line with the background-color property.</span></span>

<span data-ttu-id="a87ba-233">您現在將使用新的 Visual Studio 2012 CSS 色彩選擇器，為 [**標記**背景色彩] 屬性選擇新的色彩。</span><span class="sxs-lookup"><span data-stu-id="a87ba-233">You will now use the new Visual Studio 2012 CSS color picker to choose a new color for the **mark** background-color property.</span></span>

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a><span data-ttu-id="a87ba-234">使用 Visual Studio 2012 CSS 色彩選擇器</span><span class="sxs-lookup"><span data-stu-id="a87ba-234">Using the Visual Studio 2012 CSS Color Picker</span></span>

<span data-ttu-id="a87ba-235">Visual Studio 2012 中的 CSS 編輯器具有色彩選擇器，可讓您輕鬆地選擇和插入色彩。</span><span class="sxs-lookup"><span data-stu-id="a87ba-235">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="a87ba-236">它有一個簡單的色軸和一個可提供更細微控制的「快顯」選擇器。</span><span class="sxs-lookup"><span data-stu-id="a87ba-236">It has a simple color bar and a "pop-down" picker that offers finer control.</span></span>

<span data-ttu-id="a87ba-237">色彩選擇器包含色彩的標準調色板、支援標準色彩名稱、雜湊碼、RGB、RGBA、HSL 和 HSLA 色彩，並維護您最近在檔中使用的色彩清單。</span><span class="sxs-lookup"><span data-stu-id="a87ba-237">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="a87ba-238">在背景色彩屬性所在的行上輸入 "bc"，然後按向下鍵一次。</span><span class="sxs-lookup"><span data-stu-id="a87ba-238">On the line where the background-color property was, type "bc" and press the down arrow once.</span></span>

<span data-ttu-id="a87ba-239">當您輸入以連字號分隔的屬性（例如「背景色彩」）中每個單字的第一個字元時，IntelliSense 會篩選清單，讓您只顯示符合的屬性：</span><span class="sxs-lookup"><span data-stu-id="a87ba-239">When you type the first character of each word in a hyphen-separated property like "background-color", IntelliSense filters the list for you to show only the properties that match:</span></span>

![Intellisense 篩選值](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

<span data-ttu-id="a87ba-241">現在輸入冒號。</span><span class="sxs-lookup"><span data-stu-id="a87ba-241">Now type a colon.</span></span> <span data-ttu-id="a87ba-242">當您這麼做時，就會插入完整的背景色彩屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="a87ba-242">When you do, the full background-color property name is inserted.</span></span> <span data-ttu-id="a87ba-243">輸入 **#** 或**rgb （** ，並顯示色彩選擇器列：</span><span class="sxs-lookup"><span data-stu-id="a87ba-243">Type **#** or **rgb(**, and the color picker bar appears:</span></span>

![CSS 色彩選擇器列](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

<span data-ttu-id="a87ba-245">若要查看色彩選擇器列的運作方式，請按一下滑鼠指標的色彩，或按向下鍵，然後使用向左鍵和向右鍵來流覽色彩。</span><span class="sxs-lookup"><span data-stu-id="a87ba-245">To see how the color picker bar works, click its colors with the mouse pointer, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="a87ba-246">當您造訪色彩時，會預覽背景色彩屬性的對應值：</span><span class="sxs-lookup"><span data-stu-id="a87ba-246">When you visit a color, the corresponding value for the background-color property is previewed:</span></span>

![預覽的背景色彩屬性值](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

<span data-ttu-id="a87ba-248">此時，您可以按 Enter 鍵來選取值，然後按分號（;)以完成 CSS 專案。</span><span class="sxs-lookup"><span data-stu-id="a87ba-248">At this point, you could press Enter to select the value and then a semicolon (;) to complete the CSS entry.</span></span> <span data-ttu-id="a87ba-249">現在請移至下一節，讓您可以看到色彩選擇器快顯的運作方式。</span><span class="sxs-lookup"><span data-stu-id="a87ba-249">For now, go on to the next section so that you can see how the color picker pop-down works.</span></span>

#### <a name="using-the-color-picker-pop-down"></a><span data-ttu-id="a87ba-250">使用色彩選擇器快顯視窗</span><span class="sxs-lookup"><span data-stu-id="a87ba-250">Using the Color Picker Pop-Down</span></span>

<span data-ttu-id="a87ba-251">當色軸沒有您要尋找的確切色彩時，您可以使用 [色彩選擇器] 快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="a87ba-251">When the color bar doesn't have the exact color that you're looking for, you can use the color picker pop-down.</span></span>

<span data-ttu-id="a87ba-252">若要開啟它，請按一下色軸右端的雙燕號，或在鍵盤上按一次向下箭號或按兩次。</span><span class="sxs-lookup"><span data-stu-id="a87ba-252">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS 色彩選擇器快顯視窗](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

<span data-ttu-id="a87ba-254">按一下右側分隔號的色彩。</span><span class="sxs-lookup"><span data-stu-id="a87ba-254">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="a87ba-255">這會在主視窗中顯示該色彩的漸層。</span><span class="sxs-lookup"><span data-stu-id="a87ba-255">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="a87ba-256">按 Enter 鍵直接從分隔號中選擇色彩，或按一下主視窗中的任何點，選擇較高的精確度。</span><span class="sxs-lookup"><span data-stu-id="a87ba-256">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="a87ba-257">如果您的電腦畫面上有您想要使用的色彩（不一定要在 Visual Studio 使用者介面內），您可以使用右下方的 [滴管] 工具來捕捉其值。</span><span class="sxs-lookup"><span data-stu-id="a87ba-257">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="a87ba-258">您也可以移動色彩選擇器底部的滑杆來變更色彩的不透明度。</span><span class="sxs-lookup"><span data-stu-id="a87ba-258">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="a87ba-259">這麼做會將色彩值變更為 RGBA 值，因為 RGBA 格式可以代表不透明度。</span><span class="sxs-lookup"><span data-stu-id="a87ba-259">Doing so changes color values to RGBA values because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="a87ba-260">選擇色彩之後，請按 Enter 鍵，然後輸入分號來完成*網站 .css*檔案中的背景色彩專案。</span><span class="sxs-lookup"><span data-stu-id="a87ba-260">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="a87ba-261">Page Inspector 更新列</span><span class="sxs-lookup"><span data-stu-id="a87ba-261">The Page Inspector Update Bar</span></span>

<span data-ttu-id="a87ba-262">Page Inspector 會立即偵測到*網站 .css*檔案的變更（或應用程式中的任何檔案），並在更新列中顯示警示。</span><span class="sxs-lookup"><span data-stu-id="a87ba-262">Page Inspector immediately detects the change to the *Site.css* file (or to any file in the application) and displays an alert in an update bar.</span></span>

![更新列](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

<span data-ttu-id="a87ba-264">若要儲存所有檔案並重新整理 Page Inspector 的瀏覽器，請按 Ctrl + Alt + Enter，或按一下更新列。</span><span class="sxs-lookup"><span data-stu-id="a87ba-264">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="a87ba-265">醒目提示色彩中的變更會出現在瀏覽器中：</span><span class="sxs-lookup"><span data-stu-id="a87ba-265">The change in the highlight color appears in the browser:</span></span>

![反白顯示色彩已變更](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a><span data-ttu-id="a87ba-267">請注意，您可以直接從 Visual Studio 環境中，輕鬆地重新整理 Page Inspector 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="a87ba-267">Notice that you conveniently refreshed the Page Inspector browser right from within the Visual Studio environment.</span></span> <span data-ttu-id="a87ba-268">使用 Page Inspector 而非外部瀏覽器，可讓您在開發 web 應用程式時保持在編輯器中。</span><span class="sxs-lookup"><span data-stu-id="a87ba-268">Using Page Inspector instead of an external browser lets you stay in the editor when you develop your web applications.</span></span>

## <a name="see-also"></a><span data-ttu-id="a87ba-269">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a87ba-269">See Also</span></span>

<span data-ttu-id="a87ba-270">[Page Inspector 簡介](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector)（Channel 9 影片）</span><span class="sxs-lookup"><span data-stu-id="a87ba-270">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (Channel 9 video)</span></span>

<span data-ttu-id="a87ba-271">[Page Inspector 錯誤訊息](https://go.microsoft.com/?linkid=9813062)（MSDN）</span><span class="sxs-lookup"><span data-stu-id="a87ba-271">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
