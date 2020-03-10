---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
title: 使用 IDataErrorInfo 介面（VB）進行驗證 |Microsoft Docs
author: StephenWalther
description: Stephen Walther 將示範如何在模型類別中執行 IDataErrorInfo 介面，以顯示自訂驗證錯誤訊息。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3a8a9d9f-82dd-4959-b7c6-960e9ce95df1
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 8ff3adc5db8114dcca2c66d937e1706f0bac0d30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542501"
---
# <a name="validating-with-the-idataerrorinfo-interface-vb"></a><span data-ttu-id="37aa0-103">驗證與 IDataErrorInfo 介面 (VB)</span><span class="sxs-lookup"><span data-stu-id="37aa0-103">Validating with the IDataErrorInfo Interface (VB)</span></span>

<span data-ttu-id="37aa0-104">依[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="37aa0-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="37aa0-105">Stephen Walther 將示範如何在模型類別中執行 IDataErrorInfo 介面，以顯示自訂驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="37aa0-105">Stephen Walther shows you how to display custom validation error messages by implementing the IDataErrorInfo interface in a model class.</span></span>

<span data-ttu-id="37aa0-106">本教學課程的目的是要說明在 ASP.NET MVC 應用程式中執行驗證的一種方法。</span><span class="sxs-lookup"><span data-stu-id="37aa0-106">The goal of this tutorial is to explain one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="37aa0-107">您將瞭解如何防止某人提交 HTML 表單，而不需要為必要的表單欄位提供值。</span><span class="sxs-lookup"><span data-stu-id="37aa0-107">You learn how to prevent someone from submitting an HTML form without providing values for required form fields.</span></span> <span data-ttu-id="37aa0-108">在本教學課程中，您將瞭解如何使用 IErrorDataInfo 介面來執行驗證。</span><span class="sxs-lookup"><span data-stu-id="37aa0-108">In this tutorial, you learn how to perform validation by using the IErrorDataInfo interface.</span></span>

## <a name="assumptions"></a><span data-ttu-id="37aa0-109">假設</span><span class="sxs-lookup"><span data-stu-id="37aa0-109">Assumptions</span></span>

<span data-ttu-id="37aa0-110">在本教學課程中，我將使用 MoviesDB 資料庫和電影資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="37aa0-110">In this tutorial, I'll use the MoviesDB database and the Movies database table.</span></span> <span data-ttu-id="37aa0-111">這個資料表具有下列資料行：</span><span class="sxs-lookup"><span data-stu-id="37aa0-111">This table has the following columns:</span></span>

<a id="0.6_table01"></a>

| <span data-ttu-id="37aa0-112">**資料行名稱**</span><span class="sxs-lookup"><span data-stu-id="37aa0-112">**Column Name**</span></span> | <span data-ttu-id="37aa0-113">**資料類型**</span><span class="sxs-lookup"><span data-stu-id="37aa0-113">**Data Type**</span></span> | <span data-ttu-id="37aa0-114">**允許 Null**</span><span class="sxs-lookup"><span data-stu-id="37aa0-114">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="37aa0-115">ID</span><span class="sxs-lookup"><span data-stu-id="37aa0-115">Id</span></span> | <span data-ttu-id="37aa0-116">Int</span><span class="sxs-lookup"><span data-stu-id="37aa0-116">Int</span></span> | <span data-ttu-id="37aa0-117">False</span><span class="sxs-lookup"><span data-stu-id="37aa0-117">False</span></span> |
| <span data-ttu-id="37aa0-118">標題</span><span class="sxs-lookup"><span data-stu-id="37aa0-118">Title</span></span> | <span data-ttu-id="37aa0-119">NVarchar （100）</span><span class="sxs-lookup"><span data-stu-id="37aa0-119">Nvarchar(100)</span></span> | <span data-ttu-id="37aa0-120">False</span><span class="sxs-lookup"><span data-stu-id="37aa0-120">False</span></span> |
| <span data-ttu-id="37aa0-121">導演</span><span class="sxs-lookup"><span data-stu-id="37aa0-121">Director</span></span> | <span data-ttu-id="37aa0-122">NVarchar （100）</span><span class="sxs-lookup"><span data-stu-id="37aa0-122">Nvarchar(100)</span></span> | <span data-ttu-id="37aa0-123">False</span><span class="sxs-lookup"><span data-stu-id="37aa0-123">False</span></span> |
| <span data-ttu-id="37aa0-124">DateReleased</span><span class="sxs-lookup"><span data-stu-id="37aa0-124">DateReleased</span></span> | <span data-ttu-id="37aa0-125">DateTime</span><span class="sxs-lookup"><span data-stu-id="37aa0-125">DateTime</span></span> | <span data-ttu-id="37aa0-126">False</span><span class="sxs-lookup"><span data-stu-id="37aa0-126">False</span></span> |

<span data-ttu-id="37aa0-127">在本教學課程中，我使用 Microsoft Entity Framework 來產生資料庫模型類別。</span><span class="sxs-lookup"><span data-stu-id="37aa0-127">In this tutorial, I use the Microsoft Entity Framework to generate my database model classes.</span></span> <span data-ttu-id="37aa0-128">Entity Framework 所產生的 Movie 類別如 [圖 1] 所示。</span><span class="sxs-lookup"><span data-stu-id="37aa0-128">The Movie class generated by the Entity Framework is displayed in Figure 1.</span></span>

<span data-ttu-id="37aa0-129">[![Movie 實體](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="37aa0-129">[![The Movie entity](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)</span></span>

<span data-ttu-id="37aa0-130">**圖 01**： Movie 實體（[按一下以觀看完整大小的影像](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="37aa0-130">**Figure 01**: The Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png))</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="37aa0-131">若要深入瞭解如何使用 Entity Framework 來產生您的資料庫模型類別，請參閱我的教學課程，其標題為使用 Entity Framework 建立模型類別。</span><span class="sxs-lookup"><span data-stu-id="37aa0-131">To learn more about using the Entity Framework to generate your database model classes, see my tutorial entitled Creating Model Classes with the Entity Framework.</span></span>

## <a name="the-controller-class"></a><span data-ttu-id="37aa0-132">控制器類別</span><span class="sxs-lookup"><span data-stu-id="37aa0-132">The Controller Class</span></span>

<span data-ttu-id="37aa0-133">我們使用 Home 控制器來列出電影，並建立新的電影。</span><span class="sxs-lookup"><span data-stu-id="37aa0-133">We use the Home controller to list movies and create new movies.</span></span> <span data-ttu-id="37aa0-134">此類別的程式碼包含在 [清單 1] 中。</span><span class="sxs-lookup"><span data-stu-id="37aa0-134">The code for this class is contained in Listing 1.</span></span>

<span data-ttu-id="37aa0-135">**清單 1-Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="37aa0-135">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample1.vb)]

<span data-ttu-id="37aa0-136">[清單 1] 中的 Home 控制器類別包含兩個 Create （）動作。</span><span class="sxs-lookup"><span data-stu-id="37aa0-136">The Home controller class in Listing 1 contains two Create() actions.</span></span> <span data-ttu-id="37aa0-137">第一個動作會顯示用來建立新電影的 HTML 表單。</span><span class="sxs-lookup"><span data-stu-id="37aa0-137">The first action displays the HTML form for creating a new movie.</span></span> <span data-ttu-id="37aa0-138">第二個 Create （）動作會執行將新電影的實際插入到資料庫中。</span><span class="sxs-lookup"><span data-stu-id="37aa0-138">The second Create() action performs the actual insert of the new movie into the database.</span></span> <span data-ttu-id="37aa0-139">當第一個 Create （）動作所顯示的表單提交至伺服器時，會叫用第二個 Create （）動作。</span><span class="sxs-lookup"><span data-stu-id="37aa0-139">The second Create() action is invoked when the form displayed by the first Create() action is submitted to the server.</span></span>

<span data-ttu-id="37aa0-140">請注意，第二個 Create （）動作包含下列幾行程式碼：</span><span class="sxs-lookup"><span data-stu-id="37aa0-140">Notice that the second Create() action contains the following lines of code:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample2.vb)]

