---
uid: web-forms/overview/getting-started/creating-a-basic-web-forms-page
title: 使用 Visual Studio 2013 建立基本的 ASP.NET 4.5 Web Forms 網頁
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: a2f1c635-0817-4a9a-8c13-d5b5d29727c0
msc.legacyurl: /web-forms/overview/getting-started/creating-a-basic-web-forms-page
msc.type: authoredcontent
ms.openlocfilehash: 5d13a51128eecd92a82cfd06054448582a348e11
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629756"
---
# <a name="using-visual-studio-2013-to-create-a-basic-aspnet-45-web-forms-page"></a><span data-ttu-id="bc68c-102">使用 Visual Studio 2013 建立基本的 ASP.NET 4.5 Web Forms 網頁</span><span class="sxs-lookup"><span data-stu-id="bc68c-102">Using Visual Studio 2013 to create a Basic ASP.NET 4.5 Web Forms Page</span></span>

<span data-ttu-id="bc68c-103">依[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="bc68c-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

[!INCLUDE[](~/includes/rp.md)]

<span data-ttu-id="bc68c-104">本逐步解說提供[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)和[web Microsoft Visual Studio Express 2013](https://www.microsoft.com/visualstudio/11/downloads#express-web)中 網頁程式開發環境的簡介。</span><span class="sxs-lookup"><span data-stu-id="bc68c-104">This walkthrough provides you with an introduction to the Web development environment in [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) and in [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="bc68c-105">本逐步解說會引導您建立簡單的 ASP.NET Web form 頁面，並說明建立新頁面、加入控制項和撰寫程式碼的基本技巧。</span><span class="sxs-lookup"><span data-stu-id="bc68c-105">This walkthrough guides you through creating a simple ASP.NET Web Forms page and illustrates the basic techniques of creating a new page, adding controls, and writing code.</span></span>

<span data-ttu-id="bc68c-106">這個逐步解說中所述的工作包括：</span><span class="sxs-lookup"><span data-stu-id="bc68c-106">Tasks illustrated in this walkthrough include:</span></span>

- <span data-ttu-id="bc68c-107">建立檔案系統 Web Forms 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="bc68c-107">Creating a file system Web Forms application project.</span></span>
- <span data-ttu-id="bc68c-108">使用 Visual Studio 熟悉自己。</span><span class="sxs-lookup"><span data-stu-id="bc68c-108">Familiarizing yourself with Visual Studio.</span></span>
- <span data-ttu-id="bc68c-109">建立 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="bc68c-109">Creating an ASP.NET page.</span></span>
- <span data-ttu-id="bc68c-110">加入控制項。</span><span class="sxs-lookup"><span data-stu-id="bc68c-110">Adding controls.</span></span>
- <span data-ttu-id="bc68c-111">加入事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="bc68c-111">Adding event handlers.</span></span>
- <span data-ttu-id="bc68c-112">從 Visual Studio 執行和測試頁面。</span><span class="sxs-lookup"><span data-stu-id="bc68c-112">Running and testing a page from Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc68c-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bc68c-113">Prerequisites</span></span>

<span data-ttu-id="bc68c-114">若要完成這個逐步解說，您將需要：</span><span class="sxs-lookup"><span data-stu-id="bc68c-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="bc68c-115">[適用于 Web 的](https://www.microsoft.com/visualstudio/11/downloads#express-web) [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或 Microsoft Visual Studio Express 2013。</span><span class="sxs-lookup"><span data-stu-id="bc68c-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="bc68c-116">.NET Framework 會自動安裝。</span><span class="sxs-lookup"><span data-stu-id="bc68c-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="bc68c-117">Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 for Web 通常會在本教學課程系列中稱為 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="bc68c-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="bc68c-118">如果您使用 Visual Studio，本逐步解說會假設您在第一次啟動 Visual Studio 時選取了 [ **Web 開發**] 集合。</span><span class="sxs-lookup"><span data-stu-id="bc68c-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="bc68c-119">如需詳細資訊，請參閱[如何：選取 Web 開發環境設定](https://msdn.microsoft.com/library/ff521558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bc68c-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="bc68c-120">建立 Web 應用程式專案和頁面</span><span class="sxs-lookup"><span data-stu-id="bc68c-120">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="bc68c-121">在逐步解說的這個部分中，您將建立 Web 應用程式專案，並在其中加入新的頁面。</span><span class="sxs-lookup"><span data-stu-id="bc68c-121">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span> <span data-ttu-id="bc68c-122">您也會新增 HTML 文字，並在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="bc68c-122">You will also add HTML text and run the page in your browser.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="bc68c-123">若要建立 Web 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="bc68c-123">To create a Web application project</span></span>

1. <span data-ttu-id="bc68c-124">開啟 Microsoft Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="bc68c-124">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="bc68c-125">在 [檔案] 功能表上，選取 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="bc68c-125">On the **File** menu, select **New Project**.</span></span>  
    <span data-ttu-id="bc68c-126">![檔案 功能表](creating-a-basic-web-forms-page/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bc68c-126">![File Menu](creating-a-basic-web-forms-page/_static/image1.png)</span></span>

    <span data-ttu-id="bc68c-127">[ **新增專案** ] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="bc68c-127">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="bc68c-128">選取左側的 [&gt; **Visual C#**  -&gt; **Web** templates] 群組 -**範本**。</span><span class="sxs-lookup"><span data-stu-id="bc68c-128">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="bc68c-129">選擇中間欄的 [ASP.NET Web 應用程式] 範本。</span><span class="sxs-lookup"><span data-stu-id="bc68c-129">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="bc68c-130">將專案命名為***BasicWebApp*** ，然後按一下 [**確定]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bc68c-130">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
<span data-ttu-id="bc68c-131">![[New Project] \(新增專案\) 對話方塊](creating-a-basic-web-forms-page/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="bc68c-131">![New Project dialog box](creating-a-basic-web-forms-page/_static/image2.png)</span></span>
6. <span data-ttu-id="bc68c-132">接下來，選取 [ **Web** form] 範本，然後按一下 [**確定]** 按鈕以建立專案。</span><span class="sxs-lookup"><span data-stu-id="bc68c-132">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
<span data-ttu-id="bc68c-133">![[New ASP.NET Project] 對話方塊](creating-a-basic-web-forms-page/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="bc68c-133">![New ASP.NET Project dialog box](creating-a-basic-web-forms-page/_static/image3.png)</span></span>  

    <span data-ttu-id="bc68c-134">Visual Studio 會建立新的專案，其中包含根據 Web form 範本預先建立的功能。</span><span class="sxs-lookup"><span data-stu-id="bc68c-134">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span> <span data-ttu-id="bc68c-135">它不只會提供您一個*首頁 .aspx* *頁面，* 也就是一個*Contact .aspx*頁面，但也包含成員資格功能，可註冊使用者並儲存其認證，讓他們可以登入您的網站。</span><span class="sxs-lookup"><span data-stu-id="bc68c-135">It not only provides you with a *Home.aspx* page, an *About.aspx* page, a *Contact.aspx* page, but also includes membership functionality that registers users and saves their credentials so that they can log in to your website.</span></span> <span data-ttu-id="bc68c-136">建立新的頁面時，根據預設，Visual Studio 會在**原始**檔視圖中顯示頁面，您可以在其中看到頁面的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="bc68c-136">When a new page is created, by default Visual Studio displays the page in **Source** view, where you can see the page's HTML elements.</span></span> <span data-ttu-id="bc68c-137">下圖顯示當您建立名為*BasicWebApp*的新網頁時，您會在 [**原始**檔視圖] 中看到的內容。</span><span class="sxs-lookup"><span data-stu-id="bc68c-137">The following illustration shows what you would see in **Source** view if you created a new Web page named *BasicWebApp.aspx*.</span></span>  
    <span data-ttu-id="bc68c-138">![原始碼檢視](creating-a-basic-web-forms-page/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="bc68c-138">![Source View](creating-a-basic-web-forms-page/_static/image4.png)</span></span>

### <a name="a-tour-of-the-visual-studio-web-development-environment"></a><span data-ttu-id="bc68c-139">Visual Studio Web 開發環境的導覽</span><span class="sxs-lookup"><span data-stu-id="bc68c-139">A Tour of the Visual Studio Web Development Environment</span></span>

<span data-ttu-id="bc68c-140">在您繼續修改頁面之前，請先熟悉 Visual Studio 開發環境。</span><span class="sxs-lookup"><span data-stu-id="bc68c-140">Before you proceed by modifying the page, it is useful to familiarize yourself with the Visual Studio development environment.</span></span> <span data-ttu-id="bc68c-141">下圖顯示 Visual Studio 和 Web Visual Studio Express 中可用的 windows 和工具。</span><span class="sxs-lookup"><span data-stu-id="bc68c-141">The following illustration shows you the windows and tools that are available in Visual Studio and Visual Studio Express for Web.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="bc68c-142">此圖顯示預設視窗和視窗位置。</span><span class="sxs-lookup"><span data-stu-id="bc68c-142">This diagram shows default windows and window locations.</span></span> <span data-ttu-id="bc68c-143">[ **View** ] 功能表可讓您顯示其他視窗，以及重新排列和調整視窗大小以符合您的喜好設定。</span><span class="sxs-lookup"><span data-stu-id="bc68c-143">The **View** menu allows you to display additional windows, and to rearrange and resize windows to suit your preferences.</span></span> <span data-ttu-id="bc68c-144">如果已經對視窗排列進行變更，您看到的內容將不符合圖例。</span><span class="sxs-lookup"><span data-stu-id="bc68c-144">If changes have already been made to the window arrangement, what you see will not match the illustration.</span></span>

 <span data-ttu-id="bc68c-145">Visual Studio 環境</span><span class="sxs-lookup"><span data-stu-id="bc68c-145">The Visual Studio environment</span></span>

![Visual Studio 環境](creating-a-basic-web-forms-page/_static/image5.png)

### <a name="familiarize-yourself-with-the-web-designer"></a><span data-ttu-id="bc68c-147">熟悉 Web 設計工具</span><span class="sxs-lookup"><span data-stu-id="bc68c-147">Familiarize yourself with the Web designer</span></span>

<span data-ttu-id="bc68c-148">檢查上圖，並將文字與下列清單比對，其中描述最常用的 windows 和工具。</span><span class="sxs-lookup"><span data-stu-id="bc68c-148">Examine the above illustration and match the text to the following list, which describes the most commonly used windows and tools.</span></span> <span data-ttu-id="bc68c-149">（並非所有您看到的視窗和工具都會列在這裡，只有在上圖中標示的）。</span><span class="sxs-lookup"><span data-stu-id="bc68c-149">(Not all windows and tools that you see are listed here, only those marked in the preceding illustration.)</span></span>

- <span data-ttu-id="bc68c-150">'.</span><span class="sxs-lookup"><span data-stu-id="bc68c-150">Toolbars.</span></span> <span data-ttu-id="bc68c-151">提供用來格式化文字、尋找文字等等的命令。</span><span class="sxs-lookup"><span data-stu-id="bc68c-151">Provide commands for formatting text, finding text, and so on.</span></span> <span data-ttu-id="bc68c-152">只有當您在**設計**視圖中工作時，才可以使用某些工具列。</span><span class="sxs-lookup"><span data-stu-id="bc68c-152">Some toolbars are available only when you are working in **Design** view.</span></span>
- <span data-ttu-id="bc68c-153">**方案總管** 視窗。</span><span class="sxs-lookup"><span data-stu-id="bc68c-153">**Solution Explorer** window.</span></span> <span data-ttu-id="bc68c-154">顯示 Web 應用程式中的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="bc68c-154">Displays the files and folders in your Web application.</span></span>
- <span data-ttu-id="bc68c-155">文件視窗。</span><span class="sxs-lookup"><span data-stu-id="bc68c-155">Document window.</span></span> <span data-ttu-id="bc68c-156">在索引標籤式視窗中顯示您正在處理的檔。</span><span class="sxs-lookup"><span data-stu-id="bc68c-156">Displays the documents you are working on in tabbed windows.</span></span> <span data-ttu-id="bc68c-157">您可以按一下 [索引標籤]，在檔之間切換。</span><span class="sxs-lookup"><span data-stu-id="bc68c-157">You can switch between documents by clicking tabs.</span></span>
- <span data-ttu-id="bc68c-158">[**屬性**] 視窗。</span><span class="sxs-lookup"><span data-stu-id="bc68c-158">**Properties** window.</span></span> <span data-ttu-id="bc68c-159">可讓您變更頁面、HTML 元素、控制項和其他物件的設定。</span><span class="sxs-lookup"><span data-stu-id="bc68c-159">Allows you to change settings for the page, HTML elements, controls, and other objects.</span></span>
- <span data-ttu-id="bc68c-160">[視圖] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bc68c-160">View tabs.</span></span> <span data-ttu-id="bc68c-161">為您提供相同檔的不同視圖。</span><span class="sxs-lookup"><span data-stu-id="bc68c-161">Present you with different views of the same document.</span></span> <span data-ttu-id="bc68c-162">**設計**視圖是近 WYSIWYG 的編輯介面。</span><span class="sxs-lookup"><span data-stu-id="bc68c-162">**Design** view is a near-WYSIWYG editing surface.</span></span> <span data-ttu-id="bc68c-163">[**來源**視圖] 是網頁的 HTML 編輯器。</span><span class="sxs-lookup"><span data-stu-id="bc68c-163">**Source** view is the HTML editor for the page.</span></span> <span data-ttu-id="bc68c-164">**分割**視圖會同時顯示檔的**設計**視圖和**原始**檔視圖。</span><span class="sxs-lookup"><span data-stu-id="bc68c-164">**Split** view displays both the **Design** view and the **Source** view for the document.</span></span> <span data-ttu-id="bc68c-165">稍後在本逐步解說中，您將會使用**設計**和**來源**視圖。</span><span class="sxs-lookup"><span data-stu-id="bc68c-165">You will work with the **Design** and **Source** views later in this walkthrough.</span></span> <span data-ttu-id="bc68c-166">如果您想要在**設計**視圖中開啟網頁，請在 [**工具**] 功能表上，按一下 [**選項**]，選取 [ **HTML 設計**工具] 節點，然後變更 [**起始頁于**] 選項。</span><span class="sxs-lookup"><span data-stu-id="bc68c-166">If you prefer to open Web pages in **Design** view, on the **Tools** menu, click **Options**, select the **HTML Designer** node, and change the **Start Pages In** option.</span></span>
- <span data-ttu-id="bc68c-167">**工具箱**。</span><span class="sxs-lookup"><span data-stu-id="bc68c-167">**ToolBox**.</span></span> <span data-ttu-id="bc68c-168">提供您可以拖曳至頁面上的控制項和 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="bc68c-168">Provides controls and HTML elements that you can drag onto your page.</span></span> <span data-ttu-id="bc68c-169">[**工具箱**] 元素是依一般函式分組。</span><span class="sxs-lookup"><span data-stu-id="bc68c-169">**Toolbox** elements are grouped by common function.</span></span>
- <span data-ttu-id="bc68c-170">S **Erver Explorer**。</span><span class="sxs-lookup"><span data-stu-id="bc68c-170">S **erver Explorer**.</span></span> <span data-ttu-id="bc68c-171">顯示資料庫連接。</span><span class="sxs-lookup"><span data-stu-id="bc68c-171">Displays database connections.</span></span> <span data-ttu-id="bc68c-172">如果看不到伺服器總管，請按一下 [View] 功能表上的 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="bc68c-172">If Server Explorer is not visible, on the View menu, click Server Explorer.</span></span>

### <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="bc68c-173">建立新的 ASP.NET Web Forms 頁面</span><span class="sxs-lookup"><span data-stu-id="bc68c-173">Creating a new ASP.NET Web Forms Page</span></span>

<span data-ttu-id="bc68c-174">當您使用**ASP.NET Web 應用程式**專案範本建立新的 Web form 應用程式時，Visual Studio 會新增名為*default.aspx*的 ASP.NET 網頁（Web form 網頁），以及其他數個檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="bc68c-174">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="bc68c-175">您可以使用*預設的 .aspx*頁面作為 Web 應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="bc68c-175">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="bc68c-176">不過，在此逐步解說中，您將建立並使用新的頁面。</span><span class="sxs-lookup"><span data-stu-id="bc68c-176">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="bc68c-177">若要將頁面新增至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="bc68c-177">To add a page to the Web application</span></span>

1. <span data-ttu-id="bc68c-178">關閉*default.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="bc68c-178">Close the *Default.aspx* page.</span></span> <span data-ttu-id="bc68c-179">若要這麼做，請按一下顯示檔案名的索引標籤，然後按一下 [關閉] 選項。</span><span class="sxs-lookup"><span data-stu-id="bc68c-179">To do this, click the tab that displays the file name and then click the close option.</span></span>
2. <span data-ttu-id="bc68c-180">在**方案總管**中，以滑鼠**按右鍵 Web**應用程式名稱（在本教學課程中，應用程式名稱是**BasicWebSite**），然後按一下 [新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="bc68c-180">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="bc68c-181">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bc68c-181">The **Add New Item** dialog box is displayed.</span></span>
3. <span data-ttu-id="bc68c-182">選取左側的 [ **Visual C#**  -&gt; **Web**範本] 群組。</span><span class="sxs-lookup"><span data-stu-id="bc68c-182">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="bc68c-183">然後，從中間清單中選取 [ **Web Form** ]，並將它命名為*FirstWebPage .aspx*。</span><span class="sxs-lookup"><span data-stu-id="bc68c-183">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    <span data-ttu-id="bc68c-184">![[加入新項目] 對話方塊](creating-a-basic-web-forms-page/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="bc68c-184">![Add New Item dialog box](creating-a-basic-web-forms-page/_static/image6.png)</span></span>
4. <span data-ttu-id="bc68c-185">按一下 [**新增**]，將網頁新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="bc68c-185">Click **Add** to add the web page to your project.</span></span>  
<span data-ttu-id="bc68c-186">Visual Studio 會建立新的頁面，並開啟它。</span><span class="sxs-lookup"><span data-stu-id="bc68c-186">Visual Studio creates the new page and opens it.</span></span>

### <a name="adding-html-to-the-page"></a><span data-ttu-id="bc68c-187">將 HTML 新增至頁面</span><span class="sxs-lookup"><span data-stu-id="bc68c-187">Adding HTML to the Page</span></span>

<span data-ttu-id="bc68c-188">在本逐步解說的這個部分中，您將會在頁面中新增一些靜態文字。</span><span class="sxs-lookup"><span data-stu-id="bc68c-188">In this part of the walkthrough, you will add some static text to the page.</span></span>

### <a name="to-add-text-to-the-page"></a><span data-ttu-id="bc68c-189">若要將文字加入至頁面</span><span class="sxs-lookup"><span data-stu-id="bc68c-189">To add text to the page</span></span>

1. <span data-ttu-id="bc68c-190">在文件視窗的底部，按一下 [**設計**] 索引標籤以切換至**設計**視圖。</span><span class="sxs-lookup"><span data-stu-id="bc68c-190">At the bottom of the document window, click the **Design** tab to switch to **Design** view.</span></span>

    <span data-ttu-id="bc68c-191">設計檢視以類似 WYSIWYG 的方式顯示目前的頁面。</span><span class="sxs-lookup"><span data-stu-id="bc68c-191">Design view displays the current page in a WYSIWYG-like way.</span></span> <span data-ttu-id="bc68c-192">此時，您在頁面上沒有任何文字或控制項，因此頁面是空白的，但外框的虛線除外。</span><span class="sxs-lookup"><span data-stu-id="bc68c-192">At this point, you do not have any text or controls on the page, so the page is blank except for a dashed line that outlines a rectangle.</span></span> <span data-ttu-id="bc68c-193">此矩形代表頁面上的**div**元素。</span><span class="sxs-lookup"><span data-stu-id="bc68c-193">This rectangle represents a **div** element on the page.</span></span>
2. <span data-ttu-id="bc68c-194">在以虛線框住的矩形內部按一下。</span><span class="sxs-lookup"><span data-stu-id="bc68c-194">Click inside the rectangle that is outlined by a dashed line.</span></span>
3. <span data-ttu-id="bc68c-195">輸入**歡迎使用 Visual Web Developer** ，然後按兩次**enter**鍵。</span><span class="sxs-lookup"><span data-stu-id="bc68c-195">Type **Welcome to Visual Web Developer** and press **ENTER** twice.</span></span>

    <span data-ttu-id="bc68c-196">下圖顯示您在 [**設計**視圖] 中輸入的文字。</span><span class="sxs-lookup"><span data-stu-id="bc68c-196">The following illustration shows the text you typed in **Design** view.</span></span>

    <span data-ttu-id="bc68c-197">![設計檢視中的歡迎文字](creating-a-basic-web-forms-page/_static/image7.png "設計檢視中的歡迎文字")</span><span class="sxs-lookup"><span data-stu-id="bc68c-197">![Welcome text in Design view](creating-a-basic-web-forms-page/_static/image7.png "Welcome text in Design view")</span></span>
4. <span data-ttu-id="bc68c-198">切換至**來源**視圖。</span><span class="sxs-lookup"><span data-stu-id="bc68c-198">Switch to **Source** view.</span></span>

    <span data-ttu-id="bc68c-199">當您在 [**設計**視圖] 中輸入時，您可以在 [**原始**檔] 視圖中看到您所建立的 HTML。</span><span class="sxs-lookup"><span data-stu-id="bc68c-199">You can see the HTML in **Source** view that you created when you typed in **Design** view.</span></span>  
    <span data-ttu-id="bc68c-200">具有靜態文字](creating-a-basic-web-forms-page/_static/image8.png) ![網頁</span><span class="sxs-lookup"><span data-stu-id="bc68c-200">![Web Page with Static Text](creating-a-basic-web-forms-page/_static/image8.png)</span></span>

### <a name="running-the-page"></a><span data-ttu-id="bc68c-201">正在執行頁面</span><span class="sxs-lookup"><span data-stu-id="bc68c-201">Running the Page</span></span>

<span data-ttu-id="bc68c-202">將控制項新增至頁面之前，您可以先執行它。</span><span class="sxs-lookup"><span data-stu-id="bc68c-202">Before you proceed by adding controls to the page, you can first run it.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="bc68c-203">若要執行頁面</span><span class="sxs-lookup"><span data-stu-id="bc68c-203">To run the page</span></span>

1. <span data-ttu-id="bc68c-204">在**方案總管**中，以滑鼠右鍵按一下 [ *FirstWebPage* ]，然後選取 [**設定為起始頁**]。</span><span class="sxs-lookup"><span data-stu-id="bc68c-204">In **Solution Explorer**, right-click *FirstWebPage.aspx* and select **Set as Start Page**.</span></span>
2. <span data-ttu-id="bc68c-205">按**CTRL + F5**執行頁面。</span><span class="sxs-lookup"><span data-stu-id="bc68c-205">Press **CTRL+F5** to run the page.</span></span>

    <span data-ttu-id="bc68c-206">網頁會顯示在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="bc68c-206">The page is displayed in the browser.</span></span> <span data-ttu-id="bc68c-207">雖然您建立的頁面副檔名為 *.aspx*，但它目前的執行方式就像任何 HTML 網頁一樣。</span><span class="sxs-lookup"><span data-stu-id="bc68c-207">Although the page you created has a file-name extension of *.aspx*, it currently runs like any HTML page.</span></span>

    <span data-ttu-id="bc68c-208">若要在瀏覽器中顯示頁面，您也可以在**方案總管**中的頁面上按一下滑鼠右鍵，然後**在瀏覽器中**選取 [View]。</span><span class="sxs-lookup"><span data-stu-id="bc68c-208">To display a page in the browser you can also right-click the page in **Solution Explorer** and select **View in Browser**.</span></span>
3. <span data-ttu-id="bc68c-209">關閉瀏覽器以停止 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc68c-209">Close the browser to stop the Web application.</span></span>

## <a name="adding-and-programming-controls"></a><span data-ttu-id="bc68c-210">加入和程式設計控制項</span><span class="sxs-lookup"><span data-stu-id="bc68c-210">Adding and Programming Controls</span></span>

<a id="sectionToggle1"></a>

<span data-ttu-id="bc68c-211">您現在會將伺服器控制項加入至頁面。</span><span class="sxs-lookup"><span data-stu-id="bc68c-211">You will now add server controls to the page.</span></span> <span data-ttu-id="bc68c-212">伺服器控制項（例如按鈕、標籤、文字方塊和其他熟悉的控制項）可為您的 Web form 頁面提供一般表單處理功能。</span><span class="sxs-lookup"><span data-stu-id="bc68c-212">Server controls, such as buttons, labels, text boxes, and other familiar controls, provide typical form-processing capabilities for your Web Forms pages.</span></span> <span data-ttu-id="bc68c-213">不過，您可以使用在伺服器上執行的程式碼（而非用戶端）來設計控制項。</span><span class="sxs-lookup"><span data-stu-id="bc68c-213">However, you can program the controls with code that runs on the server, rather than the client.</span></span>

<span data-ttu-id="bc68c-214">您會將[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控制項、 [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控制項和[Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控制項加入至頁面，並撰寫程式碼來處理[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控制項的[Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件。</span><span class="sxs-lookup"><span data-stu-id="bc68c-214">You will add a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, a [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control, and a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control to the page and write code to handle the [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>

### <a name="to-add-controls-to-the-page"></a><span data-ttu-id="bc68c-215">若要將控制項加入至頁面</span><span class="sxs-lookup"><span data-stu-id="bc68c-215">To add controls to the page</span></span>

1. <span data-ttu-id="bc68c-216">按一下 [**設計**] 索引標籤，切換至 [**設計**視圖]。</span><span class="sxs-lookup"><span data-stu-id="bc68c-216">Click the **Design** tab to switch to **Design** view.</span></span>
2. <span data-ttu-id="bc68c-217">將插入點放在 [**歡迎使用 Visual Web Developer** ] 文字的結尾，然後按**enter**五次或多次，以在 [ **div**元素] 方塊中建立一些空間。</span><span class="sxs-lookup"><span data-stu-id="bc68c-217">Put the insertion point at the end of the **Welcome to Visual Web Developer** text and press **ENTER** five or more times to make some room in the **div** element box.</span></span>
3. <span data-ttu-id="bc68c-218">在 [**工具箱**] 中，展開 [**標準**] 群組（如果尚未展開）。</span><span class="sxs-lookup"><span data-stu-id="bc68c-218">In the **Toolbox**, expand the **Standard** group if it is not already expanded.</span></span>  
<span data-ttu-id="bc68c-219">請注意，您可能需要展開左側的 [**工具箱**] 視窗以進行觀看。</span><span class="sxs-lookup"><span data-stu-id="bc68c-219">Note that you may need to expand the **Toolbox** window on the left to view it.</span></span>
4. <span data-ttu-id="bc68c-220">將[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控制項拖曳至頁面上，並將它放在第一行**歡迎使用 Visual Web Developer**的**div**元素方塊中間。</span><span class="sxs-lookup"><span data-stu-id="bc68c-220">Drag a [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control onto the page and drop it in the middle of the **div** element box that has **Welcome to Visual Web Developer** in the first line.</span></span>
5. <span data-ttu-id="bc68c-221">將 [ [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) ] 控制項拖曳至頁面上，並將它放在[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控制項的右邊。</span><span class="sxs-lookup"><span data-stu-id="bc68c-221">Drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page and drop it to the right of the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control.</span></span>
6. <span data-ttu-id="bc68c-222">將 [[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)] 控制項拖曳至頁面上，並將它放在[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控制項下方的另一行。</span><span class="sxs-lookup"><span data-stu-id="bc68c-222">Drag a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control onto the page and drop it on a separate line below the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>
7. <span data-ttu-id="bc68c-223">將插入點放在[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控制項上方，然後輸入**Enter：** 。</span><span class="sxs-lookup"><span data-stu-id="bc68c-223">Put the insertion point above the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control, and then type **Enter your name:** .</span></span>

    <span data-ttu-id="bc68c-224">此靜態 HTML 文字是[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控制項的標題。</span><span class="sxs-lookup"><span data-stu-id="bc68c-224">This static HTML text is the caption for the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control.</span></span> <span data-ttu-id="bc68c-225">您可以在相同頁面上混合使用靜態 HTML 和伺服器控制項。</span><span class="sxs-lookup"><span data-stu-id="bc68c-225">You can mix static HTML and server controls on the same page.</span></span> <span data-ttu-id="bc68c-226">下圖顯示三個控制項在**設計**視圖中的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="bc68c-226">The following illustration shows how the three controls appear in **Design** view.</span></span>

    <span data-ttu-id="bc68c-227">![設計檢視中的三個控制項](creating-a-basic-web-forms-page/_static/image9.png "設計檢視中的三個控制項")</span><span class="sxs-lookup"><span data-stu-id="bc68c-227">![Three controls in Design view](creating-a-basic-web-forms-page/_static/image9.png "Three controls in Design view")</span></span>

### <a name="setting-control-properties"></a><span data-ttu-id="bc68c-228">設定控制項屬性</span><span class="sxs-lookup"><span data-stu-id="bc68c-228">Setting Control Properties</span></span>

<span data-ttu-id="bc68c-229">Visual Studio 提供各種方式，讓您在頁面上設定控制項的屬性。</span><span class="sxs-lookup"><span data-stu-id="bc68c-229">Visual Studio offers you various ways to set the properties of controls on the page.</span></span> <span data-ttu-id="bc68c-230">在本逐步解說的這個部分中，您將會在**設計**視圖和**原始**檔視圖中設定屬性。</span><span class="sxs-lookup"><span data-stu-id="bc68c-230">In this part of the walkthrough, you will set properties in both **Design** view and **Source** view.</span></span>

### <a name="to-set-control-properties"></a><span data-ttu-id="bc68c-231">若要設定控制項屬性</span><span class="sxs-lookup"><span data-stu-id="bc68c-231">To set control properties</span></span>

1. <span data-ttu-id="bc68c-232">首先，從 [**流覽**] 功能表中選取，以顯示 [**屬性**] 視窗-&gt;**其他 Windows** -&gt; [**屬性] 視窗**。</span><span class="sxs-lookup"><span data-stu-id="bc68c-232">First, display the **Properties** windows by selecting from the **View** menu -&gt; **Other Windows** -&gt; **Properties Window**.</span></span> <span data-ttu-id="bc68c-233">您也可以選取**F4**顯示 [**屬性**] 視窗。</span><span class="sxs-lookup"><span data-stu-id="bc68c-233">You could alternatively select **F4** to display the **Properties** window.</span></span>
2. <span data-ttu-id="bc68c-234">選取 [[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)] 控制項，然後在 [**屬性**] 視窗中，將 [**文字**] 的值設定為 [**顯示名稱**]。</span><span class="sxs-lookup"><span data-stu-id="bc68c-234">Select the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, and then in the **Properties** window, set the value of **Text** to **Display Name**.</span></span> <span data-ttu-id="bc68c-235">您輸入的文字會出現在設計工具中的按鈕上，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="bc68c-235">The text you entered appears on the button in the designer, as shown in the following illustration.</span></span>

    <span data-ttu-id="bc68c-236">![設定按鈕文字](creating-a-basic-web-forms-page/_static/image10.png "設定按鈕文字")</span><span class="sxs-lookup"><span data-stu-id="bc68c-236">![Set Button text](creating-a-basic-web-forms-page/_static/image10.png "Set Button text")</span></span>
3. <span data-ttu-id="bc68c-237">切換至**來源**視圖。</span><span class="sxs-lookup"><span data-stu-id="bc68c-237">Switch to **Source** view.</span></span>

    <span data-ttu-id="bc68c-238">**來源**視圖會顯示網頁的 HTML，包括 Visual Studio 為伺服器控制項建立的元素。</span><span class="sxs-lookup"><span data-stu-id="bc68c-238">**Source** view displays the HTML for the page, including the elements that Visual Studio has created for the server controls.</span></span> <span data-ttu-id="bc68c-239">控制項是使用類似 HTML 的語法來宣告，不同的是，標記會使用前置詞**asp：** ，並包含屬性**runat =&quot;server&quot;** 。</span><span class="sxs-lookup"><span data-stu-id="bc68c-239">Controls are declared using HTML-like syntax, except that the tags use the prefix **asp:** and include the attribute **runat=&quot;server&quot;**.</span></span>

    <span data-ttu-id="bc68c-240">控制項屬性會宣告為屬性。</span><span class="sxs-lookup"><span data-stu-id="bc68c-240">Control properties are declared as attributes.</span></span> <span data-ttu-id="bc68c-241">例如，當您在步驟1中設定[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控制項的[text](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx)屬性時，實際上是在控制項的標記中設定**text**屬性。</span><span class="sxs-lookup"><span data-stu-id="bc68c-241">For example, when you set the [Text](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx) property for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, in step 1, you were actually setting the **Text** attribute in the control's markup.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="bc68c-242">所有控制項都是在**form**元素內部，也就是屬性**runat =&quot;server&quot;** 。</span><span class="sxs-lookup"><span data-stu-id="bc68c-242">All the controls are inside a **form** element, which also has the attribute **runat=&quot;server&quot;**.</span></span> <span data-ttu-id="bc68c-243">**Runat =&quot;server&quot;** 屬性，以及控制項標記的**asp：** 前置詞會標記控制項，以便在頁面執行時由伺服器上的 ASP.NET 處理。</span><span class="sxs-lookup"><span data-stu-id="bc68c-243">The **runat=&quot;server&quot;** attribute and the **asp:** prefix for control tags mark the controls so that they are processed by ASP.NET on the server when the page runs.</span></span> <span data-ttu-id="bc68c-244">&lt;形式的程式碼（ **runat）&quot;server&quot;&gt;** 和 **&lt;script runat =&quot;server&quot;&gt;** 專案會原封不動地傳送給瀏覽器，這就是為什麼 ASP.NET 程式碼必須在開頭標記包含**runat =&quot;server&quot;** 屬性的元素內部。</span><span class="sxs-lookup"><span data-stu-id="bc68c-244">Code outside of **&lt;form runat=&quot;server&quot;&gt;** and **&lt;script runat=&quot;server&quot;&gt;** elements is sent unchanged to the browser, which is why the ASP.NET code must be inside an element whose opening tag contains the **runat=&quot;server&quot;** attribute.</span></span>
4. <span data-ttu-id="bc68c-245">接下來，您會將其他屬性新增至[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控制項。</span><span class="sxs-lookup"><span data-stu-id="bc68c-245">Next, you will add an additional property to the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)  control.</span></span> <span data-ttu-id="bc68c-246">將插入點直接放在 [ **&lt;asp： label]&gt;** 標記中的 [ **asp： label** ] 後面，然後按**空格鍵**。</span><span class="sxs-lookup"><span data-stu-id="bc68c-246">Put the insertion point directly after **asp:Label** in the **&lt;asp:Label&gt;** tag, and then press **SPACEBAR**.</span></span>

    <span data-ttu-id="bc68c-247">此時會出現一個下拉式清單，顯示您可以為[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控制項設定的可用屬性清單。</span><span class="sxs-lookup"><span data-stu-id="bc68c-247">A drop-down list appears that displays the list of available properties you can set for a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span> <span data-ttu-id="bc68c-248">這項功能稱為**IntelliSense**，可協助您在**原始**檔中，使用伺服器控制項、HTML 元素和頁面上其他專案的語法。</span><span class="sxs-lookup"><span data-stu-id="bc68c-248">This feature, referred to as **IntelliSense**, helps you in **Source** view with the syntax of server controls, HTML elements, and other items on the page.</span></span> <span data-ttu-id="bc68c-249">下圖顯示 [[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)] 控制項的 [ **IntelliSense** ] 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="bc68c-249">The following illustration shows the **IntelliSense** drop-down list for the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>

    <span data-ttu-id="bc68c-250">![IntelliSense 屬性](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense 屬性")</span><span class="sxs-lookup"><span data-stu-id="bc68c-250">![IntelliSense attributes](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense attributes")</span></span>
5. <span data-ttu-id="bc68c-251">選取 [**前景**]，然後輸入等號。</span><span class="sxs-lookup"><span data-stu-id="bc68c-251">Select **ForeColor** and then type an equal sign.</span></span>

    <span data-ttu-id="bc68c-252">IntelliSense 會顯示色彩清單。</span><span class="sxs-lookup"><span data-stu-id="bc68c-252">IntelliSense displays a list of colors.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="bc68c-253">您可以在 [流覽程式碼] 時按下**CTRL + J** ，隨時顯示 [ **IntelliSense** ] 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="bc68c-253">You can display an **IntelliSense** drop-down list at any time by pressing **CTRL+J** when viewing code.</span></span>
6. <span data-ttu-id="bc68c-254">選取 **[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** 控制項文字的色彩。</span><span class="sxs-lookup"><span data-stu-id="bc68c-254">Select a color for the **[Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** control's text.</span></span> <span data-ttu-id="bc68c-255">請確定您選取的色彩夠深，可以針對白色背景閱讀。</span><span class="sxs-lookup"><span data-stu-id="bc68c-255">Make sure you select a color that is dark enough to read against a white background.</span></span>

    <span data-ttu-id="bc68c-256">**前景**屬性是以您選取的色彩完成，包括右引號。</span><span class="sxs-lookup"><span data-stu-id="bc68c-256">The **ForeColor** attribute is completed with the color that you have selected, including the closing quotation mark.</span></span>

### <a name="programming-the-button-control"></a><span data-ttu-id="bc68c-257">程式設計按鈕控制項</span><span class="sxs-lookup"><span data-stu-id="bc68c-257">Programming the Button Control</span></span>

<span data-ttu-id="bc68c-258">在此逐步解說中，您將撰寫程式碼，以讀取使用者在文字方塊中輸入的名稱，然後在 [[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)] 控制項中顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="bc68c-258">For this walkthrough, you will write code that reads the name that the user enters into the text box and then displays the name in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>

### <a name="add-a-default-button-event-handler"></a><span data-ttu-id="bc68c-259">新增預設按鈕事件處理常式</span><span class="sxs-lookup"><span data-stu-id="bc68c-259">Add a default button event handler</span></span>

1. <span data-ttu-id="bc68c-260">切換至**設計**視圖。</span><span class="sxs-lookup"><span data-stu-id="bc68c-260">Switch to **Design** view.</span></span>
2. <span data-ttu-id="bc68c-261">按兩下 [[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)] 控制項。</span><span class="sxs-lookup"><span data-stu-id="bc68c-261">Double-click the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>

    <span data-ttu-id="bc68c-262">根據預設，Visual Studio 會切換至程式碼後置檔案，並建立[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控制項的預設事件（ [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件）的基本架構事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="bc68c-262">By default, Visual Studio switches to a code-behind file and creates a skeleton event handler for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control's default event, the [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event.</span></span> <span data-ttu-id="bc68c-263">程式碼後置檔案會將您的 UI 標記（例如 HTML）與您的伺服器程式碼C#隔開（例如）。</span><span class="sxs-lookup"><span data-stu-id="bc68c-263">The code-behind file separates your UI markup (such as HTML) from your server code (such as C#).</span></span>   
   <span data-ttu-id="bc68c-264">游標會定位於此事件處理常式的加入程式碼。</span><span class="sxs-lookup"><span data-stu-id="bc68c-264">The cursor is positioned to added code for this event handler.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="bc68c-265">在 [**設計**視圖] 中按兩下控制項，只是您可以建立事件處理常式的數種方式之一。</span><span class="sxs-lookup"><span data-stu-id="bc68c-265">Double-clicking a control in **Design** view is just one of several ways you can create event handlers.</span></span>
3. <span data-ttu-id="bc68c-266">在**Button1\_按一下**[事件處理常式]，輸入**Label1** ，後面接著句號（ **.** ）。</span><span class="sxs-lookup"><span data-stu-id="bc68c-266">Inside the **Button1\_Click** event handler, type **Label1** followed by a period (**.**).</span></span>

    <span data-ttu-id="bc68c-267">當您在標籤（**Label1**）的**識別碼**之後輸入句點時，Visual Studio 會顯示[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控制項的可用成員清單，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="bc68c-267">When you type the period after the **ID** of the label (**Label1**), Visual Studio displays a list of available members for the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control, as shown in the following illustration.</span></span> <span data-ttu-id="bc68c-268">成員通常是屬性、方法或事件。</span><span class="sxs-lookup"><span data-stu-id="bc68c-268">A member commonly a property, method, or event.</span></span>

    <span data-ttu-id="bc68c-269">![程式碼視圖中的 IntelliSense](creating-a-basic-web-forms-page/_static/image12.png "程式碼檢視中的 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="bc68c-269">![IntelliSense in Code view](creating-a-basic-web-forms-page/_static/image12.png "IntelliSense in Code view")</span></span>
4. <span data-ttu-id="bc68c-270">完成按鈕的**Click**事件處理常式，使其讀取，如下列程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="bc68c-270">Finish the **Click** event handler for the button so that it reads as shown in the following code example.</span></span>

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample1.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample2.vb?highlight=2)]
5. <span data-ttu-id="bc68c-271">以滑鼠右鍵按一下**方案總管**中的 [ *FirstWebPage* ]，然後選取 [**視圖標記**]，切換回流覽 HTML 標籤的**來源**視圖。</span><span class="sxs-lookup"><span data-stu-id="bc68c-271">Switch back to viewing the **Source** view of your HTML markup by right-clicking *FirstWebPage.aspx* in the **Solution Explorer** and selecting **View Markup**.</span></span>
6. <span data-ttu-id="bc68c-272">流覽至 [ **&lt;asp：] 按鈕&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="bc68c-272">Scroll to the **&lt;asp:Button&gt;** element.</span></span> <span data-ttu-id="bc68c-273">請注意， **&lt;asp： Button&gt;** 元素現在具有屬性**Onclick =&quot;Button1\_按一下 [&quot;** ]。</span><span class="sxs-lookup"><span data-stu-id="bc68c-273">Note that the **&lt;asp:Button&gt;** element now has the attribute **onclick=&quot;Button1\_Click&quot;**.</span></span>

    <span data-ttu-id="bc68c-274">這個屬性會將按鈕的[Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件系結至您在上一個步驟中編碼的處理常式方法。</span><span class="sxs-lookup"><span data-stu-id="bc68c-274">This attribute binds the button's [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event to the handler method you coded in the previous step.</span></span>

    <span data-ttu-id="bc68c-275">事件處理常式方法可以有任何名稱;您看到的名稱是 Visual Studio 所建立的預設名稱。</span><span class="sxs-lookup"><span data-stu-id="bc68c-275">Event handler methods can have any name; the name you see is the default name created by Visual Studio.</span></span> <span data-ttu-id="bc68c-276">重點是，HTML 中用於**OnClick**屬性的名稱必須符合程式碼後置中定義之方法的名稱。</span><span class="sxs-lookup"><span data-stu-id="bc68c-276">The important point is that the name used for the **OnClick** attribute in the HTML must match the name of a method defined in the code-behind.</span></span>

### <a name="running-the-page"></a><span data-ttu-id="bc68c-277">正在執行頁面</span><span class="sxs-lookup"><span data-stu-id="bc68c-277">Running the Page</span></span>

<span data-ttu-id="bc68c-278">您現在可以在頁面上測試伺服器控制項。</span><span class="sxs-lookup"><span data-stu-id="bc68c-278">You can now test the server controls on the page.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="bc68c-279">若要執行頁面</span><span class="sxs-lookup"><span data-stu-id="bc68c-279">To run the page</span></span>

1. <span data-ttu-id="bc68c-280">按**CTRL + F5**在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="bc68c-280">Press **CTRL+F5** to run the page in the browser.</span></span> <span data-ttu-id="bc68c-281">如果發生錯誤，請重新檢查上述步驟。</span><span class="sxs-lookup"><span data-stu-id="bc68c-281">If an error occurs, recheck the steps above.</span></span>
2. <span data-ttu-id="bc68c-282">在文字方塊中輸入名稱，然後按一下 [**顯示名稱**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bc68c-282">Enter a name into the text box and click the **Display Name** button.</span></span>

    <span data-ttu-id="bc68c-283">您輸入的名稱會顯示在 [[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)] 控制項中。</span><span class="sxs-lookup"><span data-stu-id="bc68c-283">The name you entered is displayed in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span> <span data-ttu-id="bc68c-284">請注意，當您按一下按鈕時，頁面就會張貼到 Web 服務器。</span><span class="sxs-lookup"><span data-stu-id="bc68c-284">Note that when you click the button, the page is posted to the Web server.</span></span> <span data-ttu-id="bc68c-285">ASP.NET 接著會重新建立頁面，執行您的程式碼（在此案例中，[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控制項的[Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件處理常式會執行），然後將新頁面傳送至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="bc68c-285">ASP.NET then recreates the page, runs your code (in this case, the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control's [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event handler runs), and then sends the new page to the browser.</span></span> <span data-ttu-id="bc68c-286">如果您在瀏覽器中監看狀態列，您可以看到頁面在每次按一下按鈕時，都會往返 Web 服務器。</span><span class="sxs-lookup"><span data-stu-id="bc68c-286">If you watch the status bar in the browser, you can see that the page is making a round trip to the Web server each time you click the button.</span></span>
3. <span data-ttu-id="bc68c-287">在瀏覽器中，以滑鼠右鍵按一下頁面，然後選取 [ **view source**]，以查看您正在執行之網頁的來源。</span><span class="sxs-lookup"><span data-stu-id="bc68c-287">In the browser, view the source of the page you are running by right-clicking on the page and selecting **View source**.</span></span>

    <span data-ttu-id="bc68c-288">在頁面原始碼中，您會看到不含任何伺服器程式碼的 HTML。</span><span class="sxs-lookup"><span data-stu-id="bc68c-288">In the page source code, you see HTML without any server code.</span></span> <span data-ttu-id="bc68c-289">具體而言，您看不到您在**原始**檔視圖中使用的 **&lt;asp：&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="bc68c-289">Specifically, you do not see the **&lt;asp:&gt;** elements that you were working with in **Source** view.</span></span> <span data-ttu-id="bc68c-290">當頁面執行時，ASP.NET 會處理伺服器控制項，並將 HTML 專案轉譯成頁面，以執行代表控制項的函式。</span><span class="sxs-lookup"><span data-stu-id="bc68c-290">When the page runs, ASP.NET processes the server controls and renders HTML elements to the page that perform the functions that represent the control.</span></span> <span data-ttu-id="bc68c-291">例如， **&lt;asp： Button&gt;** 控制項會轉譯為 HTML **&lt;輸入類型 =&quot;提交&quot;&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="bc68c-291">For example, the **&lt;asp:Button&gt;** control is rendered as the HTML **&lt;input type=&quot;submit&quot;&gt;** element.</span></span>
4. <span data-ttu-id="bc68c-292">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="bc68c-292">Close the browser.</span></span>

## <a name="working-with-additional-controls"></a><span data-ttu-id="bc68c-293">使用其他控制項</span><span class="sxs-lookup"><span data-stu-id="bc68c-293">Working with Additional Controls</span></span>

<a id="sectionToggle2"></a>

<span data-ttu-id="bc68c-294">在本逐步解說的這個部分中，您將使用[Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項，這會一次顯示一個月的日期。</span><span class="sxs-lookup"><span data-stu-id="bc68c-294">In this part of the walkthrough, you will work with the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control, which displays dates a month at a time.</span></span> <span data-ttu-id="bc68c-295">行事[曆](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項比您使用的按鈕、文字方塊和標籤更為複雜，並說明伺服器控制項的一些進一步功能。</span><span class="sxs-lookup"><span data-stu-id="bc68c-295">The [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control is a more complex control than the button, text box, and label you have been working with and illustrates some further capabilities of server controls.</span></span>

<span data-ttu-id="bc68c-296">在本節中，您會將[WebControls](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)新增至頁面，並將其格式化。</span><span class="sxs-lookup"><span data-stu-id="bc68c-296">In this section, you will add a [System.Web.UI.WebControls.Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control to the page and format it.</span></span>

### <a name="to-add-a-calendar-control"></a><span data-ttu-id="bc68c-297">若要加入行事曆控制項</span><span class="sxs-lookup"><span data-stu-id="bc68c-297">To add a Calendar control</span></span>

1. <span data-ttu-id="bc68c-298">在 Visual Studio 中，切換至 [**設計**視圖]。</span><span class="sxs-lookup"><span data-stu-id="bc68c-298">In Visual Studio, switch to **Design** view.</span></span>
2. <span data-ttu-id="bc68c-299">從 [**工具箱**] 的 [**標準**] 區段中，將行事[曆](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項拖曳至頁面上，並放在包含其他控制項的**div**元素下方。</span><span class="sxs-lookup"><span data-stu-id="bc68c-299">From the **Standard** section of the **Toolbox**, drag a [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control onto the page and drop it below the **div** element that contains the other controls.</span></span>

    <span data-ttu-id="bc68c-300">行事曆的智慧標籤面板隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="bc68c-300">The calendar's smart tag panel is displayed.</span></span> <span data-ttu-id="bc68c-301">此面板會顯示命令，讓您輕鬆地為選取的控制項執行最常見的工作。</span><span class="sxs-lookup"><span data-stu-id="bc68c-301">The panel displays commands that make it easy for you to perform the most common tasks for the selected control.</span></span> <span data-ttu-id="bc68c-302">下圖顯示在**設計**視圖中呈現的行事[曆](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項。</span><span class="sxs-lookup"><span data-stu-id="bc68c-302">The following illustration shows the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control as rendered in **Design** view.</span></span>

    <span data-ttu-id="bc68c-303">![設計檢視中的行事曆控制項](creating-a-basic-web-forms-page/_static/image13.png "設計檢視中的 Calendar 控制項")</span><span class="sxs-lookup"><span data-stu-id="bc68c-303">![Calendar control in Design view](creating-a-basic-web-forms-page/_static/image13.png "Calendar control in Design view")</span></span>
3. <span data-ttu-id="bc68c-304">在智慧標籤面板中，選擇 [**自動格式化**]。</span><span class="sxs-lookup"><span data-stu-id="bc68c-304">In the smart tag panel, choose **Auto Format**.</span></span>

    <span data-ttu-id="bc68c-305">[**自動格式化**] 對話方塊隨即顯示，可讓您選取行事曆的格式化配置。</span><span class="sxs-lookup"><span data-stu-id="bc68c-305">The **Auto Format** dialog box is displayed, which allows you to select a formatting scheme for the calendar.</span></span> <span data-ttu-id="bc68c-306">下圖顯示[Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項的 [**自動格式化**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bc68c-306">The following illustration shows the **Auto Format** dialog box for the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control.</span></span>

    <span data-ttu-id="bc68c-307">![自動格式化對話方塊（Calendar 控制項）](creating-a-basic-web-forms-page/_static/image14.png "自動格式化對話方塊 (Calendar 控制項)")</span><span class="sxs-lookup"><span data-stu-id="bc68c-307">![Auto Format dialog box (Calendar control)](creating-a-basic-web-forms-page/_static/image14.png "Auto Format dialog box (Calendar control)")</span></span>
4. <span data-ttu-id="bc68c-308">從 [**選取配置**] 清單中，選取 [**簡單**]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="bc68c-308">From the **Select a scheme** list, select **Simple** and then click **OK**.</span></span>
5. <span data-ttu-id="bc68c-309">切換至**來源**視圖。</span><span class="sxs-lookup"><span data-stu-id="bc68c-309">Switch to **Source** view.</span></span>

    <span data-ttu-id="bc68c-310">您可以看到 **&lt;asp： Calendar&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="bc68c-310">You can see the **&lt;asp:Calendar&gt;** element.</span></span> <span data-ttu-id="bc68c-311">這個元素比您稍早建立之簡單控制項的元素長很多。</span><span class="sxs-lookup"><span data-stu-id="bc68c-311">This element is much longer than the elements for the simple controls you created earlier.</span></span> <span data-ttu-id="bc68c-312">它也包含子項目，例如 **&lt;WeekEndDayStyle&gt;** ，這代表各種格式設定。</span><span class="sxs-lookup"><span data-stu-id="bc68c-312">It also includes subelements, such as **&lt;WeekEndDayStyle&gt;**, which represent various formatting settings.</span></span> <span data-ttu-id="bc68c-313">下圖顯示 [**來源**視圖] 中的行事[曆](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項。</span><span class="sxs-lookup"><span data-stu-id="bc68c-313">The following illustration shows the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control in **Source** view.</span></span> <span data-ttu-id="bc68c-314">（您在 [**原始**檔視圖] 中看到的確切標記可能與圖例稍有不同）。</span><span class="sxs-lookup"><span data-stu-id="bc68c-314">(The exact markup that you see in **Source** view might differ slightly from the illustration.)</span></span>

    <span data-ttu-id="bc68c-315">![來源視圖中的行事曆控制項](creating-a-basic-web-forms-page/_static/image15.png "原始碼檢視中的 Calendar 控制項")</span><span class="sxs-lookup"><span data-stu-id="bc68c-315">![Calendar control in Source view](creating-a-basic-web-forms-page/_static/image15.png "Calendar control in Source view")</span></span>

### <a name="programming-the-calendar-control"></a><span data-ttu-id="bc68c-316">行事曆控制項程式設計</span><span class="sxs-lookup"><span data-stu-id="bc68c-316">Programming the Calendar Control</span></span>

<span data-ttu-id="bc68c-317">在本節中，您會將行事[曆](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項的程式設計為顯示目前選取的日期。</span><span class="sxs-lookup"><span data-stu-id="bc68c-317">In this section, you will program the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control to display the currently selected date.</span></span>

### <a name="to-program-the-calendar-control"></a><span data-ttu-id="bc68c-318">若要設計行事曆控制項的程式</span><span class="sxs-lookup"><span data-stu-id="bc68c-318">To program the Calendar control</span></span>

1. <span data-ttu-id="bc68c-319">在 [**設計**視圖] 中，按兩下 [行事[曆](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)] 控制項。</span><span class="sxs-lookup"><span data-stu-id="bc68c-319">In **Design** view, double-click the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control.</span></span>

    <span data-ttu-id="bc68c-320">新的事件處理常式隨即建立，並顯示在名為*FirstWebPage.aspx.cs*的程式碼後置檔案中。</span><span class="sxs-lookup"><span data-stu-id="bc68c-320">A new event handler is created and displayed in the code-behind file named *FirstWebPage.aspx.cs*.</span></span>
2. <span data-ttu-id="bc68c-321">使用下列程式碼完成[SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx)事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="bc68c-321">Finish the [SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx) event handler with the following code.</span></span>

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample3.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample4.vb?highlight=2)]

    <span data-ttu-id="bc68c-322">上述程式碼會將 [標籤] 控制項的文字設定為行事曆控制項的選取日期。</span><span class="sxs-lookup"><span data-stu-id="bc68c-322">The above code sets the text of the label control to the selected date of the calendar control.</span></span>

### <a name="running-the-page"></a><span data-ttu-id="bc68c-323">正在執行頁面</span><span class="sxs-lookup"><span data-stu-id="bc68c-323">Running the Page</span></span>

<span data-ttu-id="bc68c-324">您現在可以測試行事曆。</span><span class="sxs-lookup"><span data-stu-id="bc68c-324">You can now test the calendar.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="bc68c-325">若要執行頁面</span><span class="sxs-lookup"><span data-stu-id="bc68c-325">To run the page</span></span>

1. <span data-ttu-id="bc68c-326">按**CTRL + F5**在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="bc68c-326">Press **CTRL+F5** to run the page in the browser.</span></span>
2. <span data-ttu-id="bc68c-327">按一下行事曆中的日期。</span><span class="sxs-lookup"><span data-stu-id="bc68c-327">Click a date in the calendar.</span></span>

    <span data-ttu-id="bc68c-328">您所按的日期會顯示在 [[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)] 控制項中。</span><span class="sxs-lookup"><span data-stu-id="bc68c-328">The date you clicked is displayed in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>
3. <span data-ttu-id="bc68c-329">在瀏覽器中，查看頁面的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="bc68c-329">In the browser, view the source code for the page.</span></span>

    <span data-ttu-id="bc68c-330">請注意， [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項已轉譯成**資料表**，每日都是**td**元素。</span><span class="sxs-lookup"><span data-stu-id="bc68c-330">Note that the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control has been rendered to the page as a **table**, with each day as a **td** element.</span></span>
4. <span data-ttu-id="bc68c-331">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="bc68c-331">Close the browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc68c-332">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc68c-332">Next Steps</span></span>

<a id="nextStepsToggle"></a>

<span data-ttu-id="bc68c-333">本逐步解說已說明 Visual Studio 頁面設計工具的基本功能。</span><span class="sxs-lookup"><span data-stu-id="bc68c-333">This walkthrough has illustrated the basic features of the Visual Studio page designer.</span></span> <span data-ttu-id="bc68c-334">既然您已瞭解如何在 Visual Studio 中建立和編輯 Web form 頁面，您可能會想要探索其他功能。</span><span class="sxs-lookup"><span data-stu-id="bc68c-334">Now that you understand how to create and edit a Web Forms page in Visual Studio, you might want to explore other features.</span></span> <span data-ttu-id="bc68c-335">例如，您可能會想要執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="bc68c-335">For example, you might want to do the following:</span></span>

- <span data-ttu-id="bc68c-336">遵循[使用 ASP.NET 4.5 Web Forms 和 Visual Studio 2013 消費者入門](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)的逐步教學課程系列，深入瞭解如何 ASP.NET Web form。</span><span class="sxs-lookup"><span data-stu-id="bc68c-336">Learn more about ASP.NET Web Forms by following the step-by-step tutorial series [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md).</span></span>
- <span data-ttu-id="bc68c-337">深入瞭解級聯樣式表（CSS）。</span><span class="sxs-lookup"><span data-stu-id="bc68c-337">Learn more about Cascading style sheets (CSS).</span></span> <span data-ttu-id="bc68c-338">如需詳細資訊，請參閱[使用 CSS 總覽](https://msdn.microsoft.com/library/bb398931.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bc68c-338">For details, see [Working with CSS Overview](https://msdn.microsoft.com/library/bb398931.aspx).</span></span>
