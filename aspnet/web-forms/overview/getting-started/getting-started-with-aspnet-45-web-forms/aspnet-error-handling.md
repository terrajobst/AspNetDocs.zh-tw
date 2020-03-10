---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: ASP.NET 錯誤處理 |Microsoft Docs
author: Erikre
description: 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們建立 ASP.NET Web Forms 應用程式的基本概念 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 9514142ca50b33470a3f4c033e4f8e319a9ee09b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566679"
---
# <a name="aspnet-error-handling"></a><span data-ttu-id="d4260-103">ASP.NET 錯誤處理</span><span class="sxs-lookup"><span data-stu-id="d4260-103">ASP.NET Error Handling</span></span>

<span data-ttu-id="d4260-104">依[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="d4260-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="d4260-105">[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="d4260-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="d4260-106">本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 建立 ASP.NET Web Forms 應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="d4260-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="d4260-107">本教學課程系列隨附有[ C#原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案。</span><span class="sxs-lookup"><span data-stu-id="d4260-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="d4260-108">在本教學課程中，您將修改 Wingtip 玩具範例應用程式，以包含錯誤處理和錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="d4260-108">In this tutorial, you will modify the Wingtip Toys sample application to include error handling and error logging.</span></span> <span data-ttu-id="d4260-109">錯誤處理會讓應用程式正常處理錯誤，並據以顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d4260-109">Error handling will allow the application to gracefully handle errors and display error messages accordingly.</span></span> <span data-ttu-id="d4260-110">錯誤記錄可讓您尋找並修正已發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-110">Error logging will allow you to find and fix errors that have occurred.</span></span> <span data-ttu-id="d4260-111">本教學課程是以先前的「URL 路由」教學課程為基礎，而且是 Wingtip 玩具教學課程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="d4260-111">This tutorial builds on the previous tutorial "URL Routing" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="d4260-112">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="d4260-112">What you'll learn:</span></span>

- <span data-ttu-id="d4260-113">如何將全域錯誤處理新增至應用程式的設定。</span><span class="sxs-lookup"><span data-stu-id="d4260-113">How to add global error handling to the application's configuration.</span></span>
- <span data-ttu-id="d4260-114">如何在應用程式、頁面和程式碼層級加入錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="d4260-114">How to add error handling at the application, page, and code levels.</span></span>
- <span data-ttu-id="d4260-115">如何記錄錯誤以供日後審查。</span><span class="sxs-lookup"><span data-stu-id="d4260-115">How to log errors for later review.</span></span>
- <span data-ttu-id="d4260-116">如何顯示不會危及安全性的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d4260-116">How to display error messages that do not compromise security.</span></span>
- <span data-ttu-id="d4260-117">如何執行錯誤記錄模組和處理常式（ELMAH）錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="d4260-117">How to implement Error Logging Modules and Handlers (ELMAH) error logging.</span></span>

## <a name="overview"></a><span data-ttu-id="d4260-118">概觀</span><span class="sxs-lookup"><span data-stu-id="d4260-118">Overview</span></span>

<span data-ttu-id="d4260-119">ASP.NET 應用程式必須能夠以一致的方式處理執行期間所發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-119">ASP.NET applications must be able to handle errors that occur during execution in a consistent manner.</span></span> <span data-ttu-id="d4260-120">ASP.NET 使用 common language runtime （CLR），這種方式可讓您以一致的方式來通知應用程式的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-120">ASP.NET uses the common language runtime (CLR), which provides a way of notifying applications of errors in a uniform way.</span></span> <span data-ttu-id="d4260-121">發生錯誤時，會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d4260-121">When an error occurs, an exception is thrown.</span></span> <span data-ttu-id="d4260-122">例外狀況是應用程式遇到的任何錯誤、條件或非預期的行為。</span><span class="sxs-lookup"><span data-stu-id="d4260-122">An exception is any error, condition, or unexpected behavior that an application encounters.</span></span>

<span data-ttu-id="d4260-123">在 .NET Framework 中，例外狀況是從 `System.Exception` 類別繼承的物件。</span><span class="sxs-lookup"><span data-stu-id="d4260-123">In the .NET Framework, an exception is an object that inherits from the `System.Exception` class.</span></span> <span data-ttu-id="d4260-124">從發生問題的程式碼區域擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d4260-124">An exception is thrown from an area of code where a problem has occurred.</span></span> <span data-ttu-id="d4260-125">例外狀況會在呼叫堆疊中向上傳遞至一個位置，應用程式會在此處提供可處理例外狀況的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d4260-125">The exception is passed up the call stack to a place where the application provides code to handle the exception.</span></span> <span data-ttu-id="d4260-126">如果應用程式未處理例外狀況，則會強制瀏覽器顯示錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4260-126">If the application does not handle the exception, the browser is forced to display the error details.</span></span>

<span data-ttu-id="d4260-127">最佳做法是，在程式碼層級中處理 `Try`/`Catch`/`Finally` 區塊內的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-127">As a best practice, handle errors in at the code level in `Try`/`Catch`/`Finally` blocks within your code.</span></span> <span data-ttu-id="d4260-128">請嘗試放置這些區塊，讓使用者能夠更正其發生所在內容中的問題。</span><span class="sxs-lookup"><span data-stu-id="d4260-128">Try to place these blocks so that the user can correct problems in the context in which they occur.</span></span> <span data-ttu-id="d4260-129">如果錯誤處理區塊與錯誤發生的位置太遠，則為使用者提供修正問題所需的資訊會變得更難。</span><span class="sxs-lookup"><span data-stu-id="d4260-129">If the error handling blocks are too far away from where the error occurred, it becomes more difficult to provide users with the information they need to fix the problem.</span></span>

### <a name="exception-class"></a><span data-ttu-id="d4260-130">Exception 類別</span><span class="sxs-lookup"><span data-stu-id="d4260-130">Exception Class</span></span>

<span data-ttu-id="d4260-131">例外狀況類別是例外狀況繼承來源的基類。</span><span class="sxs-lookup"><span data-stu-id="d4260-131">The Exception class is the base class from which exceptions inherit.</span></span> <span data-ttu-id="d4260-132">大部分的例外狀況物件都是例外狀況類別之某些衍生類別的實例，例如 `SystemException` 類別、`IndexOutOfRangeException` 類別或 `ArgumentNullException` 類別。</span><span class="sxs-lookup"><span data-stu-id="d4260-132">Most exception objects are instances of some derived class of the Exception class, such as the `SystemException` class, the `IndexOutOfRangeException` class, or the `ArgumentNullException` class.</span></span> <span data-ttu-id="d4260-133">Exception 類別具有屬性，例如 `StackTrace` 屬性、`InnerException` 屬性和 `Message` 屬性，可提供有關所發生錯誤的特定資訊。</span><span class="sxs-lookup"><span data-stu-id="d4260-133">The Exception class has properties, such as the `StackTrace` property, the `InnerException` property, and the `Message` property, that provide specific information about the error that has occurred.</span></span>

### <a name="exception-inheritance-hierarchy"></a><span data-ttu-id="d4260-134">例外狀況繼承階層架構</span><span class="sxs-lookup"><span data-stu-id="d4260-134">Exception Inheritance Hierarchy</span></span>

<span data-ttu-id="d4260-135">執行時間具有一組基底例外狀況，衍生自在遇到例外狀況時，執行時間擲回的 `SystemException` 類別。</span><span class="sxs-lookup"><span data-stu-id="d4260-135">The runtime has a base set of exceptions deriving from the `SystemException` class that the runtime throws when an exception is encountered.</span></span> <span data-ttu-id="d4260-136">大部分繼承自例外狀況類別（例如 `IndexOutOfRangeException` 類別和 `ArgumentNullException` 類別）的類別，都不會執行其他成員。</span><span class="sxs-lookup"><span data-stu-id="d4260-136">Most of the classes that inherit from the Exception class, such as the `IndexOutOfRangeException` class and the `ArgumentNullException` class, do not implement additional members.</span></span> <span data-ttu-id="d4260-137">因此，例外狀況的最重要資訊可以在例外狀況階層、例外狀況名稱和例外狀況中包含的資訊中找到。</span><span class="sxs-lookup"><span data-stu-id="d4260-137">Therefore, the most important information for an exception can be found in the hierarchy of exceptions, the exception name, and the information contained in the exception.</span></span>

### <a name="exception-handling-hierarchy"></a><span data-ttu-id="d4260-138">例外狀況處理階層架構</span><span class="sxs-lookup"><span data-stu-id="d4260-138">Exception Handling Hierarchy</span></span>

<span data-ttu-id="d4260-139">在 ASP.NET Web Forms 應用程式中，可以根據特定的處理階層來處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d4260-139">In an ASP.NET Web Forms application, exceptions can be handled based on a specific handling hierarchy.</span></span> <span data-ttu-id="d4260-140">例外狀況可以在下列層級處理：</span><span class="sxs-lookup"><span data-stu-id="d4260-140">An exception can be handled at the following levels:</span></span>

- <span data-ttu-id="d4260-141">應用程式層級</span><span class="sxs-lookup"><span data-stu-id="d4260-141">Application level</span></span>
- <span data-ttu-id="d4260-142">分頁層級</span><span class="sxs-lookup"><span data-stu-id="d4260-142">Page level</span></span>
- <span data-ttu-id="d4260-143">程式碼層級</span><span class="sxs-lookup"><span data-stu-id="d4260-143">Code level</span></span>

<span data-ttu-id="d4260-144">當應用程式處理例外狀況時，通常會抓取並向使用者顯示繼承自例外狀況類別的例外狀況的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="d4260-144">When an application handles exceptions, additional information about the exception that is inherited from the Exception class can often be retrieved and displayed to the user.</span></span> <span data-ttu-id="d4260-145">除了應用程式、頁面和程式碼層級之外，您也可以使用 IIS 自訂處理常式來處理 HTTP 模組層級的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d4260-145">In addition to application, page, and code level, you can also handle exceptions at the HTTP module level and by using an IIS custom handler.</span></span>

### <a name="application-level-error-handling"></a><span data-ttu-id="d4260-146">應用層級錯誤處理</span><span class="sxs-lookup"><span data-stu-id="d4260-146">Application Level Error Handling</span></span>

<span data-ttu-id="d4260-147">您可以藉由修改應用程式的設定，或在應用程式的*global.asax*檔案中新增 `Application_Error` 處理常式，在應用層級處理預設錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-147">You can handle default errors at the application level either by modifying your application's configuration or by adding an `Application_Error` handler in the *Global.asax* file of your application.</span></span>

<span data-ttu-id="d4260-148">您可以藉由將 `customErrors` 區段加入至*web.config*檔案，來處理預設錯誤和 HTTP 錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-148">You can handle default errors and HTTP errors by adding a `customErrors` section to the *Web.config* file.</span></span> <span data-ttu-id="d4260-149">[`customErrors`] 區段可讓您指定在發生錯誤時，使用者將被重新導向至的預設頁面。</span><span class="sxs-lookup"><span data-stu-id="d4260-149">The `customErrors` section allows you to specify a default page that users will be redirected to when an error occurs.</span></span> <span data-ttu-id="d4260-150">它也可讓您指定特定狀態碼錯誤的個別頁面。</span><span class="sxs-lookup"><span data-stu-id="d4260-150">It also allows you to specify individual pages for specific status code errors.</span></span>

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

<span data-ttu-id="d4260-151">可惜的是，當您使用設定將使用者重新導向至不同的頁面時，您沒有發生之錯誤的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4260-151">Unfortunately, when you use the configuration to redirect the user to a different page, you do not have the details of the error that occurred.</span></span>

<span data-ttu-id="d4260-152">不過，您可以藉由將程式碼加入至*global.asax*檔案中的 `Application_Error` 處理常式，來將發生在應用程式任何位置的錯誤設為陷阱。</span><span class="sxs-lookup"><span data-stu-id="d4260-152">However, you can trap errors that occur anywhere in your application by adding code to the `Application_Error` handler in the *Global.asax* file.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a><span data-ttu-id="d4260-153">頁面層級錯誤事件處理</span><span class="sxs-lookup"><span data-stu-id="d4260-153">Page Level Error Event Handling</span></span>

<span data-ttu-id="d4260-154">頁面層級處理常式會將使用者傳回發生錯誤的頁面，但因為不會維護控制項的實例，所以頁面上不會再有任何專案。</span><span class="sxs-lookup"><span data-stu-id="d4260-154">A page-level handler returns the user to the page where the error occurred, but because instances of controls are not maintained, there will no longer be anything on the page.</span></span> <span data-ttu-id="d4260-155">若要將錯誤詳細資料提供給應用程式的使用者，您必須特別將錯誤詳細資料寫入至頁面。</span><span class="sxs-lookup"><span data-stu-id="d4260-155">To provide the error details to the user of the application, you must specifically write the error details to the page.</span></span>

<span data-ttu-id="d4260-156">您通常會使用頁面層級錯誤處理常式來記錄未處理的錯誤，或將使用者帶到可以顯示有用資訊的頁面。</span><span class="sxs-lookup"><span data-stu-id="d4260-156">You would typically use a page-level error handler to log unhandled errors or to take the user to a page that can display helpful information.</span></span>

<span data-ttu-id="d4260-157">這個程式碼範例會顯示 ASP.NET 網頁中錯誤事件的處理常式。</span><span class="sxs-lookup"><span data-stu-id="d4260-157">This code example shows a handler for the Error event in an ASP.NET Web page.</span></span> <span data-ttu-id="d4260-158">這個處理常式會在頁面中的 `try`/`catch` 區塊內，捕捉所有尚未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d4260-158">This handler catches all exceptions that are not already handled within `try`/`catch` blocks in the page.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

<span data-ttu-id="d4260-159">處理錯誤之後，您必須藉由呼叫伺服器物件的 `ClearError` 方法（`HttpServerUtility` 類別）來清除它，否則會看到先前發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-159">After you handle an error, you must clear it by calling the `ClearError` method of the Server object (`HttpServerUtility` class), otherwise you will see an error that has previously occurred.</span></span>

### <a name="code-level-error-handling"></a><span data-ttu-id="d4260-160">程式碼層級錯誤處理</span><span class="sxs-lookup"><span data-stu-id="d4260-160">Code Level Error Handling</span></span>

<span data-ttu-id="d4260-161">Try-catch 語句是由 try 區塊後面接著一個或多個 catch 子句所組成，這會指定不同例外狀況的處理常式。</span><span class="sxs-lookup"><span data-stu-id="d4260-161">The try-catch statement consists of a try block followed by one or more catch clauses, which specify handlers for different exceptions.</span></span> <span data-ttu-id="d4260-162">當擲回例外狀況時，common language runtime （CLR）會尋找處理此例外狀況的 catch 語句。</span><span class="sxs-lookup"><span data-stu-id="d4260-162">When an exception is thrown, the common language runtime (CLR) looks for the catch statement that handles this exception.</span></span> <span data-ttu-id="d4260-163">如果目前執行的方法不包含 catch 區塊，則 CLR 會查看呼叫目前方法的方法，依此類推，然後再向上呼叫堆疊。</span><span class="sxs-lookup"><span data-stu-id="d4260-163">If the currently executing method does not contain a catch block, the CLR looks at the method that called the current method, and so on, up the call stack.</span></span> <span data-ttu-id="d4260-164">如果找不到任何 catch 區塊，則 CLR 會向使用者顯示未處理的例外狀況訊息，並停止執行程式。</span><span class="sxs-lookup"><span data-stu-id="d4260-164">If no catch block is found, then the CLR displays an unhandled exception message to the user and stops execution of the program.</span></span>

<span data-ttu-id="d4260-165">下列程式碼範例顯示使用 `try`/`catch`/`finally` 來處理錯誤的常見方式。</span><span class="sxs-lookup"><span data-stu-id="d4260-165">The following code example shows a common way of using `try`/`catch`/`finally` to handle errors.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

<span data-ttu-id="d4260-166">在上述程式碼中，try 區塊包含需要針對可能的例外狀況進行防護的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d4260-166">In the above code, the try block contains the code that needs to be guarded against a possible exception.</span></span> <span data-ttu-id="d4260-167">會執行區塊，直到擲回例外狀況或成功完成區塊為止。</span><span class="sxs-lookup"><span data-stu-id="d4260-167">The block is executed until either an exception is thrown or the block is completed successfully.</span></span> <span data-ttu-id="d4260-168">如果發生 `FileNotFoundException` 例外狀況或 `IOException` 例外狀況，則會將執行轉移至不同的頁面。</span><span class="sxs-lookup"><span data-stu-id="d4260-168">If either a `FileNotFoundException` exception or an `IOException` exception occurs, the execution is transferred to a different page.</span></span> <span data-ttu-id="d4260-169">然後，就會執行包含在 finally 區塊中的程式碼，不論是否發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-169">Then, the code contained in the finally block is executed, whether an error occurred or not.</span></span>

## <a name="adding-error-logging-support"></a><span data-ttu-id="d4260-170">新增錯誤記錄支援</span><span class="sxs-lookup"><span data-stu-id="d4260-170">Adding Error Logging Support</span></span>

<span data-ttu-id="d4260-171">將錯誤處理新增至 Wingtip 玩具範例應用程式之前，您會將 `ExceptionUtility` 類別新增至*邏輯*資料夾，以新增錯誤記錄支援。</span><span class="sxs-lookup"><span data-stu-id="d4260-171">Before adding error handling to the Wingtip Toys sample application, you will add error logging support by adding an `ExceptionUtility` class to the *Logic* folder.</span></span> <span data-ttu-id="d4260-172">如此一來，每次應用程式處理錯誤時，錯誤詳細資料就會新增至錯誤記錄檔。</span><span class="sxs-lookup"><span data-stu-id="d4260-172">By doing this, each time the application handles an error, the error details will be added to the error log file.</span></span>

1. <span data-ttu-id="d4260-173">以滑鼠右鍵按一下*邏輯*資料夾，**然後選取 [** 新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="d4260-173">Right-click the *Logic* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="d4260-174">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d4260-174">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="d4260-175">選取左側的 [ **Visual C#**  -&gt; 程式**代碼**範本] 群組。</span><span class="sxs-lookup"><span data-stu-id="d4260-175">Select the **Visual C#** -&gt; **Code** templates group on the left.</span></span> <span data-ttu-id="d4260-176">然後，從中間清單中選取 [**類別**]，並將其命名為**ExceptionUtility.cs**。</span><span class="sxs-lookup"><span data-stu-id="d4260-176">Then, select **Class**from the middle list and name it **ExceptionUtility.cs**.</span></span>
3. <span data-ttu-id="d4260-177">選擇 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d4260-177">Choose **Add**.</span></span> <span data-ttu-id="d4260-178">隨即顯示新的類別檔案。</span><span class="sxs-lookup"><span data-stu-id="d4260-178">The new class file is displayed.</span></span>
4. <span data-ttu-id="d4260-179">將現有的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="d4260-179">Replace the existing code with the following:</span></span>  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

<span data-ttu-id="d4260-180">發生例外狀況時，可以藉由呼叫 `LogException` 方法，將例外狀況寫入例外狀況記錄檔。</span><span class="sxs-lookup"><span data-stu-id="d4260-180">When an exception occurs, the exception can be written to an exception log file by calling the `LogException` method.</span></span> <span data-ttu-id="d4260-181">這個方法會採用兩個參數，也就是 exception 物件和包含例外狀況來源之詳細資料的字串。</span><span class="sxs-lookup"><span data-stu-id="d4260-181">This method takes two parameters, the exception object and a string containing details about the source of the exception.</span></span> <span data-ttu-id="d4260-182">例外狀況記錄檔會寫入*應用程式\_Data*資料夾中的錯誤記錄檔 *.txt*檔案。</span><span class="sxs-lookup"><span data-stu-id="d4260-182">The exception log is written to the *ErrorLog.txt* file in the *App\_Data* folder.</span></span>

### <a name="adding-an-error-page"></a><span data-ttu-id="d4260-183">新增錯誤頁面</span><span class="sxs-lookup"><span data-stu-id="d4260-183">Adding an Error Page</span></span>

<span data-ttu-id="d4260-184">在 Wingtip 玩具範例應用程式中，會使用一個頁面來顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-184">In the Wingtip Toys sample application, one page will be used to display errors.</span></span> <span data-ttu-id="d4260-185">錯誤頁面的設計，是為了向網站的使用者顯示安全錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d4260-185">The error page is designed to show a secure error message to users of the site.</span></span> <span data-ttu-id="d4260-186">不過，如果使用者是發出 HTTP 要求的開發人員，而該服務是在程式碼所在的電腦上進行本機處理，則錯誤頁面上會顯示其他錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4260-186">However, if the user is a developer making an HTTP request that is being served locally on the machine where the code lives, additional error details will be displayed on the error page.</span></span>

1. <span data-ttu-id="d4260-187">以滑鼠右鍵按一下**方案總管**中的專案名稱（**Wingtip 玩具**），**然後選取 [** 新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="d4260-187">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="d4260-188">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d4260-188">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="d4260-189">選取左側的 [ **Visual C#**  -&gt; **Web**範本] 群組。</span><span class="sxs-lookup"><span data-stu-id="d4260-189">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="d4260-190">從中間清單中，選取 [**使用主版頁面的 Web 表單**]，並將它命名為**ErrorPage .aspx**。</span><span class="sxs-lookup"><span data-stu-id="d4260-190">From the middle list, select **Web Form with Master Page**,and name it **ErrorPage.aspx**.</span></span>
3. <span data-ttu-id="d4260-191">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d4260-191">Click **Add**.</span></span>
4. <span data-ttu-id="d4260-192">選取*網站*檔案作為主版頁面，然後選擇 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="d4260-192">Select the *Site.Master* file as the master page, and then choose **OK**.</span></span>
5. <span data-ttu-id="d4260-193">以下列內容取代現有的標記：</span><span class="sxs-lookup"><span data-stu-id="d4260-193">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. <span data-ttu-id="d4260-194">取代程式碼後置（*ErrorPage.aspx.cs*）的現有程式碼，使其看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="d4260-194">Replace the existing code of the code-behind (*ErrorPage.aspx.cs*) so that it appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

<span data-ttu-id="d4260-195">顯示錯誤頁面時，會執行 `Page_Load` 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="d4260-195">When the error page is displayed, the `Page_Load` event handler is executed.</span></span> <span data-ttu-id="d4260-196">在 `Page_Load` 處理常式中，會決定第一次處理錯誤的位置。</span><span class="sxs-lookup"><span data-stu-id="d4260-196">In the `Page_Load` handler, the location of where the error was first handled is determined.</span></span> <span data-ttu-id="d4260-197">然後，最後發生的錯誤是藉由呼叫伺服器物件的 `GetLastError` 方法來決定。</span><span class="sxs-lookup"><span data-stu-id="d4260-197">Then, the last error that occurred is determined by call the `GetLastError` method of the Server object.</span></span> <span data-ttu-id="d4260-198">如果例外狀況已不存在，則會建立一般例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d4260-198">If the exception no longer exists, a generic exception is created.</span></span> <span data-ttu-id="d4260-199">然後，如果 HTTP 要求是在本機提出，則會顯示所有錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4260-199">Then, if the HTTP request was made locally, all error details are shown.</span></span> <span data-ttu-id="d4260-200">在此情況下，只有執行 web 應用程式的本機電腦會看到這些錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4260-200">In this case, only the local machine running the web application will see these error details.</span></span> <span data-ttu-id="d4260-201">顯示錯誤資訊之後，會將錯誤新增至記錄檔，並從伺服器中清除錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-201">After the error information has been displayed, the error is added to the log file and the error is cleared from the server.</span></span>

### <a name="displaying-unhandled-error-messages-for-the-application"></a><span data-ttu-id="d4260-202">顯示應用程式的未處理錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="d4260-202">Displaying Unhandled Error Messages for the Application</span></span>

<span data-ttu-id="d4260-203">藉由將 `customErrors` 區段新增至*web.config 檔案*，您可以快速處理整個應用程式中發生的簡單錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-203">By adding a `customErrors` section to the *Web.config* file, you can quickly handle simple errors that occur throughout the application.</span></span> <span data-ttu-id="d4260-204">您也可以根據狀態碼值來指定如何處理錯誤，例如 404-找不到檔案。</span><span class="sxs-lookup"><span data-stu-id="d4260-204">You can also specify how to handle errors based on their status code value, such as 404 - File not found.</span></span>

#### <a name="update-the-configuration"></a><span data-ttu-id="d4260-205">更新設定</span><span class="sxs-lookup"><span data-stu-id="d4260-205">Update the Configuration</span></span>

<span data-ttu-id="d4260-206">將 `customErrors` 區段新增*至 web.config 檔案*，以更新設定。</span><span class="sxs-lookup"><span data-stu-id="d4260-206">Update the configuration by adding a `customErrors` section to the *Web.config* file.</span></span>

1. <span data-ttu-id="d4260-207">在**方案總管**中，尋找並開啟位於 Wingtip 玩具範例應用程式根目錄的*web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="d4260-207">In **Solution Explorer**, find and open the *Web.config* file at the root of the Wingtip Toys sample application.</span></span>
2. <span data-ttu-id="d4260-208">將 `customErrors` 區段新增至 [`<system.web>`] 節點*內的 web.config*檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d4260-208">Add the `customErrors` section to the *Web.config* file within the `<system.web>` node as follows:</span></span>   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. <span data-ttu-id="d4260-209">儲存 *Web.config* 檔案。</span><span class="sxs-lookup"><span data-stu-id="d4260-209">Save the *Web.config* file.</span></span>

<span data-ttu-id="d4260-210">`customErrors` 區段會指定模式，其設定為 "On"。</span><span class="sxs-lookup"><span data-stu-id="d4260-210">The `customErrors` section specifies the mode, which is set to "On".</span></span> <span data-ttu-id="d4260-211">它也會指定 `defaultRedirect`，這會告訴應用程式在發生錯誤時要流覽的頁面。</span><span class="sxs-lookup"><span data-stu-id="d4260-211">It also specifies the `defaultRedirect`, which tells the application which page to navigate to when an error occurs.</span></span> <span data-ttu-id="d4260-212">此外，您還加入了特定的錯誤元素，指定當找不到頁面時，如何處理404錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-212">In addition, you have added a specific error element that specifies how to handle a 404 error when a page is not found.</span></span> <span data-ttu-id="d4260-213">稍後在本教學課程中，您將會新增其他錯誤處理，以在應用層級上捕捉錯誤的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4260-213">Later in this tutorial, you will add additional error handling that will capture the details of an error at the application level.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="d4260-214">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="d4260-214">Running the Application</span></span>

<span data-ttu-id="d4260-215">您可以立即執行應用程式，以查看更新的路由。</span><span class="sxs-lookup"><span data-stu-id="d4260-215">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="d4260-216">按**F5**執行 Wingtip 玩具範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4260-216">Press **F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="d4260-217">瀏覽器會開啟並顯示*default.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="d4260-217">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="d4260-218">在瀏覽器中輸入下列 URL （請務必使用**您**的埠號碼）：</span><span class="sxs-lookup"><span data-stu-id="d4260-218">Enter the following URL into the browser (be sure to use **your** port number):</span></span>  
    `https://localhost:44300/NoPage.aspx`
3. <span data-ttu-id="d4260-219">檢查瀏覽器中顯示的*ErrorPage* 。</span><span class="sxs-lookup"><span data-stu-id="d4260-219">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 錯誤處理-找不到分頁錯誤](aspnet-error-handling/_static/image1.png)

<span data-ttu-id="d4260-221">當您要求的*NoPage*不存在時，錯誤頁面會顯示簡單的錯誤訊息，以及詳細的錯誤資訊（如果有其他詳細資料可用）。</span><span class="sxs-lookup"><span data-stu-id="d4260-221">When you request the *NoPage.aspx* page, which does not exist, the error page will show the simple error message and the detailed error information if additional details are available.</span></span> <span data-ttu-id="d4260-222">不過，如果使用者從遠端位置要求不存在的頁面，則錯誤頁面只會以紅色顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d4260-222">However, if the user requested a non-existent page from a remote location, the error page would only show the error message in red.</span></span>

### <a name="including-an-exception-for-testing-purposes"></a><span data-ttu-id="d4260-223">包含測試用途的例外狀況</span><span class="sxs-lookup"><span data-stu-id="d4260-223">Including an Exception for Testing Purposes</span></span>

<span data-ttu-id="d4260-224">若要驗證您的應用程式在發生錯誤時的運作方式，您可以故意在 ASP.NET 中建立錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="d4260-224">To verify how your application will function when an error occurs, you can deliberately create error conditions in ASP.NET.</span></span> <span data-ttu-id="d4260-225">在 Wingtip 玩具範例應用程式中，當預設頁面載入時，您將會擲回測試例外狀況，以查看發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="d4260-225">In the Wingtip Toys sample application, you will throw a test exception when the default page loads to see what happens.</span></span>

1. <span data-ttu-id="d4260-226">在 Visual Studio 中開啟*default.aspx*頁面的程式碼後置。</span><span class="sxs-lookup"><span data-stu-id="d4260-226">Open the code-behind of the *Default.aspx* page in Visual Studio.</span></span>   
   <span data-ttu-id="d4260-227">*Default.aspx.cs*程式碼後置頁面隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="d4260-227">The *Default.aspx.cs* code-behind page will be displayed.</span></span>
2. <span data-ttu-id="d4260-228">在 `Page_Load` 處理常式中，新增程式碼，讓處理常式看起來如下：</span><span class="sxs-lookup"><span data-stu-id="d4260-228">In the `Page_Load` handler, add code so that the handler appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

<span data-ttu-id="d4260-229">您可以建立各種不同類型的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d4260-229">It is possible to create various different types of exceptions.</span></span> <span data-ttu-id="d4260-230">在上述程式碼中，您會在載入*default.aspx*頁面時建立 `InvalidOperationException`。</span><span class="sxs-lookup"><span data-stu-id="d4260-230">In the above code, you are creating an `InvalidOperationException` when the *Default.aspx* page is loaded.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="d4260-231">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="d4260-231">Running the Application</span></span>

<span data-ttu-id="d4260-232">您可以執行應用程式，以查看應用程式處理例外狀況的方式。</span><span class="sxs-lookup"><span data-stu-id="d4260-232">You can run the application to see how the application handles the exception.</span></span>

1. <span data-ttu-id="d4260-233">按**CTRL + F5**執行 Wingtip 玩具範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4260-233">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="d4260-234">應用程式會擲回 InvalidOperationException。</span><span class="sxs-lookup"><span data-stu-id="d4260-234">The application throws the InvalidOperationException.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="d4260-235">您必須按**CTRL + F5**以顯示頁面，而不會中斷程式碼，以在 Visual Studio 中查看錯誤的來源。</span><span class="sxs-lookup"><span data-stu-id="d4260-235">You must press **CTRL+F5** to display the page without breaking into the code to view the source of the error in Visual Studio.</span></span>
2. <span data-ttu-id="d4260-236">檢查瀏覽器中顯示的*ErrorPage* 。</span><span class="sxs-lookup"><span data-stu-id="d4260-236">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 錯誤處理-錯誤頁面](aspnet-error-handling/_static/image2.png)

<span data-ttu-id="d4260-238">如您在錯誤詳細資料中所見， *web.config*檔案中的 `customError` 區段會攔截例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d4260-238">As you can see in the error details, the exception was trapped by the `customError` section in the *Web.config* file.</span></span>

### <a name="adding-application-level-error-handling"></a><span data-ttu-id="d4260-239">加入應用層級的錯誤處理</span><span class="sxs-lookup"><span data-stu-id="d4260-239">Adding Application-Level Error Handling</span></span>

<span data-ttu-id="d4260-240">不是*使用 web.config 檔案*中的 `customErrors` 區段來攔截例外狀況，您可以在其中取得例外狀況的少量資訊，並在應用層級攔截錯誤並取得錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4260-240">Rather than trap the exception using the `customErrors` section in the *Web.config* file, where you gain little information about the exception, you can trap the error at the application level and retrieve error details.</span></span>

1. <span data-ttu-id="d4260-241">在**方案總管**中，尋找並開啟*Global.asax.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="d4260-241">In **Solution Explorer**, find and open the *Global.asax.cs* file.</span></span>
2. <span data-ttu-id="d4260-242">新增**應用程式\_錯誤**處理常式，使其看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="d4260-242">Add an **Application\_Error** handler so that it appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

<span data-ttu-id="d4260-243">當應用程式中發生錯誤時，會呼叫 `Application_Error` 處理常式。</span><span class="sxs-lookup"><span data-stu-id="d4260-243">When an error occurs in the application, the `Application_Error` handler is called.</span></span> <span data-ttu-id="d4260-244">在此處理程式中，會抓取並審核最後一個例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d4260-244">In this handler, the last exception is retrieved and reviewed.</span></span> <span data-ttu-id="d4260-245">如果例外狀況未處理，且例外狀況包含內部例外狀況詳細資料（也就是 `InnerException` 不是 null），應用程式就會將執行轉移至顯示例外狀況詳細資料的錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="d4260-245">If the exception was unhandled and the exception contains inner-exception details (that is, `InnerException` is not null), the application transfers execution to the error page where the exception details are displayed.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="d4260-246">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="d4260-246">Running the Application</span></span>

<span data-ttu-id="d4260-247">您可以執行應用程式，以查看在應用層級處理例外狀況所提供的其他錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4260-247">You can run the application to see the additional error details provided by handling the exception at the application level.</span></span>

1. <span data-ttu-id="d4260-248">按**CTRL + F5**執行 Wingtip 玩具範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4260-248">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="d4260-249">應用程式會擲回 `InvalidOperationException`。</span><span class="sxs-lookup"><span data-stu-id="d4260-249">The application throws the `InvalidOperationException` .</span></span>
2. <span data-ttu-id="d4260-250">檢查瀏覽器中顯示的*ErrorPage* 。</span><span class="sxs-lookup"><span data-stu-id="d4260-250">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 錯誤處理-應用層級錯誤](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a><span data-ttu-id="d4260-252">加入頁面層級錯誤處理</span><span class="sxs-lookup"><span data-stu-id="d4260-252">Adding Page-Level Error Handling</span></span>

<span data-ttu-id="d4260-253">您可以將頁面層級錯誤處理加入頁面中，方法是使用將 `ErrorPage` 屬性加入至頁面的 `@Page` 指示詞，或將 `Page_Error` 事件處理常式加入至頁面的程式碼後置。</span><span class="sxs-lookup"><span data-stu-id="d4260-253">You can add page-level error handling to a page either by using adding an `ErrorPage` attribute to the `@Page` directive of the page, or by adding a `Page_Error` event handler to the code-behind of a page.</span></span> <span data-ttu-id="d4260-254">在本節中，您將會新增 `Page_Error` 事件處理常式，以將執行傳送至*ErrorPage .aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="d4260-254">In this section, you will add a `Page_Error` event handler that will transfer execution to the *ErrorPage.aspx* page.</span></span>

1. <span data-ttu-id="d4260-255">在**方案總管**中，尋找並開啟*Default.aspx.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="d4260-255">In **Solution Explorer**, find and open the *Default.aspx.cs* file.</span></span>
2. <span data-ttu-id="d4260-256">新增 `Page_Error` 處理常式，讓程式碼後置顯示如下：</span><span class="sxs-lookup"><span data-stu-id="d4260-256">Add a `Page_Error` handler so that the code-behind appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

<span data-ttu-id="d4260-257">當頁面上發生錯誤時，會呼叫 `Page_Error` 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="d4260-257">When an error occurs on the page, the `Page_Error` event handler is called.</span></span> <span data-ttu-id="d4260-258">在此處理程式中，會抓取並審核最後一個例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d4260-258">In this handler, the last exception is retrieved and reviewed.</span></span> <span data-ttu-id="d4260-259">如果發生 `InvalidOperationException`，`Page_Error` 事件處理常式會將執行傳送至顯示例外狀況詳細資料的錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="d4260-259">If an `InvalidOperationException` occurs, the `Page_Error` event handler transfers execution to the error page where the exception details are displayed.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="d4260-260">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="d4260-260">Running the Application</span></span>

<span data-ttu-id="d4260-261">您可以立即執行應用程式，以查看更新的路由。</span><span class="sxs-lookup"><span data-stu-id="d4260-261">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="d4260-262">按**CTRL + F5**執行 Wingtip 玩具範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4260-262">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="d4260-263">應用程式會擲回 `InvalidOperationException`。</span><span class="sxs-lookup"><span data-stu-id="d4260-263">The application throws the `InvalidOperationException` .</span></span>
2. <span data-ttu-id="d4260-264">檢查瀏覽器中顯示的*ErrorPage* 。</span><span class="sxs-lookup"><span data-stu-id="d4260-264">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 錯誤處理-頁面層級錯誤](aspnet-error-handling/_static/image4.png)
3. <span data-ttu-id="d4260-266">關閉瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="d4260-266">Close your browser window.</span></span>