<span data-ttu-id="37aa0-141">當發生驗證錯誤時，IsValid 屬性會傳回 false。</span><span class="sxs-lookup"><span data-stu-id="37aa0-141">The IsValid property returns false when there is a validation error.</span></span> <span data-ttu-id="37aa0-142">在此情況下，會重新顯示包含用於建立電影之 HTML 表單的 [建立] 視圖。</span><span class="sxs-lookup"><span data-stu-id="37aa0-142">In that case, the Create view that contains the HTML form for creating a movie is redisplayed.</span></span>

## <a name="creating-a-partial-class"></a><span data-ttu-id="37aa0-143">建立部分類別</span><span class="sxs-lookup"><span data-stu-id="37aa0-143">Creating a Partial Class</span></span>

<span data-ttu-id="37aa0-144">Movie 類別是由 Entity Framework 所產生。</span><span class="sxs-lookup"><span data-stu-id="37aa0-144">The Movie class is generated by the Entity Framework.</span></span> <span data-ttu-id="37aa0-145">如果您在 [方案總管] 視窗中展開 [MoviesDBModel] 檔案，並在程式碼編輯器中開啟 MoviesDBModel，則可以看到 Movie 類別的程式碼（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="37aa0-145">You can see the code for the Movie class if you expand the MoviesDBModel.edmx file in the Solution Explorer window and open the MoviesDBModel.Designer.vb file in the Code Editor (see Figure 2).</span></span>

