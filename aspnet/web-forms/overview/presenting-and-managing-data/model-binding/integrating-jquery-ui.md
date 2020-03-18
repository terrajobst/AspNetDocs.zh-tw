---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: 整合 JQuery UI Datepicker 與模型系結和 web forms |Microsoft Docs
author: Rick-Anderson
description: 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結讓資料互動更為直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: c8d711dd44950116f3a3e09d5d12c507918c543f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642475"
---
# <a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a><span data-ttu-id="af26b-104">整合 JQuery UI Datepicker 與模型系結和 web 表單</span><span class="sxs-lookup"><span data-stu-id="af26b-104">Integrating JQuery UI Datepicker with model binding and web forms</span></span>

<span data-ttu-id="af26b-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="af26b-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="af26b-106">本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。</span><span class="sxs-lookup"><span data-stu-id="af26b-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="af26b-107">模型系結可讓資料互動比處理資料來源物件（例如 ObjectDataSource 或 SqlDataSource）更直接。</span><span class="sxs-lookup"><span data-stu-id="af26b-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="af26b-108">此系列從簡介材料開始，並在稍後的教學課程中移至更先進的概念。</span><span class="sxs-lookup"><span data-stu-id="af26b-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="af26b-109">本教學課程示範如何將 JQuery UI [Datepicker widget](http://jqueryui.com/datepicker/)新增至 Web 表單，並使用模型系結以選取的值來更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="af26b-109">This tutorial shows how to add the JQuery UI [Datepicker widget](http://jqueryui.com/datepicker/) to a Web Form, and use model binding to update the database with the selected value.</span></span>
> 
> <span data-ttu-id="af26b-110">本教學課程是以數列的[第一個](retrieving-data.md)和[第二個](updating-deleting-and-creating-data.md)部分中所建立的專案為基礎。</span><span class="sxs-lookup"><span data-stu-id="af26b-110">This tutorial builds on the project created in the [first](retrieving-data.md) and [second](updating-deleting-and-creating-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="af26b-111">您可以[download](https://go.microsoft.com/fwlink/?LinkId=286116)在或 VB 中C#下載完整專案。</span><span class="sxs-lookup"><span data-stu-id="af26b-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="af26b-112">可下載的程式碼適用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="af26b-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="af26b-113">它會使用 Visual Studio 2012 範本，這與本教學課程中所顯示的 Visual Studio 2013 範本稍有不同。</span><span class="sxs-lookup"><span data-stu-id="af26b-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="af26b-114">您將建立的內容</span><span class="sxs-lookup"><span data-stu-id="af26b-114">What you'll build</span></span>

<span data-ttu-id="af26b-115">在本教學課程中，您將會：</span><span class="sxs-lookup"><span data-stu-id="af26b-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="af26b-116">將屬性新增至您的模型，以記錄學生的註冊日期</span><span class="sxs-lookup"><span data-stu-id="af26b-116">Add a property to your model to record the student's enrollment date</span></span>
2. <span data-ttu-id="af26b-117">讓使用者可以使用 JQuery UI Datepicker widget 來選取註冊日期</span><span class="sxs-lookup"><span data-stu-id="af26b-117">Enable the user to select the enrollment date using the JQuery UI Datepicker widget</span></span>
3. <span data-ttu-id="af26b-118">強制執行註冊日期的驗證規則</span><span class="sxs-lookup"><span data-stu-id="af26b-118">Enforce validation rules for the enrollment date</span></span>

<span data-ttu-id="af26b-119">JQuery UI Datepicker 小工具可讓使用者在使用者與欄位互動時，輕鬆地從行事曆選取日期。</span><span class="sxs-lookup"><span data-stu-id="af26b-119">The JQuery UI Datepicker widget enables users to easily select a date from a calendar that pops up when the user interacts with the field.</span></span> <span data-ttu-id="af26b-120">對於使用者而言，使用這個小工具會比手動輸入日期更方便。</span><span class="sxs-lookup"><span data-stu-id="af26b-120">Using this widget can be more convenient for users than manually typing a date.</span></span> <span data-ttu-id="af26b-121">將 Datepicker widget 整合到使用模型系結來進行資料作業的頁面，只需要少量的額外工作。</span><span class="sxs-lookup"><span data-stu-id="af26b-121">Integrating the Datepicker widget into a page that uses model binding for data operations requires only a small amount of additional work.</span></span>

## <a name="add-a-new-property-to-the-model"></a><span data-ttu-id="af26b-122">將新屬性新增至模型</span><span class="sxs-lookup"><span data-stu-id="af26b-122">Add a new property to the model</span></span>

<span data-ttu-id="af26b-123">首先，您會將**日期時間**屬性加入至您的學生模型，並將該變更遷移至資料庫。</span><span class="sxs-lookup"><span data-stu-id="af26b-123">First, you will add a **Datetime** property to your Student model and migrate that change to the database.</span></span> <span data-ttu-id="af26b-124">開啟**UniversityModels.cs**，並將反白顯示的程式碼新增至學生模型。</span><span class="sxs-lookup"><span data-stu-id="af26b-124">Open **UniversityModels.cs**, and add the highlighted code to the Student model.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

<span data-ttu-id="af26b-125">包含**RangeAttribute**是為了強制執行屬性的驗證規則。</span><span class="sxs-lookup"><span data-stu-id="af26b-125">The **RangeAttribute** is included to enforce validation rules for the property.</span></span> <span data-ttu-id="af26b-126">在本教學課程中，我們會假設 Contoso 大學是在2013年1月1日成立，因此較早的註冊日期是不正確。</span><span class="sxs-lookup"><span data-stu-id="af26b-126">For this tutorial, we will assume that Contoso University was founded on January 1st, 2013 and therefore earlier enrollment dates are not valid.</span></span>

<span data-ttu-id="af26b-127">在 [套件管理] 視窗中，執行 [**新增-遷移 AddEnrollmentDate**] 命令來新增遷移。</span><span class="sxs-lookup"><span data-stu-id="af26b-127">In the Package Management window, add a migration by running the command **add-migration AddEnrollmentDate**.</span></span> <span data-ttu-id="af26b-128">請注意，遷移程式碼會將新的日期時間資料行加入至 Student 資料表。</span><span class="sxs-lookup"><span data-stu-id="af26b-128">Notice that the migration code adds the new Datetime column to the Student table.</span></span> <span data-ttu-id="af26b-129">若要符合您在 RangeAttribute 中指定的值，請為新的資料行加入預設值，如下列反白顯示的程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="af26b-129">To match the value you specified in the RangeAttribute, add a default value for the new column, as shown in the highlighted code below.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

<span data-ttu-id="af26b-130">將您的變更儲存至遷移檔案。</span><span class="sxs-lookup"><span data-stu-id="af26b-130">Save your change to the migration file.</span></span>

<span data-ttu-id="af26b-131">您不需要再次植入資料。</span><span class="sxs-lookup"><span data-stu-id="af26b-131">You do not need to seed the data again.</span></span> <span data-ttu-id="af26b-132">因此，請在 [遷移] 資料夾中開啟**Configuration.cs** ，並移除或批註**植入種子**方法中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="af26b-132">Therefore, open **Configuration.cs** in the Migrations folder and remove or comment out the code in the **Seed** method.</span></span> <span data-ttu-id="af26b-133">儲存並關閉檔案。</span><span class="sxs-lookup"><span data-stu-id="af26b-133">Save and close the file.</span></span>

<span data-ttu-id="af26b-134">現在，請執行命令**update-database**。</span><span class="sxs-lookup"><span data-stu-id="af26b-134">Now, run the command **update-database**.</span></span> <span data-ttu-id="af26b-135">請注意，資料行現在存在於資料庫中，而且所有現有的記錄都有 EnrollmentDate 的預設值。</span><span class="sxs-lookup"><span data-stu-id="af26b-135">Notice that the column now exists in the database and all of the existing records have the default value for EnrollmentDate.</span></span>

## <a name="add-dynamic-controls-for-enrollment-date"></a><span data-ttu-id="af26b-136">新增註冊日期的動態控制項</span><span class="sxs-lookup"><span data-stu-id="af26b-136">Add dynamic controls for enrollment date</span></span>

<span data-ttu-id="af26b-137">您現在會加入控制項，以顯示和編輯註冊日期。</span><span class="sxs-lookup"><span data-stu-id="af26b-137">You will now add controls for displaying and editing the enrollment date.</span></span> <span data-ttu-id="af26b-138">此時，值會透過文字方塊進行編輯。</span><span class="sxs-lookup"><span data-stu-id="af26b-138">At this point, the value is edited through a text box.</span></span> <span data-ttu-id="af26b-139">稍後在本教學課程中，您會將文字方塊變更為 JQuery Datepicker widget。</span><span class="sxs-lookup"><span data-stu-id="af26b-139">Later in the tutorial, you will change the text box to the JQuery Datepicker widget.</span></span>

<span data-ttu-id="af26b-140">首先，請務必注意，您不需要對**AddStudent .aspx**檔案進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="af26b-140">First, it is important to note that you do not need to make any change to the **AddStudent.aspx** file.</span></span> <span data-ttu-id="af26b-141">DynamicEntity 控制項會自動轉譯新的屬性。</span><span class="sxs-lookup"><span data-stu-id="af26b-141">The DynamicEntity control will automatically render the new property.</span></span>

<span data-ttu-id="af26b-142">開啟 **[** student]，並新增下列反白顯示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="af26b-142">Open **Students.aspx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

<span data-ttu-id="af26b-143">執行應用程式，並注意您可以輸入日期來設定註冊日期的值。</span><span class="sxs-lookup"><span data-stu-id="af26b-143">Run the application and notice that you can set the value of the enrollment date by typing a date.</span></span> <span data-ttu-id="af26b-144">加入新的學生時：</span><span class="sxs-lookup"><span data-stu-id="af26b-144">When adding a new student:</span></span>

![設定日期](integrating-jquery-ui/_static/image1.png)

<span data-ttu-id="af26b-146">或者，編輯現有的值：</span><span class="sxs-lookup"><span data-stu-id="af26b-146">Or, editing an existing value:</span></span>

![編輯日期](integrating-jquery-ui/_static/image2.png)

<span data-ttu-id="af26b-148">輸入日期可以運作，但可能不是您想要提供的客戶體驗。</span><span class="sxs-lookup"><span data-stu-id="af26b-148">Typing the date works, but it might not be the customer experience you wish to provide.</span></span> <span data-ttu-id="af26b-149">在下一節中，您將會啟用透過行事曆選取日期。</span><span class="sxs-lookup"><span data-stu-id="af26b-149">In the next section, you will enable selecting a date through a calendar.</span></span>

## <a name="install-nuget-package-to-work-with-jquery-ui"></a><span data-ttu-id="af26b-150">安裝 NuGet 套件以使用 JQuery UI</span><span class="sxs-lookup"><span data-stu-id="af26b-150">Install NuGet package to work with JQuery UI</span></span>

<span data-ttu-id="af26b-151">**JUICE UI** NuGet 套件可讓 JQuery UI widget 輕鬆地整合到您的 web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="af26b-151">The **Juice UI** NuGet package enables easy integration of the JQuery UI widgets into your web application.</span></span> <span data-ttu-id="af26b-152">若要使用此套件，請透過 NuGet 進行安裝。</span><span class="sxs-lookup"><span data-stu-id="af26b-152">To use this package, install it through NuGet.</span></span>

![新增 Juice UI](integrating-jquery-ui/_static/image3.png)

<span data-ttu-id="af26b-154">您安裝的 Juice UI 版本可能會與應用程式中的 JQuery 版本衝突。</span><span class="sxs-lookup"><span data-stu-id="af26b-154">The version of Juice UI that you install may conflict with the version of JQuery in your application.</span></span> <span data-ttu-id="af26b-155">繼續進行本教學課程之前，請先試著執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="af26b-155">Before proceeding with this tutorial, try running your application.</span></span> <span data-ttu-id="af26b-156">如果您遇到 JavaScript 錯誤，您需要協調 JQuery 版本。</span><span class="sxs-lookup"><span data-stu-id="af26b-156">If you encounter a JavaScript error, you need to reconcile the JQuery version.</span></span> <span data-ttu-id="af26b-157">您可以在腳本資料夾中加入預期的 JQuery 版本（在撰寫本教學課程時的版本1.8.2），或在 [網站] 中，指定 JQuery 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="af26b-157">You can either add the expected version of JQuery to your Scripts folder (version 1.8.2 at time of writing this tutorial), or in Site.master specify the path to the JQuery file.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a><span data-ttu-id="af26b-158">自訂日期時間範本以包含 Datepicker widget</span><span class="sxs-lookup"><span data-stu-id="af26b-158">Customize DateTime template to include Datepicker widget</span></span>

<span data-ttu-id="af26b-159">您會將 Datepicker widget 新增至動態資料範本，以編輯日期時間值。</span><span class="sxs-lookup"><span data-stu-id="af26b-159">You will add the Datepicker widget to the dynamic data template for editing a datetime value.</span></span> <span data-ttu-id="af26b-160">藉由將 widget 新增至範本，它會自動以用於新增學生的表單，以及在編輯學生的方格視圖中轉譯。</span><span class="sxs-lookup"><span data-stu-id="af26b-160">By adding the widget to the template, it is automatically rendered in both the form for adding a new student and in the grid view for editing students.</span></span> <span data-ttu-id="af26b-161">開啟**DateTime\_編輯 .ascx**，並新增下列反白顯示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="af26b-161">Open **DateTime\_Edit.ascx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

<span data-ttu-id="af26b-162">在程式碼後置檔案中，您會設定 DatePicker 的最小和最大日期。</span><span class="sxs-lookup"><span data-stu-id="af26b-162">In the code-behind file, you will set the minimum and maximum dates for the DatePicker.</span></span> <span data-ttu-id="af26b-163">藉由設定這些值，您將可防止使用者流覽至不正確日期。</span><span class="sxs-lookup"><span data-stu-id="af26b-163">By setting these values, you will prevent users from navigating to invalid dates.</span></span> <span data-ttu-id="af26b-164">您將會從日期時間屬性的**RangeAttribute**中取得最小和最大值（如果有提供的話）。</span><span class="sxs-lookup"><span data-stu-id="af26b-164">You will retrieve the minimum and maximum values from the **RangeAttribute** on the DateTime property, if one is provided.</span></span> <span data-ttu-id="af26b-165">開啟**DateTime\_Edit.ascx.cs**，並將下列反白顯示的程式碼新增至頁面\_載入方法。</span><span class="sxs-lookup"><span data-stu-id="af26b-165">Open **DateTime\_Edit.ascx.cs**, and add the following highlighted code to the Page\_Load method.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

<span data-ttu-id="af26b-166">執行 web 應用程式，並流覽至 [AddStudent] 頁面。</span><span class="sxs-lookup"><span data-stu-id="af26b-166">Run the web application and navigate to the AddStudent page.</span></span> <span data-ttu-id="af26b-167">提供欄位的值，並注意當您按一下 [註冊日期] 文字方塊時，會顯示行事曆。</span><span class="sxs-lookup"><span data-stu-id="af26b-167">Provide values for the fields and notice that when you click on the text box for Enrollment Date, the calendar is displayed.</span></span>

![日期選擇器](integrating-jquery-ui/_static/image4.png)

<span data-ttu-id="af26b-169">挑選日期，然後按一下 [**插入**]。</span><span class="sxs-lookup"><span data-stu-id="af26b-169">Pick a date, and click **Insert**.</span></span> <span data-ttu-id="af26b-170">RangeAttribute 會在伺服器上強制執行驗證。</span><span class="sxs-lookup"><span data-stu-id="af26b-170">The RangeAttribute enforces validation on the server.</span></span> <span data-ttu-id="af26b-171">藉由在 Datepicker 上設定 minDate 屬性，您也可以在用戶端上套用驗證。</span><span class="sxs-lookup"><span data-stu-id="af26b-171">By setting the minDate property on the Datepicker, you also apply validation on the client.</span></span> <span data-ttu-id="af26b-172">行事曆不會讓使用者流覽至 minDate 值之前的日期。</span><span class="sxs-lookup"><span data-stu-id="af26b-172">The calendar does not let the user navigate to a date prior to the value of minDate.</span></span>

<span data-ttu-id="af26b-173">當您編輯方格視圖中的記錄時，也會顯示行事曆。</span><span class="sxs-lookup"><span data-stu-id="af26b-173">When you edit a record in the grid view, the calendar is also displayed.</span></span>

![GridView 中的 Datepicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a><span data-ttu-id="af26b-175">結論</span><span class="sxs-lookup"><span data-stu-id="af26b-175">Conclusion</span></span>

<span data-ttu-id="af26b-176">在本教學課程中，您已瞭解如何將 JQuery widget 併入使用模型系結的 web 表單。</span><span class="sxs-lookup"><span data-stu-id="af26b-176">In this tutorial, you learned how to incorporate a JQuery widget into a web form that uses model binding.</span></span>

<span data-ttu-id="af26b-177">在下一個[教學](using-query-string-values-to-retrieve-data.md)課程中，您將會在選取資料時使用查詢字串值。</span><span class="sxs-lookup"><span data-stu-id="af26b-177">In the next [tutorial](using-query-string-values-to-retrieve-data.md), you will use a query string value when selecting data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="af26b-178">[上一頁](sorting-paging-and-filtering-data.md)
> [下一頁](using-query-string-values-to-retrieve-data.md)</span><span class="sxs-lookup"><span data-stu-id="af26b-178">[Previous](sorting-paging-and-filtering-data.md)
[Next](using-query-string-values-to-retrieve-data.md)</span></span>