### <a name="removing-the-exception-used-for-testing"></a><span data-ttu-id="d4260-267">移除用於測試的例外狀況</span><span class="sxs-lookup"><span data-stu-id="d4260-267">Removing the Exception Used for Testing</span></span>

<span data-ttu-id="d4260-268">若要允許 Wingtip 玩具範例應用程式正常運作，而不擲回您稍早在本教學課程中新增的例外狀況，請移除例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d4260-268">To allow the Wingtip Toys sample application to function without throwing the exception you added earlier in this tutorial, remove the exception.</span></span>

1. <span data-ttu-id="d4260-269">開啟*default.aspx*頁面的程式碼後置。</span><span class="sxs-lookup"><span data-stu-id="d4260-269">Open the code-behind of the *Default.aspx* page.</span></span>
2. <span data-ttu-id="d4260-270">在 `Page_Load` 處理常式中，移除擲回例外狀況的程式碼，讓處理常式看起來如下：</span><span class="sxs-lookup"><span data-stu-id="d4260-270">In the `Page_Load` handler, remove the code that throws the exception so that the handler appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a><span data-ttu-id="d4260-271">加入程式碼層級錯誤記錄</span><span class="sxs-lookup"><span data-stu-id="d4260-271">Adding Code-Level Error Logging</span></span>