<span data-ttu-id="37aa0-146">[![Movie 實體的程式碼](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="37aa0-146">[![The code for the Movie entity](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)</span></span>

<span data-ttu-id="37aa0-147">**圖 02**： Movie 實體的程式碼（[按一下以觀看完整大小的影像](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="37aa0-147">**Figure 02**: The code for the Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png))</span></span>

<span data-ttu-id="37aa0-148">Movie 類別是部分類別。</span><span class="sxs-lookup"><span data-stu-id="37aa0-148">The Movie class is a partial class.</span></span> <span data-ttu-id="37aa0-149">這表示我們可以加入另一個具有相同名稱的部分類別，以擴充 Movie 類別的功能。</span><span class="sxs-lookup"><span data-stu-id="37aa0-149">That means that we can add another partial class with the same name to extend the functionality of the Movie class.</span></span> <span data-ttu-id="37aa0-150">我們會將驗證邏輯新增至新的部分類別。</span><span class="sxs-lookup"><span data-stu-id="37aa0-150">We'll add our validation logic to the new partial class.</span></span>

<span data-ttu-id="37aa0-151">將 [清單 2] 中的類別新增至 [模型] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="37aa0-151">Add the class in Listing 2 to the Models folder.</span></span>

<span data-ttu-id="37aa0-152">**清單 2-Models\Movie.vb**</span><span class="sxs-lookup"><span data-stu-id="37aa0-152">**Listing 2 - Models\Movie.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample3.vb)]

<span data-ttu-id="37aa0-153">請注意，[清單 2] 中的類別包含*部分*修飾詞。</span><span class="sxs-lookup"><span data-stu-id="37aa0-153">Notice that the class in Listing 2 includes the *partial* modifier.</span></span> <span data-ttu-id="37aa0-154">您新增至此類別的任何方法或屬性，都會成為 Entity Framework 所產生之 Movie 類別的一部分。</span><span class="sxs-lookup"><span data-stu-id="37aa0-154">Any methods or properties that you add to this class become part of the Movie class generated by the Entity Framework.</span></span>

## <a name="adding-onchanging-and-onchanged-partial-methods"></a><span data-ttu-id="37aa0-155">新增 OnChanging 和 OnChanged 部分方法</span><span class="sxs-lookup"><span data-stu-id="37aa0-155">Adding OnChanging and OnChanged Partial Methods</span></span>

<span data-ttu-id="37aa0-156">當 Entity Framework 產生實體類別時，Entity Framework 會自動將部分方法新增至類別。</span><span class="sxs-lookup"><span data-stu-id="37aa0-156">When the Entity Framework generates an entity class, the Entity Framework adds partial methods to the class automatically.</span></span> <span data-ttu-id="37aa0-157">Entity Framework 會產生對應至類別之每個屬性的 OnChanging 和 OnChanged 部分方法。</span><span class="sxs-lookup"><span data-stu-id="37aa0-157">The Entity Framework generates OnChanging and OnChanged partial methods that correspond to each property of the class.</span></span>

<span data-ttu-id="37aa0-158">就 Movie 類別而言，Entity Framework 會建立下列方法：</span><span class="sxs-lookup"><span data-stu-id="37aa0-158">In the case of the Movie class, the Entity Framework creates the following methods:</span></span>

