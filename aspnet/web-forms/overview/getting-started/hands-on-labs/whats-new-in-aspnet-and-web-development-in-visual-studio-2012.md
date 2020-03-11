---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: Visual Studio 2012 中 ASP.NET 和 Web 程式開發的新功能 |Microsoft Docs
author: rick-anderson
description: 新版本的 Visual Studio 引進了一些增強功能，著重于改善使用 Web 技術時的體驗和效能 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 80c77ec65ed86b06e417d3f6ba608e404c46768b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525932"
---
# <a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a><span data-ttu-id="ca73d-103">Visual Studio 2012 中的 ASP.NET 和網頁程式開發的新功能</span><span class="sxs-lookup"><span data-stu-id="ca73d-103">What's New in ASP.NET and Web Development in Visual Studio 2012</span></span>

<span data-ttu-id="ca73d-104">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="ca73d-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="ca73d-105">新版本的 Visual Studio 引進了許多增強功能，著重于改善使用 Web 技術時的體驗和效能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-105">The new version of Visual Studio introduces a number of enhancements focused on improving the experience and performance when working with Web technologies.</span></span> <span data-ttu-id="ca73d-106">CSS 的 Visual Studio 編輯器、JavaScript 和 HTML 已完全改頭換面，以包含許多最隨選的程式碼輔助，例如 IntelliSense 和自動縮排。</span><span class="sxs-lookup"><span data-stu-id="ca73d-106">Visual Studio Editors for CSS, JavaScript and HTML have been completely revamped to include many of the most in-demand code aids, such as IntelliSense and automatic indentation.</span></span> <span data-ttu-id="ca73d-107">關於效能、組合和縮制現在已整合為內建功能，可輕鬆地減少頁面載入時間。</span><span class="sxs-lookup"><span data-stu-id="ca73d-107">Regarding performance, bundling and minification are now integrated as built-in features to easily reduce page load time.</span></span>
> 
> <span data-ttu-id="ca73d-108">Visual Studio 可讓您使用最新的網站技術。</span><span class="sxs-lookup"><span data-stu-id="ca73d-108">Visual Studio enables you to work with the latest website technologies.</span></span> <span data-ttu-id="ca73d-109">您可以使用跨瀏覽器 CSS3 程式碼片段，確保您的網站無論用戶端平臺如何運作，同時也會利用新的 HTML5 元素和功能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-109">You can use cross-browser CSS3 Snippets to make sure your site works regardless of the client platform while also taking advantage of the new HTML5 elements and features.</span></span>
> 
> <span data-ttu-id="ca73d-110">使用此 Visual Studio 版本，撰寫和分析 JavaScript 程式碼應該更容易。</span><span class="sxs-lookup"><span data-stu-id="ca73d-110">Writing and profiling JavaScript code should be easier with this Visual Studio version.</span></span> <span data-ttu-id="ca73d-111">IntelliSense 清單、整合式 XML 檔和導覽功能現在可供 JavaScript 程式碼使用。</span><span class="sxs-lookup"><span data-stu-id="ca73d-111">IntelliSense lists, integrated XML documentation and navigation features are now available for JavaScript code.</span></span> <span data-ttu-id="ca73d-112">您現在可以輕鬆地擁有 JavaScript 目錄。</span><span class="sxs-lookup"><span data-stu-id="ca73d-112">You now have the JavaScript catalog at your fingertips.</span></span> <span data-ttu-id="ca73d-113">此外，您可以檢查 ECMAScript5 是否符合您的腳本，並在早期階段偵測語法錯誤。</span><span class="sxs-lookup"><span data-stu-id="ca73d-113">Additionally, you can check ECMAScript5 compliance with your scripts and detect syntax errors at an early stage.</span></span>
> 
> <span data-ttu-id="ca73d-114">最後，這個 Visual Studio 版本會執行內建的組合和縮制。</span><span class="sxs-lookup"><span data-stu-id="ca73d-114">Last but not least, this Visual Studio version implements built-in bundling and minification.</span></span> <span data-ttu-id="ca73d-115">您的腳本檔案和樣式表單將會進行封裝和壓縮，讓網站執行的速度更快。</span><span class="sxs-lookup"><span data-stu-id="ca73d-115">Your script files and style sheets will be packed and compressed so that the site performs faster.</span></span>
> 
> <span data-ttu-id="ca73d-116">本實驗室將針對源資料夾中提供的範例 Web 應用程式套用次要變更，引導您完成先前所述的增強功能和新功能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="ca73d-117">所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)取得。</span><span class="sxs-lookup"><span data-stu-id="ca73d-117">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="ca73d-118">目標</span><span class="sxs-lookup"><span data-stu-id="ca73d-118">Objectives</span></span>

<span data-ttu-id="ca73d-119">在此實習實驗室中，您將瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="ca73d-119">In this hands on lab, you will learn how to:</span></span>

- <span data-ttu-id="ca73d-120">使用 CSS 編輯器中的新功能和改進</span><span class="sxs-lookup"><span data-stu-id="ca73d-120">Use the new features and improvements in the CSS editor</span></span>
- <span data-ttu-id="ca73d-121">使用 HTML 編輯器中的新功能和改進</span><span class="sxs-lookup"><span data-stu-id="ca73d-121">Use the new features and improvements in the HTML editor</span></span>
- <span data-ttu-id="ca73d-122">使用 JavaScript 編輯器的新功能和改進</span><span class="sxs-lookup"><span data-stu-id="ca73d-122">Use the new features and improvements in the JavaScript editor</span></span>
- <span data-ttu-id="ca73d-123">設定及使用配套和縮制</span><span class="sxs-lookup"><span data-stu-id="ca73d-123">Configure and use bundling and minification</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="ca73d-124">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ca73d-124">Prerequisites</span></span>

- <span data-ttu-id="ca73d-125">適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需有關如何安裝的指示，請參閱[附錄 A](#AppendixA) ）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-125">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="ca73d-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) （適用于安裝腳本-已安裝在 windows 8 和 windows Server 2008 R2 上）</span><span class="sxs-lookup"><span data-stu-id="ca73d-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) (for setup scripts - already installed on Windows 8 and Windows Server 2008 R2)</span></span>
- <span data-ttu-id="ca73d-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home)或符合 HTML5 的瀏覽器</span><span class="sxs-lookup"><span data-stu-id="ca73d-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) - or an HTML5 compliant browser</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="ca73d-128">練習</span><span class="sxs-lookup"><span data-stu-id="ca73d-128">Exercises</span></span>

<span data-ttu-id="ca73d-129">這堂實習實驗室包含下列練習：</span><span class="sxs-lookup"><span data-stu-id="ca73d-129">This hands on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="ca73d-130">練習1： CSS 編輯器的新功能</span><span class="sxs-lookup"><span data-stu-id="ca73d-130">Exercise 1: What's New in the CSS Editor</span></span>](#Exercise1)
2. [<span data-ttu-id="ca73d-131">練習2： HTML 編輯器的新功能</span><span class="sxs-lookup"><span data-stu-id="ca73d-131">Exercise 2: What's New in the HTML Editor</span></span>](#Exercise2)
3. [<span data-ttu-id="ca73d-132">練習3： JavaScript 編輯器的新功能</span><span class="sxs-lookup"><span data-stu-id="ca73d-132">Exercise 3: What's New in the JavaScript Editor</span></span>](#Exercise3)
4. [<span data-ttu-id="ca73d-133">練習4：捆綁和縮制</span><span class="sxs-lookup"><span data-stu-id="ca73d-133">Exercise 4: Bundling and Minification</span></span>](#Exercise4)

<span data-ttu-id="ca73d-134">完成此實驗室的預估時間： **60 分鐘**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-134">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a><span data-ttu-id="ca73d-135">練習1： CSS 編輯器的新功能</span><span class="sxs-lookup"><span data-stu-id="ca73d-135">Exercise 1: What's New in the CSS Editor</span></span>

<span data-ttu-id="ca73d-136">Web 開發人員應該很熟悉與 CSS 編輯相關的許多困難之處。</span><span class="sxs-lookup"><span data-stu-id="ca73d-136">Web developers should be familiar with many of the difficulties related to CSS editing.</span></span> <span data-ttu-id="ca73d-137">CSS 樣式的最大問題之一，就是跨瀏覽器的相容性。</span><span class="sxs-lookup"><span data-stu-id="ca73d-137">One of the biggest issues of CSS styling is cross-browser compatibility.</span></span> <span data-ttu-id="ca73d-138">通常會發生這種情況，在將樣式套用至您的網站之後，您會注意到，如果您在另一個瀏覽器或裝置中開啟，它看起來會不同。</span><span class="sxs-lookup"><span data-stu-id="ca73d-138">It often happens that, after applying styles to your site, you notice that it looks different if you open it in another browser or device.</span></span> <span data-ttu-id="ca73d-139">因此，您可能會花相當長的時間來修正這些視覺問題，以瞭解當您最後讓它在一個瀏覽器中工作時，它會在其他人中中斷。</span><span class="sxs-lookup"><span data-stu-id="ca73d-139">Therefore, you may spend a considerable time on fixing those visual issues to realize that, when you finally make it work in one browser, it is broken in the others.</span></span>

<span data-ttu-id="ca73d-140">Visual Studio 現在包含可協助開發人員有效率地存取、工作及組織 CSS 樣式表單的功能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-140">Visual Studio now includes features that help developers access, work and organize CSS style sheets effectively.</span></span> <span data-ttu-id="ca73d-141">在此練習中，您將會符合有效組織和版本的新功能，以及跨瀏覽器相容性的 CSS3 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ca73d-141">Throughout this exercise, you will meet the new features for an effective organization and edition, as well as the CSS3 Code Snippets for cross-browser compatibility.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a><span data-ttu-id="ca73d-142">工作 1-新編輯器功能</span><span class="sxs-lookup"><span data-stu-id="ca73d-142">Task 1 - New Editor Features</span></span>

<span data-ttu-id="ca73d-143">在這項工作中，您將探索 CSS 編輯器的新功能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-143">In this task, you will discover the new features of the CSS Editor.</span></span> <span data-ttu-id="ca73d-144">這個新的編輯器將利用新的智慧型縮排、改良的程式碼批註和增強的 IntelliSense 清單，協助您提高生產力。</span><span class="sxs-lookup"><span data-stu-id="ca73d-144">This new editor will help you increase your productivity by taking advantage of the new smart indentation, the improved code comments and the enhanced IntelliSense list.</span></span>

1. <span data-ttu-id="ca73d-145">啟動**Visual Studio** ，然後開啟位於此實驗室的**Source\WhatsNewASPNET**資料夾中的 [ **WhatsNewASPNET** ] 方案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-145">Start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="ca73d-146">在方案總管中，開啟位於 [**樣式**] 資料夾底下的 [ **.css** ] 檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-146">In Solution Explorer, open the **Site.css** file located under the **Styles** folder.</span></span> <span data-ttu-id="ca73d-147">請確定 [**文字編輯器**] 工具顯示在工具列上。</span><span class="sxs-lookup"><span data-stu-id="ca73d-147">Make sure the **Text Editor** tools are visible on the toolbar.</span></span> <span data-ttu-id="ca73d-148">若要這麼做，請選取 [ **View** | **工具列**] 功能表選項，然後勾選 [**文字編輯器**] 選項。</span><span class="sxs-lookup"><span data-stu-id="ca73d-148">To do that, select the **View** | **Toolbars** menu option, and check the **Text Editor** options.</span></span> <span data-ttu-id="ca73d-149">您會注意到，自這個新版本起，[**批註**] 按鈕（![的 [批註] 按鈕](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png)）和 [**取消**批註] 按鈕（![[取消批註] 按鈕](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png)）也會針對 CSS 編輯器啟用。</span><span class="sxs-lookup"><span data-stu-id="ca73d-149">You will notice that, since this new version, the **Comment** button (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png) ) and the **Uncomment** button (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png) ) are also enabled for the CSS editor.</span></span>

    <span data-ttu-id="ca73d-150">![啟用編輯器和 CSS 工具](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "啟用編輯器和 CSS 工具")</span><span class="sxs-lookup"><span data-stu-id="ca73d-150">![Enabling Editor and CSS Tools](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "Enabling Editor and CSS Tools")</span></span>

    <span data-ttu-id="ca73d-151">*啟用編輯器和 CSS 工具*</span><span class="sxs-lookup"><span data-stu-id="ca73d-151">*Enabling Editor and CSS Tools*</span></span>
3. <span data-ttu-id="ca73d-152">請滾動程式碼，然後選取任何 CSS 類別定義。</span><span class="sxs-lookup"><span data-stu-id="ca73d-152">Scroll the code and select any CSS class definition.</span></span> <span data-ttu-id="ca73d-153">按一下 **批註** \ （![批註按鈕](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png)） 按鈕，以批註選取的行。</span><span class="sxs-lookup"><span data-stu-id="ca73d-153">Click the **Comment** (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png) ) button to comment the selected lines.</span></span> <span data-ttu-id="ca73d-154">然後，按一下 **取消**批註 （![取消批註 按鈕](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png)）按鈕來復原變更。</span><span class="sxs-lookup"><span data-stu-id="ca73d-154">Then, click the **Uncomment** (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png) ) button to undo the changes.</span></span>
4. <span data-ttu-id="ca73d-155">按一下折**迭（![** 折迭](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png)），然後**展開\*\*（![展開 [](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png)]）按鈕，其位於文字的左邊界。</span><span class="sxs-lookup"><span data-stu-id="ca73d-155">Click the **Collapse** (![collapse](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png) ) and **Expand** (![expand](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png) ) buttons located on the left margin of the text.</span></span> <span data-ttu-id="ca73d-156">請注意，您現在可以隱藏不會使用的樣式以讓您擁有更整潔的觀點。</span><span class="sxs-lookup"><span data-stu-id="ca73d-156">Notice that you can now hide the styles you don't use to have a cleaner view.</span></span>

    <span data-ttu-id="ca73d-157">![折迭 CSS 類別](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "折迭 CSS 類別")</span><span class="sxs-lookup"><span data-stu-id="ca73d-157">![Collapsing CSS classes](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "Collapsing CSS classes")</span></span>

    <span data-ttu-id="ca73d-158">*折迭 CSS 類別*</span><span class="sxs-lookup"><span data-stu-id="ca73d-158">*Collapsing CSS classes*</span></span>
5. <span data-ttu-id="ca73d-159">請確定已啟用 [智慧型縮排] 功能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-159">Make sure that the smart indentation feature is enabled.</span></span> <span data-ttu-id="ca73d-160">選取 **工具** | **選項** 功能表選項，然後在畫面的左窗格中選取 **文字編輯器** |  **CSS** | **格式** 頁面。</span><span class="sxs-lookup"><span data-stu-id="ca73d-160">Select the **Tools** | **Options** menu option, and then select the **Text Editor** | **CSS** | **Formatting** page in the left pane of the screen.</span></span> <span data-ttu-id="ca73d-161">選取 [**階層式縮排**] 選項。</span><span class="sxs-lookup"><span data-stu-id="ca73d-161">Check the **Hierarchical indentation** option.</span></span>

    <span data-ttu-id="ca73d-162">![啟用階層式縮排](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "啟用階層式縮排")</span><span class="sxs-lookup"><span data-stu-id="ca73d-162">![Enabling hierarchical indentation](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "Enabling hierarchical indentation")</span></span>

    <span data-ttu-id="ca73d-163">*啟用階層式縮排*</span><span class="sxs-lookup"><span data-stu-id="ca73d-163">*Enabling hierarchical indentation*</span></span>
6. <span data-ttu-id="ca73d-164">找出主要類別定義（main），並將樣式附加至 div 元素。</span><span class="sxs-lookup"><span data-stu-id="ca73d-164">Locate the main class definition (.main) and append a style to the div elements.</span></span> <span data-ttu-id="ca73d-165">您會發現程式碼會自動對齊，協助使用者一目了然地尋找父類別。</span><span class="sxs-lookup"><span data-stu-id="ca73d-165">You will notice that the code aligns automatically, helping users to find the parent classes at a glance.</span></span>

    <span data-ttu-id="ca73d-166">CSS</span><span class="sxs-lookup"><span data-stu-id="ca73d-166">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    <span data-ttu-id="ca73d-167">![CSS 中的階層對齊](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "CSS 中的階層對齊")</span><span class="sxs-lookup"><span data-stu-id="ca73d-167">![Hierarchical alignment in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "Hierarchical alignment in CSS")</span></span>

    <span data-ttu-id="ca73d-168">*CSS 中的階層對齊*</span><span class="sxs-lookup"><span data-stu-id="ca73d-168">*Hierarchical alignment in CSS*</span></span>
