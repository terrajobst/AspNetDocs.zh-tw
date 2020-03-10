---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 建立新的 ASP.NET MVC 專案 |Microsoft Docs
author: microsoft
description: 步驟1顯示如何將基本 NerdDinner 應用程式結構放在原處。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 189ddc187fc83db14106b2da199ba12a70a32b45
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580931"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="cd69a-103">建立新的 ASP.NET MVC 專案</span><span class="sxs-lookup"><span data-stu-id="cd69a-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="cd69a-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="cd69a-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="cd69a-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="cd69a-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="cd69a-106">這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟1，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd69a-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="cd69a-107">步驟1顯示如何將基本 NerdDinner 應用程式結構放在原處。</span><span class="sxs-lookup"><span data-stu-id="cd69a-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="cd69a-108">如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="cd69a-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="cd69a-109">NerdDinner 步驟1：檔案&gt;新專案</span><span class="sxs-lookup"><span data-stu-id="cd69a-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="cd69a-110">我們會在 Visual Studio 2008 或免費的 Visual Web Developer 2008 Express 中選取檔案 **&gt;[新增專案**] 功能表項目，以開始我們的 NerdDinner 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd69a-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="cd69a-111">這會顯示 [新增專案] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="cd69a-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="cd69a-112">若要建立新的 ASP.NET MVC 應用程式，我們會選取對話方塊左側的 [Web] 節點，然後選擇右側的 [ASP.NET MVC Web 應用程式] 專案範本：</span><span class="sxs-lookup"><span data-stu-id="cd69a-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="cd69a-113">*重要事項：請確定您已下載並安裝 ASP.NET MVC，否則它不會顯示在 [新增專案] 對話方塊中。如果您尚未安裝[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) ，您可以使用 V2 （ASP.NET MVC 可在「Web 平臺-&gt;架構和執行時間」一節中取得）。*</span><span class="sxs-lookup"><span data-stu-id="cd69a-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="cd69a-114">我們會將新專案命名為 "NerdDinner"，然後按一下 [確定] 按鈕加以建立。</span><span class="sxs-lookup"><span data-stu-id="cd69a-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="cd69a-115">當我們按下 [Visual Studio 確定] 時，會出現一個額外的對話方塊，提示我們選擇性地為新的應用程式建立單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="cd69a-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="cd69a-116">這個單元測試專案可讓我們建立自動化的測試，以驗證應用程式的功能和行為（我們將在本教學課程稍後討論的內容）。</span><span class="sxs-lookup"><span data-stu-id="cd69a-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="cd69a-117">上述對話方塊中的 [測試架構] 下拉式清單會填入電腦上安裝的所有可用 ASP.NET MVC 單元測試專案範本。</span><span class="sxs-lookup"><span data-stu-id="cd69a-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="cd69a-118">您可以下載 NUnit、MBUnit 和 XUnit 的版本。</span><span class="sxs-lookup"><span data-stu-id="cd69a-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="cd69a-119">此外，也支援內建的 Visual Studio 單元測試架構。</span><span class="sxs-lookup"><span data-stu-id="cd69a-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="cd69a-120">*注意： Visual Studio 單元測試架構僅適用于 Visual Studio 2008 Professional 和更新版本。如果您使用 VS 2008 Standard Edition 或 Visual Web Developer 2008 Express，您將需要下載並安裝 ASP.NET MVC 的 NUnit、MBUnit 或 XUnit 擴充功能，才能顯示此對話方塊。如果未安裝任何測試架構，則不會顯示對話方塊。*</span><span class="sxs-lookup"><span data-stu-id="cd69a-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="cd69a-121">我們會針對我們所建立的測試專案使用預設的「NerdDinner」名稱，並使用「Visual Studio 單元測試」架構選項。</span><span class="sxs-lookup"><span data-stu-id="cd69a-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="cd69a-122">當我們按一下 [確定] 按鈕時 Visual Studio 會為我們建立一個解決方案，其中包含兩個專案，一個用於我們的 web 應用程式，一個用於我們的單元測試：</span><span class="sxs-lookup"><span data-stu-id="cd69a-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="cd69a-123">檢查 NerdDinner 目錄結構</span><span class="sxs-lookup"><span data-stu-id="cd69a-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="cd69a-124">當您使用 Visual Studio 建立新的 ASP.NET MVC 應用程式時，它會自動將一些檔案和目錄新增至專案：</span><span class="sxs-lookup"><span data-stu-id="cd69a-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="cd69a-125">ASP.NET MVC 專案預設會有六個最上層目錄：</span><span class="sxs-lookup"><span data-stu-id="cd69a-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="cd69a-126">**目錄**</span><span class="sxs-lookup"><span data-stu-id="cd69a-126">**Directory**</span></span> | <span data-ttu-id="cd69a-127">**目的**</span><span class="sxs-lookup"><span data-stu-id="cd69a-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="cd69a-128">**/Controllers**</span><span class="sxs-lookup"><span data-stu-id="cd69a-128">**/Controllers**</span></span> | <span data-ttu-id="cd69a-129">放置處理 URL 要求的控制器類別的位置</span><span class="sxs-lookup"><span data-stu-id="cd69a-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="cd69a-130">**/Models**</span><span class="sxs-lookup"><span data-stu-id="cd69a-130">**/Models**</span></span> | <span data-ttu-id="cd69a-131">在其中放置代表和運算元據的類別</span><span class="sxs-lookup"><span data-stu-id="cd69a-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="cd69a-132">**/Views**</span><span class="sxs-lookup"><span data-stu-id="cd69a-132">**/Views**</span></span> | <span data-ttu-id="cd69a-133">放置負責轉譯輸出的 UI 範本檔案的位置</span><span class="sxs-lookup"><span data-stu-id="cd69a-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="cd69a-134">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="cd69a-134">**/Scripts**</span></span> | <span data-ttu-id="cd69a-135">放置 JavaScript 程式庫檔案和腳本的位置（.js）</span><span class="sxs-lookup"><span data-stu-id="cd69a-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="cd69a-136">**/Content**</span><span class="sxs-lookup"><span data-stu-id="cd69a-136">**/Content**</span></span> | <span data-ttu-id="cd69a-137">放置 CSS 和影像檔案的位置，以及其他非動態/非 JavaScript 內容</span><span class="sxs-lookup"><span data-stu-id="cd69a-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="cd69a-138">**/App\_資料**</span><span class="sxs-lookup"><span data-stu-id="cd69a-138">**/App\_Data**</span></span> | <span data-ttu-id="cd69a-139">儲存您想要讀取/寫入的資料檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="cd69a-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="cd69a-140">ASP.NET MVC 不需要此結構。</span><span class="sxs-lookup"><span data-stu-id="cd69a-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="cd69a-141">事實上，處理大型應用程式的開發人員通常會在多個專案之間分割應用程式，使其更容易管理（例如：資料模型類別通常會從 web 應用程式移至不同的類別庫專案）。</span><span class="sxs-lookup"><span data-stu-id="cd69a-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="cd69a-142">不過，預設的專案結構的確提供了一個不錯的預設目錄慣例，可讓我們用來將應用程式的顧慮保持乾淨。</span><span class="sxs-lookup"><span data-stu-id="cd69a-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="cd69a-143">當我們展開/Controllers 目錄時，我們會發現 Visual Studio 新增了兩個控制器類別– HomeController 和 AccountController –預設為專案：</span><span class="sxs-lookup"><span data-stu-id="cd69a-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="cd69a-144">當我們展開/Views 目錄時，我們會發現三個子目錄（/Home、/Account 和/Shared），而且它們內的數個範本檔案也會依預設新增至專案：</span><span class="sxs-lookup"><span data-stu-id="cd69a-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="cd69a-145">當我們展開/Content 和/Scripts 目錄時，我們會發現一個網站 .css 檔案，該檔案用來為網站上的所有 HTML 樣式，以及可在應用程式內啟用 ASP.NET AJAX 和 jQuery 支援的 JavaScript 程式庫：</span><span class="sxs-lookup"><span data-stu-id="cd69a-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="cd69a-146">當我們展開 [NerdDinner] 專案時，我們會發現兩個類別，其中包含控制器類別的單元測試：</span><span class="sxs-lookup"><span data-stu-id="cd69a-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="cd69a-147">Visual Studio 新增的這些預設檔案，會為我們提供一個基本結構，讓應用程式得以完成，其中包含首頁、[關於] 頁面、帳戶登入/登出/註冊頁面，以及未處理的錯誤頁面（所有的有線和作用中）。</span><span class="sxs-lookup"><span data-stu-id="cd69a-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="cd69a-148">執行 NerdDinner 應用程式</span><span class="sxs-lookup"><span data-stu-id="cd69a-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="cd69a-149">我們可以藉由選擇 [ **debug-&gt;] [開始調試**程式] 或 [ **Debug-&gt;啟動但不調試**] 功能表項目來執行專案：</span><span class="sxs-lookup"><span data-stu-id="cd69a-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="cd69a-150">這會啟動 Visual Studio 隨附的內建 ASP.NET Web 服務器，並執行我們的應用程式：</span><span class="sxs-lookup"><span data-stu-id="cd69a-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="cd69a-151">以下是新專案（URL： "/"）執行時的首頁：</span><span class="sxs-lookup"><span data-stu-id="cd69a-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="cd69a-152">按一下 [關於] 索引標籤會顯示 [關於] 頁面（URL： "/Home/About"）：</span><span class="sxs-lookup"><span data-stu-id="cd69a-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="cd69a-153">按一下右上角的 [登入] 連結，會將我們帶到登入頁面（URL： "/Account/LogOn"）</span><span class="sxs-lookup"><span data-stu-id="cd69a-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="cd69a-154">如果沒有登入帳戶，我們可以按一下 [註冊] 連結（URL： "/Account/Register"）來建立一個：</span><span class="sxs-lookup"><span data-stu-id="cd69a-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="cd69a-155">當我們建立新專案時，預設會新增執行上述 [首頁]、[關於] 和 [登出/註冊] 功能的程式碼。</span><span class="sxs-lookup"><span data-stu-id="cd69a-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="cd69a-156">我們將使用它做為應用程式的起點。</span><span class="sxs-lookup"><span data-stu-id="cd69a-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="cd69a-157">測試 NerdDinner 應用程式</span><span class="sxs-lookup"><span data-stu-id="cd69a-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="cd69a-158">如果我們使用 Professional Edition 或更高版本的 Visual Studio 2008，我們可以在 Visual Studio 中使用內建的單元測試 IDE 支援來測試專案：</span><span class="sxs-lookup"><span data-stu-id="cd69a-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="cd69a-159">選擇上述其中一個選項，將會在 IDE 中開啟 [測試結果] 窗格，並在涵蓋內建功能的新專案中所包含的27個單元測試上提供「通過/失敗」狀態：</span><span class="sxs-lookup"><span data-stu-id="cd69a-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="cd69a-160">稍後在本教學課程中，我們將詳細討論自動化測試，並加入涵蓋我們所實行之應用程式功能的其他單元測試。</span><span class="sxs-lookup"><span data-stu-id="cd69a-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="cd69a-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cd69a-161">Next Step</span></span>

<span data-ttu-id="cd69a-162">我們現在已具備基本的應用程式結構。</span><span class="sxs-lookup"><span data-stu-id="cd69a-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="cd69a-163">現在讓我們[建立資料庫來儲存我們的應用程式資料](create-a-database.md)。</span><span class="sxs-lookup"><span data-stu-id="cd69a-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cd69a-164">[上一頁](introducing-the-nerddinner-tutorial.md)
> [下一頁](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="cd69a-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