- <span data-ttu-id="37aa0-159">OnIdChanging</span><span class="sxs-lookup"><span data-stu-id="37aa0-159">OnIdChanging</span></span>
- <span data-ttu-id="37aa0-160">OnIdChanged</span><span class="sxs-lookup"><span data-stu-id="37aa0-160">OnIdChanged</span></span>
- <span data-ttu-id="37aa0-161">OnTitleChanging</span><span class="sxs-lookup"><span data-stu-id="37aa0-161">OnTitleChanging</span></span>
- <span data-ttu-id="37aa0-162">OnTitleChanged</span><span class="sxs-lookup"><span data-stu-id="37aa0-162">OnTitleChanged</span></span>
- <span data-ttu-id="37aa0-163">OnDirectorChanging</span><span class="sxs-lookup"><span data-stu-id="37aa0-163">OnDirectorChanging</span></span>
- <span data-ttu-id="37aa0-164">OnDirectorChanged</span><span class="sxs-lookup"><span data-stu-id="37aa0-164">OnDirectorChanged</span></span>
- <span data-ttu-id="37aa0-165">OnDateReleasedChanging</span><span class="sxs-lookup"><span data-stu-id="37aa0-165">OnDateReleasedChanging</span></span>
- <span data-ttu-id="37aa0-166">OnDateReleasedChanged</span><span class="sxs-lookup"><span data-stu-id="37aa0-166">OnDateReleasedChanged</span></span>

<span data-ttu-id="37aa0-167">OnChanging 方法會在對應的屬性變更之前呼叫。</span><span class="sxs-lookup"><span data-stu-id="37aa0-167">The OnChanging method is called right before the corresponding property is changed.</span></span> <span data-ttu-id="37aa0-168">OnChanged 方法會在屬性變更之後立即呼叫。</span><span class="sxs-lookup"><span data-stu-id="37aa0-168">The OnChanged method is called right after the property is changed.</span></span>

<span data-ttu-id="37aa0-169">您可以利用這些部分方法，將驗證邏輯新增至 Movie 類別。</span><span class="sxs-lookup"><span data-stu-id="37aa0-169">You can take advantage of these partial methods to add validation logic to the Movie class.</span></span> <span data-ttu-id="37aa0-170">[清單 3] 中的 [更新電影] 類別會驗證標題和主管屬性是否指派為非空白值。</span><span class="sxs-lookup"><span data-stu-id="37aa0-170">The update Movie class in Listing 3 verifies that the Title and Director properties are assigned nonempty values.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="37aa0-171">部分方法是在類別中定義的方法，而您不需要執行此方法。</span><span class="sxs-lookup"><span data-stu-id="37aa0-171">A partial method is a method defined in a class that you are not required to implement.</span></span> <span data-ttu-id="37aa0-172">如果您未執行部分方法，則編譯器會移除方法簽章和所有對方法的呼叫，因此不會有與部分方法相關聯的執行時間成本。</span><span class="sxs-lookup"><span data-stu-id="37aa0-172">If you don't implement a partial method then the compiler removes the method signature and all calls to the method so there are no run-time costs associated with the partial method.</span></span> <span data-ttu-id="37aa0-173">在 Visual Studio Code 編輯器中，您可以藉由輸入關鍵字*partial*後面加上空格來新增部分方法，以查看要執行的部分清單。</span><span class="sxs-lookup"><span data-stu-id="37aa0-173">In the Visual Studio Code Editor, you can add a partial method by typing the keyword *partial* followed by a space to view a list of partials to implement.</span></span>

<span data-ttu-id="37aa0-174">**清單 3-Models\Movie.vb**</span><span class="sxs-lookup"><span data-stu-id="37aa0-174">**Listing 3 - Models\Movie.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample4.vb)]

<span data-ttu-id="37aa0-175">例如，如果您嘗試將空字串指派給 Title 屬性，則會將錯誤訊息指派給名為 \_錯誤的字典。</span><span class="sxs-lookup"><span data-stu-id="37aa0-175">For example, if you attempt to assign an empty string to the Title property, then an error message is assigned to a Dictionary named \_errors.</span></span>

<span data-ttu-id="37aa0-176">此時，當您將空字串指派給 Title 屬性，而將錯誤加入 [私用 \_錯誤] 欄位時，實際上不會發生任何事。</span><span class="sxs-lookup"><span data-stu-id="37aa0-176">At this point, nothing actually happens when you assign an empty string to the Title property and an error is added to the private \_errors field.</span></span> <span data-ttu-id="37aa0-177">我們需要執行 IDataErrorInfo 介面，將這些驗證錯誤公開給 ASP.NET MVC 架構。</span><span class="sxs-lookup"><span data-stu-id="37aa0-177">We need to implement the IDataErrorInfo interface to expose these validation errors to the ASP.NET MVC framework.</span></span>

