---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 使用 Visual Studio 的程式設計 ASP.NET Web Pages （Razor） |Microsoft Docs
author: Rick-Anderson
description: 本附錄說明您可以如何使用 Visual Studio 2010 或 Visual Web Developer 2010 Express，以 Razor 語法來程式 ASP.NET Web Pages。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 1a76098779d05912bf7bdf2de5fdce024770752c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633508"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="f56a2-103">使用 Visual Studio 的程式設計 ASP.NET Web Pages （Razor）</span><span class="sxs-lookup"><span data-stu-id="f56a2-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="f56a2-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f56a2-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f56a2-105">本文說明如何使用 Visual Studio 或 Visual Web Developer Express 來程式 ASP.NET Web Pages （Razor）網站。</span><span class="sxs-lookup"><span data-stu-id="f56a2-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="f56a2-106">您將學到什麼</span><span class="sxs-lookup"><span data-stu-id="f56a2-106">What you'll learn</span></span>
>
> - <span data-ttu-id="f56a2-107">您需要安裝的內容（如果有的話），才能與您的 Visual Studio 版本中的 ASP.NET Web Pages 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="f56a2-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="f56a2-108">如何將 ASP.NET Web Pages 的支援新增至 Visual Web Developer 2010 Express。</span><span class="sxs-lookup"><span data-stu-id="f56a2-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="f56a2-109">如何使用 Visual Studio 中的功能來處理 ASP.NET Razor 頁面，包括 IntelliSense 和偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="f56a2-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f56a2-110">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="f56a2-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="f56a2-111">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="f56a2-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="f56a2-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="f56a2-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="f56a2-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="f56a2-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="f56a2-114">本教學課程也適用于 ASP.NET Web Pages 2、Visual Studio 2012、Visual Studio 2010 和 WebMatrix 2。</span><span class="sxs-lookup"><span data-stu-id="f56a2-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="f56a2-115">您可以使用 WebMatrix 或許多其他程式碼編輯器，利用 Razor 語法來設計 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="f56a2-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="f56a2-116">您也可以使用 Microsoft Visual Studio，這是功能完整的整合式開發環境（IDE），可提供一組強大的工具來建立許多類型的應用程式（而不只是網站）。</span><span class="sxs-lookup"><span data-stu-id="f56a2-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="f56a2-117">若要使用 ASP.NET Razor 頁面，您可以使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="f56a2-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="f56a2-118">Visual Studio 為使用 ASP.NET Razor 網頁進行程式設計所提供的兩個特別有用的功能如下：</span><span class="sxs-lookup"><span data-stu-id="f56a2-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="f56a2-119">*IntelliSense*。</span><span class="sxs-lookup"><span data-stu-id="f56a2-119">*IntelliSense*.</span></span> <span data-ttu-id="f56a2-120">Visual Studio 內建的 IntelliSense 功能比 WebMatrix 中的 IntelliSense 更全面。</span><span class="sxs-lookup"><span data-stu-id="f56a2-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="f56a2-121">*偵錯工具*。</span><span class="sxs-lookup"><span data-stu-id="f56a2-121">*Debugger*.</span></span> <span data-ttu-id="f56a2-122">偵錯工具可讓您針對程式碼進行疑難排解，方法是停止執行中的程式、檢查變數，然後逐行執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="f56a2-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="f56a2-123">使用不同版本的 Visual Studio ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="f56a2-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="f56a2-124">若要在 Visual Studio 2017 中開發 ASP.NET web 應用程式，請安裝**ASP.NET 和 網頁程式開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="f56a2-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="f56a2-125">Visual Studio 2012 和 Visual Studio 2013 包含 ASP.NET Web Pages 的支援。</span><span class="sxs-lookup"><span data-stu-id="f56a2-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="f56a2-126">（當您安裝 Visual Studio 時，會安裝支援 ASP.NET Web Pages 所需的套件）。</span><span class="sxs-lookup"><span data-stu-id="f56a2-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="f56a2-127">Visual Studio 2010 預設不包含 ASP.NET Web Pages 的支援。</span><span class="sxs-lookup"><span data-stu-id="f56a2-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="f56a2-128">若要使用 ASP.NET Web Pages 搭配 Visual Studio 2010，您必須安裝 ASP.NET MVC 封裝。</span><span class="sxs-lookup"><span data-stu-id="f56a2-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="f56a2-129">若要取得 ASP.NET Web Pages 2，請安裝 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="f56a2-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="f56a2-130">下表摘要說明不同 Visual Studio 版本中 ASP.NET Web Pages 的支援。</span><span class="sxs-lookup"><span data-stu-id="f56a2-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="f56a2-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="f56a2-131">Visual Studio 2010</span></span> | <span data-ttu-id="f56a2-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="f56a2-132">Visual Studio 2012</span></span> | <span data-ttu-id="f56a2-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="f56a2-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f56a2-134">**ASP.NET Web Pages 2**</span><span class="sxs-lookup"><span data-stu-id="f56a2-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="f56a2-135">安裝 ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="f56a2-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="f56a2-136">含</span><span class="sxs-lookup"><span data-stu-id="f56a2-136">(Included)</span></span> | <span data-ttu-id="f56a2-137">含</span><span class="sxs-lookup"><span data-stu-id="f56a2-137">(Included)</span></span> |
| <span data-ttu-id="f56a2-138">**ASP.NET Web Pages 3**</span><span class="sxs-lookup"><span data-stu-id="f56a2-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="f56a2-139">透過 NuGet 更新為 ASP.NET Web Pages 3</span><span class="sxs-lookup"><span data-stu-id="f56a2-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="f56a2-140">含</span><span class="sxs-lookup"><span data-stu-id="f56a2-140">(Included)</span></span> |