<span data-ttu-id="d4260-272">如本教學課程稍早所述，您可以加入 try/catch 語句來嘗試執行程式碼區段，並處理第一個發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-272">As mentioned earlier in this tutorial, you can add try/catch statements to attempt to run a section of code and handle the first error that occurs.</span></span> <span data-ttu-id="d4260-273">在此範例中，您只會將錯誤詳細資料寫入錯誤記錄檔中，以便稍後可以檢查錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-273">In this example, you will only write the error details to the error log file so that the error can be reviewed later.</span></span>

1. <span data-ttu-id="d4260-274">在**方案總管**的*邏輯*資料夾中，尋找並開啟*PayPalFunctions.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="d4260-274">In **Solution Explorer**, in the *Logic* folder, find and open the *PayPalFunctions.cs* file.</span></span>
2. <span data-ttu-id="d4260-275">更新 `HttpCall` 方法，讓程式碼看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="d4260-275">Update the `HttpCall` method so that the code appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

<span data-ttu-id="d4260-276">上述程式碼會呼叫包含在 `ExceptionUtility` 類別中的 `LogException` 方法。</span><span class="sxs-lookup"><span data-stu-id="d4260-276">The above code calls the `LogException` method that is contained in the `ExceptionUtility` class.</span></span> <span data-ttu-id="d4260-277">您已將*ExceptionUtility.cs*類別檔案新增至本教學課程稍早的*邏輯*資料夾。</span><span class="sxs-lookup"><span data-stu-id="d4260-277">You added the *ExceptionUtility.cs* class file to the *Logic* folder earlier in this tutorial.</span></span> <span data-ttu-id="d4260-278">`LogException` 方法會接受兩個參數。</span><span class="sxs-lookup"><span data-stu-id="d4260-278">The `LogException` method takes two parameters.</span></span> <span data-ttu-id="d4260-279">第一個參數是例外狀況物件。</span><span class="sxs-lookup"><span data-stu-id="d4260-279">The first parameter is the exception object.</span></span> <span data-ttu-id="d4260-280">第二個參數是用來辨識錯誤來源的字串。</span><span class="sxs-lookup"><span data-stu-id="d4260-280">The second parameter is a string used to recognize the source of the error.</span></span>

