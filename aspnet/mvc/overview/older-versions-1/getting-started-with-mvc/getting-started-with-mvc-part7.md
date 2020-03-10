---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: 將驗證加入至模型 |Microsoft Docs
author: shanselman
description: 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 建立可從資料庫讀取和寫入的簡單 web 應用程式。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 9403be574324c34edf93bef1e0e4fd7ba68a3a9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543642"
---
# <a name="adding-validation-to-the-model"></a><span data-ttu-id="e1c85-104">將驗證新增至模型</span><span class="sxs-lookup"><span data-stu-id="e1c85-104">Adding Validation to the Model</span></span>

<span data-ttu-id="e1c85-105">由[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="e1c85-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="e1c85-106">這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="e1c85-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="e1c85-107">您將建立可從資料庫讀取和寫入的簡單 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1c85-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="e1c85-108">請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。</span><span class="sxs-lookup"><span data-stu-id="e1c85-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="e1c85-109">在本節中，我們將會執行在應用程式內啟用輸入驗證所需的支援。</span><span class="sxs-lookup"><span data-stu-id="e1c85-109">In this section we are going to implement the support necessary to enable input validation within our application.</span></span> <span data-ttu-id="e1c85-110">我們會確保資料庫內容一律是正確的，並在使用者嘗試輸入不正確電影資料時，為他們提供有用的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="e1c85-110">We'll ensure that our database content is always correct, and provide helpful error messages to end users when they try and enter Movie data which is not valid.</span></span> <span data-ttu-id="e1c85-111">首先，我們會將少量驗證邏輯新增至 Movie 類別。</span><span class="sxs-lookup"><span data-stu-id="e1c85-111">We'll begin by adding a little validation logic to the Movie class.</span></span>

<span data-ttu-id="e1c85-112">以滑鼠右鍵按一下 [模型] 資料夾，然後選取 [新增類別]。</span><span class="sxs-lookup"><span data-stu-id="e1c85-112">Right click on the Model folder and select Add Class.</span></span> <span data-ttu-id="e1c85-113">將您的類別命名為 Movie。</span><span class="sxs-lookup"><span data-stu-id="e1c85-113">Name your class Movie.</span></span>

<span data-ttu-id="e1c85-114">當我們稍早建立電影實體模型時，IDE 會建立 Movie 類別。</span><span class="sxs-lookup"><span data-stu-id="e1c85-114">When we created the Movie Entity Model earlier, the IDE created a Movie class.</span></span> <span data-ttu-id="e1c85-115">事實上，Movie 類別的一部分可以放在一個檔案中，而另一個檔案則部分。</span><span class="sxs-lookup"><span data-stu-id="e1c85-115">In fact, part of the Movie class can be in one file and part in another.</span></span> <span data-ttu-id="e1c85-116">這稱為部分類別。</span><span class="sxs-lookup"><span data-stu-id="e1c85-116">This is called a Partial Class.</span></span> <span data-ttu-id="e1c85-117">我們要從另一個檔案延伸 Movie 類別。</span><span class="sxs-lookup"><span data-stu-id="e1c85-117">We're going to extend the Movie class from another file.</span></span>

<span data-ttu-id="e1c85-118">我們將建立一個指向 "好友 class" 的部分 movie 類別，其中包含一些屬性，可將驗證提示提供給系統。</span><span class="sxs-lookup"><span data-stu-id="e1c85-118">We'll create a partial movie class that points to a "buddy class" with some attributes that will give validation hints to the system.</span></span> <span data-ttu-id="e1c85-119">我們會視需要標示 [標題] 和 [價格]，並堅持該價格在特定範圍內。</span><span class="sxs-lookup"><span data-stu-id="e1c85-119">We'll mark the Title and Price as Required, and also insist that the Price be within a certain range.</span></span> <span data-ttu-id="e1c85-120">以滑鼠右鍵按一下 [模型] 資料夾，然後選取 [新增類別]。</span><span class="sxs-lookup"><span data-stu-id="e1c85-120">Right click the Models folder and select Add Class.</span></span> <span data-ttu-id="e1c85-121">將您的類別命名為 Movie，然後按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e1c85-121">Name your class Movie and Click the OK button.</span></span> <span data-ttu-id="e1c85-122">我們的部分 Movie 類別看起來像這樣。</span><span class="sxs-lookup"><span data-stu-id="e1c85-122">Here's what our partial Movie class looks like.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

<span data-ttu-id="e1c85-123">重新執行您的應用程式，並嘗試輸入價格超過100的電影。</span><span class="sxs-lookup"><span data-stu-id="e1c85-123">Re-Run your application and try to enter a movie with a price over 100.</span></span> <span data-ttu-id="e1c85-124">提交表單之後，您會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="e1c85-124">You'll get an error after you've submitted the form.</span></span> <span data-ttu-id="e1c85-125">此錯誤會在伺服器端攔截，並在表單公佈之後發生。</span><span class="sxs-lookup"><span data-stu-id="e1c85-125">The error is caught on the server side and occurs after the Form is POSTed.</span></span> <span data-ttu-id="e1c85-126">請注意，ASP.NET MVC 的內建 HTML 協助程式如何聰明地顯示錯誤訊息，並在 textbox 元素內維護我們的值：</span><span class="sxs-lookup"><span data-stu-id="e1c85-126">Notice how ASP.NET MVC's built-in HTML helpers were smart enough to display the error message and maintain the values for us within the textbox elements:</span></span>

<span data-ttu-id="e1c85-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e1c85-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span></span>

<span data-ttu-id="e1c85-128">這項功能很好用，但是如果我們可以立即在用戶端上告知使用者，就很好用。</span><span class="sxs-lookup"><span data-stu-id="e1c85-128">This works great, but it'd be nice if we could tell the user on the client-side, immediately, before the server gets involved.</span></span>

<span data-ttu-id="e1c85-129">讓我們啟用一些使用 JavaScript 的用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="e1c85-129">Let's enable some client-side validation with JavaScript.</span></span>

## <a name="adding-client-side-validation"></a><span data-ttu-id="e1c85-130">加入用戶端驗證</span><span class="sxs-lookup"><span data-stu-id="e1c85-130">Adding Client-Side Validation</span></span>

<span data-ttu-id="e1c85-131">由於電影類別已經有一些驗證屬性，因此我們只需要將一些 JavaScript 檔案新增至 [建立 .aspx 視圖] 範本，然後新增一行程式碼，就可以進行用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="e1c85-131">Since our Movie class already has some validation attributes, we'll just need to add a few JavaScript files to our Create.aspx View template and add a line of code to enable client-side validation to take place.</span></span>

<span data-ttu-id="e1c85-132">從 VWD 中，移至 [Views/Movie] 資料夾，然後開啟 [建立 .aspx]。</span><span class="sxs-lookup"><span data-stu-id="e1c85-132">From within VWD go our Views/Movie folder and open up Create.aspx.</span></span>

<span data-ttu-id="e1c85-133">開啟 方案總管中的 腳本 資料夾，然後將下列三個腳本拖曳至 &lt;標頭&gt; 標記內。</span><span class="sxs-lookup"><span data-stu-id="e1c85-133">Open up the Scripts folder in the Solution Explorer and drag the following three scripts to within the &lt;head&gt; tag.</span></span>

- <span data-ttu-id="e1c85-134">Microsoftajax.debug.js .js</span><span class="sxs-lookup"><span data-stu-id="e1c85-134">MicrosoftAjax.js</span></span>
- <span data-ttu-id="e1c85-135">Microsoftmvcvalidation.js .js</span><span class="sxs-lookup"><span data-stu-id="e1c85-135">MicrosoftMvcValidation.js</span></span>

<span data-ttu-id="e1c85-136">您想要這些腳本檔案以這種順序出現。</span><span class="sxs-lookup"><span data-stu-id="e1c85-136">You want these script files to appear in this order.</span></span>

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

<span data-ttu-id="e1c85-137">此外，在 Html.beginform 的上方新增此一行：</span><span class="sxs-lookup"><span data-stu-id="e1c85-137">Also, add this single line above the Html.BeginForm:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

<span data-ttu-id="e1c85-138">以下是 IDE 中顯示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e1c85-138">Here's the code shown within the IDE.</span></span>

<span data-ttu-id="e1c85-139">[![電影-Microsoft Visual Web Developer 2010 Express （10）](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e1c85-139">[![Movies - Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span></span>

<span data-ttu-id="e1c85-140">執行您的應用程式並再次流覽/Movies/Create，然後按一下 [建立] 而不輸入任何資料。</span><span class="sxs-lookup"><span data-stu-id="e1c85-140">Run your application and visit /Movies/Create again, and click Create without entering any data.</span></span> <span data-ttu-id="e1c85-141">錯誤訊息會立即顯示，而不會有與將資料一起傳送回伺服器相關聯的 page flash。</span><span class="sxs-lookup"><span data-stu-id="e1c85-141">The error messages appear immediately without the page flash that we associate with sending data all the way back to the server.</span></span> <span data-ttu-id="e1c85-142">這是因為 ASP.NET MVC 現在會驗證用戶端（使用 JavaScript）和伺服器上的輸入。</span><span class="sxs-lookup"><span data-stu-id="e1c85-142">This is because ASP.NET MVC is now validating the input on both the client (using JavaScript) and on the server.</span></span>

<span data-ttu-id="e1c85-143">[![建立-Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="e1c85-143">[![Create - Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span></span>

<span data-ttu-id="e1c85-144">這看起來不錯！</span><span class="sxs-lookup"><span data-stu-id="e1c85-144">This is looking good!</span></span> <span data-ttu-id="e1c85-145">現在讓我們在資料庫中加入一個額外的資料行。</span><span class="sxs-lookup"><span data-stu-id="e1c85-145">Let's now add one additional column to the database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e1c85-146">[上一頁](getting-started-with-mvc-part6.md)
> [下一頁](getting-started-with-mvc-part8.md)</span><span class="sxs-lookup"><span data-stu-id="e1c85-146">[Previous](getting-started-with-mvc-part6.md)
[Next](getting-started-with-mvc-part8.md)</span></span>
