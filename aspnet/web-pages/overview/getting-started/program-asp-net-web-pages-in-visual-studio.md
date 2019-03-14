---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 程式設計 ASP.NET Web Pages (Razor) 使用 Visual Studio |Microsoft Docs
author: Rick-Anderson
description: 此附錄將解釋如何使用 Visual Studio 2010 或 Visual Web Developer 2010 Express 含有 Razor 語法的 ASP.NET Web Pages 程式。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 5b8df17ec1021d133579e23cb4f5b0d0f67d4c7c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57058315"
---
<a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="504d9-103">程式設計使用 Visual Studio 的 ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="504d9-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>
====================
<span data-ttu-id="504d9-104">藉由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="504d9-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="504d9-105">這篇文章說明如何使用 Visual Studio 或 Visual Web Developer Express 程式 ASP.NET Web Pages (Razor) 網站。</span><span class="sxs-lookup"><span data-stu-id="504d9-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="504d9-106">您將學到什麼</span><span class="sxs-lookup"><span data-stu-id="504d9-106">What you'll learn</span></span>
>
> - <span data-ttu-id="504d9-107">您需要以 ASP.NET Web Pages 用於您版本的 Visual Studio 安裝 （如果有任何項目）。</span><span class="sxs-lookup"><span data-stu-id="504d9-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="504d9-108">如何加入支援 ASP.NET Web Pages Visual Web Developer 2010 Express。</span><span class="sxs-lookup"><span data-stu-id="504d9-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="504d9-109">如何使用 Visual Studio 中的功能，才能使用 ASP.NET Razor 頁面，包括 IntelliSense 和偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="504d9-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="504d9-110">在本教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="504d9-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="504d9-111">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="504d9-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="504d9-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="504d9-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="504d9-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="504d9-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="504d9-114">本教學課程也適用於 ASP.NET Web Pages 2、 與 Visual Studio 2012、 Visual Studio 2010，WebMatrix 2。</span><span class="sxs-lookup"><span data-stu-id="504d9-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>


<span data-ttu-id="504d9-115">您可以使用 Razor 語法使用 WebMatrix 或許多其他程式碼編輯器進行程式設計的 ASP.NET Web pages。</span><span class="sxs-lookup"><span data-stu-id="504d9-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="504d9-116">您也可以使用 Microsoft Visual Studio 也就是功能完整的整合式的開發環境 (IDE)，提供一組強大的工具建立的多種應用程式 （不只是網站）。</span><span class="sxs-lookup"><span data-stu-id="504d9-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="504d9-117">若要使用 ASP.NET Razor 頁面，您可以使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="504d9-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="504d9-118">Visual Studio 提供使用 ASP.NET Razor 網頁進行程式設計的兩個特別有用功能如下：</span><span class="sxs-lookup"><span data-stu-id="504d9-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="504d9-119">*IntelliSense*。</span><span class="sxs-lookup"><span data-stu-id="504d9-119">*IntelliSense*.</span></span> <span data-ttu-id="504d9-120">Visual Studio 內建的 IntelliSense 功能會比在 WebMatrix 中的 IntelliSense 更完整。</span><span class="sxs-lookup"><span data-stu-id="504d9-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="504d9-121">*偵錯工具*。</span><span class="sxs-lookup"><span data-stu-id="504d9-121">*Debugger*.</span></span> <span data-ttu-id="504d9-122">偵錯工具可讓您疑難排解您的程式碼執行、 檢查變數，並逐步執行逐行程式碼時停止程式。</span><span class="sxs-lookup"><span data-stu-id="504d9-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="504d9-123">使用 Visual Studio 使用不同版本的 ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="504d9-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="504d9-124">若要開發 Visual Studio 2017 中的 ASP.NET web 應用程式，安裝**ASP.NET 和 web 開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="504d9-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="504d9-125">Visual Studio 2012 和 Visual Studio 2013 包含支援 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="504d9-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="504d9-126">（只有當您安裝 Visual Studio 會安裝才能支援 ASP.NET 網頁的封裝）。</span><span class="sxs-lookup"><span data-stu-id="504d9-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="504d9-127">Visual Studio 2010 不支援預設包含 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="504d9-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="504d9-128">若要使用 Visual Studio 2010 中的 ASP.NET Web Pages，您必須安裝 ASP.NET MVC 套件。</span><span class="sxs-lookup"><span data-stu-id="504d9-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="504d9-129">若要取得 ASP.NET Web Pages 2，您會安裝 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="504d9-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="504d9-130">下表摘要說明支援 ASP.NET Web Pages 中不同版本的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="504d9-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="504d9-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="504d9-131">Visual Studio 2010</span></span> | <span data-ttu-id="504d9-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="504d9-132">Visual Studio 2012</span></span> | <span data-ttu-id="504d9-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="504d9-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="504d9-134">**ASP.NET Web Pages 2**</span><span class="sxs-lookup"><span data-stu-id="504d9-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="504d9-135">安裝 ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="504d9-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="504d9-136">（包含）</span><span class="sxs-lookup"><span data-stu-id="504d9-136">(Included)</span></span> | <span data-ttu-id="504d9-137">（包含）</span><span class="sxs-lookup"><span data-stu-id="504d9-137">(Included)</span></span> |
| <span data-ttu-id="504d9-138">**ASP.NET Web Pages 3**</span><span class="sxs-lookup"><span data-stu-id="504d9-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="504d9-139">更新至 ASP.NET Web Pages 3 透過 NuGet</span><span class="sxs-lookup"><span data-stu-id="504d9-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="504d9-140">（包含）</span><span class="sxs-lookup"><span data-stu-id="504d9-140">(Included)</span></span> |

