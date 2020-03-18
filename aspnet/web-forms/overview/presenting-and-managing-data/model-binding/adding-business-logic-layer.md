---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: 將商務邏輯層新增至使用模型系結和 web forms 的專案 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結讓資料互動更為直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a824d06d3781e11706f2a48d44ea3ad89bdb7c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634831"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a><span data-ttu-id="a6837-104">將商務邏輯層新增至使用模型系結和 web form 的專案</span><span class="sxs-lookup"><span data-stu-id="a6837-104">Adding business logic layer to a project that uses model binding and web forms</span></span>

<span data-ttu-id="a6837-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a6837-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a6837-106">本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。</span><span class="sxs-lookup"><span data-stu-id="a6837-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="a6837-107">模型系結可讓資料互動比處理資料來源物件（例如 ObjectDataSource 或 SqlDataSource）更直接。</span><span class="sxs-lookup"><span data-stu-id="a6837-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="a6837-108">此系列從簡介材料開始，並在稍後的教學課程中移至更先進的概念。</span><span class="sxs-lookup"><span data-stu-id="a6837-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="a6837-109">本教學課程說明如何搭配商務邏輯層使用模型系結。</span><span class="sxs-lookup"><span data-stu-id="a6837-109">This tutorial shows how to use model binding with a business logic layer.</span></span> <span data-ttu-id="a6837-110">您將設定 OnCallingDataMethods 成員，以指定目前頁面以外的物件用來呼叫資料方法。</span><span class="sxs-lookup"><span data-stu-id="a6837-110">You will set the OnCallingDataMethods member to specify that an object other than the current page is used to call the data methods.</span></span>
> 
> <span data-ttu-id="a6837-111">本教學課程是根據在系列的[先前](retrieving-data.md)部分中所建立的專案來建立。</span><span class="sxs-lookup"><span data-stu-id="a6837-111">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="a6837-112">您可以[download](https://go.microsoft.com/fwlink/?LinkId=286116)在或 VB 中C#下載完整專案。</span><span class="sxs-lookup"><span data-stu-id="a6837-112">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="a6837-113">可下載的程式碼適用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="a6837-113">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="a6837-114">它會使用 Visual Studio 2012 範本，這與本教學課程中所顯示的 Visual Studio 2013 範本稍有不同。</span><span class="sxs-lookup"><span data-stu-id="a6837-114">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="a6837-115">您將建立的內容</span><span class="sxs-lookup"><span data-stu-id="a6837-115">What you'll build</span></span>

<span data-ttu-id="a6837-116">模型系結可讓您將資料互動程式碼放在網頁的程式碼後置檔案或個別的商業邏輯類別中。</span><span class="sxs-lookup"><span data-stu-id="a6837-116">Model binding enables you to put your data interaction code in either the code-behind file for a web page or in a separate business logic class.</span></span> <span data-ttu-id="a6837-117">先前的教學課程已示範如何將程式碼後置檔案用於資料互動程式碼。</span><span class="sxs-lookup"><span data-stu-id="a6837-117">The previous tutorials have shown how to use the code-behind files for data interaction code.</span></span> <span data-ttu-id="a6837-118">這種方法適用于小型網站，但在維護大型網站時，可能會導致程式碼重複和更困難。</span><span class="sxs-lookup"><span data-stu-id="a6837-118">This approach works for small sites but it can lead to code repetition and greater difficulty when maintaining a large site.</span></span> <span data-ttu-id="a6837-119">您也可能很難以以程式設計方式測試位於程式碼後置檔案中的程式碼，因為沒有抽象層。</span><span class="sxs-lookup"><span data-stu-id="a6837-119">It can also be very difficult to programmatically test code that resides in code behind files because there is no abstraction layer.</span></span>

<span data-ttu-id="a6837-120">若要集中資料互動程式碼，您可以建立商務邏輯層，其中包含與資料互動的所有邏輯。</span><span class="sxs-lookup"><span data-stu-id="a6837-120">To centralize the data interaction code, you can create a business logic layer that contains all of the logic for interacting with data.</span></span> <span data-ttu-id="a6837-121">然後從您的網頁呼叫商務邏輯層。</span><span class="sxs-lookup"><span data-stu-id="a6837-121">You then call the business logic layer from your web pages.</span></span> <span data-ttu-id="a6837-122">本教學課程示範如何將您在先前的教學課程中撰寫的所有程式碼移至商務邏輯層，然後從頁面使用該程式碼。</span><span class="sxs-lookup"><span data-stu-id="a6837-122">This tutorial shows how to move all of the code you have written in the previous tutorials into a business logic layer, and then use that code from the pages.</span></span>

<span data-ttu-id="a6837-123">在本教學課程中，您將會：</span><span class="sxs-lookup"><span data-stu-id="a6837-123">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="a6837-124">將程式碼後置檔案中的程式碼移至商務邏輯層</span><span class="sxs-lookup"><span data-stu-id="a6837-124">Move the code from code-behind files to a business logic layer</span></span>
2. <span data-ttu-id="a6837-125">變更您的資料繫結控制項，以呼叫商務邏輯層中的方法</span><span class="sxs-lookup"><span data-stu-id="a6837-125">Change your data bound controls to call the methods in the business logic layer</span></span>

## <a name="create-business-logic-layer"></a><span data-ttu-id="a6837-126">建立商務邏輯層</span><span class="sxs-lookup"><span data-stu-id="a6837-126">Create business logic layer</span></span>

<span data-ttu-id="a6837-127">現在，您將建立從網頁呼叫的類別。</span><span class="sxs-lookup"><span data-stu-id="a6837-127">Now, you will create the class that is called from the web pages.</span></span> <span data-ttu-id="a6837-128">此類別中的方法看起來類似于您在先前的教學課程中使用的方法，並包含值提供者屬性。</span><span class="sxs-lookup"><span data-stu-id="a6837-128">The methods in this class look similar to the methods you used in the previous tutorials and include the value provider attributes.</span></span>

<span data-ttu-id="a6837-129">首先，新增名為**BLL**的新資料夾。</span><span class="sxs-lookup"><span data-stu-id="a6837-129">First, add a new folder called **BLL**.</span></span>

![新增資料夾](adding-business-logic-layer/_static/image1.png)

<span data-ttu-id="a6837-131">在 [BLL] 資料夾中，建立名為**SchoolBL.cs**的新類別。</span><span class="sxs-lookup"><span data-stu-id="a6837-131">In the BLL folder, create a new class named **SchoolBL.cs**.</span></span> <span data-ttu-id="a6837-132">它將包含原本位於程式碼後置檔案中的所有資料作業。</span><span class="sxs-lookup"><span data-stu-id="a6837-132">It will contain all of the data operations that originally resided in code-behind files.</span></span> <span data-ttu-id="a6837-133">方法幾乎與程式碼後置檔案中的方法相同，但會包含一些變更。</span><span class="sxs-lookup"><span data-stu-id="a6837-133">The methods are almost the same as the methods in the code-behind file, but will include some changes.</span></span>

<span data-ttu-id="a6837-134">要注意的最重要變更是您不再從**Page**類別的實例中執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="a6837-134">The most important change to note is that you are no longer executing the code from within an instance of **Page** class.</span></span> <span data-ttu-id="a6837-135">Page 類別包含**TryUpdateModel**方法和**ModelState**屬性。</span><span class="sxs-lookup"><span data-stu-id="a6837-135">The Page class contains the **TryUpdateModel** method and the **ModelState** property.</span></span> <span data-ttu-id="a6837-136">當此程式碼移至商務邏輯層時，您就不再有 Page 類別的實例可以呼叫這些成員。</span><span class="sxs-lookup"><span data-stu-id="a6837-136">When this code is moved to a business logic layer, you no longer have an instance of the Page class to call these members.</span></span> <span data-ttu-id="a6837-137">若要解決此問題，您必須將**ModelMethodCoNtext**參數新增至任何存取 TryUpdateModel 或 ModelState 的方法。</span><span class="sxs-lookup"><span data-stu-id="a6837-137">To get around this issue, you must add a **ModelMethodContext** parameter to any method that accesses TryUpdateModel or ModelState.</span></span> <span data-ttu-id="a6837-138">您可以使用這個 ModelMethodCoNtext 參數來呼叫 TryUpdateModel 或取出 ModelState。</span><span class="sxs-lookup"><span data-stu-id="a6837-138">You use this ModelMethodContext parameter to call TryUpdateModel or retrieve ModelState.</span></span> <span data-ttu-id="a6837-139">您不需要變更網頁中的任何專案來考慮這個新的參數。</span><span class="sxs-lookup"><span data-stu-id="a6837-139">You do not need to change anything in the web page to account for this new parameter.</span></span>

<span data-ttu-id="a6837-140">將 SchoolBL.cs 中的程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="a6837-140">Replace the code in SchoolBL.cs with the following code.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a><span data-ttu-id="a6837-141">修訂現有頁面以從商務邏輯層取出資料</span><span class="sxs-lookup"><span data-stu-id="a6837-141">Revise existing pages to retrieve data from business logic layer</span></span>

<span data-ttu-id="a6837-142">最後，您會將 AddStudent 的頁面從程式碼後置檔案中的查詢轉換成使用商務邏輯層。</span><span class="sxs-lookup"><span data-stu-id="a6837-142">Finally, you will convert the pages Students.aspx, AddStudent.aspx, and Courses.aspx from using queries in the code-behind file to using the business logic layer.</span></span>

<span data-ttu-id="a6837-143">在學生、AddStudent 和課程的程式碼後置檔案中，刪除或批註下列查詢方法：</span><span class="sxs-lookup"><span data-stu-id="a6837-143">In the code-behind files for Students, AddStudent, and Courses, delete or comment out the following query methods:</span></span>

- <span data-ttu-id="a6837-144">studentsGrid\_的</span><span class="sxs-lookup"><span data-stu-id="a6837-144">studentsGrid\_GetData</span></span>
- <span data-ttu-id="a6837-145">studentsGrid\_UpdateItem</span><span class="sxs-lookup"><span data-stu-id="a6837-145">studentsGrid\_UpdateItem</span></span>
- <span data-ttu-id="a6837-146">studentsGrid\_DeleteItem</span><span class="sxs-lookup"><span data-stu-id="a6837-146">studentsGrid\_DeleteItem</span></span>
- <span data-ttu-id="a6837-147">addStudentForm\_InsertItem</span><span class="sxs-lookup"><span data-stu-id="a6837-147">addStudentForm\_InsertItem</span></span>
- <span data-ttu-id="a6837-148">coursesGrid\_的</span><span class="sxs-lookup"><span data-stu-id="a6837-148">coursesGrid\_GetData</span></span>

<span data-ttu-id="a6837-149">在程式碼後置檔案中，您現在不應該有與資料作業相關的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a6837-149">You now should have no code in the code-behind file that pertains to data operations.</span></span>

<span data-ttu-id="a6837-150">**OnCallingDataMethods**事件處理常式可讓您指定要用於資料方法的物件。</span><span class="sxs-lookup"><span data-stu-id="a6837-150">The **OnCallingDataMethods** event handler enables you to specify an object to use for the data methods.</span></span> <span data-ttu-id="a6837-151">在 [student] 中，為該事件處理常式新增一個值，並將資料方法的名稱變更為商務邏輯類別中的方法名稱。</span><span class="sxs-lookup"><span data-stu-id="a6837-151">In Students.aspx, add a value for that event handler and change the names of the data methods to the names of the methods in the business logic class.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

<span data-ttu-id="a6837-152">在 default.aspx 的程式碼後置檔案中，定義 CallingDataMethods 事件的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="a6837-152">In the code-behind file for Students.aspx, define the event handler for the CallingDataMethods event.</span></span> <span data-ttu-id="a6837-153">在這個事件處理常式中，您可以指定資料作業的商務邏輯類別。</span><span class="sxs-lookup"><span data-stu-id="a6837-153">In this event handler, you specify the business logic class for data operations.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

<span data-ttu-id="a6837-154">在 AddStudent 中進行類似的變更。</span><span class="sxs-lookup"><span data-stu-id="a6837-154">In AddStudent.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

<span data-ttu-id="a6837-155">在 default.aspx 中，進行類似的變更。</span><span class="sxs-lookup"><span data-stu-id="a6837-155">In Courses.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

<span data-ttu-id="a6837-156">執行應用程式，並注意所有頁面的運作方式都與先前相同。</span><span class="sxs-lookup"><span data-stu-id="a6837-156">Run the application and notice that all of the pages function as they had previously.</span></span> <span data-ttu-id="a6837-157">驗證邏輯也會正確運作。</span><span class="sxs-lookup"><span data-stu-id="a6837-157">The validation logic also works correctly.</span></span>

## <a name="conclusion"></a><span data-ttu-id="a6837-158">結論</span><span class="sxs-lookup"><span data-stu-id="a6837-158">Conclusion</span></span>

<span data-ttu-id="a6837-159">在本教學課程中，您會重新結構化應用程式以使用資料存取層和商務邏輯層。</span><span class="sxs-lookup"><span data-stu-id="a6837-159">In this tutorial, you re-structured your application to use a data access layer and business logic layer.</span></span> <span data-ttu-id="a6837-160">您指定資料控制項使用的物件不是資料作業的目前頁面。</span><span class="sxs-lookup"><span data-stu-id="a6837-160">You specified that the data controls use an object that is not the current page for data operations.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a6837-161">上一步</span><span class="sxs-lookup"><span data-stu-id="a6837-161">Previous</span></span>](using-query-string-values-to-retrieve-data.md)