### <a name="inspecting-the-error-logging-information"></a><span data-ttu-id="d4260-281">檢查錯誤記錄資訊</span><span class="sxs-lookup"><span data-stu-id="d4260-281">Inspecting the Error Logging Information</span></span>

<span data-ttu-id="d4260-282">如先前所述，您可以使用錯誤記錄檔來判斷應該先修正應用程式中的哪些錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-282">As mentioned previously, you can use the error log to determine which errors in your application should be fixed first.</span></span> <span data-ttu-id="d4260-283">當然，只會記錄已被攔截並寫入錯誤記錄檔的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-283">Of course, only errors that have been trapped and written to the error log will be recorded.</span></span>

1. <span data-ttu-id="d4260-284">在**方案總管**中，尋找並開啟*應用程式\_Data*資料夾中的錯誤記錄檔 *.txt*檔案。</span><span class="sxs-lookup"><span data-stu-id="d4260-284">In **Solution Explorer**, find and open the *ErrorLog.txt* file in the *App\_Data* folder.</span></span>   
 <span data-ttu-id="d4260-285">您可能需要從 [**方案總管**] 頂端選取 [**顯示所有**檔案] 選項或 [重新**整理] 選項**，才能查看錯誤記錄檔 *.txt*檔案。</span><span class="sxs-lookup"><span data-stu-id="d4260-285">You may need to select the "**Show All Files**" option or the "**Refresh**" option from the top of **Solution Explorer** to see the *ErrorLog.txt* file.</span></span>