## <a name="implementing-the-idataerrorinfo-interface"></a><span data-ttu-id="37aa0-178">執行 IDataErrorInfo 介面</span><span class="sxs-lookup"><span data-stu-id="37aa0-178">Implementing the IDataErrorInfo Interface</span></span>

<span data-ttu-id="37aa0-179">從第一個版本開始，IDataErrorInfo 介面是 .NET framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="37aa0-179">The IDataErrorInfo interface has been part of the .NET framework since the first version.</span></span> <span data-ttu-id="37aa0-180">這個介面是非常簡單的介面：</span><span class="sxs-lookup"><span data-stu-id="37aa0-180">This interface is a very simple interface:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample5.vb)]

<span data-ttu-id="37aa0-181">如果類別會實 IDataErrorInfo 介面，則 ASP.NET MVC 架構會在建立類別的實例時使用此介面。</span><span class="sxs-lookup"><span data-stu-id="37aa0-181">If a class implements the IDataErrorInfo interface, the ASP.NET MVC framework will use this interface when creating an instance of the class.</span></span> <span data-ttu-id="37aa0-182">例如，「主控制器建立」（）動作會接受 Movie 類別的實例：</span><span class="sxs-lookup"><span data-stu-id="37aa0-182">For example, the Home controller Create() action accepts an instance of the Movie class:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample6.vb)]

<span data-ttu-id="37aa0-183">ASP.NET MVC 架構會使用模型系結器（DefaultModelBinder），建立傳遞至 Create （）動作的電影實例。</span><span class="sxs-lookup"><span data-stu-id="37aa0-183">The ASP.NET MVC framework creates the instance of the Movie passed to the Create() action by using a model binder (the DefaultModelBinder).</span></span> <span data-ttu-id="37aa0-184">「模型系結器」負責建立 Movie 物件的實例，方法是將 HTML 表單欄位系結至 Movie 物件的實例。</span><span class="sxs-lookup"><span data-stu-id="37aa0-184">The model binder is responsible for creating an instance of the Movie object by binding the HTML form fields to an instance of the Movie object.</span></span>

<span data-ttu-id="37aa0-185">DefaultModelBinder 會偵測類別是否會實作為 IDataErrorInfo 介面。</span><span class="sxs-lookup"><span data-stu-id="37aa0-185">The DefaultModelBinder detects whether or not a class implements the IDataErrorInfo interface.</span></span> <span data-ttu-id="37aa0-186">如果類別會實作為此介面，則模型系結器會叫用 IDataErrorInfo。此為類別的每個屬性。</span><span class="sxs-lookup"><span data-stu-id="37aa0-186">If a class implements this interface then the model binder invokes the IDataErrorInfo.this indexer for each property of the class.</span></span> <span data-ttu-id="37aa0-187">如果索引子傳回錯誤訊息，則模型系結器會自動將此錯誤訊息新增至模型狀態。</span><span class="sxs-lookup"><span data-stu-id="37aa0-187">If the indexer returns an error message then the model binder adds this error message to model state automatically.</span></span>

<span data-ttu-id="37aa0-188">DefaultModelBinder 也會檢查 IDataErrorInfo 屬性。</span><span class="sxs-lookup"><span data-stu-id="37aa0-188">The DefaultModelBinder also checks the IDataErrorInfo.Error property.</span></span> <span data-ttu-id="37aa0-189">這個屬性主要是用來表示與類別相關聯的非屬性特定驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="37aa0-189">This property is intended to represent non-property specific validation errors associated with the class.</span></span> <span data-ttu-id="37aa0-190">例如，您可能會想要強制執行取決於 Movie 類別的多個屬性值的驗證規則。</span><span class="sxs-lookup"><span data-stu-id="37aa0-190">For example, you might want to enforce a validation rule that depends on the values of multiple properties of the Movie class.</span></span> <span data-ttu-id="37aa0-191">在這種情況下，您會從 Error 屬性傳回驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="37aa0-191">In that case, you would return a validation error from the Error property.</span></span>

<span data-ttu-id="37aa0-192">清單4中已更新的 Movie 類別會執行 IDataErrorInfo 介面。</span><span class="sxs-lookup"><span data-stu-id="37aa0-192">The updated Movie class in Listing 4 implements the IDataErrorInfo interface.</span></span>