7. <span data-ttu-id="ca73d-169">在 [**主要 div** ] 類別內，找出框線結尾處的游標 **： 0px;** 然後按**enter**以顯示 IntelliSense 清單。</span><span class="sxs-lookup"><span data-stu-id="ca73d-169">Inside **.main div** class, locate the cursor at the end of **border: 0px;** and press **Enter** to display the IntelliSense list.</span></span> <span data-ttu-id="ca73d-170">開始輸入**top** ，並注意清單在您輸入時的篩選方式。</span><span class="sxs-lookup"><span data-stu-id="ca73d-170">Start typing **top** and notice how the list is filtered as you type.</span></span> <span data-ttu-id="ca73d-171">此清單會顯示在單字的任何部分包含**頂端**的元素（在舊版的 Visual Studio 中，清單會依*以詞彙開頭*的專案進行篩選）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-171">The list will display the elements that contain **top** at any part of the word (In prior versions of Visual Studio, the list is filtered by the items that *begin* with the term).</span></span>

    <span data-ttu-id="ca73d-172">![CSS 中的 IntelliSense 增強功能](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "CSS 中的 IntelliSense 增強功能")</span><span class="sxs-lookup"><span data-stu-id="ca73d-172">![IntelliSense enhancements in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "IntelliSense enhancements in CSS")</span></span>

    <span data-ttu-id="ca73d-173">*CSS 中的 IntelliSense 增強功能*</span><span class="sxs-lookup"><span data-stu-id="ca73d-173">*IntelliSense enhancements in CSS*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a><span data-ttu-id="ca73d-174">工作 2-色彩選擇器</span><span class="sxs-lookup"><span data-stu-id="ca73d-174">Task 2 - The Color Picker</span></span>

<span data-ttu-id="ca73d-175">在這項工作中，您會發現整合到 Visual Studio IntelliSense 的新 CSS 色彩選擇器。</span><span class="sxs-lookup"><span data-stu-id="ca73d-175">In this task, you will discover the new CSS Color Picker integrated into Visual Studio IntelliSense.</span></span>

1. <span data-ttu-id="ca73d-176">在 .css 中 **，** 找出標頭類別定義（. header），並將游標放在 **背景色彩**屬性 旁，在 &quot;：&quot; 和 &quot;#&quot; 該程式程式碼的字元之間 **。**</span><span class="sxs-lookup"><span data-stu-id="ca73d-176">In **Site.css,** locate the header class definition (.header) and place the cursor next to **background-color** attribute, between the &quot;:&quot; and &quot;#&quot; characters on that line of code **.**</span></span>

    <span data-ttu-id="ca73d-177">![尋找游標](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "尋找游標")</span><span class="sxs-lookup"><span data-stu-id="ca73d-177">![Locating the cursor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "Locating the cursor")</span></span>

    <span data-ttu-id="ca73d-178">*尋找游標*</span><span class="sxs-lookup"><span data-stu-id="ca73d-178">*Locating the cursor*</span></span>
2. <span data-ttu-id="ca73d-179">刪除**冒號**（:)然後再寫一次，以顯示色彩選擇器。</span><span class="sxs-lookup"><span data-stu-id="ca73d-179">Delete the **colon** (:) and write it again to display the color picker.</span></span> <span data-ttu-id="ca73d-180">請注意，您會看到的第一種色彩是最常用的網站色彩。</span><span class="sxs-lookup"><span data-stu-id="ca73d-180">Notice that the first colors you will see are the most frequent colors of your site.</span></span> <span data-ttu-id="ca73d-181">如果您按一下白色色彩，其 HTML 色彩代碼（#fff）將會取代樣式表單中目前的色彩代碼。</span><span class="sxs-lookup"><span data-stu-id="ca73d-181">If you click the white color, its HTML color code (#fff) will replace the current color code in the stylesheet.</span></span>

    <span data-ttu-id="ca73d-182">![色彩選擇器](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "色彩選擇器")</span><span class="sxs-lookup"><span data-stu-id="ca73d-182">![Color picker](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "Color picker")</span></span>

    <span data-ttu-id="ca73d-183">*色彩選擇器*</span><span class="sxs-lookup"><span data-stu-id="ca73d-183">*Color picker*</span></span>
3. <span data-ttu-id="ca73d-184">按下色彩選擇器上的 [**展開**（![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png)）] 按鈕，以顯示色彩漸層，然後拖曳漸層游標來選取不同的色彩。</span><span class="sxs-lookup"><span data-stu-id="ca73d-184">Press the **Expand** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png) ) button on the color picker to display the color gradient, and then drag the gradient cursor to select a different color.</span></span> <span data-ttu-id="ca73d-185">之後，請按一下 [**滴管**] 按鈕，然後從螢幕中選取任何色彩。</span><span class="sxs-lookup"><span data-stu-id="ca73d-185">After that, click the **Eyedropper** button and select any color from the screen.</span></span> <span data-ttu-id="ca73d-186">請注意，當您移動游標時，背景色彩值會動態變更。</span><span class="sxs-lookup"><span data-stu-id="ca73d-186">Notice that background color value changes dynamically while you move the cursor.</span></span>

    <span data-ttu-id="ca73d-187">![色彩選擇器漸層](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "色彩選擇器漸層")</span><span class="sxs-lookup"><span data-stu-id="ca73d-187">![Color picker gradient](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "Color picker gradient")</span></span>

    <span data-ttu-id="ca73d-188">*色彩選擇器漸層*</span><span class="sxs-lookup"><span data-stu-id="ca73d-188">*Color picker gradient*</span></span>
4. <span data-ttu-id="ca73d-189">在 [**不透明度**] 滑杆中，將選取器移至橫條的中央，以減少不透明度。</span><span class="sxs-lookup"><span data-stu-id="ca73d-189">In the **Opacity** slider, move the selector to the center of the bar to reduce the opacity.</span></span> <span data-ttu-id="ca73d-190">請注意，[背景色彩] 值現在會將其縮放比例變更為 RGBA。</span><span class="sxs-lookup"><span data-stu-id="ca73d-190">Notice that background-color value now changes its scale to RGBA.</span></span>

    <span data-ttu-id="ca73d-191">![色彩選擇器不透明度](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "色彩選擇器不透明度")</span><span class="sxs-lookup"><span data-stu-id="ca73d-191">![Color picker Opacity](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "Color picker Opacity")</span></span>

    <span data-ttu-id="ca73d-192">*色彩選擇器不透明度*</span><span class="sxs-lookup"><span data-stu-id="ca73d-192">*Color picker Opacity*</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca73d-193">CSS3 中的 RGBA （紅色、綠色、藍色、Alpha）色彩定義，可讓您定義單一專案的色彩不透明度值。</span><span class="sxs-lookup"><span data-stu-id="ca73d-193">The RGBA (Red, Green, Blue, Alpha) color definition in CSS3 enables you to define the color opacity value for a single item.</span></span> <span data-ttu-id="ca73d-194">不同于**不透明度-** 類似的 CSS 屬性 **-** RGBA 色彩也會與最新的瀏覽器相容。</span><span class="sxs-lookup"><span data-stu-id="ca73d-194">Unlike **opacity -** a similar CSS attribute **-** RGBA colors are also compatible with the latest browsers.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a><span data-ttu-id="ca73d-195">工作 3-CSS 相容程式碼片段</span><span class="sxs-lookup"><span data-stu-id="ca73d-195">Task 3 - CSS Compatible Code Snippets</span></span>

<span data-ttu-id="ca73d-196">在這項工作中，您將瞭解如何使用跨瀏覽器相容的 CSS3 程式碼片段，以在您的網站中執行一些功能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-196">In this task, you will learn how to use cross-browser compatible CSS3 snippets in order to implement some features in your website.</span></span>