<span data-ttu-id="f56a2-141">若要使用 Visual Studio 2010，請參閱[在 Visual Studio 2010 中安裝 ASP.NET Web Pages 的支援](#vs2010support)。</span><span class="sxs-lookup"><span data-stu-id="f56a2-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="f56a2-142">從 WebMatrix 啟動 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f56a2-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="f56a2-143">如果您已在 WebMatrix 中啟動專案，並想要切換至 Visual Studio，WebMatrix 會提供一個按鈕，讓您輕鬆地在 Visual Studio 中開啟專案。</span><span class="sxs-lookup"><span data-stu-id="f56a2-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="f56a2-144">您必須在電腦上安裝 Visual Studio，才能啟用此按鈕。</span><span class="sxs-lookup"><span data-stu-id="f56a2-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="f56a2-145">下圖顯示 WebMatrix 中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="f56a2-145">The following image shows the button in WebMatrix.</span></span>

![啟動 Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="f56a2-147">當您按一下按鈕時，專案會以 Visual Studio 開啟。</span><span class="sxs-lookup"><span data-stu-id="f56a2-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="f56a2-148">您可以在 WebMatrix 與 Visual Studio 之間來回切換，而不會發生任何問題。</span><span class="sxs-lookup"><span data-stu-id="f56a2-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="f56a2-149">如果其他環境中有任何檔案已變更，而且需要重載以取得最新的變更，您將會收到通知。</span><span class="sxs-lookup"><span data-stu-id="f56a2-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="f56a2-150">在 Visual Studio 中建立 ASP.NET Razor 網站</span><span class="sxs-lookup"><span data-stu-id="f56a2-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="f56a2-151">在 Visual Studio 中建立 ASP.NET Razor 網站：</span><span class="sxs-lookup"><span data-stu-id="f56a2-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="f56a2-152">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f56a2-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="f56a2-153">**在 [檔案**] 功能表中，按一下 [**新網站**]。</span><span class="sxs-lookup"><span data-stu-id="f56a2-153">In the **File** menu, click **New Web Site**.</span></span>

    ![建立新網站](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="f56a2-155">在 [**新網站**] 對話方塊中，選取要使用的語言（[ C#視覺效果] 或 [Visual Basic]）。</span><span class="sxs-lookup"><span data-stu-id="f56a2-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="f56a2-156">選取 [ **ASP.NET 網站（Razor）** ] 範本。</span><span class="sxs-lookup"><span data-stu-id="f56a2-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![razor 網站](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="f56a2-158">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f56a2-158">Click **OK**.</span></span>

<span data-ttu-id="f56a2-159">您的新專案已存在，並已填入一些可協助您開始使用的預設網頁。</span><span class="sxs-lookup"><span data-stu-id="f56a2-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="f56a2-160">Using IntelliSense</span><span class="sxs-lookup"><span data-stu-id="f56a2-160">Using IntelliSense</span></span>

<span data-ttu-id="f56a2-161">既然您已建立網站，就可以查看 IntelliSense 在 Visual Studio 中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="f56a2-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="f56a2-162">在您剛建立的網站中，開啟 [*預設的. cshtml* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="f56a2-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="f56a2-163">在頁面中 `<h3>` 標記之後，輸入 `@ServerInfo.` （包括點）。</span><span class="sxs-lookup"><span data-stu-id="f56a2-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="f56a2-164">請注意 IntelliSense 如何在下拉式清單中顯示 `ServerInfo` helper 的可用方法。</span><span class="sxs-lookup"><span data-stu-id="f56a2-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![IntelliSense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="f56a2-166">從清單中選取 [`GetHtml`] 方法，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="f56a2-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="f56a2-167">IntelliSense 會自動填入方法。</span><span class="sxs-lookup"><span data-stu-id="f56a2-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="f56a2-168">（如同中C#的任何方法，您必須在方法後面加上 `()` 字元）。`GetHtml` 方法的完整程式碼如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f56a2-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="f56a2-169">按 Ctrl + F5 執行頁面。</span><span class="sxs-lookup"><span data-stu-id="f56a2-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="f56a2-170">這是頁面在瀏覽器中顯示時的樣子：</span><span class="sxs-lookup"><span data-stu-id="f56a2-170">This is what the page looks like when displayed in a browser:</span></span>

    ![瀏覽器中的預設頁面](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="f56a2-172">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f56a2-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="f56a2-173">使用偵錯工具</span><span class="sxs-lookup"><span data-stu-id="f56a2-173">Using the Debugger</span></span>

1. <span data-ttu-id="f56a2-174">在預設的 [ *cshtml* ] 頁面頂端，以 `Page.Title`開頭的那一行之後，加入下列程式程式碼：</span><span class="sxs-lookup"><span data-stu-id="f56a2-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="f56a2-175">在編輯器灰色邊界的程式碼左側，按一下這個新行的 [下一步]，以新增*中斷點*。</span><span class="sxs-lookup"><span data-stu-id="f56a2-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="f56a2-176">「中斷點」是一種標記，會告知偵錯工具在該時間點停止執行程式，讓您可以查看發生的狀況。</span><span class="sxs-lookup"><span data-stu-id="f56a2-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![設定中斷點](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="f56a2-178">移除對 `ServerInfo.GetHtml` 方法的呼叫，並在其位置加入 `@myTime` 變數的呼叫。</span><span class="sxs-lookup"><span data-stu-id="f56a2-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="f56a2-179">此呼叫會顯示新的程式程式碼所傳回的目前時間值。</span><span class="sxs-lookup"><span data-stu-id="f56a2-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="f56a2-180">按 F5 以在偵錯工具中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="f56a2-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="f56a2-181">頁面會在您設定的中斷點上停止。</span><span class="sxs-lookup"><span data-stu-id="f56a2-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="f56a2-182">下圖顯示在編輯器中，使用中斷點時頁面的外觀（以黃色表示）。</span><span class="sxs-lookup"><span data-stu-id="f56a2-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![調試中斷點](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="f56a2-184">在 [偵錯工具] 工具列中，按一下 [**逐步**執行] 按鈕（或按 F11）以執行下一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="f56a2-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="f56a2-185">每當您按一下此按鈕時，就會將執行前移至下一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="f56a2-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![[逐步執行] 按鈕](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="f56a2-187">藉由將滑鼠指標停留在其上方或檢查 [**區域變數**] 和 [**呼叫堆疊**] 視窗中顯示的值，檢查 `myTime` 變數的值。</span><span class="sxs-lookup"><span data-stu-id="f56a2-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="f56a2-188">Visual Studio 顯示變數的值。</span><span class="sxs-lookup"><span data-stu-id="f56a2-188">Visual Studio display the value of the variable.</span></span>

    ![顯示時間值](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="f56a2-190">當您完成檢查變數並逐步執行程式碼時，請按 F5 繼續執行頁面，而不會在每一行停止。</span><span class="sxs-lookup"><span data-stu-id="f56a2-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="f56a2-191">當您完成逐步執行所有程式碼時，瀏覽器會顯示頁面。</span><span class="sxs-lookup"><span data-stu-id="f56a2-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="f56a2-192">若要深入瞭解偵錯工具，以及如何在 Visual Studio 中偵錯工具代碼，請參閱[逐步解說：在 Visual Web Developer 中偵測網頁](https://msdn.microsoft.com/library/z9e7w6cs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f56a2-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="f56a2-193">在 ASP.NET MVC 專案中使用 Razor 搭配 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f56a2-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="f56a2-194">Razor 語法也廣泛用於 ASP.NET MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="f56a2-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="f56a2-195">MVC 是一種功能強大、以模式為基礎的方式，可建立動態網站。</span><span class="sxs-lookup"><span data-stu-id="f56a2-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="f56a2-196">如果您的 ASP.NET Web Pages 網站變得難以維護，您可能會想要考慮將它轉換成 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f56a2-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="f56a2-197">如需建立 MVC 應用程式的範例，請參閱[使用 ASP.NET MVC 5 消費者入門](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f56a2-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="f56a2-198">在 Visual Studio 2010 中安裝 ASP.NET Web Pages 的支援</span><span class="sxs-lookup"><span data-stu-id="f56a2-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="f56a2-199">本節說明如何安裝 Visual Web Developer Express 2010 和適用于 Visual Studio 的 ASP.NET Web Pages 工具。</span><span class="sxs-lookup"><span data-stu-id="f56a2-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="f56a2-200">如果您還沒有 Web Platform Installer，請從下列 URL 下載：</span><span class="sxs-lookup"><span data-stu-id="f56a2-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="f56a2-201">執行 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="f56a2-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="f56a2-202">按一下 [**產品**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f56a2-202">Click the **Products** tab.</span></span>

    ![WebPI 產品索引標籤](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="f56a2-204">搜尋**ASP.NET MVC 4** （適用于 ASP.NET Web Pages 2），然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="f56a2-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="f56a2-205">這些產品包括用來建立 ASP.NET Razor 網站的 Visual Studio 工具。</span><span class="sxs-lookup"><span data-stu-id="f56a2-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi 安裝選項](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="f56a2-207">按一下 [**安裝**] 以完成安裝。</span><span class="sxs-lookup"><span data-stu-id="f56a2-207">Click **Install** to complete the installation.</span></span>