<span data-ttu-id="37aa0-193">**清單 4-Models\Movie.vb （實 IDataErrorInfo）**</span><span class="sxs-lookup"><span data-stu-id="37aa0-193">**Listing 4 - Models\Movie.vb (implements IDataErrorInfo)**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample7.vb)]

<span data-ttu-id="37aa0-194">在 [清單 4] 中，索引子屬性會檢查 \_錯誤集合，以查看它是否包含對應至傳遞至索引子之屬性名稱的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="37aa0-194">In Listing 4, the indexer property checks the \_errors collection to see if it contains a key that corresponds to the property name passed to the indexer.</span></span> <span data-ttu-id="37aa0-195">如果沒有與屬性相關聯的驗證錯誤，則會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="37aa0-195">If there is no validation error associated with the property then an empty string is returned.</span></span>

<span data-ttu-id="37aa0-196">您不需要以任何方式修改 Home 控制器，即可使用修改過的 Movie 類別。</span><span class="sxs-lookup"><span data-stu-id="37aa0-196">You don't need to modify the Home controller in any way to use the modified Movie class.</span></span> <span data-ttu-id="37aa0-197">[圖 3] 中所顯示的頁面說明在沒有輸入標題或導演表單欄位的值時，會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="37aa0-197">The page displayed in Figure 3 illustrates what happens when no value is entered for the Title or Director form fields.</span></span>

<span data-ttu-id="37aa0-198">[![自動建立動作方法](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="37aa0-198">[![Creating action methods automatically](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)</span></span>

<span data-ttu-id="37aa0-199">**圖 03**：含有遺漏值的表單（[按一下以查看完整大小的影像](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="37aa0-199">**Figure 03**: A form with missing values ([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png))</span></span>

<span data-ttu-id="37aa0-200">請注意，系統會自動驗證 DateReleased 值。</span><span class="sxs-lookup"><span data-stu-id="37aa0-200">Notice that the DateReleased value is validated automatically.</span></span> <span data-ttu-id="37aa0-201">因為 DateReleased 屬性不接受 Null 值，所以當這個屬性沒有值時，DefaultModelBinder 會自動產生驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="37aa0-201">Because the DateReleased property does not accept NULL values, the DefaultModelBinder generates a validation error for this property automatically when it does not have a value.</span></span> <span data-ttu-id="37aa0-202">如果您想要修改 DateReleased 屬性的錯誤訊息，則需要建立自訂模型系結器。</span><span class="sxs-lookup"><span data-stu-id="37aa0-202">If you want to modify the error message for the DateReleased property then you need to create a custom model binder.</span></span>

## <a name="summary"></a><span data-ttu-id="37aa0-203">總結</span><span class="sxs-lookup"><span data-stu-id="37aa0-203">Summary</span></span>

<span data-ttu-id="37aa0-204">在本教學課程中，您已瞭解如何使用 IDataErrorInfo 介面來產生驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="37aa0-204">In this tutorial, you learned how to use the IDataErrorInfo interface to generate validation error messages.</span></span> <span data-ttu-id="37aa0-205">首先，我們建立了部分 Movie 類別，以擴充 Entity Framework 所產生之部分 Movie 類別的功能。</span><span class="sxs-lookup"><span data-stu-id="37aa0-205">First, we created a partial Movie class that extends the functionality of the partial Movie class generated by the Entity Framework.</span></span> <span data-ttu-id="37aa0-206">接下來，我們已將驗證邏輯新增至 Movie 類別 OnTitleChanging （）和 OnDirectorChanging （）部分方法。</span><span class="sxs-lookup"><span data-stu-id="37aa0-206">Next, we added validation logic to the Movie class OnTitleChanging() and OnDirectorChanging() partial methods.</span></span> <span data-ttu-id="37aa0-207">最後，我們會實 IDataErrorInfo 介面，以便將這些驗證訊息公開給 ASP.NET MVC 架構。</span><span class="sxs-lookup"><span data-stu-id="37aa0-207">Finally, we implemented the IDataErrorInfo interface in order to expose these validation messages to the ASP.NET MVC framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="37aa0-208">[上一頁](performing-simple-validation-vb.md)
> [下一頁](validating-with-a-service-layer-vb.md)</span><span class="sxs-lookup"><span data-stu-id="37aa0-208">[Previous](performing-simple-validation-vb.md)
[Next](validating-with-a-service-layer-vb.md)</span></span>