<span data-ttu-id="504d9-141">若要使用 Visual Studio 2010，請參閱[安裝支援的 Visual Studio 2010 中 ASP.NET Web Pages](#vs2010support)。</span><span class="sxs-lookup"><span data-stu-id="504d9-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="504d9-142">啟動 Visual Studio 從 WebMatrix</span><span class="sxs-lookup"><span data-stu-id="504d9-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="504d9-143">如果您已在 WebMatrix 中啟動專案，並想要切換至 Visual Studio，WebMatrix 便會提供按鈕，以輕鬆地在 Visual Studio 中開啟專案。</span><span class="sxs-lookup"><span data-stu-id="504d9-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="504d9-144">您必須安裝 Visual Studio 這個按鈕，在電腦上啟用。</span><span class="sxs-lookup"><span data-stu-id="504d9-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="504d9-145">下圖顯示在 WebMatrix 中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="504d9-145">The following image shows the button in WebMatrix.</span></span>

![啟動 Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="504d9-147">當您按一下按鈕時，就會在 Visual Studio 中開啟專案。</span><span class="sxs-lookup"><span data-stu-id="504d9-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="504d9-148">您可以切換來回 WebMatrix 和 Visual Studio 沒有任何問題。</span><span class="sxs-lookup"><span data-stu-id="504d9-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="504d9-149">如果任何檔案在另一個環境中已經變更，而且需要重新載入，才能取得最新的變更，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="504d9-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="504d9-150">在 Visual Studio 中建立 ASP.NET Razor 網站</span><span class="sxs-lookup"><span data-stu-id="504d9-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="504d9-151">若要在 Visual Studio 中建立 ASP.NET Razor 網站：</span><span class="sxs-lookup"><span data-stu-id="504d9-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="504d9-152">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="504d9-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="504d9-153">在 **檔案**功能表上，按一下**新的網站**。</span><span class="sxs-lookup"><span data-stu-id="504d9-153">In the **File** menu, click **New Web Site**.</span></span>

    ![建立新的網站](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="504d9-155">在 **新的網站**對話方塊方塊中，選取要使用 （Visual C# 或 Visual Basic） 的語言。</span><span class="sxs-lookup"><span data-stu-id="504d9-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="504d9-156">選取  **ASP.NET 網站 (Razor)** 範本。</span><span class="sxs-lookup"><span data-stu-id="504d9-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![razor 的站台](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="504d9-158">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="504d9-158">Click **OK**.</span></span>

<span data-ttu-id="504d9-159">新的專案存在，而且會填入一些預設網頁 」，以協助您開始著手。</span><span class="sxs-lookup"><span data-stu-id="504d9-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="504d9-160">Using IntelliSense</span><span class="sxs-lookup"><span data-stu-id="504d9-160">Using IntelliSense</span></span>

<span data-ttu-id="504d9-161">既然您已建立站台，您可以看到 IntelliSense 在 Visual Studio 中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="504d9-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="504d9-162">在您剛才建立的網站中，開啟*Default.cshtml*頁面。</span><span class="sxs-lookup"><span data-stu-id="504d9-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="504d9-163">在後`<h3>`標記，在頁面中，輸入`@ServerInfo.`（包括點）。</span><span class="sxs-lookup"><span data-stu-id="504d9-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="504d9-164">請注意 IntelliSense 如何顯示可用的方法`ServerInfo`下拉式清單中的協助程式。</span><span class="sxs-lookup"><span data-stu-id="504d9-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="504d9-166">選取`GetHtml`方法清單，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="504d9-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="504d9-167">IntelliSense 會自動填入此方法。</span><span class="sxs-lookup"><span data-stu-id="504d9-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="504d9-168">(使用 C# 中的任何方法，您必須新增`()`方法之後的字元。)完整程式碼`GetHtml`方法如以下範例所示：</span><span class="sxs-lookup"><span data-stu-id="504d9-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="504d9-169">按 Ctrl + F5 執行頁面。</span><span class="sxs-lookup"><span data-stu-id="504d9-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="504d9-170">這是頁面看起來像時顯示在瀏覽器：</span><span class="sxs-lookup"><span data-stu-id="504d9-170">This is what the page looks like when displayed in a browser:</span></span>

    ![在瀏覽器中的預設頁面](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="504d9-172">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="504d9-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="504d9-173">使用偵錯工具</span><span class="sxs-lookup"><span data-stu-id="504d9-173">Using the Debugger</span></span>

1. <span data-ttu-id="504d9-174">在頂端*Default.cshtml*頁面上，以開頭的行後方`Page.Title`，新增下列程式碼行：</span><span class="sxs-lookup"><span data-stu-id="504d9-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="504d9-175">左邊的程式碼編輯器的灰色邊界，按一下旁邊的 這個新的一行以新增*中斷點*。</span><span class="sxs-lookup"><span data-stu-id="504d9-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="504d9-176">中斷點會告知偵錯工具停止在該點執行程式，以便您可以看到發生的事情的標記。</span><span class="sxs-lookup"><span data-stu-id="504d9-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![設定中斷點](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="504d9-178">移除對呼叫`ServerInfo.GetHtml`方法，並將呼叫加入`@myTime`變數在它的位置。</span><span class="sxs-lookup"><span data-stu-id="504d9-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="504d9-179">這個呼叫會顯示新的一行程式碼所傳回的目前時間值。</span><span class="sxs-lookup"><span data-stu-id="504d9-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="504d9-180">按 F5 以偵錯工具中執行的頁面。</span><span class="sxs-lookup"><span data-stu-id="504d9-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="504d9-181">頁面會在您設定的中斷點上停止。</span><span class="sxs-lookup"><span data-stu-id="504d9-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="504d9-182">下圖顯示頁面的外觀在編輯器中使用的中斷點 （黃色）。</span><span class="sxs-lookup"><span data-stu-id="504d9-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![偵錯中斷點](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="504d9-184">在 偵錯 工具列中，按一下**逐步執行**執行下的一行程式碼 按鈕 （或按 F11）。</span><span class="sxs-lookup"><span data-stu-id="504d9-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="504d9-185">每次您按一下此按鈕時，您會繼續執行至下一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="504d9-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![逐步執行按鈕](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="504d9-187">檢查的值`myTime`變數上方按住滑鼠指標，或藉由檢查中顯示的值**區域變數**並**呼叫堆疊**windows。</span><span class="sxs-lookup"><span data-stu-id="504d9-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="504d9-188">Visual Studio 會顯示變數的值。</span><span class="sxs-lookup"><span data-stu-id="504d9-188">Visual Studio display the value of the variable.</span></span>

    ![顯示的時間值](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="504d9-190">完成檢查變數及逐步執行程式碼之後，請按 f5 鍵繼續執行而不需停止每一行程式碼的網頁。</span><span class="sxs-lookup"><span data-stu-id="504d9-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="504d9-191">當您完成逐步執行所有程式碼時，在瀏覽器會顯示頁面。</span><span class="sxs-lookup"><span data-stu-id="504d9-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="504d9-192">若要深入了解如何在 Visual Studio 中的程式碼進行偵錯以及偵錯工具，請參閱[逐步解說：偵錯 Visual Web Developer 中的網頁](https://msdn.microsoft.com/library/z9e7w6cs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="504d9-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="504d9-193">使用 Visual Studio 的 ASP.NET MVC 專案中使用 Razor</span><span class="sxs-lookup"><span data-stu-id="504d9-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="504d9-194">Razor 語法也會在 ASP.NET MVC 專案中廣泛使用。</span><span class="sxs-lookup"><span data-stu-id="504d9-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="504d9-195">MVC 是功能強大、 以模式為基礎的方式建置動態網站。</span><span class="sxs-lookup"><span data-stu-id="504d9-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="504d9-196">如果您的 ASP.NET Web Pages 網站變得難以維護，您可能要考慮將它轉換成 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="504d9-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="504d9-197">如需建立 MVC 應用程式的範例，請參閱 < [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="504d9-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="504d9-198">在 Visual Studio 2010 中安裝 ASP.NET Web 網頁的支援</span><span class="sxs-lookup"><span data-stu-id="504d9-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="504d9-199">本節說明如何安裝 Visual Web Developer Express 2010 和 ASP.NET Web Pages Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="504d9-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="504d9-200">如果您還沒有 Web Platform Installer，請從下列 URL 下載：</span><span class="sxs-lookup"><span data-stu-id="504d9-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="504d9-201">執行 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="504d9-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="504d9-202">按一下 [**產品**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="504d9-202">Click the **Products** tab.</span></span>

    ![WebPI 產品 索引標籤](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="504d9-204">搜尋**ASP.NET MVC 4** （適用於 ASP.NET Web Pages 2)，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="504d9-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="504d9-205">這些產品包括 Visual Studio 工具，用於建置 ASP.NET Razor 網站。</span><span class="sxs-lookup"><span data-stu-id="504d9-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi 安裝選項](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="504d9-207">按一下 **安裝**才能完成安裝。</span><span class="sxs-lookup"><span data-stu-id="504d9-207">Click **Install** to complete the installation.</span></span>