---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: Visual Studio 2013 中的程式碼編輯 ASP.NET Web Forms |Microsoft Docs
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 3473ad476fbbebc58e12586334b4600f57cf17ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632745"
---
# <a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a><span data-ttu-id="6648e-102">在 Visual Studio 2013 中以程式碼編輯 ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="6648e-102">Code Editing ASP.NET Web Forms in Visual Studio 2013</span></span>

<span data-ttu-id="6648e-103">依[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="6648e-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="6648e-104">在許多 ASP.NET Web Form 頁面中，您可以 Visual Basic、 C#或其他語言撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="6648e-104">In many ASP.NET Web Form pages, you write code in Visual Basic, C#, or another language.</span></span> <span data-ttu-id="6648e-105">Visual Studio 中的程式碼編輯器可協助您快速撰寫程式碼，同時協助您避免錯誤。</span><span class="sxs-lookup"><span data-stu-id="6648e-105">The code editor in Visual Studio can help you write code quickly while helping you avoid errors.</span></span> <span data-ttu-id="6648e-106">此外，編輯器也提供一些方法，讓您建立可重複使用的程式碼，以協助減少您需要執行的工作量。</span><span class="sxs-lookup"><span data-stu-id="6648e-106">In addition, the editor provides ways for you to create reusable code to help reduce the amount of work you need to do.</span></span>

<span data-ttu-id="6648e-107">本逐步解說說明 Visual Studio 程式碼編輯器的各種功能。</span><span class="sxs-lookup"><span data-stu-id="6648e-107">This walkthrough illustrates various features of the Visual Studio code editor.</span></span>

<span data-ttu-id="6648e-108">在這個逐步解說期間，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="6648e-108">During this walkthrough, you will learn how to:</span></span>

- <span data-ttu-id="6648e-109">修正內嵌程式碼錯誤。</span><span class="sxs-lookup"><span data-stu-id="6648e-109">Correct inline coding errors.</span></span>
- <span data-ttu-id="6648e-110">重構和重新命名程式碼。</span><span class="sxs-lookup"><span data-stu-id="6648e-110">Refactor and rename code.</span></span>
- <span data-ttu-id="6648e-111">重新命名變數和物件。</span><span class="sxs-lookup"><span data-stu-id="6648e-111">Rename variables and objects.</span></span>
- <span data-ttu-id="6648e-112">插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="6648e-112">Insert code snippets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6648e-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6648e-113">Prerequisites</span></span>

<span data-ttu-id="6648e-114">若要完成這個逐步解說，您將需要：</span><span class="sxs-lookup"><span data-stu-id="6648e-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="6648e-115">[適用于 Web 的](https://www.microsoft.com/visualstudio/11/downloads#express-web) [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或 Microsoft Visual Studio Express 2013。</span><span class="sxs-lookup"><span data-stu-id="6648e-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="6648e-116">.NET Framework 會自動安裝。</span><span class="sxs-lookup"><span data-stu-id="6648e-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="6648e-117">Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 for Web 通常會在本教學課程系列中稱為 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6648e-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="6648e-118">如果您使用 Visual Studio，本逐步解說會假設您在第一次啟動 Visual Studio 時選取了 [ **Web 開發**] 集合。</span><span class="sxs-lookup"><span data-stu-id="6648e-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="6648e-119">如需詳細資訊，請參閱[如何：選取 Web 開發環境設定](https://msdn.microsoft.com/library/ff521558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6648e-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="6648e-120">建立 Web 應用程式專案和頁面</span><span class="sxs-lookup"><span data-stu-id="6648e-120">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="6648e-121">在逐步解說的這個部分中，您將建立 Web 應用程式專案，並在其中加入新的頁面。</span><span class="sxs-lookup"><span data-stu-id="6648e-121">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="6648e-122">若要建立 Web 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="6648e-122">To create a Web application project</span></span>

1. <span data-ttu-id="6648e-123">開啟 Microsoft Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6648e-123">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="6648e-124">在 [檔案] 功能表上，選取 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="6648e-124">On the **File** menu, select **New Project**.</span></span>  
    <span data-ttu-id="6648e-125">![檔案 功能表](code-editing-in-web-forms-pages/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6648e-125">![File Menu](code-editing-in-web-forms-pages/_static/image1.png)</span></span>

    <span data-ttu-id="6648e-126">[ **新增專案** ] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="6648e-126">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="6648e-127">選取左側的 [&gt; **Visual C#**  -&gt; **Web** templates] 群組 -**範本**。</span><span class="sxs-lookup"><span data-stu-id="6648e-127">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="6648e-128">選擇中間欄的 [ASP.NET Web 應用程式] 範本。</span><span class="sxs-lookup"><span data-stu-id="6648e-128">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="6648e-129">將專案命名為***BasicWebApp*** ，然後按一下 [**確定]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6648e-129">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
<span data-ttu-id="6648e-130">![[New Project] \(新增專案\) 對話方塊](code-editing-in-web-forms-pages/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="6648e-130">![New Project dialog box](code-editing-in-web-forms-pages/_static/image2.png)</span></span>
6. <span data-ttu-id="6648e-131">接下來，選取 [ **Web** form] 範本，然後按一下 [**確定]** 按鈕以建立專案。</span><span class="sxs-lookup"><span data-stu-id="6648e-131">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
<span data-ttu-id="6648e-132">![[New ASP.NET Project] 對話方塊](code-editing-in-web-forms-pages/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="6648e-132">![New ASP.NET Project dialog box](code-editing-in-web-forms-pages/_static/image3.png)</span></span>  

    <span data-ttu-id="6648e-133">Visual Studio 會建立新的專案，其中包含根據 Web form 範本預先建立的功能。</span><span class="sxs-lookup"><span data-stu-id="6648e-133">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span>

## <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="6648e-134">建立新的 ASP.NET Web Forms 頁面</span><span class="sxs-lookup"><span data-stu-id="6648e-134">Creating a new ASP.NET Web Forms Page</span></span>

<span data-ttu-id="6648e-135">當您使用**ASP.NET Web 應用程式**專案範本建立新的 Web form 應用程式時，Visual Studio 會新增名為*default.aspx*的 ASP.NET 網頁（Web form 網頁），以及其他數個檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="6648e-135">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="6648e-136">您可以使用*預設的 .aspx*頁面作為 Web 應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="6648e-136">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="6648e-137">不過，在此逐步解說中，您將建立並使用新的頁面。</span><span class="sxs-lookup"><span data-stu-id="6648e-137">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="6648e-138">若要將頁面新增至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6648e-138">To add a page to the Web application</span></span>

1. <span data-ttu-id="6648e-139">在**方案總管**中，以滑鼠**按右鍵 Web**應用程式名稱（在本教學課程中，應用程式名稱是**BasicWebSite**），然後按一下 [新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="6648e-139">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="6648e-140">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6648e-140">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="6648e-141">選取左側的 [ **Visual C#**  -&gt; **Web**範本] 群組。</span><span class="sxs-lookup"><span data-stu-id="6648e-141">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="6648e-142">然後，從中間清單中選取 [ **Web Form** ]，並將它命名為*FirstWebPage .aspx*。</span><span class="sxs-lookup"><span data-stu-id="6648e-142">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    <span data-ttu-id="6648e-143">![[加入新項目] 對話方塊](code-editing-in-web-forms-pages/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="6648e-143">![Add New Item dialog box](code-editing-in-web-forms-pages/_static/image4.png)</span></span>
3. <span data-ttu-id="6648e-144">按一下 [**新增**]，將 Web form 頁面加入至您的專案。</span><span class="sxs-lookup"><span data-stu-id="6648e-144">Click **Add** to add the Web Forms page to your project.</span></span>  
 <span data-ttu-id="6648e-145">Visual Studio 會建立新的頁面，並開啟它。</span><span class="sxs-lookup"><span data-stu-id="6648e-145">Visual Studio creates the new page and opens it.</span></span>
4. <span data-ttu-id="6648e-146">接下來，將此新頁面設定為預設的啟動頁面。</span><span class="sxs-lookup"><span data-stu-id="6648e-146">Next, set this new page as the default startup page.</span></span> <span data-ttu-id="6648e-147">在**方案總管**中，以滑鼠右鍵按一下名為*FirstWebPage*的新頁面，然後選取 [**設定為起始頁**]。</span><span class="sxs-lookup"><span data-stu-id="6648e-147">In **Solution Explorer**, right-click the new page named *FirstWebPage.aspx* and select **Set As Start Page**.</span></span> <span data-ttu-id="6648e-148">下一次執行此應用程式來測試進度時，您會在瀏覽器中自動看到這個新頁面。</span><span class="sxs-lookup"><span data-stu-id="6648e-148">The next time you run this application to test our progress, you will automatically see this new page in the browser.</span></span>

## <a name="correcting-inline-coding-errors"></a><span data-ttu-id="6648e-149">修正內嵌程式碼錯誤</span><span class="sxs-lookup"><span data-stu-id="6648e-149">Correcting Inline Coding Errors</span></span>

<span data-ttu-id="6648e-150">Visual Studio 中的程式碼編輯器可協助您在撰寫程式碼時避免錯誤，而且如果您發生錯誤，則程式碼編輯器會協助您更正錯誤。</span><span class="sxs-lookup"><span data-stu-id="6648e-150">The code editor in Visual Studio helps you to avoid errors as you write code, and if you have made an error, the code editor helps you to correct the error.</span></span> <span data-ttu-id="6648e-151">在本逐步解說的這個部分中，您將撰寫一行程式碼，以說明編輯器中的錯誤修正功能。</span><span class="sxs-lookup"><span data-stu-id="6648e-151">In this part of the walkthrough, you will write a line of code that illustrate the error correction features in the editor.</span></span>

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a><span data-ttu-id="6648e-152">更正 Visual Studio 中的簡單編碼錯誤</span><span class="sxs-lookup"><span data-stu-id="6648e-152">To correct simple coding errors in Visual Studio</span></span>

1. <span data-ttu-id="6648e-153">在**設計**視圖中，按兩下空白頁面，為頁面的**Load**事件建立處理常式。</span><span class="sxs-lookup"><span data-stu-id="6648e-153">In **Design** view, double-click the blank page to create a handler for the **Load** event for the page.</span></span>   
   <span data-ttu-id="6648e-154">您只會使用事件處理常式做為撰寫一些程式碼的位置。</span><span class="sxs-lookup"><span data-stu-id="6648e-154">You are using the event handler only as a place to write some code.</span></span>
2. <span data-ttu-id="6648e-155">在處理常式中，輸入下列包含錯誤的行，然後按**enter**：</span><span class="sxs-lookup"><span data-stu-id="6648e-155">Inside the handler, type the following line that contains an error and press **ENTER**:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   <span data-ttu-id="6648e-156">當您按下**enter**時，程式碼編輯器會在發生問題的程式碼區域下，加上綠色和紅色底線（通常會呼叫 &quot;彎曲&quot; 線）。</span><span class="sxs-lookup"><span data-stu-id="6648e-156">When you press **ENTER**, the code editor places green and red underlines (commonly call &quot;squiggly&quot; lines) under areas of the code that have issues.</span></span> <span data-ttu-id="6648e-157">綠色底線表示警告。</span><span class="sxs-lookup"><span data-stu-id="6648e-157">A green underline indicates a warning.</span></span> <span data-ttu-id="6648e-158">紅色波浪線表示您必須修正的錯誤。</span><span class="sxs-lookup"><span data-stu-id="6648e-158">A red underline indicates an error that you must fix.</span></span> 

    <span data-ttu-id="6648e-159">將滑鼠指標放在 `myStr` 上方，即可看到工具提示，告訴您有關警告的資訊。</span><span class="sxs-lookup"><span data-stu-id="6648e-159">Hold the mouse pointer over `myStr` to see a tooltip that tells you about the warning.</span></span> <span data-ttu-id="6648e-160">此外，請將滑鼠指標停留在紅色底線上，以查看錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="6648e-160">Also, hold your mouse pointer over the red underline to see the error message.</span></span>

    <span data-ttu-id="6648e-161">下圖顯示具有底線的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6648e-161">The following image shows the code with the underlines.</span></span>

    <span data-ttu-id="6648e-162">![設計檢視中的歡迎文字](code-editing-in-web-forms-pages/_static/image5.png "設計檢視中的歡迎文字")</span><span class="sxs-lookup"><span data-stu-id="6648e-162">![Welcome text in Design view](code-editing-in-web-forms-pages/_static/image5.png "Welcome text in Design view")</span></span>  
   <span data-ttu-id="6648e-163">若要修正此錯誤，您必須在行尾 `;` 加上分號。</span><span class="sxs-lookup"><span data-stu-id="6648e-163">The error must be fixed by adding a semicolon `;` to the end of the line.</span></span> <span data-ttu-id="6648e-164">警告只會通知您尚未使用 `myStr` 變數。</span><span class="sxs-lookup"><span data-stu-id="6648e-164">The warning simply notifies you that you haven't used the `myStr` variable yet.</span></span>  

    > [!NOTE] 
    > 
    > <span data-ttu-id="6648e-165">在 Visual Studio 中，您可以選取 **工具** -&gt;**選項** -&gt; 字型**和色彩**，來查看目前的程式碼格式設定。</span><span class="sxs-lookup"><span data-stu-id="6648e-165">You view your current code formatting settings in Visual Studio by selecting **Tools** -&gt; **Options** -&gt; **Fonts and Colors**.</span></span>

## <a name="refactoring-and-renaming"></a><span data-ttu-id="6648e-166">重構和重新命名</span><span class="sxs-lookup"><span data-stu-id="6648e-166">Refactoring and Renaming</span></span>

<span data-ttu-id="6648e-167">重構是一種軟體方法，其中牽涉到重構您的程式碼，讓您更容易瞭解和維護，同時保留其功能。</span><span class="sxs-lookup"><span data-stu-id="6648e-167">Refactoring is a software methodology that involves restructuring your code to make it easier to understand and to maintain, while preserving its functionality.</span></span> <span data-ttu-id="6648e-168">簡單的範例可能是您在事件處理常式中撰寫程式碼，以從資料庫取得資料。</span><span class="sxs-lookup"><span data-stu-id="6648e-168">A simple example might be that you write code in an event handler to get data from a database.</span></span> <span data-ttu-id="6648e-169">當您開發頁面時，您會發現需要從數個不同的處理常式存取資料。</span><span class="sxs-lookup"><span data-stu-id="6648e-169">As you develop your page, you discover that you need to access the data from several different handlers.</span></span> <span data-ttu-id="6648e-170">因此，您可以在頁面中建立資料存取方法，並在處理常式中插入方法的呼叫，以重構頁面的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6648e-170">Therefore, you refactor the page's code by creating a data-access method in the page and inserting calls to the method in the handlers.</span></span>

<span data-ttu-id="6648e-171">[程式碼編輯器] 包含可協助您執行各種重構工作的工具。</span><span class="sxs-lookup"><span data-stu-id="6648e-171">The code editor includes tools to help you perform various refactoring tasks.</span></span> <span data-ttu-id="6648e-172">在此逐步解說中，您將使用兩種重構技術：重新命名變數和解壓縮方法。</span><span class="sxs-lookup"><span data-stu-id="6648e-172">In this walkthrough, you will work with two refactoring techniques: renaming variables and extracting methods.</span></span> <span data-ttu-id="6648e-173">其他重構選項包括封裝欄位、將區域變數升級為方法參數，以及管理方法參數。</span><span class="sxs-lookup"><span data-stu-id="6648e-173">Other refactoring options include encapsulating fields, promoting local variables to method parameters, and managing method parameters.</span></span> <span data-ttu-id="6648e-174">這些重構選項的可用性取決於程式碼中的位置。</span><span class="sxs-lookup"><span data-stu-id="6648e-174">The availability of these refactoring options depends on the location in the code.</span></span>

### <a name="refactoring-code"></a><span data-ttu-id="6648e-175">重構程式碼</span><span class="sxs-lookup"><span data-stu-id="6648e-175">Refactoring Code</span></span>

<span data-ttu-id="6648e-176">常見的重構案例是從另一個成員內的程式碼建立（解壓縮）方法，例如方法。</span><span class="sxs-lookup"><span data-stu-id="6648e-176">A common refactoring scenario is to create (extract) a method from code that is inside another member, such as a method.</span></span> <span data-ttu-id="6648e-177">這會減少原始成員的大小，並讓解壓縮的程式碼可重複使用。</span><span class="sxs-lookup"><span data-stu-id="6648e-177">This reduces the size of the original member and makes the extracted code reusable.</span></span>

<span data-ttu-id="6648e-178">在逐步解說的這個部分中，您將撰寫一些簡單的程式碼，然後從它解壓縮方法。</span><span class="sxs-lookup"><span data-stu-id="6648e-178">In this part of the walkthrough, you will write some simple code, and then extract a method from it.</span></span> <span data-ttu-id="6648e-179">支援重構C#，因此您將建立使用C#作為其程式設計語言的頁面。</span><span class="sxs-lookup"><span data-stu-id="6648e-179">Refactoring is supported for C#, so you will create a page that uses C# as its programming language.</span></span>

### <a name="to-extract-a-method-in-a-c-page"></a><span data-ttu-id="6648e-180">若要在C#頁面中解壓縮方法</span><span class="sxs-lookup"><span data-stu-id="6648e-180">To extract a method in a C# page</span></span>

1. <span data-ttu-id="6648e-181">切換至**設計**視圖。</span><span class="sxs-lookup"><span data-stu-id="6648e-181">Switch to **Design** view.</span></span>
2. <span data-ttu-id="6648e-182">在 [**工具箱**] 的 [**標準**] 索引標籤中，將 [[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)] 控制項拖曳至頁面上。</span><span class="sxs-lookup"><span data-stu-id="6648e-182">In the **Toolbox**, from the **Standard** tab, drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page.</span></span>
3. <span data-ttu-id="6648e-183">按兩下 [**按鈕**] 控制項，以建立其[click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件的處理常式，然後新增下列反白顯示的程式碼：</span><span class="sxs-lookup"><span data-stu-id="6648e-183">Double-click the **Button** control to create a handler for its [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event, and then add the following highlighted code:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   <span data-ttu-id="6648e-184">程式碼會建立**arraylist**物件，並使用迴圈將其載入值，然後使用另一個迴圈來顯示**ArrayList**物件的內容。</span><span class="sxs-lookup"><span data-stu-id="6648e-184">The code creates an **ArrayList** object, uses a loop to load it with values, and then uses another loop to display the contents of the **ArrayList** object.</span></span>
4. <span data-ttu-id="6648e-185">按**CTRL + F5**執行頁面，然後按一下**按鈕**以確定您看到下列輸出：</span><span class="sxs-lookup"><span data-stu-id="6648e-185">Press **CTRL+F5** to run the page, and then click the **button** to make sure that you see the following output:</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. <span data-ttu-id="6648e-186">返回程式碼編輯器，然後在事件處理常式中選取下列幾行。</span><span class="sxs-lookup"><span data-stu-id="6648e-186">Return to the code editor, and then select the following lines in the event handler.</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. <span data-ttu-id="6648e-187">以滑鼠右鍵按一下選取範圍，按一下 [**重構**]，然後選擇 [**解壓縮方法**]。</span><span class="sxs-lookup"><span data-stu-id="6648e-187">Right-click the selection, click **Refactor**, and then choose **Extract Method**.</span></span> 

    <span data-ttu-id="6648e-188">[**解壓縮方法**] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="6648e-188">The **Extract Method** dialog box appears.</span></span>
7. <span data-ttu-id="6648e-189">在 [**新方法名稱**] 方塊中，輸入**DisplayArray**，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="6648e-189">In the **New Method Name** box, type **DisplayArray**, and then click **OK**.</span></span> 

    <span data-ttu-id="6648e-190">[程式碼編輯器] 會建立名為 `DisplayArray`的新方法，然後在迴圈最初的**Click**處理常式中呼叫新的方法。</span><span class="sxs-lookup"><span data-stu-id="6648e-190">The code editor creates a new method named `DisplayArray`, and puts a call to the new method in the **Click** handler where the loop was originally.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. <span data-ttu-id="6648e-191">按**CTRL + F5**再次執行頁面，然後按一下**按鈕**。</span><span class="sxs-lookup"><span data-stu-id="6648e-191">Press **CTRL+F5** to run the page again, and click the **button**.</span></span>

    <span data-ttu-id="6648e-192">頁面的運作方式與之前相同。</span><span class="sxs-lookup"><span data-stu-id="6648e-192">The page functions the same as it did before.</span></span> <span data-ttu-id="6648e-193">現在可以從 page 類別中的任何位置呼叫 `DisplayArray` 方法。</span><span class="sxs-lookup"><span data-stu-id="6648e-193">The `DisplayArray` method can now be call from anywhere in the page class.</span></span>

## <a name="renaming-variables"></a><span data-ttu-id="6648e-194">重新命名變數</span><span class="sxs-lookup"><span data-stu-id="6648e-194">Renaming Variables</span></span>

<span data-ttu-id="6648e-195">當您使用變數和物件時，您可能會想要在程式碼中參考它們之後將它們重新命名。</span><span class="sxs-lookup"><span data-stu-id="6648e-195">When you work with variables, as well as objects, you might want to rename them after they are already referenced in your code.</span></span> <span data-ttu-id="6648e-196">不過，如果您錯過重新命名其中一個參考，則重新命名變數和物件可能會導致程式碼中斷。</span><span class="sxs-lookup"><span data-stu-id="6648e-196">However, renaming variables and objects can cause the code to break if you miss renaming one of the references.</span></span> <span data-ttu-id="6648e-197">因此，您可以使用重構來執行重新命名。</span><span class="sxs-lookup"><span data-stu-id="6648e-197">Therefore, you can use refactoring to perform the renaming.</span></span>

### <a name="to-use-refactoring-to-rename-a-variable"></a><span data-ttu-id="6648e-198">若要使用重構來重新命名變數</span><span class="sxs-lookup"><span data-stu-id="6648e-198">To use refactoring to rename a variable</span></span>

1. <span data-ttu-id="6648e-199">在**Click**事件處理常式中，找出下面這一行：</span><span class="sxs-lookup"><span data-stu-id="6648e-199">In the **Click** event handler, locate the following line:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. <span data-ttu-id="6648e-200">以滑鼠右鍵按一下變數名稱 `alist`，選擇 [**重構**]，然後選擇 [**重新命名**]。</span><span class="sxs-lookup"><span data-stu-id="6648e-200">Right-click the variable name `alist`, choose **Refactor**, and then choose **Rename**.</span></span>

    <span data-ttu-id="6648e-201">[**重新命名**] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="6648e-201">The **Rename** dialog box appears.</span></span>
3. <span data-ttu-id="6648e-202">在 [**新名稱**] 方塊中，輸入**ArrayList1** ，並確認已選取 [**預覽參考變更**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6648e-202">In the **New name** box, type **ArrayList1** and make sure the **Preview reference changes** checkbox has been selected.</span></span> <span data-ttu-id="6648e-203">然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6648e-203">Then click **OK**.</span></span>

    <span data-ttu-id="6648e-204">[**預覽變更**] 對話方塊隨即出現，並顯示一個樹狀結構，其中包含您要重新命名之變數的所有參考。</span><span class="sxs-lookup"><span data-stu-id="6648e-204">The **Preview Changes** dialog box appears, and displays a tree that contains all references to the variable that you are renaming.</span></span>
4. <span data-ttu-id="6648e-205">按一下 **[** 套用] 以關閉 [**預覽變更**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6648e-205">Click **Apply** to close the **Preview Changes** dialog box.</span></span>

    <span data-ttu-id="6648e-206">明確參考您所選取之實例的變數會重新命名。</span><span class="sxs-lookup"><span data-stu-id="6648e-206">The variables that refer specifically to the instance that you selected are renamed.</span></span> <span data-ttu-id="6648e-207">不過要注意的是，下面這一行中的變數 `alist` 不會重新命名。</span><span class="sxs-lookup"><span data-stu-id="6648e-207">Note, however, that the variable `alist` in the following line is not renamed.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    <span data-ttu-id="6648e-208">這一行中的變數 `alist` 不會重新命名，因為它不代表您重新命名之變數 `alist` 的相同值。</span><span class="sxs-lookup"><span data-stu-id="6648e-208">The variable `alist` in this line is not renamed because it does not represent the same value as the variable `alist` that you renamed.</span></span> <span data-ttu-id="6648e-209">`DisplayArray` 宣告中的變數 `alist` 是該方法的本機變數。</span><span class="sxs-lookup"><span data-stu-id="6648e-209">The variable `alist` in the `DisplayArray` declaration is a local variable for that method.</span></span> <span data-ttu-id="6648e-210">這說明使用重構來重新命名變數與直接在編輯器中執行「尋找和取代」動作不同。重構會以其所使用之變數的語義知識來重新命名變數。</span><span class="sxs-lookup"><span data-stu-id="6648e-210">This illustrates that using refactoring to rename variables is different than simply performing a find-and-replace action in the editor; refactoring renames variables with knowledge of the semantics of the variable that it is working with.</span></span>

## <a name="inserting-snippets"></a><span data-ttu-id="6648e-211">插入程式碼片段</span><span class="sxs-lookup"><span data-stu-id="6648e-211">Inserting Snippets</span></span>

<span data-ttu-id="6648e-212">由於 Web Forms 開發人員經常需要執行許多編碼工作，程式碼編輯器會提供程式碼片段的程式庫或預先編寫的程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="6648e-212">Because there are many coding tasks that Web Forms developers frequently need to perform, the code editor provides a library of snippets, or blocks of prewritten code.</span></span> <span data-ttu-id="6648e-213">您可以將這些程式碼片段插入至您的頁面。</span><span class="sxs-lookup"><span data-stu-id="6648e-213">You can insert these snippets into your page.</span></span>

<span data-ttu-id="6648e-214">您在 Visual Studio 中使用的每一種語言在插入程式碼片段的方式上有些許差異。</span><span class="sxs-lookup"><span data-stu-id="6648e-214">Each language that you use in Visual Studio has slight differences in the way you insert code snippets.</span></span> <span data-ttu-id="6648e-215">如需插入程式碼片段的詳細資訊，請參閱[Visual Basic IntelliSense 程式碼片段](https://msdn.microsoft.com/library/18yz4be4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6648e-215">For information about inserting snippets, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx).</span></span> <span data-ttu-id="6648e-216">如需在視覺效果C#中插入程式碼片段的詳細資訊，請參閱[visual C#程式碼片段](https://msdn.microsoft.com/library/z41h7fat.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6648e-216">For information about inserting snippets in Visual C#, see [Visual C# Code Snippets](https://msdn.microsoft.com/library/z41h7fat.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6648e-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6648e-217">Next Steps</span></span>

<span data-ttu-id="6648e-218">本逐步解說已說明了 Visual Studio 2010 程式碼編輯器的基本功能，可用於更正程式碼中的錯誤、重構程式碼、重新命名變數，以及在程式碼中插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="6648e-218">This walkthrough has illustrated the basic features of the Visual Studio 2010 code editor for correcting errors in your code, refactoring code, renaming variables, and inserting code snippets into your code.</span></span> <span data-ttu-id="6648e-219">編輯器中的其他功能可以快速輕鬆地開發應用程式。</span><span class="sxs-lookup"><span data-stu-id="6648e-219">Additional features in the editor can make application development fast and easy.</span></span> <span data-ttu-id="6648e-220">例如，您可能要：</span><span class="sxs-lookup"><span data-stu-id="6648e-220">For example, you might want to:</span></span>

- <span data-ttu-id="6648e-221">深入瞭解 IntelliSense 的功能，例如修改 IntelliSense 選項、管理程式碼片段，以及線上搜尋程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="6648e-221">Learn more about the features of IntelliSense, such as modifying IntelliSense options, managing code snippets, and searching for code snippets online.</span></span> <span data-ttu-id="6648e-222">如需詳細資訊，請參閱 [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6648e-222">For more information, see [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx).</span></span>
- <span data-ttu-id="6648e-223">瞭解如何建立您自己的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="6648e-223">Learn how to create your own code snippets.</span></span> <span data-ttu-id="6648e-224">如需詳細資訊，請參閱[建立和使用 IntelliSense 程式碼片段](https://msdn.microsoft.com/library/ms165392.aspx)</span><span class="sxs-lookup"><span data-stu-id="6648e-224">For more information, see [Creating and Using IntelliSense Code Snippets](https://msdn.microsoft.com/library/ms165392.aspx)</span></span>
- <span data-ttu-id="6648e-225">深入瞭解 IntelliSense 程式碼片段的 Visual Basic 特定功能，例如自訂程式碼片段和疑難排解。</span><span class="sxs-lookup"><span data-stu-id="6648e-225">Learn more about the Visual Basic-specific features of IntelliSense code snippets, such as customizing the snippets and troubleshooting.</span></span> <span data-ttu-id="6648e-226">如需詳細資訊，請參閱[Visual Basic IntelliSense 程式碼片段](https://msdn.microsoft.com/library/18yz4be4.aspx)</span><span class="sxs-lookup"><span data-stu-id="6648e-226">For more information, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx)</span></span>
- <span data-ttu-id="6648e-227">深入瞭解 IntelliSense 的C#特定功能，例如重構和程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="6648e-227">Learn more about the C#-specific features of IntelliSense, such as refactoring and code snippets.</span></span> <span data-ttu-id="6648e-228">如需詳細資訊，請參閱[Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6648e-228">For more information, see [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx).</span></span>