2. <span data-ttu-id="d4260-286">檢查 Visual Studio 中顯示的錯誤記錄檔：</span><span class="sxs-lookup"><span data-stu-id="d4260-286">Review the error log displayed in Visual Studio:</span></span> 

    ![ASP.NET 錯誤處理-錯誤記錄檔 .txt](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a><span data-ttu-id="d4260-288">安全錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="d4260-288">Safe Error Messages</span></span>

<span data-ttu-id="d4260-289">**請務必注意**，當您的應用程式顯示錯誤訊息時，應該不會提供惡意使用者在攻擊您的應用程式時可能會有説明的資訊。</span><span class="sxs-lookup"><span data-stu-id="d4260-289">It is **important to note** that when your application displays error messages, it should not give away information that a malicious user might find helpful in attacking your application.</span></span> <span data-ttu-id="d4260-290">例如，如果您的應用程式未成功地嘗試寫入資料庫，則不應該顯示包含所使用之使用者名稱的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d4260-290">For example, if your application unsuccessfully tries to write in to a database, it should not display an error message that includes the user name it is using.</span></span> <span data-ttu-id="d4260-291">因此，使用者會看到紅色的一般錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d4260-291">For this reason, a generic error message in red is displayed to the user.</span></span> <span data-ttu-id="d4260-292">所有其他錯誤詳細資料只會對本機電腦上的開發人員顯示。</span><span class="sxs-lookup"><span data-stu-id="d4260-292">All additional error details are only displayed to the developer on the local machine.</span></span>

## <a name="using-elmah"></a><span data-ttu-id="d4260-293">使用 ELMAH</span><span class="sxs-lookup"><span data-stu-id="d4260-293">Using ELMAH</span></span>

<span data-ttu-id="d4260-294">ELMAH （錯誤記錄模組和處理常式）是一種錯誤記錄工具，您可以將 ASP.NET 應用程式插入為 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="d4260-294">ELMAH (Error Logging Modules and Handlers) is an error logging facility that you plug into your ASP.NET application as a NuGet package.</span></span> <span data-ttu-id="d4260-295">ELMAH 提供下列功能：</span><span class="sxs-lookup"><span data-stu-id="d4260-295">ELMAH provides the following capabilities:</span></span>

- <span data-ttu-id="d4260-296">記錄未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d4260-296">Logging of unhandled exceptions.</span></span>
- <span data-ttu-id="d4260-297">用來查看重新編碼未處理之例外狀況之完整記錄的網頁。</span><span class="sxs-lookup"><span data-stu-id="d4260-297">A web page to view the entire log of recoded unhandled exceptions.</span></span>
- <span data-ttu-id="d4260-298">用來查看每個已記錄例外狀況之完整詳細資料的網頁。</span><span class="sxs-lookup"><span data-stu-id="d4260-298">A web page to view the full details of each logged exception.</span></span>
- <span data-ttu-id="d4260-299">每次發生錯誤時的電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="d4260-299">An email notification of each error at the time it occurs.</span></span>
- <span data-ttu-id="d4260-300">記錄檔最後15個錯誤的 RSS 摘要。</span><span class="sxs-lookup"><span data-stu-id="d4260-300">An RSS feed of the last 15 errors from the log.</span></span>

<span data-ttu-id="d4260-301">在您可以使用 ELMAH 之前，您必須先安裝它。</span><span class="sxs-lookup"><span data-stu-id="d4260-301">Before you can work with the ELMAH, you must install it.</span></span> <span data-ttu-id="d4260-302">使用*NuGet*套件安裝程式很容易。</span><span class="sxs-lookup"><span data-stu-id="d4260-302">This is easy using the *NuGet* package installer.</span></span> <span data-ttu-id="d4260-303">如稍早在本教學課程系列中所述，NuGet 是 Visual Studio 延伸模組，可讓您輕鬆地安裝和更新 Visual Studio 中的開放原始碼程式庫和工具。</span><span class="sxs-lookup"><span data-stu-id="d4260-303">As mentioned earlier in this tutorial series, NuGet is a Visual Studio extension that makes it easy to install and update open source libraries and tools in Visual Studio.</span></span>

1. <span data-ttu-id="d4260-304">在 Visual Studio 中，從 **工具** 功能表選取  **nuget 套件管理員**， > **管理解決方案的 nuget 套件**。</span><span class="sxs-lookup"><span data-stu-id="d4260-304">Within Visual Studio, from the **Tools** menu, select **NuGet Package Manager** > **Manage NuGet Packages for Solution**.</span></span> 

    ![ASP.NET 錯誤處理-管理解決方案的 NuGet 套件](aspnet-error-handling/_static/image6.png)
2. <span data-ttu-id="d4260-306">[**管理 NuGet 封裝**] 對話方塊會顯示在 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="d4260-306">The **Manage NuGet Packages** dialog box is displayed within Visual Studio.</span></span>
3. <span data-ttu-id="d4260-307">在 [**管理 NuGet 封裝**] 對話方塊中，展開左側的 [**線上**]，然後選取 [ **nuget.org**]。然後，在線上可用的套件清單中，尋找並安裝**ELMAH**套件。</span><span class="sxs-lookup"><span data-stu-id="d4260-307">In the **Manage NuGet Packages** dialog box, expand **Online** on the left, and then select **nuget.org**. Then, find and install the **ELMAH** package from the list of available packages online.</span></span> 

    ![ASP.NET 錯誤處理-ELMA NuGet 套件](aspnet-error-handling/_static/image7.png)
4. <span data-ttu-id="d4260-309">您將需要有網際網路連線才能下載套件。</span><span class="sxs-lookup"><span data-stu-id="d4260-309">You will need to have an internet connection to download the package.</span></span>
5. <span data-ttu-id="d4260-310">在 [**選取專案**] 對話方塊中，確認已選取**WingtipToys**選項，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="d4260-310">In the **Select Projects** dialog box, make sure the **WingtipToys** selection is selected, and then click **OK**.</span></span> 

    ![ASP.NET 錯誤處理-[選取專案] 對話方塊](aspnet-error-handling/_static/image8.png)
6. <span data-ttu-id="d4260-312">如有需要，請按一下 [**管理 NuGet 套件**] 對話方塊中的 [**關閉**]。</span><span class="sxs-lookup"><span data-stu-id="d4260-312">Click **Close** in the **Manage NuGet Packages** dialog box if needed.</span></span>
7. <span data-ttu-id="d4260-313">如果 Visual Studio 要求您重載任何開啟的檔案，請選取 [**全部皆是**]。</span><span class="sxs-lookup"><span data-stu-id="d4260-313">If Visual Studio requests that you reload any open files, select "**Yes to All**".</span></span>
8. <span data-ttu-id="d4260-314">ELMAH 封裝會在專案*根目錄的 web.config*檔案中，新增其本身的專案。</span><span class="sxs-lookup"><span data-stu-id="d4260-314">The ELMAH package adds entries for itself in the *Web.config* file at the root of your project.</span></span> <span data-ttu-id="d4260-315">如果 Visual Studio 詢問您是否要重載已修改的*web.config*檔案，請按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="d4260-315">If Visual Studio asks you if you want to reload the modified *Web.config* file, click **Yes**.</span></span>

<span data-ttu-id="d4260-316">ELMAH 現在已準備好儲存任何發生的未處理錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-316">ELMAH is now ready to store any unhandled errors that occur.</span></span>

### <a name="viewing-the-elmah-log"></a><span data-ttu-id="d4260-317">查看 ELMAH 記錄檔</span><span class="sxs-lookup"><span data-stu-id="d4260-317">Viewing the ELMAH Log</span></span>

<span data-ttu-id="d4260-318">查看 ELMAH 記錄檔很簡單，但首先您會建立一個未處理的例外狀況，並將記錄在 ELMAH 記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="d4260-318">Viewing the ELMAH log is easy, but first you will create an unhandled exception that will be recorded in the ELMAH log.</span></span>

1. <span data-ttu-id="d4260-319">按**CTRL + F5**執行 Wingtip 玩具範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4260-319">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>
2. <span data-ttu-id="d4260-320">若要將未處理的例外狀況寫入 ELMAH 記錄檔，請在瀏覽器中流覽至下列 URL （使用您的埠號碼）：</span><span class="sxs-lookup"><span data-stu-id="d4260-320">To write an unhandled exception to the ELMAH log, navigate in your browser to the following URL (using your port number):</span></span>  
    <span data-ttu-id="d4260-321">將會顯示 [錯誤] 頁面 `https://localhost:44300/NoPage.aspx`。</span><span class="sxs-lookup"><span data-stu-id="d4260-321">`https://localhost:44300/NoPage.aspx` The error page will be displayed.</span></span>
3. <span data-ttu-id="d4260-322">若要顯示 ELMAH 記錄檔，請在瀏覽器中流覽至下列 URL （使用您的埠號碼）：</span><span class="sxs-lookup"><span data-stu-id="d4260-322">To display the ELMAH log, navigate in your browser to the following URL (using your port number):</span></span>  
    `https://localhost:44300/elmah.axd`

    ![ASP.NET 錯誤處理-ELMAH 錯誤記錄檔](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a><span data-ttu-id="d4260-324">總結</span><span class="sxs-lookup"><span data-stu-id="d4260-324">Summary</span></span>

<span data-ttu-id="d4260-325">在本教學課程中，您已瞭解如何在應用層級、頁面層級和程式碼層級處理錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4260-325">In this tutorial, you have learned about handling errors at the application level, the page level, and the code level.</span></span> <span data-ttu-id="d4260-326">您也已瞭解如何記錄已處理和未處理的錯誤，以供日後審查。</span><span class="sxs-lookup"><span data-stu-id="d4260-326">You have also learned how to log handled and unhandled errors for later review.</span></span> <span data-ttu-id="d4260-327">您已新增 ELMAH 公用程式，以使用 NuGet 為您的應用程式提供例外狀況記錄和通知。</span><span class="sxs-lookup"><span data-stu-id="d4260-327">You added the ELMAH utility to provide exception logging and notification to your application using NuGet.</span></span> <span data-ttu-id="d4260-328">此外，您也已經瞭解安全錯誤訊息的重要性。</span><span class="sxs-lookup"><span data-stu-id="d4260-328">Additionally, you have learned about the importance of safe error messages.</span></span>

## <a name="tutorial-series-conclusion"></a><span data-ttu-id="d4260-329">教學課程系列結論</span><span class="sxs-lookup"><span data-stu-id="d4260-329">Tutorial Series Conclusion</span></span>

<span data-ttu-id="d4260-330">感謝您的關注。</span><span class="sxs-lookup"><span data-stu-id="d4260-330">Thanks for following along.</span></span> <span data-ttu-id="d4260-331">我希望這組教學課程協助您更熟悉 ASP.NET Web form。</span><span class="sxs-lookup"><span data-stu-id="d4260-331">I hope this set of tutorials helped you become more familiar with ASP.NET Web Forms.</span></span> <span data-ttu-id="d4260-332">如果您需要 ASP.NET 4.5 和 Visual Studio 2013 中可用 Web form 功能的詳細資訊，請參閱[ASP.NET 和 Web 工具以取得 Visual Studio 2013 版本](../../../../visual-studio/overview/2013/release-notes.md)資訊。</span><span class="sxs-lookup"><span data-stu-id="d4260-332">If you need more information about Web Forms features available in ASP.NET 4.5 and Visual Studio 2013, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span> <span data-ttu-id="d4260-333">此外，請務必查看**後續步驟**一節中所述的教學課程，並 defintely 試用[免費的 Azure 試用版](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="d4260-333">Also, be sure to take a look at the tutorial mentioned in the **Next Steps** section and defintely try out the [free Azure trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

![感謝-Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a><span data-ttu-id="d4260-335">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d4260-335">Next Steps</span></span>

<span data-ttu-id="d4260-336">若要深入瞭解如何將 web 應用程式部署至 Microsoft Azure，請參閱[使用成員資格、OAuth 和 SQL Database 將安全的 ASP.NET Web Forms 應用程式部署到 Azure 網站](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="d4260-336">Learn more about deploying your web application to Microsoft Azure, see [Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to an Azure Web Site](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/).</span></span>

## <a name="free-trial"></a><span data-ttu-id="d4260-337">免費試用</span><span class="sxs-lookup"><span data-stu-id="d4260-337">Free Trial</span></span>

[<span data-ttu-id="d4260-338">Microsoft Azure 免費試用</span><span class="sxs-lookup"><span data-stu-id="d4260-338">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)  
 <span data-ttu-id="d4260-339">將您的網站發佈到 Microsoft Azure 可以節省您的時間、維護和費用。</span><span class="sxs-lookup"><span data-stu-id="d4260-339">Publishing your website to Microsoft Azure will save you time, maintenance and expense.</span></span> <span data-ttu-id="d4260-340">這是將您的 web 應用程式部署至 Azure 的快速流程。</span><span class="sxs-lookup"><span data-stu-id="d4260-340">It's a quick process to deploying your web app to Azure.</span></span> <span data-ttu-id="d4260-341">當您需要維護及監視 web 應用程式時，Azure 會提供各種不同的工具和服務。</span><span class="sxs-lookup"><span data-stu-id="d4260-341">When you need to maintain and monitor your web app, Azure offers a variety of tools and services.</span></span> <span data-ttu-id="d4260-342">管理 Azure 中的資料、流量、身分識別、備份、訊息、媒體和效能。</span><span class="sxs-lookup"><span data-stu-id="d4260-342">Manage data, traffic, identity, backups, messaging, media and performance in Azure.</span></span> <span data-ttu-id="d4260-343">而且這一切都是以非常符合成本效益的方式提供。</span><span class="sxs-lookup"><span data-stu-id="d4260-343">And, all of this is provided in a very cost effective approach.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d4260-344">其他資源</span><span class="sxs-lookup"><span data-stu-id="d4260-344">Additional Resources</span></span>

<span data-ttu-id="d4260-345">[使用 ASP.NET 健全狀況監視記錄錯誤詳細資料](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md) </span><span class="sxs-lookup"><span data-stu-id="d4260-345">[Logging Error Details with ASP.NET Health Monitoring](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md) </span></span>  
[<span data-ttu-id="d4260-346">ELMAH</span><span class="sxs-lookup"><span data-stu-id="d4260-346">ELMAH</span></span>](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a><span data-ttu-id="d4260-347">通知</span><span class="sxs-lookup"><span data-stu-id="d4260-347">Acknowledgements</span></span>

<span data-ttu-id="d4260-348">我想感謝下列人對本教學課程系列的內容做出重大貢獻：</span><span class="sxs-lookup"><span data-stu-id="d4260-348">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="d4260-349">Alberto Poblacion，MVP &amp; MCT，西班牙</span><span class="sxs-lookup"><span data-stu-id="d4260-349">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- <span data-ttu-id="d4260-350">[Alex Thissen，荷蘭](http://blog.alexthissen.nl/)（twitter： [@alexthissen](http://twitter.com/alexthissen)）</span><span class="sxs-lookup"><span data-stu-id="d4260-350">[Alex Thissen, Netherlands](http://blog.alexthissen.nl/) (twitter: [@alexthissen](http://twitter.com/alexthissen))</span></span>
- [<span data-ttu-id="d4260-351">美國 Andre Tournier</span><span class="sxs-lookup"><span data-stu-id="d4260-351">Andre Tournier, USA</span></span>](http://andret503.wordpress.com/)
- <span data-ttu-id="d4260-352">Apurva Joshi，Microsoft</span><span class="sxs-lookup"><span data-stu-id="d4260-352">Apurva Joshi, Microsoft</span></span>
- [<span data-ttu-id="d4260-353">Bojan Vrhovnik，斯洛維尼亞</span><span class="sxs-lookup"><span data-stu-id="d4260-353">Bojan Vrhovnik, Slovenia</span></span>](http://twitter.com/bvrhovnik)
- <span data-ttu-id="d4260-354">[Bruno sonnino 此將，巴西](http://msmvps.com/blogs/bsonnino)（twitter： [@bsonnino](http://twitter.com/bsonnino)）</span><span class="sxs-lookup"><span data-stu-id="d4260-354">[Bruno Sonnino, Brazil](http://msmvps.com/blogs/bsonnino) (twitter: [@bsonnino](http://twitter.com/bsonnino))</span></span>
- [<span data-ttu-id="d4260-355">Carlos dos Santos，巴西</span><span class="sxs-lookup"><span data-stu-id="d4260-355">Carlos dos Santos, Brazil</span></span>](http://www.carloscds.net/)
- <span data-ttu-id="d4260-356">[美國 Dave Campbell](http://www.wynapse.com/) （twitter： [@windowsdevnews](http://twitter.com/windowsdevnews)）</span><span class="sxs-lookup"><span data-stu-id="d4260-356">[Dave Campbell, USA](http://www.wynapse.com/) (twitter: [@windowsdevnews](http://twitter.com/windowsdevnews))</span></span>
- <span data-ttu-id="d4260-357">[Jon Galloway，Microsoft](https://weblogs.asp.net/jgalloway) （twitter： [@jongalloway](http://twitter.com/jongalloway)）</span><span class="sxs-lookup"><span data-stu-id="d4260-357">[Jon Galloway, Microsoft](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span></span>
- <span data-ttu-id="d4260-358">美國（twitter： [@mrsharps](http://twitter.com/mrsharps)） [Michael Sharps](http://www.930solutions.com/)</span><span class="sxs-lookup"><span data-stu-id="d4260-358">[Michael Sharps, USA](http://www.930solutions.com/) (twitter: [@mrsharps](http://twitter.com/mrsharps))</span></span>
- <span data-ttu-id="d4260-359">Mike Pope</span><span class="sxs-lookup"><span data-stu-id="d4260-359">Mike Pope</span></span>
- <span data-ttu-id="d4260-360">[美國 Mitchel 賣方](http://www.mitchelsellers.com/)（twitter： [@MitchelSellers](http://twitter.com/MitchelSellers)）</span><span class="sxs-lookup"><span data-stu-id="d4260-360">[Mitchel Sellers, USA](http://www.mitchelsellers.com/) (twitter: [@MitchelSellers](http://twitter.com/MitchelSellers))</span></span>
- [<span data-ttu-id="d4260-361">Paul Cociuba，Microsoft</span><span class="sxs-lookup"><span data-stu-id="d4260-361">Paul Cociuba, Microsoft</span></span>](http://linqto.me/Links/pcociuba)
- [<span data-ttu-id="d4260-362">聖保羅 Morgado，葡萄牙</span><span class="sxs-lookup"><span data-stu-id="d4260-362">Paulo Morgado, Portugal</span></span>](http://paulomorgado.net/)
- [<span data-ttu-id="d4260-363">Pranav 請參閱 rastogi，Microsoft</span><span class="sxs-lookup"><span data-stu-id="d4260-363">Pranav Rastogi, Microsoft</span></span>](https://blogs.msdn.com/b/pranav_rastogi)
- [<span data-ttu-id="d4260-364">Tim Ammann，Microsoft</span><span class="sxs-lookup"><span data-stu-id="d4260-364">Tim Ammann, Microsoft</span></span>](https://blogs.iis.net/timamm/default.aspx)
- [<span data-ttu-id="d4260-365">Tom 作者: dykstra，Microsoft</span><span class="sxs-lookup"><span data-stu-id="d4260-365">Tom Dykstra, Microsoft</span></span>](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a><span data-ttu-id="d4260-366">社群貢獻</span><span class="sxs-lookup"><span data-stu-id="d4260-366">Community Contributions</span></span>

- <span data-ttu-id="d4260-367">Graham Mendick （[@grahammendick](http://twitter.com/grahammendick)）</span><span class="sxs-lookup"><span data-stu-id="d4260-367">Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))</span></span>  
  <span data-ttu-id="d4260-368">MSDN 上 Visual Studio 2012 相關程式碼範例：[導覽 Wingtip 玩具](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)</span><span class="sxs-lookup"><span data-stu-id="d4260-368">Visual Studio 2012 related code sample on MSDN: [Navigation Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)</span></span>
- <span data-ttu-id="d4260-369">James Chaney （[jchaney@agvance.net](mailto:jchaney@agvance.net)）</span><span class="sxs-lookup"><span data-stu-id="d4260-369">James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))</span></span>  
  <span data-ttu-id="d4260-370">MSDN 上的 Visual Studio 2012 相關程式碼範例： [Visual Basic 中的 ASP.NET 4.5 Web Forms 教學課程系列](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)</span><span class="sxs-lookup"><span data-stu-id="d4260-370">Visual Studio 2012 related code sample on MSDN: [ASP.NET 4.5 Web Forms Tutorial Series in Visual Basic](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)</span></span>
- <span data-ttu-id="d4260-371">Andrielle Azevedo-Microsoft 技術物件參與者（twitter： @driazevedo）</span><span class="sxs-lookup"><span data-stu-id="d4260-371">Andrielle Azevedo - Microsoft Technical Audience Contributor (twitter: @driazevedo)</span></span>  
  <span data-ttu-id="d4260-372">Visual Studio 2012 轉譯： [Iniciando com ASP.NET Web Forms 4.5-Parte 1-Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)</span><span class="sxs-lookup"><span data-stu-id="d4260-372">Visual Studio 2012 translation: [Iniciando com ASP.NET Web Forms 4.5 - Parte 1 - Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d4260-373">上一篇</span><span class="sxs-lookup"><span data-stu-id="d4260-373">Previous</span></span>](url-routing.md)