1. <span data-ttu-id="ca73d-197">在 [ **.css** ] 檔案中，找出**標頭**css 類別定義（. header），並將游標放在 [ **/\*框線半徑\*/** 預留位置] 下方，以加入新的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ca73d-197">In the **Site.css** file, locate the **header** CSS class definition (.header) and place the cursor below the **/\*border radius\*/** placeholder to add a new snippet.</span></span> <span data-ttu-id="ca73d-198">按**enter**以顯示 IntelliSense 清單並輸入**radius**以篩選清單。</span><span class="sxs-lookup"><span data-stu-id="ca73d-198">Press **Enter** to display the IntelliSense list and type **radius** to filter the list.</span></span> <span data-ttu-id="ca73d-199">選取清單中的 [**框線-半徑**] 選項，並按兩下，然後按下**tab**鍵以插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ca73d-199">Select the **border-radius** option from the list with a double click, and then press the **TAB** key to insert the snippet.</span></span> <span data-ttu-id="ca73d-200">然後，輸入以圖元為單位的 radius 大小，然後按**enter**鍵。</span><span class="sxs-lookup"><span data-stu-id="ca73d-200">Then, type a radius size in pixels and press **Enter**.</span></span> <span data-ttu-id="ca73d-201">例如，輸入**15px**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-201">For instance, type **15px**.</span></span>

    <span data-ttu-id="ca73d-202">程式碼片段所新增的 CSS3 屬性會在大部分的 HTML5 合規性瀏覽器中轉譯圓角框線，包括 Mozilla 和 WebKit 為基礎的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="ca73d-202">The CSS3 attributes added by the snippet will render rounded borders in most HTML5 compliance browsers, including Mozilla and WebKit-based browsers.</span></span>

    <span data-ttu-id="ca73d-203">![使用框線-radius 程式碼片段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "使用框線-radius 程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="ca73d-203">![Using a border-radius snippet](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "Using a border-radius snippet")</span></span>

    <span data-ttu-id="ca73d-204">*使用框線-radius 程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="ca73d-204">*Using a border-radius snippet*</span></span>
2. <span data-ttu-id="ca73d-205">將相同的**框線**程式碼片段套用到頁面樣式（. page）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-205">Apply the same **border** snippets in the page style (.page).</span></span>

    <span data-ttu-id="ca73d-206">CSS</span><span class="sxs-lookup"><span data-stu-id="ca73d-206">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. <span data-ttu-id="ca73d-207">按 **F5** 執行方案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-207">Press **F5** to run the solution.</span></span> <span data-ttu-id="ca73d-208">請注意，每個頁面現在都有圓角框線。</span><span class="sxs-lookup"><span data-stu-id="ca73d-208">Notice that each page now has rounded borders.</span></span>

    <span data-ttu-id="ca73d-209">![圓角](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "圓角")</span><span class="sxs-lookup"><span data-stu-id="ca73d-209">![Rounded corners](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "Rounded corners")</span></span>

    <span data-ttu-id="ca73d-210">*圓角*</span><span class="sxs-lookup"><span data-stu-id="ca73d-210">*Rounded corners*</span></span>
4. <span data-ttu-id="ca73d-211">關閉瀏覽器並返回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ca73d-211">Close the browser and return to Visual Studio.</span></span>
5. <span data-ttu-id="ca73d-212">開啟位於 [**樣式**] 資料夾底下的**自訂 .css**檔案，並將游標放在 [div] 中 **。**</span><span class="sxs-lookup"><span data-stu-id="ca73d-212">Open the **Custom.css** file located under the **Styles** folder and place the cursor inside **div.images ul li img** class definition.</span></span>
6. <span data-ttu-id="ca73d-213">按 enter 以顯示 [IntelliSense] 清單、輸入**box-陰影**，然後按兩次**tab**鍵，將預設的陰影程式碼片段插入類別定義內。</span><span class="sxs-lookup"><span data-stu-id="ca73d-213">Press enter to display the IntelliSense list, type **box-shadow** and press the **TAB** key twice to insert the default shadow code snippet inside the class definition.</span></span> <span data-ttu-id="ca73d-214">將陰影值設定為**10px 10px 5px #888**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-214">Set the shadow values to **10px 10px 5px #888**.</span></span> <span data-ttu-id="ca73d-215">然後，輸入**框線半徑**，並插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ca73d-215">Then, type **border-radius** and insert the code snippet.</span></span> <span data-ttu-id="ca73d-216">輸入**15px**以設定 radius 大小，然後按**enter**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-216">Type **15px** to set radius size and press **ENTER**.</span></span>

    <span data-ttu-id="ca73d-217">![具有陰影的圓角](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "具有陰影的圓角")</span><span class="sxs-lookup"><span data-stu-id="ca73d-217">![Rounded corners with shadow](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "Rounded corners with shadow")</span></span>

    <span data-ttu-id="ca73d-218">*具有陰影的圓角*</span><span class="sxs-lookup"><span data-stu-id="ca73d-218">*Rounded corners with shadow*</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca73d-219">此時，陰影屬性會以對應的前置詞（moz-appearance、webkit、o）插入，以支援 Mozilla 和 Webkit （Chrome、Safari、Konkeror）瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="ca73d-219">At this moment, the shadow attribute is inserted with the corresponding prefix (moz, webkit, o) to support Mozilla and Webkit (Chrome, Safari, Konkeror) browsers.</span></span>
7. <span data-ttu-id="ca73d-220">建立新的類別**div。影像 ul li img：將滑鼠停留**在**div. images u l i m g**類別定義底下，並將游標放在方括弧內 **。**</span><span class="sxs-lookup"><span data-stu-id="ca73d-220">Create a new class **div.images ul li img:hover** below the **div.images ul li img** class definition and place the cursor inside the brackets **.**</span></span>

    <span data-ttu-id="ca73d-221">CSS</span><span class="sxs-lookup"><span data-stu-id="ca73d-221">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. <span data-ttu-id="ca73d-222">輸入**轉換**，並按兩次**tab**鍵以插入轉換程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ca73d-222">Type **transform** and press the **TAB** key twice in order to insert the transform snippet.</span></span> <span data-ttu-id="ca73d-223">然後，輸入**旋轉（-15deg）** ，以在影像暫留時變更旋轉角度值。</span><span class="sxs-lookup"><span data-stu-id="ca73d-223">Then, enter **rotate(-15deg)** to change the rotation angle value when images are hovered.</span></span>

    <span data-ttu-id="ca73d-224">CSS</span><span class="sxs-lookup"><span data-stu-id="ca73d-224">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. <span data-ttu-id="ca73d-225">按**F5**執行方案，並流覽至 [CSS3] 頁面。</span><span class="sxs-lookup"><span data-stu-id="ca73d-225">Press **F5** to run the solution and browse to the CSS3 page.</span></span> <span data-ttu-id="ca73d-226">請注意，影像具有圓角和方塊陰影。</span><span class="sxs-lookup"><span data-stu-id="ca73d-226">Notice that the images have rounded corners and box shadows.</span></span> <span data-ttu-id="ca73d-227">將滑鼠停留在影像上，並觀賞它們旋轉。</span><span class="sxs-lookup"><span data-stu-id="ca73d-227">Hover the mouse over the images and watch them rotate.</span></span>

    <span data-ttu-id="ca73d-228">![旋轉影像的轉換程式碼片段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "旋轉影像的轉換程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="ca73d-228">![Transform snippet rotating an image](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "Transform snippet rotating an image")</span></span>

    <span data-ttu-id="ca73d-229">*旋轉影像的轉換程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="ca73d-229">*Transform snippet rotating an image*</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca73d-230">如果您使用的是 Internet Explorer 10，而且看不到陰影，請確定 [檔案模式] 設定為 [IE10 標準]。</span><span class="sxs-lookup"><span data-stu-id="ca73d-230">If you are using Internet Explorer 10 and cannot see the shadows, make sure the document mode is set to IE10 standards.</span></span> <span data-ttu-id="ca73d-231">按**F12**開啟 Internet Explorer 開發人員工具，然後按一下 [**檔案模式]** 變更為 IE10 標準。</span><span class="sxs-lookup"><span data-stu-id="ca73d-231">Press **F12** to open Internet Explorer developer tools and click **Document Mode** to change to IE10 standards.</span></span>

    ![關於-us](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a><span data-ttu-id="ca73d-233">練習2： HTML 編輯器的新功能</span><span class="sxs-lookup"><span data-stu-id="ca73d-233">Exercise 2: What's New in the HTML Editor</span></span>

<span data-ttu-id="ca73d-234">Visual Studio 具有改良的 HTML 編輯器。</span><span class="sxs-lookup"><span data-stu-id="ca73d-234">Visual Studio has an improved HTML editor.</span></span> <span data-ttu-id="ca73d-235">此版本中包含的一些增強功能包括 HTML 檔案中的智慧型縮排、HTML5 程式碼片段、HTML 開始和結束標記比對，以及 HTML 驗證。</span><span class="sxs-lookup"><span data-stu-id="ca73d-235">Some of the enhancements included in this version are smart indentation in HTML documents, HTML5 snippets, HTML start and end tag matching, and HTML validation.</span></span> <span data-ttu-id="ca73d-236">在此練習中，您將會在網站標記中工作時，看到這些變更如何改善您的順暢。</span><span class="sxs-lookup"><span data-stu-id="ca73d-236">Throughout this exercise, you will see how these changes improve your fluency when working in the website markup.</span></span>

<span data-ttu-id="ca73d-237">如同 CSS 編輯器，HTML 編輯器也已經過改善。</span><span class="sxs-lookup"><span data-stu-id="ca73d-237">Like the CSS editor, the HTML editor was also improved.</span></span> <span data-ttu-id="ca73d-238">這些改良功能大多是讓 Web 開發人員的生活變得更簡單的小部分。</span><span class="sxs-lookup"><span data-stu-id="ca73d-238">Most of these improvements are small ones that make the Web developer's life easier.</span></span> <span data-ttu-id="ca73d-239">針對 HTML 檔案 DOCTYPE 進行編輯和驗證時，像是 HTML5、智慧型縮排、比對開始和結束標記等更多程式碼片段的專案，就是其中一些改良功能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-239">Things like more code snippets for HTML5, smart indentation, matching start and end tags when editing and validation targeting the HTML document DOCTYPE are some of these improvements.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a><span data-ttu-id="ca73d-240">工作 1-改良的 DOCTYPE 驗證</span><span class="sxs-lookup"><span data-stu-id="ca73d-240">Task 1 - Improved DOCTYPE Validation</span></span>

<span data-ttu-id="ca73d-241">HTML 編輯器現在可以檢查頁面的 DOCTYPE，即使定義可能在主版頁面中也一樣。</span><span class="sxs-lookup"><span data-stu-id="ca73d-241">The HTML editor now has the ability to check the DOCTYPE of your page, even though the definition might be in the master page.</span></span> <span data-ttu-id="ca73d-242">根據頁面的 DOCTYPE，HTML 編輯器會使用正確的規則集進行驗證，並會篩選 IntelliSense 清單並考慮 DOCTYPE 元素。</span><span class="sxs-lookup"><span data-stu-id="ca73d-242">Depending on the DOCTYPE of your page, the HTML editor will validate with the correct set of rules and will filter the IntelliSense list considering the DOCTYPE elements.</span></span>

<span data-ttu-id="ca73d-243">在這項工作中，您將變更頁面的 DOCTYPE，以查看 HTML 編輯器的行為如何隨之變更。</span><span class="sxs-lookup"><span data-stu-id="ca73d-243">In this task, you will change the DOCTYPE of a page to see how the HTML editor behavior changes accordingly.</span></span>

1. <span data-ttu-id="ca73d-244">如果尚未開啟，請啟動**Visual Studio** ，然後開啟位於此實驗室的**Source\WhatsNewASPNET**資料夾中的**WhatsNewASPNET。**</span><span class="sxs-lookup"><span data-stu-id="ca73d-244">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="ca73d-245">開啟 [**網站**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="ca73d-245">Open the **Site.Master** page.</span></span>
3. <span data-ttu-id="ca73d-246">請注意 [驗證] 工具列的 [目標架構]。</span><span class="sxs-lookup"><span data-stu-id="ca73d-246">Notice the Target Schema for Validation Toolbar.</span></span> <span data-ttu-id="ca73d-247">HTML 編輯器的運作方式（驗證、IntelliSense 等等）會適當地變更，以符合所選的 Doctype。</span><span class="sxs-lookup"><span data-stu-id="ca73d-247">The way the HTML editor behaves (Validation, IntelliSense, etc.) will properly change to fit the Doctype selected.</span></span>

    <span data-ttu-id="ca73d-248">![在 HTML 原始檔編輯工具列中使用 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "在 HTML 原始檔編輯工具列中使用 Doctype")</span><span class="sxs-lookup"><span data-stu-id="ca73d-248">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="ca73d-249">*在 HTML 原始檔編輯工具列中使用 Doctype*</span><span class="sxs-lookup"><span data-stu-id="ca73d-249">*Use Doctype in HTML Source Editing toolbar*</span></span>
4. <span data-ttu-id="ca73d-250">將目標架構變更為 HTML 4.01。</span><span class="sxs-lookup"><span data-stu-id="ca73d-250">Change the Target Schema to HTML 4.01.</span></span>

    <span data-ttu-id="ca73d-251">![在 HTML 原始檔編輯工具列中變更 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "在 HTML 原始檔編輯工具列中變更 Doctype")</span><span class="sxs-lookup"><span data-stu-id="ca73d-251">![Changing Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "Changing Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="ca73d-252">*在 HTML 原始檔編輯工具列中變更 Doctype*</span><span class="sxs-lookup"><span data-stu-id="ca73d-252">*Changing Doctype in HTML Source Editing toolbar*</span></span>
5. <span data-ttu-id="ca73d-253">將游標放在**body**元素底下，然後開始輸入 HTML5 元素的名稱（例如**影片**）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-253">Place the cursor under the **body** element, and start typing the name of an HTML5 element (for example, **video**).</span></span> <span data-ttu-id="ca73d-254">請注意，[IntelliSense] 清單中不提供此元素。</span><span class="sxs-lookup"><span data-stu-id="ca73d-254">Notice that the element is not available in the IntelliSense list.</span></span>

    <span data-ttu-id="ca73d-255">![未列出 HTML5 元素](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "未列出 HTML5 元素")</span><span class="sxs-lookup"><span data-stu-id="ca73d-255">![HTML5 elements not listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "HTML5 elements not listed")</span></span>

    <span data-ttu-id="ca73d-256">*未列出 HTML5 元素*</span><span class="sxs-lookup"><span data-stu-id="ca73d-256">*HTML5 elements not listed*</span></span>
6. <span data-ttu-id="ca73d-257">復原 [驗證] 工具列之 [目標架構] 的變更，並從下拉式清單中挑選 [DOCTYPE： XHTML5]。</span><span class="sxs-lookup"><span data-stu-id="ca73d-257">Undo the changes to the Target Schema for Validation Toolbar, picking DOCTYPE: XHTML5 from the dropdown list.</span></span>

    <span data-ttu-id="ca73d-258">![在 HTML 原始檔編輯工具列中使用 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "在 HTML 原始檔編輯工具列中使用 Doctype")</span><span class="sxs-lookup"><span data-stu-id="ca73d-258">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="ca73d-259">*在 HTML 原始檔編輯工具列中重設 Doctype*</span><span class="sxs-lookup"><span data-stu-id="ca73d-259">*Reset Doctype in HTML Source Editing toolbar*</span></span>
7. <span data-ttu-id="ca73d-260">將游標放在**body**元素底下，然後再次開始輸入 HTML5 元素（例如，像是**影片**）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-260">Place the cursor under the **body** element and start typing an HTML5 element again (For example, like **video**).</span></span> <span data-ttu-id="ca73d-261">請注意，HTML5 元素現在可以在 IntelliSense 清單中取得。</span><span class="sxs-lookup"><span data-stu-id="ca73d-261">Notice that the HTML5 elements are now available in the IntelliSense list.</span></span>

    <span data-ttu-id="ca73d-262">![列出的 HTML5 元素](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "列出的 HTML5 元素")</span><span class="sxs-lookup"><span data-stu-id="ca73d-262">![HTML5 elements being listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "HTML5 elements being listed")</span></span>

    <span data-ttu-id="ca73d-263">*列出的 HTML5 元素*</span><span class="sxs-lookup"><span data-stu-id="ca73d-263">*HTML5 elements being listed*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a><span data-ttu-id="ca73d-264">工作 2-開始/結束標記自動更新</span><span class="sxs-lookup"><span data-stu-id="ca73d-264">Task 2 - Start/End Tags Automatic Update</span></span>

<span data-ttu-id="ca73d-265">Visual Studio 現在會更新您正在編輯之專案的 HTML 開頭或結束記號，使兩者彼此相符。</span><span class="sxs-lookup"><span data-stu-id="ca73d-265">Visual Studio now updates the HTML opening or closing tags of the element that you are editing to match each other.</span></span> <span data-ttu-id="ca73d-266">這項新功能可改善您編輯 HTML 標籤時的生產力。</span><span class="sxs-lookup"><span data-stu-id="ca73d-266">This new feature will improve your productivity when editing HTML tags.</span></span>

1. <span data-ttu-id="ca73d-267">在**default.aspx**頁面上，新增包含標題的**H3**元素（例如，Visual Studio 2012 Rocks！）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-267">On the **Default.aspx** page, add an **H3** element with a title (for example, Visual Studio 2012 Rocks!).</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. <span data-ttu-id="ca73d-268">變更**H3**標記並輸入**H2**或**H1。**</span><span class="sxs-lookup"><span data-stu-id="ca73d-268">Change the **H3** tag and type **H2** or **H1.**</span></span>

    <span data-ttu-id="ca73d-269">請注意，結束標記會自動更新。</span><span class="sxs-lookup"><span data-stu-id="ca73d-269">Notice that the end tag automatically updates.</span></span> <span data-ttu-id="ca73d-270">您也可以修改結束標記，以查看啟動標記也會一併更新。</span><span class="sxs-lookup"><span data-stu-id="ca73d-270">You can also modify the end tag to see that the start tag updates accordingly too.</span></span>

    <span data-ttu-id="ca73d-271">![結束標記的自動更新](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "結束標記的自動更新")</span><span class="sxs-lookup"><span data-stu-id="ca73d-271">![Automatic update of the end tag](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "Automatic update of the end tag")</span></span>

    <span data-ttu-id="ca73d-272">*結束標記的自動更新*</span><span class="sxs-lookup"><span data-stu-id="ca73d-272">*Automatic update of the end tag*</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a><span data-ttu-id="ca73d-273">工作 3-新的 HTML5 程式碼片段</span><span class="sxs-lookup"><span data-stu-id="ca73d-273">Task 3 - New HTML5 Code Snippets</span></span>

<span data-ttu-id="ca73d-274">Visual Studio 現在包含數個 HTML5 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ca73d-274">Visual Studio now includes several HTML5 code snippets.</span></span> <span data-ttu-id="ca73d-275">在這項工作中，您將使用其中一些程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ca73d-275">In this task, you will use some of these snippets.</span></span>

1. <span data-ttu-id="ca73d-276">將名為 [**音訊**] 的新資料夾新增至網站資料夾的根目錄。</span><span class="sxs-lookup"><span data-stu-id="ca73d-276">Add a new folder named **audio** to the root of the web site folder.</span></span> <span data-ttu-id="ca73d-277">開啟 [Windows Explorer]，並將任何音訊檔案複製到 [ **WhatsNewASPNET** ] 方案的 [**音訊**] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ca73d-277">Open Windows Explorer and copy any audio file into the **audio** folder of the **WhatsNewASPNET.sln** solution.</span></span>
2. <span data-ttu-id="ca73d-278">在**default.aspx**頁面中，找出 Web11 Rocks！！底下的游標</span><span class="sxs-lookup"><span data-stu-id="ca73d-278">In the **Default.aspx** page, locate the cursor under the Web11 Rocks!!</span></span> <span data-ttu-id="ca73d-279">標頭。</span><span class="sxs-lookup"><span data-stu-id="ca73d-279">Header.</span></span> <span data-ttu-id="ca73d-280">輸入**音訊**，然後按下 tab 鍵。</span><span class="sxs-lookup"><span data-stu-id="ca73d-280">Type **audio** and press the TAB key.</span></span>

    <span data-ttu-id="ca73d-281">新的 HTML 編輯器包含 HTML5 內容的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ca73d-281">The new HTML editor includes code snippets for HTML5 content.</span></span> <span data-ttu-id="ca73d-282">請記得使用適當的 DOCTYPE 定義來啟用 HTML5 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ca73d-282">Remember to use the proper DOCTYPE definition to enable the HTML5 snippets.</span></span>

    <span data-ttu-id="ca73d-283">![插入 HTML5 程式碼片段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "插入 HTML5 程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="ca73d-283">![Inserting HTML5 Code Snippets](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "Inserting HTML5 Code Snippets")</span></span>

    <span data-ttu-id="ca73d-284">*插入 HTML5 程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="ca73d-284">*Inserting HTML5 Code Snippets*</span></span>
3. <span data-ttu-id="ca73d-285">更新音訊來源以指向現有的音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-285">Update the audio source to point to an existing audio file.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > <span data-ttu-id="ca73d-286">您必須將音訊檔案新增至方案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-286">You will need to add the audio file to the solution.</span></span>
4. <span data-ttu-id="ca73d-287">按**F5**鍵執行網站並播放音訊。</span><span class="sxs-lookup"><span data-stu-id="ca73d-287">Press **F5** to run the site and play the audio.</span></span>

    <span data-ttu-id="ca73d-288">![執行音訊控制項](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "執行音訊控制項")</span><span class="sxs-lookup"><span data-stu-id="ca73d-288">![Running the audio control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "Running the audio control")</span></span>

    <span data-ttu-id="ca73d-289">*執行音訊控制項*</span><span class="sxs-lookup"><span data-stu-id="ca73d-289">*Running the audio control*</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca73d-290">您也可以嘗試 Visual Studio 中包含的程式碼片段，例如影片、圖等等。</span><span class="sxs-lookup"><span data-stu-id="ca73d-290">You can also try more snippets included in Visual Studio, such as video, figure, etc.</span></span>
5. <span data-ttu-id="ca73d-291">現在，請嘗試在頁面的某個部分插入控制項。</span><span class="sxs-lookup"><span data-stu-id="ca73d-291">Now, try to insert a control in some part of the page.</span></span> <span data-ttu-id="ca73d-292">例如，請嘗試插入**GridView**控制項，但不要輸入 **&lt;Gri，** 而是開始輸入 **&lt;GV**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-292">For example, try to insert a **GridView** control, but instead of typing **&lt;Gri,** start typing **&lt;GV**.</span></span> <span data-ttu-id="ca73d-293">請注意，[IntelliSense] 清單會顯示**asp： GridView**控制項。</span><span class="sxs-lookup"><span data-stu-id="ca73d-293">Notice that the IntelliSense list shows the **asp:GridView** control.</span></span>

    <span data-ttu-id="ca73d-294">HTML 編輯器中的 IntelliSense 現在提供標題大小寫搜尋，以及部分比對（抓取包含詞彙的所有元素）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-294">IntelliSense in the HTML Editor now provides title-casing search, as well as partial matching (retrieving all elements that contains the term).</span></span>

    <span data-ttu-id="ca73d-295">![使用 IntelliSense 清單插入 GridView](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "使用 IntelliSense 清單插入 GridView")</span><span class="sxs-lookup"><span data-stu-id="ca73d-295">![Inserting a GridView with IntelliSense lists](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "Inserting a GridView with IntelliSense lists")</span></span>

    <span data-ttu-id="ca73d-296">*使用 IntelliSense 清單插入 GridView*</span><span class="sxs-lookup"><span data-stu-id="ca73d-296">*Inserting a GridView with IntelliSense lists*</span></span>

    <span data-ttu-id="ca73d-297">如果您輸入 **&lt;方格**，則會取得符合該詞彙的所有專案，但 Visual Studio 會建議**gridview**控制項：</span><span class="sxs-lookup"><span data-stu-id="ca73d-297">If you type **&lt;grid** you will get all the items that match the term, but Visual Studio will suggest the **gridview** control:</span></span>

    <span data-ttu-id="ca73d-298">![使用 IntelliSense 清單和部分比對插入 GridView](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "使用 IntelliSense 清單和部分比對插入 GridView")</span><span class="sxs-lookup"><span data-stu-id="ca73d-298">![Inserting a GridView with IntelliSense lists and partial matching](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "Inserting a GridView with IntelliSense lists and partial matching")</span></span>

    <span data-ttu-id="ca73d-299">*使用 IntelliSense 清單和部分比對插入 GridView*</span><span class="sxs-lookup"><span data-stu-id="ca73d-299">*Inserting a GridView with IntelliSense lists and partial matching*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a><span data-ttu-id="ca73d-300">工作 4-HTML 編輯器智慧標籤</span><span class="sxs-lookup"><span data-stu-id="ca73d-300">Task 4 - HTML Editor Smart Tags</span></span>

<span data-ttu-id="ca73d-301">HTML 編輯器中的另一項改進是智慧標籤功能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-301">Another improvement in the HTML Editor is the Smart Tags feature.</span></span> <span data-ttu-id="ca73d-302">智慧標籤可讓您以每個控制項為基礎，輕鬆地執行一般或重複性的開發工作。</span><span class="sxs-lookup"><span data-stu-id="ca73d-302">Smart tags make it easy to perform common or repetitive development tasks on a per-control basis.</span></span> <span data-ttu-id="ca73d-303">這項功能已在 HTML 設計工具中提供，但無法在 HTML 編輯器中使用。</span><span class="sxs-lookup"><span data-stu-id="ca73d-303">This feature was already available in the HTML Designer, but not in the HTML Editor.</span></span>

1. <span data-ttu-id="ca73d-304">開啟 [ **Master** ]，然後找出 [ **asp： Menu** ] 元素。</span><span class="sxs-lookup"><span data-stu-id="ca73d-304">Open **Site.Master** and locate the **asp:Menu** element.</span></span> <span data-ttu-id="ca73d-305">將游標放在開始標記上，並注意在專案底部顯示的小型字元-按一下以開啟 [智慧型工作] 功能表。</span><span class="sxs-lookup"><span data-stu-id="ca73d-305">Place the cursor on the start tag and notice that the small glyph displayed at the bottom of the element - click it to open the smart tasks menu.</span></span> <span data-ttu-id="ca73d-306">請注意，您可以快速存取與功能表控制項相關的某些工作。</span><span class="sxs-lookup"><span data-stu-id="ca73d-306">Notice that you have quick access to some tasks related to the Menu control.</span></span>

    <span data-ttu-id="ca73d-307">![Menu 控制項的智慧型工作](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Menu 控制項的智慧型工作")</span><span class="sxs-lookup"><span data-stu-id="ca73d-307">![Smart tasks for the Menu control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Smart tasks for the Menu control")</span></span>

    <span data-ttu-id="ca73d-308">*Menu 控制項的智慧型工作*</span><span class="sxs-lookup"><span data-stu-id="ca73d-308">*Smart tasks for the Menu control*</span></span>

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a><span data-ttu-id="ca73d-309">工作 5-智慧型縮排</span><span class="sxs-lookup"><span data-stu-id="ca73d-309">Task 5 - Smart Indentation</span></span>

<span data-ttu-id="ca73d-310">HTML 中的其中一個最佳做法是縮排嵌套的元素，讓程式碼可讀取。</span><span class="sxs-lookup"><span data-stu-id="ca73d-310">One of the best practices in HTML is indenting the nested elements to keep the code readable.</span></span> <span data-ttu-id="ca73d-311">在 Visual Studio 2012 中，您會注意到，當您撰寫程式碼時，編輯器會自動縮排元素。</span><span class="sxs-lookup"><span data-stu-id="ca73d-311">In Visual Studio 2012, you will notice that the editor automatically indents the elements while you are writing the code.</span></span>

> [!NOTE]
> <span data-ttu-id="ca73d-312">在舊版的 Visual Studio 中，智慧型縮排可以在 XML 編輯器中使用，但在 HTML 編輯器中則不提供。</span><span class="sxs-lookup"><span data-stu-id="ca73d-312">In previous version of Visual Studio, smart indentation was available in the XML editor but not in the HTML editor.</span></span>

1. <span data-ttu-id="ca73d-313">請確定 [HTML 編輯器] 上的 [縮排設定] 已設為 [智慧型縮排]。</span><span class="sxs-lookup"><span data-stu-id="ca73d-313">Make sure that the Indenting configuration on the HTML Editor is set to Smart Indentation.</span></span> <span data-ttu-id="ca73d-314">若要這麼做，請選取 [**工具] |[選項**] 功能表選項，然後選取 [**文字編輯器] |HTML |[索引**標籤] 頁面，位於畫面的左窗格中。</span><span class="sxs-lookup"><span data-stu-id="ca73d-314">To do that, select the **Tools | Options** menu option and then select the **Text Editor | HTML | Tabs** page in the left pane of the screen.</span></span> <span data-ttu-id="ca73d-315">選取 [智慧型縮排] 選項。</span><span class="sxs-lookup"><span data-stu-id="ca73d-315">Select the Smart indentation option.</span></span>

    <span data-ttu-id="ca73d-316">![HTML 編輯器設定](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML 編輯器設定")</span><span class="sxs-lookup"><span data-stu-id="ca73d-316">![HTML Editor settings](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML Editor settings")</span></span>

    <span data-ttu-id="ca73d-317">*HTML 編輯器設定*</span><span class="sxs-lookup"><span data-stu-id="ca73d-317">*HTML Editor settings*</span></span>
2. <span data-ttu-id="ca73d-318">在**default.aspx**頁面上，移除 [音訊] 元素下的所有內容。</span><span class="sxs-lookup"><span data-stu-id="ca73d-318">On the **Default.aspx** page, remove all the content under the audio element.</span></span>
3. <span data-ttu-id="ca73d-319">將游標放在開頭**音訊**元素的結尾，然後按**ENTER 鍵**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-319">Place the cursor at the end of the opening **audio** element and hit **ENTER**.</span></span>

    <span data-ttu-id="ca73d-320">請注意，資料指標的新位置有額外的縮排層級。</span><span class="sxs-lookup"><span data-stu-id="ca73d-320">Notice that the new position of cursor has an additional indentation level.</span></span>

    <span data-ttu-id="ca73d-321">![HTML 編輯器中的智慧型縮排](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "HTML 編輯器中的智慧型縮排")</span><span class="sxs-lookup"><span data-stu-id="ca73d-321">![Smart indentation in the HTML Editor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "Smart indentation in the HTML Editor")</span></span>

    <span data-ttu-id="ca73d-322">*HTML 編輯器中的智慧型縮排*</span><span class="sxs-lookup"><span data-stu-id="ca73d-322">*Smart indentation in the HTML Editor*</span></span>
4. <span data-ttu-id="ca73d-323">使用已移除的內容還原音訊標記，或關閉**default.aspx**而不儲存變更。</span><span class="sxs-lookup"><span data-stu-id="ca73d-323">Restore the audio tag with the content you have removed, or close **Default.aspx** without saving the changes.</span></span>

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a><span data-ttu-id="ca73d-324">工作 6-解壓縮至使用者控制項</span><span class="sxs-lookup"><span data-stu-id="ca73d-324">Task 6 - Extract to User Control</span></span>

<span data-ttu-id="ca73d-325">包含在 Visual Studio 中的重構工具（例如，將部分程式碼解壓縮至函式）是很棒的功能，可協助改善和重構現有的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ca73d-325">The Refactoring tools included in Visual Studio, such as extracting a portion of code to a function, are great features that facilitate the improvement and the refactoring the existing code.</span></span> <span data-ttu-id="ca73d-326">ASP.NET 網頁的對應項就是將 HTML 程式碼解壓縮至使用者控制項。</span><span class="sxs-lookup"><span data-stu-id="ca73d-326">The counterpart for ASP.NET pages would be the extraction of HTML code to a User Control.</span></span> <span data-ttu-id="ca73d-327">手動執行作業牽涉到幾個步驟，例如建立新的使用者控制項、將程式碼區段移至使用者控制項、註冊使用者控制項的標記前置詞，最後再將頁面上的使用者控制項具現化。</span><span class="sxs-lookup"><span data-stu-id="ca73d-327">Doing it manually would involve several steps, like creating a new User Control, moving the code section to the User Control, registering a tag prefix for the User Control, and, finally, instantiating the User Control on the pages.</span></span> <span data-ttu-id="ca73d-328">現在，新的 [*解壓縮至使用者控制*] 工具會自動為您執行所有這些步驟。</span><span class="sxs-lookup"><span data-stu-id="ca73d-328">Now, the new *Extract to User Control* tool automatically performs all those steps for you.</span></span>

<span data-ttu-id="ca73d-329">在這項工作中，您將使用新的 [解壓縮至使用者控制項] 內容作業，從選取的程式碼產生新的使用者控制項。</span><span class="sxs-lookup"><span data-stu-id="ca73d-329">In this task, you will use the new Extract to User Control contextual operation to generate a new user control from the selected code.</span></span>

1. <span data-ttu-id="ca73d-330">在 [ **default.aspx** ] 頁面上，選取 [ **H2** ] 和 [**音訊**] 元素。</span><span class="sxs-lookup"><span data-stu-id="ca73d-330">On the **Default.aspx** page, select the **H2** and **audio** elements.</span></span>
2. <span data-ttu-id="ca73d-331">按一下滑鼠右鍵，然後選取 [**解壓縮至使用者控制項**]。</span><span class="sxs-lookup"><span data-stu-id="ca73d-331">Right click and select **Extract to User Control**.</span></span>

    <span data-ttu-id="ca73d-332">![[解壓縮至使用者控制項] 功能表選項](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "[解壓縮至使用者控制項] 功能表選項")</span><span class="sxs-lookup"><span data-stu-id="ca73d-332">![Extract to User Control menu option](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "Extract to User Control menu option")</span></span>

    <span data-ttu-id="ca73d-333">*[解壓縮至使用者控制項] 功能表選項*</span><span class="sxs-lookup"><span data-stu-id="ca73d-333">*Extract to User Control menu option*</span></span>
3. <span data-ttu-id="ca73d-334">輸入新使用者控制項的名稱。</span><span class="sxs-lookup"><span data-stu-id="ca73d-334">Type a name for the new user control.</span></span> <span data-ttu-id="ca73d-335">例如，[ **Jukebox**]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="ca73d-335">For instance, **Jukebox.ascx**, and then click **OK**.</span></span>

    <span data-ttu-id="ca73d-336">![儲存已解壓縮的使用者控制項](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "儲存已解壓縮的使用者控制項")</span><span class="sxs-lookup"><span data-stu-id="ca73d-336">![Saving the extracted user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "Saving the extracted user control")</span></span>

    <span data-ttu-id="ca73d-337">*儲存已解壓縮的使用者控制項*</span><span class="sxs-lookup"><span data-stu-id="ca73d-337">*Saving the extracted user control*</span></span>
4. <span data-ttu-id="ca73d-338">請注意，選取的程式碼已解壓縮至使用者控制項，而所選取程式碼的原始位置已取代為新使用者控制項的實例。</span><span class="sxs-lookup"><span data-stu-id="ca73d-338">Notice that the selected code was extracted to a user control and the original location of the selected code was replaced with an instance of the new user control.</span></span>

    <span data-ttu-id="ca73d-339">![頁面會自動更新以使用新的使用者控制項](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "頁面會自動更新以使用新的使用者控制項")</span><span class="sxs-lookup"><span data-stu-id="ca73d-339">![Page automatically updated to use the new user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "Page automatically updated to use the new user control")</span></span>

    <span data-ttu-id="ca73d-340">*頁面會自動更新以使用新的使用者控制項*</span><span class="sxs-lookup"><span data-stu-id="ca73d-340">*Page automatically updated to use the new user control*</span></span>
5. <span data-ttu-id="ca73d-341">按**F5**執行頁面，並確認控制項可以運作。</span><span class="sxs-lookup"><span data-stu-id="ca73d-341">Press **F5** to run the page and verify that the control works.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a><span data-ttu-id="ca73d-342">練習3： JavaScript 編輯器的新功能</span><span class="sxs-lookup"><span data-stu-id="ca73d-342">Exercise 3: What's New in the JavaScript Editor</span></span>

<span data-ttu-id="ca73d-343">撰寫或編輯 JavaScript 程式碼不是簡單的工作，特別是當您的應用程式開始變大時，您會發現自己處理的是長檔案和數以百計的功能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-343">Writing or editing JavaScript code is not an easy task, especially when your application starts to grow in size and you find yourself dealing with long files and hundreds of functions.</span></span> <span data-ttu-id="ca73d-344">腳本開發人員通常必須執行一些額外的工作，以維護程式碼的可讀性，並跨檔案進行流覽。</span><span class="sxs-lookup"><span data-stu-id="ca73d-344">Script developers usually have to do some extra work to maintain code legibility and navigate across files.</span></span> <span data-ttu-id="ca73d-345">隨著 jQuery 這類 JavaScript 程式庫的包含，腳本導覽也會因為程式碼長度而變得很困難。</span><span class="sxs-lookup"><span data-stu-id="ca73d-345">With the inclusion of JavaScript libraries like jQuery, script navigation has become a challenge itself because of the code length.</span></span>

<span data-ttu-id="ca73d-346">Visual Studio 已更新 JavaScript 編輯器，使其具備可供存取和組織程式碼模式的承諾。</span><span class="sxs-lookup"><span data-stu-id="ca73d-346">Visual Studio has renewed the JavaScript editor with the promise to make the code mode accessible and organized.</span></span> <span data-ttu-id="ca73d-347">已經存在C#或 VB 編輯器中的許多 Visual Studio 功能現在都是在 JavaScript 編輯器中執行： [移至定義]、[自動縮排]、[檔集] 和 [驗證] （當您撰寫時）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-347">Many Visual Studio features that already existed in C# or VB editors are now implemented in the JavaScript editor: Go To Definition, automatic indentation, documentation and validation when you are writing.</span></span> <span data-ttu-id="ca73d-348">在更新的 IntelliSense 清單中，您可以輕鬆地擁有 JavaScript 函數目錄。</span><span class="sxs-lookup"><span data-stu-id="ca73d-348">With the renewed IntelliSense list you will have the JavaScript function catalog at your fingertips.</span></span>

<span data-ttu-id="ca73d-349">在此練習中，您將瞭解 JavaScript 編輯器的一些新功能和改進。</span><span class="sxs-lookup"><span data-stu-id="ca73d-349">In this exercise, you will learn some of the new features and improvements of JavaScript editor.</span></span> <span data-ttu-id="ca73d-350">您將流覽範例檔案，並探索每個新特性，讓您的 JavaScript 程式設計在 Visual Studio 2012 內更有效率。</span><span class="sxs-lookup"><span data-stu-id="ca73d-350">You will browse sample files and discover each of the new characteristics that will make your JavaScript programming more efficient within Visual Studio 2012.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a><span data-ttu-id="ca73d-351">工作 1-JavaScript 編輯器的新功能</span><span class="sxs-lookup"><span data-stu-id="ca73d-351">Task 1 - JavaScript Editor New Features</span></span>

<span data-ttu-id="ca73d-352">這項工作會向您介紹一些新的 JavaScript 編輯器功能，其中著重于組織您的程式碼，並提供更好的使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="ca73d-352">This task will introduce you to some of the new JavaScript editor features, which focus on organizing your code and bringing a better user experience.</span></span>

1. <span data-ttu-id="ca73d-353">如果尚未開啟，請啟動**Visual Studio** ，然後開啟位於此實驗室的**Source\WhatsNewASPNET**資料夾中的**WhatsNewASPNET。**</span><span class="sxs-lookup"><span data-stu-id="ca73d-353">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="ca73d-354">按**F5**執行應用程式，然後按一下巡覽列中的 [JavaScript] 連結。</span><span class="sxs-lookup"><span data-stu-id="ca73d-354">Press **F5** to run the application, then click the JavaScript link in the navigation bar.</span></span> <span data-ttu-id="ca73d-355">重新整理頁面數次，並檢查計數器的遞增方式。</span><span class="sxs-lookup"><span data-stu-id="ca73d-355">Refresh the page several times and check how the counter increments.</span></span>

    <span data-ttu-id="ca73d-356">![頁面計數器](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "頁面計數器")</span><span class="sxs-lookup"><span data-stu-id="ca73d-356">![Page counter](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "Page counter")</span></span>

    <span data-ttu-id="ca73d-357">*頁面計數器*</span><span class="sxs-lookup"><span data-stu-id="ca73d-357">*Page counter*</span></span>
3. <span data-ttu-id="ca73d-358">關閉瀏覽器，然後返回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ca73d-358">Close the browser and go back to Visual Studio.</span></span>
4. <span data-ttu-id="ca73d-359">開啟 [ **JavaScript .aspx** ] 頁面，並找出 **&lt;腳本&gt;** 區塊（如下所示）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-359">Open the **JavaScript.aspx** page and locate the **&lt;script&gt;** block (shown below).</span></span>

    <span data-ttu-id="ca73d-360">下列程式碼會使用 HTML5 本機儲存區來儲存*pageLoadCount*變數，以儲存目前使用者已造訪過頁面的次數。</span><span class="sxs-lookup"><span data-stu-id="ca73d-360">The following code uses HTML5 local storage to store a *pageLoadCount* variable that stores the number of times the page has been visited by the current user.</span></span> <span data-ttu-id="ca73d-361">本機儲存體是以 HTML5 標準引進的用戶端索引鍵/值資料庫。</span><span class="sxs-lookup"><span data-stu-id="ca73d-361">Local Storage is a client-side key-value database introduced with the HTML5 standard.</span></span> <span data-ttu-id="ca73d-362">資料會儲存在本機電腦上的使用者瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="ca73d-362">The data is saved on the local machine, inside the user's browser.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="ca73d-363">請先確定 DOCTYPE 已設定為 XHTML5，再繼續進行後續步驟。</span><span class="sxs-lookup"><span data-stu-id="ca73d-363">Ensure the DOCTYPE is set to XHTML5 before proceeding with the next steps.</span></span>
5. <span data-ttu-id="ca73d-364">編輯程式碼，並注意適用于 JavaScript 的 IntelliSense 包含 HTML5 功能，例如本機儲存體和其內部方法。</span><span class="sxs-lookup"><span data-stu-id="ca73d-364">Edit the code and notice that IntelliSense for JavaScript includes HTML5 features, like local storage, and their inner methods.</span></span>

    <span data-ttu-id="ca73d-365">![JavaScript 中的 HTML5 JavaScript 功能](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "JavaScript 中的 HTML5 JavaScript 功能")</span><span class="sxs-lookup"><span data-stu-id="ca73d-365">![HTML5 JavaScript features in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "HTML5 JavaScript features in JavaScript")</span></span>

    <span data-ttu-id="ca73d-366">*JavaScript 中的 HTML5 JavaScript 功能*</span><span class="sxs-lookup"><span data-stu-id="ca73d-366">*HTML5 JavaScript features in JavaScript*</span></span>
6. <span data-ttu-id="ca73d-367">按一下腳本程式碼中的任何左括弧（ **{** ），並注意括弧會反白顯示。</span><span class="sxs-lookup"><span data-stu-id="ca73d-367">Click any opening bracket (**{**) from the scripting code and notice that the brackets are highlighted.</span></span>

    <span data-ttu-id="ca73d-368">![括弧會反白顯示](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "括弧會反白顯示")</span><span class="sxs-lookup"><span data-stu-id="ca73d-368">![Brackets are highlighted](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "Brackets are highlighted")</span></span>

    <span data-ttu-id="ca73d-369">*括弧會反白顯示*</span><span class="sxs-lookup"><span data-stu-id="ca73d-369">*Brackets are highlighted*</span></span>
7. <span data-ttu-id="ca73d-370">取消批註函數**testAutoAlign （）** （選取三行，您可以使用**CTRL** + **K**;**CTRL** + **U**），並找出函式程式碼內的游標。</span><span class="sxs-lookup"><span data-stu-id="ca73d-370">Uncomment the function **testAutoAlign()** (select the three lines and you can use **CTRL** + **K**; **CTRL** + **U**) and locate the cursor inside the function code.</span></span> <span data-ttu-id="ca73d-371">按 enter 鍵以附加第二行。</span><span class="sxs-lookup"><span data-stu-id="ca73d-371">Press enter to append a second line.</span></span> <span data-ttu-id="ca73d-372">請注意，程式碼現在已**對齊**並**自動縮排**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-372">Notice that the code is now **aligned** and **auto-indented**.</span></span>

    <span data-ttu-id="ca73d-373">![JavaScript 程式碼已自動對齊](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript 程式碼已自動對齊")</span><span class="sxs-lookup"><span data-stu-id="ca73d-373">![JavaScript code is auto aligned](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript code is auto aligned")</span></span>

    <span data-ttu-id="ca73d-374">*JavaScript 程式碼已自動對齊*</span><span class="sxs-lookup"><span data-stu-id="ca73d-374">*JavaScript code is auto aligned*</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a><span data-ttu-id="ca73d-375">工作 2-驗證 JavaScript</span><span class="sxs-lookup"><span data-stu-id="ca73d-375">Task 2 - Validating JavaScript</span></span>

<span data-ttu-id="ca73d-376">在這項工作中，您將探索 ECMAScript5 standard 的新 JavaScript 驗證。</span><span class="sxs-lookup"><span data-stu-id="ca73d-376">In this task, you will discover the new JavaScript validation for the ECMAScript5 standard.</span></span> <span data-ttu-id="ca73d-377">這項功能可協助您撰寫相容的 JavaScript 程式碼，同時在網站部署之前防止腳本問題。</span><span class="sxs-lookup"><span data-stu-id="ca73d-377">This feature will help you to write compliant JavaScript code, while preventing scripting issues before site deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="ca73d-378">Visual Studio 2010 實行 ECMAStript3 合規性，而 Visual Studio 2012 則提供 ECMAScript5 合規性。</span><span class="sxs-lookup"><span data-stu-id="ca73d-378">Visual Studio 2010 implemented ECMAStript3 compliance, while Visual Studio 2012 provides ECMAScript5 compliance.</span></span>

1. <span data-ttu-id="ca73d-379">開啟位於**Scripts\custom**專案資料夾底下的**ECMA5script5** 。</span><span class="sxs-lookup"><span data-stu-id="ca73d-379">Open **ECMA5script5.js** located under the **Scripts\custom** project folder.</span></span> <span data-ttu-id="ca73d-380">您現在會測試 ECMAScript5 standard 的驗證。</span><span class="sxs-lookup"><span data-stu-id="ca73d-380">You will now test validation for ECMAScript5 standard.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    <span data-ttu-id="ca73d-381">您可以在檔案的第一行中查看 &quot;**使用嚴格**的 &quot; 方向，這會啟用 ECMAScript5 **strict 模式**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-381">You can check out the &quot; **use strict** &quot; direction in the first line of the file, which enables ECMAScript5 **strict mode**.</span></span> <span data-ttu-id="ca73d-382">這個模式是由語言的子集所組成，其中包含過去版本的多義性，並加入一些新功能，例如 getter 和 setter、JSON 的程式庫支援，以及更完整的物件屬性反映。</span><span class="sxs-lookup"><span data-stu-id="ca73d-382">This mode consists in a subset of the language that clarifies ambiguities from the past edition, and adds some new features, such as getters and setters, library support for JSON, and more complete reflection on object properties.</span></span>
2. <span data-ttu-id="ca73d-383">開啟 [**錯誤清單**] （如果尚未開啟）（[**視圖**] 功能表 |**錯誤清單**）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-383">Open the **Error List** if not already opened (**View** menu | **Error List**).</span></span> <span data-ttu-id="ca73d-384">請注意，**函數**聲明會加上底線。</span><span class="sxs-lookup"><span data-stu-id="ca73d-384">Notice the **function** declaration is underlined.</span></span> <span data-ttu-id="ca73d-385">這是因為在 ECMA5 標準函式中，不能嵌套于語言結構內部。</span><span class="sxs-lookup"><span data-stu-id="ca73d-385">This is because in ECMA5 standard functions cannot be nested inside language structures.</span></span> <span data-ttu-id="ca73d-386">在下面的 [錯誤清單] 中，您會看到警告詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ca73d-386">In the error list below you will see the warning details.</span></span>

    <span data-ttu-id="ca73d-387">![JavaScript 驗證錯誤訊息](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript 驗證錯誤訊息")</span><span class="sxs-lookup"><span data-stu-id="ca73d-387">![JavaScript validation error message](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript validation error message")</span></span>

    <span data-ttu-id="ca73d-388">*JavaScript 驗證錯誤訊息*</span><span class="sxs-lookup"><span data-stu-id="ca73d-388">*JavaScript validation error message*</span></span>
3. <span data-ttu-id="ca73d-389">批註外 **&quot;使用嚴格的&quot;** 方向，並注意錯誤會消失，但仍會出現警告。</span><span class="sxs-lookup"><span data-stu-id="ca73d-389">Comment out the **&quot;use strict&quot;** direction and notice that errors disappear, but the warnings remain.</span></span>
4. <span data-ttu-id="ca73d-390">在檔案的最後一行中，寫入任何字串（例如 **&quot;測試&quot;** （包含引號來表示它是字串）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-390">In the last line of the file, write any string like **&quot;test&quot;** (include the quotation marks to indicate it is as string).</span></span> <span data-ttu-id="ca73d-391">在字串旁邊撰寫一個句點以顯示 IntelliSense 清單，然後選取 [**修剪**] 選項。</span><span class="sxs-lookup"><span data-stu-id="ca73d-391">Write a period next to the string to display the IntelliSense list, and select the **trim** option.</span></span>

    <span data-ttu-id="ca73d-392">在 ECMAScript5 standard 中，字串值和變數也會定義字串方法，例如 trim、大寫、搜尋和取代。</span><span class="sxs-lookup"><span data-stu-id="ca73d-392">In ECMAScript5 standard, string values and variables also have string methods defined, like trim, uppercase, search and replace.</span></span>

    <span data-ttu-id="ca73d-393">![JavaScript 中的 IntelliSense 清單](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "JavaScript 中的 IntelliSense 清單")</span><span class="sxs-lookup"><span data-stu-id="ca73d-393">![IntelliSense list in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "IntelliSense list in JavaScript")</span></span>

    <span data-ttu-id="ca73d-394">*JavaScript 中的 IntelliSense 清單*</span><span class="sxs-lookup"><span data-stu-id="ca73d-394">*IntelliSense list in JavaScript*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a><span data-ttu-id="ca73d-395">工作 3-JavaScript 的 XML 檔</span><span class="sxs-lookup"><span data-stu-id="ca73d-395">Task 3 - XML Documentation for JavaScript</span></span>

<span data-ttu-id="ca73d-396">在這項工作中，您將探索 JavaScript 中的 XML 檔 Visual Studio 功能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-396">In this task, you will explore Visual Studio features for XML documentation in JavaScript.</span></span> <span data-ttu-id="ca73d-397">您會看到 JavaScript IntelliSense 清單現在會顯示每個函式的 XML 檔。</span><span class="sxs-lookup"><span data-stu-id="ca73d-397">You will see the JavaScript IntelliSense list now shows the XML documentation of each function.</span></span> <span data-ttu-id="ca73d-398">此外，您將探索 JavaScript 中的導覽功能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-398">Additionally, you will discover the navigation feature in JavaScript.</span></span>

1. <span data-ttu-id="ca73d-399">開啟位於**腳本/自訂**專案資料夾中的**XMLDoc。**</span><span class="sxs-lookup"><span data-stu-id="ca73d-399">Open **XMLDoc.js** file located in **Scripts/custom** project folder.</span></span> <span data-ttu-id="ca73d-400">此檔案包含每個 JavaScript 函數的 XML 檔。</span><span class="sxs-lookup"><span data-stu-id="ca73d-400">This file contains XML documentation on each of the JavaScript functions.</span></span>

    <span data-ttu-id="ca73d-401">![整合至 IntelliSense 的 JavaScript XML 檔](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "整合至 IntelliSense 的 JavaScript XML 檔")</span><span class="sxs-lookup"><span data-stu-id="ca73d-401">![JavaScript XML documentation integrated to IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "JavaScript XML documentation integrated to IntelliSense")</span></span>

    <span data-ttu-id="ca73d-402">*整合至 IntelliSense 的 JavaScript XML 檔*</span><span class="sxs-lookup"><span data-stu-id="ca73d-402">*JavaScript XML documentation integrated to IntelliSense*</span></span>
2. <span data-ttu-id="ca73d-403">在**XMLDoc**的 **[新增函式] 底下，** 建立名為**test**的新函數。</span><span class="sxs-lookup"><span data-stu-id="ca73d-403">Below **add** function in **XMLDoc.js** file, create a new function named **test**.</span></span>
3. <span data-ttu-id="ca73d-404">在**測試**函式中，呼叫接收兩個參數的**乘法**函數。</span><span class="sxs-lookup"><span data-stu-id="ca73d-404">In the **test** function, call the **multiply** function that receives two parameters.</span></span> <span data-ttu-id="ca73d-405">請注意，[工具提示] 方塊會顯示 [**乘法**函數] 檔。</span><span class="sxs-lookup"><span data-stu-id="ca73d-405">Notice the tooltip box is showing the **multiply** function documentation.</span></span>

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    <span data-ttu-id="ca73d-406">![JavaScript 函式的 XML 檔](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "JavaScript 函式的 XML 檔")</span><span class="sxs-lookup"><span data-stu-id="ca73d-406">![XML documentation for JavaScript functions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "XML documentation for JavaScript functions")</span></span>

    <span data-ttu-id="ca73d-407">*JavaScript 函式的 XML 檔*</span><span class="sxs-lookup"><span data-stu-id="ca73d-407">*XML documentation for JavaScript functions*</span></span>
4. <span data-ttu-id="ca73d-408">完成函式呼叫語句，並輸入一個*點*來開啟所傳回值的 IntelliSense 清單。</span><span class="sxs-lookup"><span data-stu-id="ca73d-408">Complete the function call statement and type a *dot* to open the IntelliSense list on the returned value.</span></span> <span data-ttu-id="ca73d-409">請注意，Visual Studio 會偵測檔中的**傳回值，** 並將該值視為數位。</span><span class="sxs-lookup"><span data-stu-id="ca73d-409">Notice that Visual Studio is detecting the **return** value in the documentation, treating the value as a number.</span></span>

    <span data-ttu-id="ca73d-410">![傳回類型的 XML 檔](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "傳回類型的 XML 檔")</span><span class="sxs-lookup"><span data-stu-id="ca73d-410">![XML documentation for return types](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "XML documentation for return types")</span></span>

    <span data-ttu-id="ca73d-411">*傳回類型的 XML 檔*</span><span class="sxs-lookup"><span data-stu-id="ca73d-411">*XML documentation for return types*</span></span>
5. <span data-ttu-id="ca73d-412">現在，插入呼叫以加入函數。</span><span class="sxs-lookup"><span data-stu-id="ca73d-412">Now, insert a call to add function.</span></span> <span data-ttu-id="ca73d-413">請注意，JavaScript 編輯器現在支援函數多載。</span><span class="sxs-lookup"><span data-stu-id="ca73d-413">Notice that the JavaScript editor now supports function overloads.</span></span> <span data-ttu-id="ca73d-414">當您撰寫函式名稱時，您將能夠選取在檔中指定的任何可用的多載。</span><span class="sxs-lookup"><span data-stu-id="ca73d-414">When you write a function name, you will be able to select any of the available overloads specified in the documentation.</span></span>

    <span data-ttu-id="ca73d-415">![多載的 XML 檔](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "多載的 XML 檔")</span><span class="sxs-lookup"><span data-stu-id="ca73d-415">![XML documentation for overloads](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "XML documentation for overloads")</span></span>

    <span data-ttu-id="ca73d-416">*多載的 XML 檔*</span><span class="sxs-lookup"><span data-stu-id="ca73d-416">*XML documentation for overloads*</span></span>
6. <span data-ttu-id="ca73d-417">開啟**GotoDefinition** ，並找出 **$ （） .html （）** 函式呼叫。</span><span class="sxs-lookup"><span data-stu-id="ca73d-417">Open **GotoDefinition.js** file and locate the **$().html()** function call.</span></span> <span data-ttu-id="ca73d-418">在**html**上尋找游標。</span><span class="sxs-lookup"><span data-stu-id="ca73d-418">Locate the cursor on **html**.</span></span>
7. <span data-ttu-id="ca73d-419">按**F12**並流覽至定義。</span><span class="sxs-lookup"><span data-stu-id="ca73d-419">Press **F12** and navigate to the definition.</span></span> <span data-ttu-id="ca73d-420">請注意，您現在可以存取和流覽 JavaScript 程式碼，而不需要使用 [**尋找**] 工具。</span><span class="sxs-lookup"><span data-stu-id="ca73d-420">Notice you can now access and browse your JavaScript code without using the **Find** tool.</span></span>
8. <span data-ttu-id="ca73d-421">在程式碼檔案底部的簽章區塊之前，于 jQuery 指令上尋找游標。</span><span class="sxs-lookup"><span data-stu-id="ca73d-421">Locate the cursor on the jQuery instruction prior to the signature block at the bottom of the code file.</span></span> <span data-ttu-id="ca73d-422">按**F12**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-422">Press **F12**.</span></span> <span data-ttu-id="ca73d-423">您將流覽至 jQuery 程式庫檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-423">You will navigate to the jQuery library file.</span></span> <span data-ttu-id="ca73d-424">請注意，您也可以使用**F12**跨 jQuery 檔案進行流覽。</span><span class="sxs-lookup"><span data-stu-id="ca73d-424">Notice you can also navigate across the jQuery files using **F12**.</span></span>

    <span data-ttu-id="ca73d-425">![導覽至 jQuery 定義](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "導覽至 jQuery 定義")</span><span class="sxs-lookup"><span data-stu-id="ca73d-425">![Navigating to jQuery definitions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "Navigating to jQuery definitions")</span></span>

    <span data-ttu-id="ca73d-426">*導覽至 jQuery 定義*</span><span class="sxs-lookup"><span data-stu-id="ca73d-426">*Navigating to jQuery definitions*</span></span>

> [!NOTE]
> <span data-ttu-id="ca73d-427">在儲存檔案之前，請確定 GotoDefinition 沒有任何語法錯誤。</span><span class="sxs-lookup"><span data-stu-id="ca73d-427">Make sure that GotoDefinition.js has no syntax errors before saving the file.</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a><span data-ttu-id="ca73d-428">練習4：捆綁和縮制</span><span class="sxs-lookup"><span data-stu-id="ca73d-428">Exercise 4: Bundling and Minification</span></span>

<span data-ttu-id="ca73d-429">您的網站有多少次包含一個以上的 JavaScript 或 CSS 檔案？</span><span class="sxs-lookup"><span data-stu-id="ca73d-429">How many times do your websites include more than one JavaScript or CSS file?</span></span> <span data-ttu-id="ca73d-430">這是一個很常見的案例，其中的組合和縮制有助於減少檔案大小，並讓網站執行速度更快。</span><span class="sxs-lookup"><span data-stu-id="ca73d-430">This is a very common scenario where bundling and minification can help to reduce the file size and make the site perform faster.</span></span> <span data-ttu-id="ca73d-431">ASP.NET 4.5 中的新配套功能會將一組 JS 或 CSS 檔案封裝成單一專案，並藉由縮小內容來減少其大小（也就是移除不必要的空格、移除批註、減少識別碼）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-431">The new bundling feature in ASP.NET 4.5 packs a set of JS or CSS files into a single element, and reduces its size by minifying the content ( i.e. removing not required blank spaces, removing comments, reducing identifiers ).</span></span>

<span data-ttu-id="ca73d-432">ASP.NET 4.5 中的組合和縮制是在執行時間執行，因此，進程可以識別使用者代理程式（例如 IE、Mozilla 等等），並藉由鎖定使用者瀏覽器（例如，移除 Mozilla 特定的內容）來改善壓縮。當要求來自 IE 時）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-432">Bundling and minification in ASP.NET 4.5 is performed at runtime, so that the process can identify the user agent (for example IE, Mozilla, etc), and thus, improve the compression by targeting the user browser (for instance, removing stuff that is Mozilla specific when the request comes from IE).</span></span>

<span data-ttu-id="ca73d-433">在此練習中，您將瞭解如何在 ASP.NET 4.5 中啟用和使用不同類型的組合和縮制。</span><span class="sxs-lookup"><span data-stu-id="ca73d-433">In this exercise, you will learn how to enable and use the different types of bundling and minification in ASP.NET 4.5.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a><span data-ttu-id="ca73d-434">工作 1-從 NuGet 安裝封裝和縮制套件</span><span class="sxs-lookup"><span data-stu-id="ca73d-434">Task 1 - Installing the Bundling and Minification Package from NuGet</span></span>

1. <span data-ttu-id="ca73d-435">如果尚未開啟，請啟動**Visual Studio** ，然後開啟位於此實驗室的**Source\WhatsNewASPNET**資料夾中的**WhatsNewASPNET。**</span><span class="sxs-lookup"><span data-stu-id="ca73d-435">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="ca73d-436">開啟 NuGet 套件管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="ca73d-436">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="ca73d-437">若要這麼做，請使用功能表**視圖** | **其他 Windows** | **套件管理員主控台**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-437">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>

    <span data-ttu-id="ca73d-438">![開啟封裝管理員 file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "開啟套件管理員主控台")</span><span class="sxs-lookup"><span data-stu-id="ca73d-438">![Opening the package manager file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "Opening the package manager console")</span></span>

    <span data-ttu-id="ca73d-439">*開啟套件管理員主控台*</span><span class="sxs-lookup"><span data-stu-id="ca73d-439">*Opening the package manager console*</span></span>
3. <span data-ttu-id="ca73d-440">在 [**套件管理員主控台**] 中，輸入**Install-Package** Web.config，然後按**enter**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-440">In the **Package Manager Console,** type **Install-Package Microsoft.Web.Optimization** and press **ENTER**.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a><span data-ttu-id="ca73d-441">工作 2-預設組合</span><span class="sxs-lookup"><span data-stu-id="ca73d-441">Task 2 - Default Bundles</span></span>

<span data-ttu-id="ca73d-442">使用配套和縮制最簡單的方式，就是啟用預設組合。</span><span class="sxs-lookup"><span data-stu-id="ca73d-442">The simplest way to use bundling and minification is to enable the default bundles.</span></span> <span data-ttu-id="ca73d-443">這個方法會使用慣例，讓您參考資料夾中 JS 和 CSS 檔案的配套和縮減版本。</span><span class="sxs-lookup"><span data-stu-id="ca73d-443">This method uses conventions to let you reference the bundled and minified version for the JS and CSS files in a folder.</span></span>

<span data-ttu-id="ca73d-444">在這項工作中，您將學習如何啟用和參考配套的和縮減 JS 和 CSS 檔案，並查看產生的輸出。</span><span class="sxs-lookup"><span data-stu-id="ca73d-444">In this task, you will learn how to enable and reference the bundled and minified JS and CSS files and view the resulting output.</span></span>

1. <span data-ttu-id="ca73d-445">如果尚未開啟，請啟動**Visual Studio** ，然後開啟位於此實驗室的**Source\WhatsNewASPNET**資料夾中的**WhatsNewASPNET。**</span><span class="sxs-lookup"><span data-stu-id="ca73d-445">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="ca73d-446">在 **方案總管**中，展開 **樣式**、 **Scripts\custom**  和  **Scripts\bundle**  資料夾。</span><span class="sxs-lookup"><span data-stu-id="ca73d-446">In the **Solution Explorer**, expand the **Styles**, **Scripts\custom** and **Scripts\bundle** folders.</span></span>

    <span data-ttu-id="ca73d-447">請注意，應用程式會使用一個以上的 CSS 和 JS 檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-447">Notice that the application is using more than one CSS and JS file.</span></span>

    <span data-ttu-id="ca73d-448">![應用程式中的多個樣式表單和 JavaScript 檔案](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "應用程式中的多個樣式表單和 JavaScript 檔案")</span><span class="sxs-lookup"><span data-stu-id="ca73d-448">![Multiple Stylesheets and JavaScript files in the application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "Multiple Stylesheets and JavaScript files in the application")</span></span>

    <span data-ttu-id="ca73d-449">*應用程式中的多個樣式表單和 JavaScript 檔案*</span><span class="sxs-lookup"><span data-stu-id="ca73d-449">*Multiple Stylesheets and JavaScript files in the application*</span></span>
3. <span data-ttu-id="ca73d-450">開啟**Global.asax.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-450">Open the **Global.asax.cs** file.</span></span>

    <span data-ttu-id="ca73d-451">請注意，新的**Microsoft. Web. 優化**命名空間在檔案開頭會加上批註。</span><span class="sxs-lookup"><span data-stu-id="ca73d-451">Notice that the new **Microsoft.Web.Optimization** namespace is commented out at the beginning of the file.</span></span> <span data-ttu-id="ca73d-452">取消批註 using 指示詞，以包含捆綁和縮制功能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-452">Uncomment the using directive to include the bundling and minification features.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. <span data-ttu-id="ca73d-453">找出**應用程式\_Start**方法。</span><span class="sxs-lookup"><span data-stu-id="ca73d-453">Locate the **Application\_Start** method.</span></span>

    <span data-ttu-id="ca73d-454">在此方法中，取消批註 EnableDefaultBundles 呼叫，如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="ca73d-454">In this method, uncomment the EnableDefaultBundles call as shown in the snippet below.</span></span> <span data-ttu-id="ca73d-455">這可讓我們使用資料夾的路徑，以及 &quot;CSS&quot; 或 &quot;JS&quot; 尾碼，來參考資料夾中的 CSS 檔案配套集合。</span><span class="sxs-lookup"><span data-stu-id="ca73d-455">This enables us to reference a bundled collection of CSS files in a folder by using the path to that folder, plus the &quot;CSS&quot; or the &quot;JS&quot; suffix.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. <span data-ttu-id="ca73d-456">開啟 [**優化 .aspx**檔案]，並找出**HeadContent**的內容控制項。</span><span class="sxs-lookup"><span data-stu-id="ca73d-456">Open the **Optimization.aspx** file and locate the content control for **HeadContent**.</span></span>

    <span data-ttu-id="ca73d-457">請注意，CSS 檔案和 JS 檔案有一個參考的標記。</span><span class="sxs-lookup"><span data-stu-id="ca73d-457">Notice the CSS files and the JS files have a single referenced tag.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > <span data-ttu-id="ca73d-458">這段程式碼是為了示範之用。</span><span class="sxs-lookup"><span data-stu-id="ca73d-458">This code is for demo purposes.</span></span> <span data-ttu-id="ca73d-459">在理想的情況下，您將會參考網站中的套件組合。</span><span class="sxs-lookup"><span data-stu-id="ca73d-459">Ideally, you will reference the bundles in the Site.Master file.</span></span> <span data-ttu-id="ca73d-460">在此範例程式碼中，您會發現一些配套的檔案也被網站主控檔案參照，因此最後一個參考是多餘的。</span><span class="sxs-lookup"><span data-stu-id="ca73d-460">In this sample code, you will find that some of the bundled files are also being referenced by the Site.Master file, making this last reference redundant.</span></span>
6. <span data-ttu-id="ca73d-461">請注意，連結會使用**href**屬性中的組合慣例，分別從 [樣式] 和 [Scripts\custom] 資料夾取得所有 CSS 或 JS 檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-461">Notice that the links are using the bundling conventions in the **href** attribute to get all the CSS or JS files from the Styles and Scripts\custom folder respectively.</span></span>

    <span data-ttu-id="ca73d-462">您可以使用如下所示的路徑**腳本/自訂/JS** ，在**腳本/自訂**資料夾內組合及縮小所有 JS 檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-462">You can use the path **Scripts/custom/JS** as shown below to bundle and minify all the JS files inside a **Scripts/custom** folder.</span></span> <span data-ttu-id="ca73d-463">這是預設的組合的預設行為。</span><span class="sxs-lookup"><span data-stu-id="ca73d-463">This is the default behavior with the default bundles.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. <span data-ttu-id="ca73d-464">開啟**Styles\Site.css**檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-464">Open the **Styles\Site.css** file.</span></span>

    <span data-ttu-id="ca73d-465">請注意，原始的 CSS 檔案包含縮排的程式碼、空白空格和用來放大檔案的批註。</span><span class="sxs-lookup"><span data-stu-id="ca73d-465">Notice that the original CSS file contains indented code, blank spaces and comments that enlarge the file.</span></span> <span data-ttu-id="ca73d-466">（此外，JavaScript 檔案也包含空格和批註）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-466">(Also the JavaScript file contains blank spaces and comments).</span></span>

    <span data-ttu-id="ca73d-467">![[腳本] 資料夾中的其中一個原始 CSS 檔案](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "[腳本] 資料夾中的其中一個原始 CSS 檔案")</span><span class="sxs-lookup"><span data-stu-id="ca73d-467">![One of the original CSS files in the Scripts folder](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "One of the original CSS files in the Scripts folder")</span></span>

    <span data-ttu-id="ca73d-468">*[腳本] 資料夾中的其中一個原始 CSS 檔案*</span><span class="sxs-lookup"><span data-stu-id="ca73d-468">*One of the original CSS files in the Scripts folder*</span></span>
8. <span data-ttu-id="ca73d-469">按**F5**執行應用程式，並流覽至 [**優化**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="ca73d-469">Press **F5** to run the application and navigate to the **Optimization** page.</span></span>
9. <span data-ttu-id="ca73d-470">按一下 [ **CSS**配套] 連結，以下載並開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-470">Click on the **CSS Bundle** link to download and open the file.</span></span>

    <span data-ttu-id="ca73d-471">查看縮減配套的檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-471">Check out the minified bundled file.</span></span> <span data-ttu-id="ca73d-472">您會發現所有的空格、批註和縮排字元都已移除，產生較小的檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-472">You will notice that all the blank spaces, comments and indentation characters have been removed, generating a smaller file.</span></span>

    <span data-ttu-id="ca73d-473">![配套的 CSS 檔案](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "配套的 CSS 檔案")</span><span class="sxs-lookup"><span data-stu-id="ca73d-473">![Bundled CSS files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "Bundled CSS files")</span></span>

    <span data-ttu-id="ca73d-474">*配套的 CSS 檔案*</span><span class="sxs-lookup"><span data-stu-id="ca73d-474">*Bundled CSS files*</span></span>
10. <span data-ttu-id="ca73d-475">現在，按一下 [ **JS**套件組合] 連結，以開啟 JavaScript 配套的檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-475">Now click the **JS Bundle** link to open the JavaScript bundled file.</span></span> <span data-ttu-id="ca73d-476">您可以放心地忽略 explorer 警告。</span><span class="sxs-lookup"><span data-stu-id="ca73d-476">You can safely disregard the explorer warning.</span></span> <span data-ttu-id="ca73d-477">請注意，**自訂**資料夾下的 JavaScript 檔案也已配套並縮減。</span><span class="sxs-lookup"><span data-stu-id="ca73d-477">Notice the JavaScript files under the **custom** folder are also bundled and minified.</span></span>

    <span data-ttu-id="ca73d-478">![配套的 JavaScript 檔案](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "配套的 JavaScript 檔案")</span><span class="sxs-lookup"><span data-stu-id="ca73d-478">![Bundled JavaScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "Bundled JavaScript files")</span></span>

    <span data-ttu-id="ca73d-479">*配套的 JavaScript 檔案*</span><span class="sxs-lookup"><span data-stu-id="ca73d-479">*Bundled JavaScript files*</span></span>

    <span data-ttu-id="ca73d-480">在先前的 ASP.NET 版本中，啟用 CSS 或 JS 檔案的壓縮更為複雜。</span><span class="sxs-lookup"><span data-stu-id="ca73d-480">Enabling compression for CSS or JS files was much more complicated in previous ASP.NET version.</span></span> <span data-ttu-id="ca73d-481">現在，如您所見，您只需要在*global.asax*檔案中加入一行來啟用組合，然後從您的網站參考配套的檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-481">Now, as you have seen, you just need to add one line in the *Global.asax* file to enable bundling, and then reference the bundled files from your site.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a><span data-ttu-id="ca73d-482">工作 3-靜態組合</span><span class="sxs-lookup"><span data-stu-id="ca73d-482">Task 3 - Static Bundles</span></span>

<span data-ttu-id="ca73d-483">靜態組合方法可讓您自訂要組合的一組檔案、參考和將使用的縮制方法。</span><span class="sxs-lookup"><span data-stu-id="ca73d-483">The static bundle approach allows you to customize the set of files to bundle, the reference and the minification method that will be used.</span></span>

<span data-ttu-id="ca73d-484">在這項工作中，您將設定靜態組合，以定義要配套和縮小的一組特定檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-484">In this task, you will configure a static bundle to define a specific set of files to bundle and minify.</span></span>

1. <span data-ttu-id="ca73d-485">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="ca73d-485">Close the browser.</span></span>
2. <span data-ttu-id="ca73d-486">開啟**Global.asax.cs**檔案，並找出**應用程式\_Start**方法。</span><span class="sxs-lookup"><span data-stu-id="ca73d-486">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
3. <span data-ttu-id="ca73d-487">取消批註靜態組合程式碼，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="ca73d-487">Uncomment the static bundle code as shown in the code below.</span></span>

    <span data-ttu-id="ca73d-488">您正在定義將使用 &quot; **~/StaticBundle**&quot; 虛擬路徑來參考的靜態組合，並使用**JsMinify**來縮制所有具有**AddFile**方法的指定檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-488">You are defining a static bundle that will be referenced with the &quot;**~/StaticBundle**&quot; virtual path and use **JsMinify** for minification of all the specified files with the **AddFile** method.</span></span> <span data-ttu-id="ca73d-489">最後，您會將靜態組合新增至**當**並加以啟用。</span><span class="sxs-lookup"><span data-stu-id="ca73d-489">Finally, you are adding the static bundle to the **BundleTable** and enabling it.</span></span>

    <span data-ttu-id="ca73d-490">請注意，檔案不是位於相同的位置;這是預設的配套的另一個優點。</span><span class="sxs-lookup"><span data-stu-id="ca73d-490">Notice that the files are not located in the same place; this is another advantage over the default bundling.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. <span data-ttu-id="ca73d-491">開啟 [**優化 .aspx**檔案]。</span><span class="sxs-lookup"><span data-stu-id="ca73d-491">Open the **Optimization.aspx** file.</span></span>

    <span data-ttu-id="ca73d-492">請注意，當您在 Global.asax.cs 檔案中設定靜態組合時，**靜態 JS**套件組合的連結會使用您所宣告的路徑： **/StaticBundle**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-492">Notice that the link to **Static JS Bundle** is using the path you have declared when you configured the static bundle in the Global.asax.cs file: **/StaticBundle**.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. <span data-ttu-id="ca73d-493">按**F5**執行應用程式，然後流覽至 [**優化**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="ca73d-493">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
6. <span data-ttu-id="ca73d-494">按一下 [**靜態 JS**組合] 連結以開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-494">Click on the **Static JS Bundle** link to open the file.</span></span>

    <span data-ttu-id="ca73d-495">請注意，縮減配套的 JavaScript 檔案是在靜態套件組合檔案中設定的所有 JavaScript 檔案的輸出，該檔案位於&quot;的路徑 &quot;的/StaticBundle。</span><span class="sxs-lookup"><span data-stu-id="ca73d-495">Notice that the minified bundled JavaScript file is the output for all the JavaScript files configured in the static bundle file under the path &quot;/StaticBundle&quot;.</span></span>

    <span data-ttu-id="ca73d-496">![靜態 JavaScript 檔案配套](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "靜態 JavaScript 檔案配套")</span><span class="sxs-lookup"><span data-stu-id="ca73d-496">![Static JavaScript files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "Static JavaScript files bundle")</span></span>

    <span data-ttu-id="ca73d-497">*靜態 JavaScript 檔案配套*</span><span class="sxs-lookup"><span data-stu-id="ca73d-497">*Static JavaScript files bundle*</span></span>
7. <span data-ttu-id="ca73d-498">關閉瀏覽器並返回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ca73d-498">Close the browser and return to Visual Studio.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a><span data-ttu-id="ca73d-499">工作 4-動態資料夾組合</span><span class="sxs-lookup"><span data-stu-id="ca73d-499">Task 4 - Dynamic Folder Bundles</span></span>

<span data-ttu-id="ca73d-500">在這項工作中，您將瞭解如何設定動態資料夾組合。</span><span class="sxs-lookup"><span data-stu-id="ca73d-500">In this task, you will learn how to configure dynamic folder bundles.</span></span> <span data-ttu-id="ca73d-501">動態組合的威力在於，您可以在編譯成 JavaScript 的語言中包含靜態 JavaScript 和其他檔案，因此在執行組合之前，需要進行一些處理。</span><span class="sxs-lookup"><span data-stu-id="ca73d-501">The power of dynamic bundling is that you can include static JavaScript, as well as other files in languages that compiles into JavaScript, and thus, require some processing before the bundling is executed.</span></span>

<span data-ttu-id="ca73d-502">在此範例中，您將瞭解如何使用**DynamicFolderBundle**類別，為以 CofeeScript 撰寫的檔案建立動態組合。</span><span class="sxs-lookup"><span data-stu-id="ca73d-502">In this example, you will learn how to use the **DynamicFolderBundle** class to create a dynamic bundle for files written in CofeeScript.</span></span> <span data-ttu-id="ca73d-503">CofeeScript 是一種程式設計語言，它會編譯成 JavaScript，並提供更簡單的語法來撰寫 JavaScript 程式碼，強化 JavaScript 的簡潔性和可讀性。</span><span class="sxs-lookup"><span data-stu-id="ca73d-503">CofeeScript is a programming language that compiles into JavaScript and provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability.</span></span>

1. <span data-ttu-id="ca73d-504">開啟**Global.asax.cs**檔案，並找出**應用程式\_Start**方法。</span><span class="sxs-lookup"><span data-stu-id="ca73d-504">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
2. <span data-ttu-id="ca73d-505">取消批註動態套件組合程式碼，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="ca73d-505">Uncomment the dynamic bundle code as shown in the code below.</span></span>

    <span data-ttu-id="ca73d-506">您所定義的動態資料夾配套會使用**CoffeeMinify**自訂縮制處理器，此套件只會套用至具有 &quot;**咖啡**&quot; 延伸模組（CoffeeScript 檔案）的檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-506">You are defining a dynamic folder bundle that will use the **CoffeeMinify** custom minification processor that will only apply to the files with the &quot;**.coffee**&quot; extension (CoffeeScript files).</span></span> <span data-ttu-id="ca73d-507">請注意，您可以使用搜尋模式來選取要在資料夾內組合的檔案，例如 '\*咖啡 '。</span><span class="sxs-lookup"><span data-stu-id="ca73d-507">Notice that you can use a search pattern to select the files to bundle within a folder, like '\*.coffee'.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. <span data-ttu-id="ca73d-508">開啟 NuGet 套件管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="ca73d-508">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="ca73d-509">若要這麼做，請使用功能表**視圖** | **其他 Windows** | **套件管理員主控台**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-509">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>
4. <span data-ttu-id="ca73d-510">在 [**套件管理員主控台**] 中，輸入**Install-Package CoffeeSharp** ，然後按**enter**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-510">In the **Package Manager Console,** type **Install-Package CoffeeSharp** and press **ENTER**.</span></span>
5. <span data-ttu-id="ca73d-511">按一下 [**方案總管**] 視窗中的 [**顯示所有**檔案] 按鈕</span><span class="sxs-lookup"><span data-stu-id="ca73d-511">Click the **Show All Files** button in the **Solution Explorer** window</span></span>

    <span data-ttu-id="ca73d-512">![顯示所有檔案](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "顯示所有檔案")</span><span class="sxs-lookup"><span data-stu-id="ca73d-512">![Showing all files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "Showing all files")</span></span>

    <span data-ttu-id="ca73d-513">*顯示所有檔案*</span><span class="sxs-lookup"><span data-stu-id="ca73d-513">*Showing all files*</span></span>
6. <span data-ttu-id="ca73d-514">以滑鼠右鍵按一下**方案總管**中的**CoffeeMinify.cs**檔案，然後選取 [**包含在專案中**]</span><span class="sxs-lookup"><span data-stu-id="ca73d-514">Right click the **CoffeeMinify.cs** file in the **Solution Explorer** and select **Include in Project**</span></span>

    <span data-ttu-id="ca73d-515">![將 CoffeeMinify.cs 檔案包含在專案中](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "將 CoffeeMinify.cs 檔案包含在專案中")</span><span class="sxs-lookup"><span data-stu-id="ca73d-515">![Include the CoffeeMinify.cs file in the project](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "Include the CoffeeMinify.cs file in the project")</span></span>

    <span data-ttu-id="ca73d-516">*將 CoffeeMinify.cs 檔案包含在專案中*</span><span class="sxs-lookup"><span data-stu-id="ca73d-516">*Include the CoffeeMinify.cs file in the project*</span></span>
7. <span data-ttu-id="ca73d-517">開啟**CoffeeMinify.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-517">Open the **CoffeeMinify.cs** file.</span></span>

    <span data-ttu-id="ca73d-518">這個類別繼承自 JsMinify，以縮小 CoffeeScript 程式碼編譯所產生的 JavaScript 輸出。</span><span class="sxs-lookup"><span data-stu-id="ca73d-518">This class inherits from JsMinify to minify the JavaScript output resulting from the CoffeeScript code compilation.</span></span> <span data-ttu-id="ca73d-519">它會呼叫 CoffeeScript 編譯器先產生 JavaScript 程式碼，然後將它傳送至 JsMinify 方法，以縮小產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ca73d-519">It calls the CoffeeScript compiler to generate the JavaScript code first, and then it sends it to the JsMinify.Process method to minify the resulting code.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. <span data-ttu-id="ca73d-520">從 [**腳本/** 組合] 資料夾開啟**Script1 咖啡**和**Script2 咖啡**檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-520">Open the **Script1.coffee** and **Script2.coffee** files from the **Scripts/bundle** folder.</span></span>

    <span data-ttu-id="ca73d-521">這些檔案會包含在使用 CoffeeMinify 類別執行組合時所要編譯的 CoffeScript 程式碼。</span><span class="sxs-lookup"><span data-stu-id="ca73d-521">These files will include the CoffeScript code to be compiled while performing the bundling with the CoffeeMinify class.</span></span>

    <span data-ttu-id="ca73d-522">為了簡單起見，所提供的 CoffeeScript 檔案只包含 CoffeeScript 範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="ca73d-522">For simplicity purposes, the CoffeeScript files provided are only including CoffeeScript sample code.</span></span> <span data-ttu-id="ca73d-523">批註會由 JsMinify 流程排除。</span><span class="sxs-lookup"><span data-stu-id="ca73d-523">The comments are excluded by the JsMinify process.</span></span>

    <span data-ttu-id="ca73d-524">![CoffeeScript 檔案](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript 檔案")</span><span class="sxs-lookup"><span data-stu-id="ca73d-524">![CoffeeScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript files")</span></span>

    <span data-ttu-id="ca73d-525">*CoffeeScript 檔案*</span><span class="sxs-lookup"><span data-stu-id="ca73d-525">*CoffeeScript files*</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca73d-526">[CofeeScript](https://github.com/jashkenas/coffeescript/)提供更簡單的語法來撰寫 javascript 程式碼、增強 javascript 的簡潔性和可讀性，以及加入其他功能，例如陣列理解和模式比對。</span><span class="sxs-lookup"><span data-stu-id="ca73d-526">[CofeeScript](https://github.com/jashkenas/coffeescript/) provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability, as well as adding other features like array comprehension and pattern matching.</span></span>
9. <span data-ttu-id="ca73d-527">開啟 [**優化 .aspx**檔案]，並找出 [組合] 連結。</span><span class="sxs-lookup"><span data-stu-id="ca73d-527">Open the **Optimization.aspx** file and locate the bundle links.</span></span>

    <span data-ttu-id="ca73d-528">請注意，**動態 JS**配套的連結會使用您為動態資料夾配套所設定的 **/Coffee**尾碼來參考**腳本/** 組合資料夾。</span><span class="sxs-lookup"><span data-stu-id="ca73d-528">Notice that the link to **Dynamic JS Bundle** is referencing the **Scripts/bundle** folder by using the **/Coffee** suffix you configured for the dynamic folder bundle.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. <span data-ttu-id="ca73d-529">按**F5**執行應用程式，然後流覽至 [**優化**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="ca73d-529">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
11. <span data-ttu-id="ca73d-530">按一下 [**動態 JS**套件組合] 連結，以開啟產生的檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-530">Click on the **Dynamic JS Bundle** link to open the generated file.</span></span>

    <span data-ttu-id="ca73d-531">請注意，此配套中包含的內容只包含**咖啡**檔案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-531">Notice that the content that was included in this bundle only contains **.coffee** files.</span></span> <span data-ttu-id="ca73d-532">您也可以看到 CoffeeScript 程式碼已編譯成 JavaScript，而且已移除批註的行。</span><span class="sxs-lookup"><span data-stu-id="ca73d-532">You can also see that the CoffeeScript code was compiled to JavaScript and the commented-out lines has been removed.</span></span>

    <span data-ttu-id="ca73d-533">![動態 JS 檔案配套](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "動態 JS 檔案配套")</span><span class="sxs-lookup"><span data-stu-id="ca73d-533">![Dynamic JS files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "Dynamic JS files bundle")</span></span>

    <span data-ttu-id="ca73d-534">*動態 JS 檔案配套*</span><span class="sxs-lookup"><span data-stu-id="ca73d-534">*Dynamic JS files bundle*</span></span>

> [!NOTE]
> <span data-ttu-id="ca73d-535">此外，您可以遵循[附錄 B：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式](#AppendixB)，將此應用程式部署到 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="ca73d-535">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="ca73d-536">總結</span><span class="sxs-lookup"><span data-stu-id="ca73d-536">Summary</span></span>

<span data-ttu-id="ca73d-537">此實驗室可協助您瞭解 Visual Studio 2012 中 ASP.NET 和 Web 開發的新功能，以及如何利用 Visual Studio 2012 中的各種增強功能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-537">This lab helps you to understand what New in ASP.NET and Web Development in Visual Studio 2012 is and how to take advantage of the variety of enhancements in Visual Studio 2012.</span></span>

<span data-ttu-id="ca73d-538">藉由完成此實際操作實驗室，您就可以學會如何使用適用于 CSS、JavaScript 和 HTML 的 Visual Studio 2012 編輯器中的新功能和改善。</span><span class="sxs-lookup"><span data-stu-id="ca73d-538">By completing this Hands-On Lab, you have learnt how to use the new features and improvements in Visual Studio 2012 Editors for CSS, JavaScript and HTML.</span></span> <span data-ttu-id="ca73d-539">此外，您還學會了 Visual Studio 2012 如何實行內建的組合和縮制。</span><span class="sxs-lookup"><span data-stu-id="ca73d-539">In addition, you have learnt how Visual Studio 2012 implements built-in bundling and minification.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="ca73d-540">附錄 A：安裝 Web 的 Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="ca73d-540">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="ca73d-541">您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="ca73d-541">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="ca73d-542">下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="ca73d-542">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="ca73d-543">移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="ca73d-543">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="ca73d-544">或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。</span><span class="sxs-lookup"><span data-stu-id="ca73d-544">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="ca73d-545">按一下 [**立即安裝**]。</span><span class="sxs-lookup"><span data-stu-id="ca73d-545">Click on **Install Now**.</span></span> <span data-ttu-id="ca73d-546">如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="ca73d-546">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="ca73d-547">開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。</span><span class="sxs-lookup"><span data-stu-id="ca73d-547">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="ca73d-548">![安裝 Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "安裝 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="ca73d-548">![Install Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="ca73d-549">*安裝 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="ca73d-549">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="ca73d-550">閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。</span><span class="sxs-lookup"><span data-stu-id="ca73d-550">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受授權條款](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    <span data-ttu-id="ca73d-552">*接受授權條款*</span><span class="sxs-lookup"><span data-stu-id="ca73d-552">*Accepting the license terms*</span></span>
5. <span data-ttu-id="ca73d-553">等到下載和安裝程式完成為止。</span><span class="sxs-lookup"><span data-stu-id="ca73d-553">Wait until the downloading and installation process completes.</span></span>

    ![安裝進度](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    <span data-ttu-id="ca73d-555">*安裝進度*</span><span class="sxs-lookup"><span data-stu-id="ca73d-555">*Installation progress*</span></span>
6. <span data-ttu-id="ca73d-556">當安裝完成時，按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="ca73d-556">When the installation completes, click **Finish**.</span></span>

    ![安裝已完成](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    <span data-ttu-id="ca73d-558">*安裝已完成*</span><span class="sxs-lookup"><span data-stu-id="ca73d-558">*Installation completed*</span></span>
7. <span data-ttu-id="ca73d-559">按一下 **[** 結束] 以關閉 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="ca73d-559">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="ca73d-560">若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。</span><span class="sxs-lookup"><span data-stu-id="ca73d-560">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磚](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    <span data-ttu-id="ca73d-562">*VS Express for Web 磚*</span><span class="sxs-lookup"><span data-stu-id="ca73d-562">*VS Express for Web tile*</span></span>

---

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="ca73d-563">附錄 B：使用 Web Deploy 發行 ASP.NET MVC 4 應用程式</span><span class="sxs-lookup"><span data-stu-id="ca73d-563">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="ca73d-564">本附錄將告訴您如何從 Windows Azure 管理入口網站建立新的網站，以及如何發佈您在實驗室之後取得的應用程式，利用 Windows Azure 提供的 Web Deploy 發行功能。</span><span class="sxs-lookup"><span data-stu-id="ca73d-564">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="ca73d-565">工作 1-從 Windows Azure 入口網站建立新的網站</span><span class="sxs-lookup"><span data-stu-id="ca73d-565">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="ca73d-566">移至[Windows Azure 管理入口網站](https://manage.windowsazure.com/)並使用與您的訂用帳戶相關聯的 Microsoft 認證登入。</span><span class="sxs-lookup"><span data-stu-id="ca73d-566">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca73d-567">有了 Windows Azure，您可以免費裝載10個 ASP.NET 網站，然後隨著流量的成長而調整。</span><span class="sxs-lookup"><span data-stu-id="ca73d-567">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="ca73d-568">您可以在[這裡](https://aka.ms/aspnet-hol-azure)註冊。</span><span class="sxs-lookup"><span data-stu-id="ca73d-568">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="ca73d-569">![登入 Windows Azure 入口網站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "登入 Windows Azure 入口網站")</span><span class="sxs-lookup"><span data-stu-id="ca73d-569">![Log on to Windows Azure portal](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="ca73d-570">*登入 Windows Azure 管理入口網站*</span><span class="sxs-lookup"><span data-stu-id="ca73d-570">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="ca73d-571">按一下命令列上的 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="ca73d-571">Click **New** on the command bar.</span></span>

    <span data-ttu-id="ca73d-572">![建立新網站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "建立新網站")</span><span class="sxs-lookup"><span data-stu-id="ca73d-572">![Creating a new Web Site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="ca73d-573">*建立新網站*</span><span class="sxs-lookup"><span data-stu-id="ca73d-573">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="ca73d-574">按一下 [**計算** | 的**網站**]。</span><span class="sxs-lookup"><span data-stu-id="ca73d-574">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="ca73d-575">然後選取 [**快速建立**] 選項。</span><span class="sxs-lookup"><span data-stu-id="ca73d-575">Then select **Quick Create** option.</span></span> <span data-ttu-id="ca73d-576">提供新網站的可用 URL，然後按一下 [**建立網站**]。</span><span class="sxs-lookup"><span data-stu-id="ca73d-576">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca73d-577">Windows Azure 網站是在雲端中執行之 Web 應用程式的主機，您可以控制和管理。</span><span class="sxs-lookup"><span data-stu-id="ca73d-577">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="ca73d-578">[快速建立] 選項可讓您從入口網站外部，將已完成的 web 應用程式部署至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="ca73d-578">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="ca73d-579">它不包含設定資料庫的步驟。</span><span class="sxs-lookup"><span data-stu-id="ca73d-579">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="ca73d-580">![使用 [快速建立] 建立新的網站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "使用 [快速建立] 建立新的網站")</span><span class="sxs-lookup"><span data-stu-id="ca73d-580">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="ca73d-581">*使用 [快速建立] 建立新的網站*</span><span class="sxs-lookup"><span data-stu-id="ca73d-581">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="ca73d-582">等到新**網站**建立完畢。</span><span class="sxs-lookup"><span data-stu-id="ca73d-582">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="ca73d-583">建立網站之後，請按一下 [ **URL** ] 資料行下方的連結。</span><span class="sxs-lookup"><span data-stu-id="ca73d-583">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="ca73d-584">檢查新網站是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="ca73d-584">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="ca73d-585">![流覽至新網站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "流覽至新網站")</span><span class="sxs-lookup"><span data-stu-id="ca73d-585">![Browsing to the new web site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="ca73d-586">*流覽至新網站*</span><span class="sxs-lookup"><span data-stu-id="ca73d-586">*Browsing to the new web site*</span></span>

    <span data-ttu-id="ca73d-587">![網站正在執行](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "網站正在執行")</span><span class="sxs-lookup"><span data-stu-id="ca73d-587">![Web site running](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "Web site running")</span></span>

    <span data-ttu-id="ca73d-588">*網站正在執行*</span><span class="sxs-lookup"><span data-stu-id="ca73d-588">*Web site running*</span></span>
6. <span data-ttu-id="ca73d-589">返回入口網站，然後按一下 [**名稱**] 欄底下的網站名稱，以顯示管理頁面。</span><span class="sxs-lookup"><span data-stu-id="ca73d-589">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="ca73d-590">![開啟網站管理頁面](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "開啟網站管理頁面")</span><span class="sxs-lookup"><span data-stu-id="ca73d-590">![Opening the web site management pages](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="ca73d-591">*開啟網站管理頁面*</span><span class="sxs-lookup"><span data-stu-id="ca73d-591">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="ca73d-592">在 [**儀表板**] 頁面的 [**快速概覽**] 區段下，按一下 [**下載發行設定檔**] 連結。</span><span class="sxs-lookup"><span data-stu-id="ca73d-592">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca73d-593">*發行設定檔*包含將 web 應用程式發佈至 Windows Azure 網站所需的所有資訊，以供每個已啟用的發行方法使用。</span><span class="sxs-lookup"><span data-stu-id="ca73d-593">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="ca73d-594">發行設定檔包含 URL、使用者認證和資料庫字串，這些都是用來連接到已啟用發行方法的每個端點並進行驗證的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="ca73d-594">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="ca73d-595">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支援讀取發行設定檔，以將這些程式的設定自動化，以將 Web 應用程式發佈至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="ca73d-595">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="ca73d-596">![正在下載網站發行設定檔](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "正在下載網站發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="ca73d-596">![Downloading the web site publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="ca73d-597">*正在下載網站發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="ca73d-597">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="ca73d-598">將發行設定檔下載到已知的位置。</span><span class="sxs-lookup"><span data-stu-id="ca73d-598">Download the publish profile file to a known location.</span></span> <span data-ttu-id="ca73d-599">在此練習中，您將瞭解如何使用此檔案，將 web 應用程式從 Visual Studio 發行至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="ca73d-599">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="ca73d-600">![儲存發行設定檔](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "正在儲存發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="ca73d-600">![Saving the publish profile file](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "Saving the publish profile")</span></span>

    <span data-ttu-id="ca73d-601">*儲存發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="ca73d-601">*Saving the publish profile file*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="ca73d-602">工作 2-設定資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="ca73d-602">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="ca73d-603">如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca73d-603">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="ca73d-604">如果您想要部署不使用 SQL Server 的簡單應用程式，您可能會略過這項工作。</span><span class="sxs-lookup"><span data-stu-id="ca73d-604">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="ca73d-605">您將需要 SQL Database 伺服器來儲存應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="ca73d-605">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="ca73d-606">您可以在 Windows Azure 管理入口網站的  **SQL 資料庫** | **伺服器** | **伺服器的儀表板**上，從您的訂用帳戶中查看 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca73d-606">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="ca73d-607">如果您沒有建立伺服器，可以使用命令列上的 [**新增**] 按鈕建立一個。</span><span class="sxs-lookup"><span data-stu-id="ca73d-607">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="ca73d-608">記下 [**伺服器名稱] 和 [URL]、[系統管理員登入名稱] 和 [密碼**]，因為您將在後續工作中使用它們。</span><span class="sxs-lookup"><span data-stu-id="ca73d-608">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="ca73d-609">請不要建立資料庫，因為它會在稍後的階段中建立。</span><span class="sxs-lookup"><span data-stu-id="ca73d-609">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="ca73d-610">![SQL Database Server 儀表板](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database Server 儀表板")</span><span class="sxs-lookup"><span data-stu-id="ca73d-610">![SQL Database Server Dashboard](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="ca73d-611">*SQL Database Server 儀表板*</span><span class="sxs-lookup"><span data-stu-id="ca73d-611">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="ca73d-612">在下一項工作中，您將會從 Visual Studio 測試資料庫連線，因此您必須在伺服器的**允許 IP 位址**清單中包含本機 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ca73d-612">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="ca73d-613">若要這麼做，請按一下 [**設定**]，選取**目前用戶端 IP 位址**的 ip 位址，並將它貼在 [**起始 Ip 位址**] 和 [**結束 ip 位址**] 文字方塊上。</span><span class="sxs-lookup"><span data-stu-id="ca73d-613">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes.</span></span> <span data-ttu-id="ca73d-614">輸入規則的名稱，然後按一下 ![新增-用戶端-ip-位址-確定 按鈕](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ca73d-614">Enter a name for the rule and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) button.</span></span>

    ![正在新增用戶端 IP 位址](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    <span data-ttu-id="ca73d-616">*正在新增用戶端 IP 位址*</span><span class="sxs-lookup"><span data-stu-id="ca73d-616">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="ca73d-617">將**用戶端 Ip 位址**新增至 [允許的 ip 位址] 清單之後，按一下 [**儲存**] 以確認變更。</span><span class="sxs-lookup"><span data-stu-id="ca73d-617">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![確認變更](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    <span data-ttu-id="ca73d-619">*確認變更*</span><span class="sxs-lookup"><span data-stu-id="ca73d-619">*Confirm Changes*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="ca73d-620">工作 3-使用 Web Deploy 發行 ASP.NET MVC 4 應用程式</span><span class="sxs-lookup"><span data-stu-id="ca73d-620">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="ca73d-621">返回 ASP.NET MVC 4 解決方案。</span><span class="sxs-lookup"><span data-stu-id="ca73d-621">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="ca73d-622">在 **方案總管**中，以滑鼠右鍵按一下 網站 專案，然後選取 **發佈**。</span><span class="sxs-lookup"><span data-stu-id="ca73d-622">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="ca73d-623">![發行應用程式](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "發行應用程式")</span><span class="sxs-lookup"><span data-stu-id="ca73d-623">![Publishing the Application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "Publishing the Application")</span></span>

    <span data-ttu-id="ca73d-624">*發行網站*</span><span class="sxs-lookup"><span data-stu-id="ca73d-624">*Publishing the web site*</span></span>
2. <span data-ttu-id="ca73d-625">匯入您在第一個工作中儲存的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="ca73d-625">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="ca73d-626">![匯入發行設定檔](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "匯入發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="ca73d-626">![Importing the publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "Importing the publish profile")</span></span>

    <span data-ttu-id="ca73d-627">*正在匯入發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="ca73d-627">*Importing publish profile*</span></span>
3. <span data-ttu-id="ca73d-628">按一下 [**驗證連接**]。</span><span class="sxs-lookup"><span data-stu-id="ca73d-628">Click **Validate Connection**.</span></span> <span data-ttu-id="ca73d-629">驗證完成後，按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="ca73d-629">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca73d-630">當您看到 [驗證連線] 按鈕旁出現綠色核取記號時，驗證就會完成。</span><span class="sxs-lookup"><span data-stu-id="ca73d-630">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="ca73d-631">![正在驗證連接](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "正在驗證連接")</span><span class="sxs-lookup"><span data-stu-id="ca73d-631">![Validating connection](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "Validating connection")</span></span>

    <span data-ttu-id="ca73d-632">*正在驗證連接*</span><span class="sxs-lookup"><span data-stu-id="ca73d-632">*Validating connection*</span></span>
4. <span data-ttu-id="ca73d-633">在 [**設定**] 頁面的 [**資料庫**] 區段底下，按一下資料庫連接的文字方塊旁邊的按鈕（也就是**DefaultConnection**）。</span><span class="sxs-lookup"><span data-stu-id="ca73d-633">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="ca73d-634">![Web deploy 設定](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web deploy 設定")</span><span class="sxs-lookup"><span data-stu-id="ca73d-634">![Web deploy configuration](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web deploy configuration")</span></span>

    <span data-ttu-id="ca73d-635">*Web deploy 設定*</span><span class="sxs-lookup"><span data-stu-id="ca73d-635">*Web deploy configuration*</span></span>
5. <span data-ttu-id="ca73d-636">設定資料庫連接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ca73d-636">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="ca73d-637">在 [**伺服器名稱**] 中，使用*tcp：* prefix 輸入您的 SQL Database 伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="ca73d-637">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="ca73d-638">在 [**使用者名稱**] 中，輸入您的伺服器管理員登入名稱。</span><span class="sxs-lookup"><span data-stu-id="ca73d-638">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="ca73d-639">在 [**密碼**] 中輸入您的伺服器管理員登入密碼。</span><span class="sxs-lookup"><span data-stu-id="ca73d-639">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="ca73d-640">輸入新的資料庫名稱，例如： *MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="ca73d-640">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="ca73d-641">![正在設定目的地連接字串](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "正在設定目的地連接字串")</span><span class="sxs-lookup"><span data-stu-id="ca73d-641">![Configuring destination connection string](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="ca73d-642">*正在設定目的地連接字串*</span><span class="sxs-lookup"><span data-stu-id="ca73d-642">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="ca73d-643">然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ca73d-643">Then click **OK**.</span></span> <span data-ttu-id="ca73d-644">當系統提示您建立資料庫時，請按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="ca73d-644">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="ca73d-645">![建立資料庫](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "建立資料庫字串")</span><span class="sxs-lookup"><span data-stu-id="ca73d-645">![Creating the database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "Creating the database string")</span></span>

    <span data-ttu-id="ca73d-646">*建立資料庫*</span><span class="sxs-lookup"><span data-stu-id="ca73d-646">*Creating the database*</span></span>
7. <span data-ttu-id="ca73d-647">您將用來連接到 Windows Azure 中 SQL Database 的連接字串會顯示在 [預設連接] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="ca73d-647">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="ca73d-648">然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="ca73d-648">Then click **Next**.</span></span>

    <span data-ttu-id="ca73d-649">![指向 SQL Database 的連接字串](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "指向 SQL Database 的連接字串")</span><span class="sxs-lookup"><span data-stu-id="ca73d-649">![Connection string pointing to SQL Database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="ca73d-650">*指向 SQL Database 的連接字串*</span><span class="sxs-lookup"><span data-stu-id="ca73d-650">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="ca73d-651">在 [**預覽**] 頁面中，按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="ca73d-651">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="ca73d-652">![發行 web 應用程式](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "發行 web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="ca73d-652">![Publishing the web application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "Publishing the web application")</span></span>

    <span data-ttu-id="ca73d-653">*發行 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="ca73d-653">*Publishing the web application*</span></span>
9. <span data-ttu-id="ca73d-654">發佈程式完成後，您的預設瀏覽器會開啟已發行的網站。</span><span class="sxs-lookup"><span data-stu-id="ca73d-654">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="ca73d-655">![發行至 Windows Azure 的應用程式](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "發行至 Windows Azure 的應用程式")</span><span class="sxs-lookup"><span data-stu-id="ca73d-655">![Application published to Windows Azure](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="ca73d-656">*發行至 Windows Azure 的應用程式*</span><span class="sxs-lookup"><span data-stu-id="ca73d-656">*Application published to Windows Azure*</span></span>
