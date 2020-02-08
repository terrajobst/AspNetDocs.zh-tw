---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: 使用 jQuery UI 將新的分類新增至 DropDownList |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: cb9053593e2ea788638aec063c845cb91121861b
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075108"
---
# <a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a><span data-ttu-id="4d901-102">使用 jQuery UI 將新的分類新增至 DropDownList</span><span class="sxs-lookup"><span data-stu-id="4d901-102">Adding a New Category to the DropDownList using jQuery UI</span></span>

<span data-ttu-id="4d901-103">依[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="4d901-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

<span data-ttu-id="4d901-104">HTML `Select` 標記非常適合用來呈現固定類別目錄資料的清單，但通常需要加入新的類別。</span><span class="sxs-lookup"><span data-stu-id="4d901-104">The HTML `Select` tag is ideal for presenting a list of fixed category data, but often times you need to add a new category.</span></span> <span data-ttu-id="4d901-105">假設我們想要將「Opera」類型新增至資料庫中的類別目錄嗎？</span><span class="sxs-lookup"><span data-stu-id="4d901-105">Suppose we want to add the genre "Opera" to the categories in our database?</span></span> <span data-ttu-id="4d901-106">在本節中，我們將使用 jQuery UI 來加入可用於加入新分類的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4d901-106">In this section, we will use jQuery UI to add a dialog box we can use to add a new category.</span></span> <span data-ttu-id="4d901-107">下圖顯示 UI 在瀏覽器中的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="4d901-107">The image below shows how the UI will present in the browser.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

<span data-ttu-id="4d901-108">當使用者選取 [**加入新**的內容類型] 連結時，快顯視窗對話方塊會提示使用者輸入新的內容類型名稱（並選擇性地顯示描述）。</span><span class="sxs-lookup"><span data-stu-id="4d901-108">When a user selects the **Add New Genre** link, a pop-up dialog box prompts the user for a new genre name (and optionally a description).</span></span> <span data-ttu-id="4d901-109">下圖顯示 [**新增**內容類型] 快顯對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4d901-109">The image below show the **Add Genre** pop-up dialog.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

<span data-ttu-id="4d901-110">輸入新的內容類型名稱並推送 [**儲存**] 按鈕時，將會發生下列情況：</span><span class="sxs-lookup"><span data-stu-id="4d901-110">When a new genre name is entered and the **Save** button is pushed, the following happens:</span></span>

1. <span data-ttu-id="4d901-111">AJAX 呼叫會將資料張貼至內容類型控制器的 Create 方法，以將新的內容類型儲存至資料庫，並以 JSON 形式傳回新的內容類型資訊（類型名稱和識別碼）。</span><span class="sxs-lookup"><span data-stu-id="4d901-111">An AJAX call posts the data to the Create method of the Genre Controller, which saves the new genre to the database and returns the new genre information (genre name and ID) as JSON.</span></span>
2. <span data-ttu-id="4d901-112">JavaScript 會將新的內容類型資料新增至選取清單。</span><span class="sxs-lookup"><span data-stu-id="4d901-112">JavaScript adds the new genre data to the select list.</span></span>
3. <span data-ttu-id="4d901-113">JavaScript 讓新的內容類型成為選取的專案。</span><span class="sxs-lookup"><span data-stu-id="4d901-113">JavaScript makes the new genre the selected item.</span></span>

   <span data-ttu-id="4d901-114">在下圖中， **Opera**已加入至資料庫，並已**在 [內容**類型] 下拉式清單中選取。</span><span class="sxs-lookup"><span data-stu-id="4d901-114">In the image below, **Opera** was added to the database and selected in the **Genre** drop down list.</span></span> 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

<span data-ttu-id="4d901-115">開啟*Views\StoreManager\Create.cshtml*檔案，並以下列程式碼取代內容類型標記：</span><span class="sxs-lookup"><span data-stu-id="4d901-115">Open the *Views\StoreManager\Create.cshtml* file and replace the genre markup with the following the following code:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

<span data-ttu-id="4d901-116">`_ChooseGenre` 部分視圖將包含連結 JavaScript 的所有邏輯，以及用來執行 [加入新的內容類型] 功能的 jQuery。</span><span class="sxs-lookup"><span data-stu-id="4d901-116">The `_ChooseGenre` partial view will contain all the logic to hook up the JavaScript and jQuery used to implement the add new genre feature.</span></span> <span data-ttu-id="4d901-117">完成程式碼之後，就可以輕鬆地使用演出者 UI 來執行相同動作。</span><span class="sxs-lookup"><span data-stu-id="4d901-117">Once we have completed the code it will be simple to do the same with the artist UI.</span></span>

<span data-ttu-id="4d901-118">在方案總管中，以滑鼠右鍵按一下*Views\StoreManager*資料夾，然後依序選取 [**新增**] 和 [**查看**]。</span><span class="sxs-lookup"><span data-stu-id="4d901-118">In Solution Explorer, right click the *Views\StoreManager* folder and select **Add**, then **View**.</span></span> <span data-ttu-id="4d901-119">在 [ **View name** ] 輸入中，輸入 `_ChooseGenre` 然後選取 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="4d901-119">In the **View name** input, enter `_ChooseGenre` then select **Add**.</span></span> <span data-ttu-id="4d901-120">以下列內容取代*Views\StoreManager\\_ChooseGenre. cshtml*檔案中的標記：</span><span class="sxs-lookup"><span data-stu-id="4d901-120">Replace the markup in the *Views\StoreManager\\_ChooseGenre.cshtml* file with the following:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

<span data-ttu-id="4d901-121">第一行宣告我們以模型的形式傳入 `Album`，與在 Create view 中找到的模型語句完全相同。</span><span class="sxs-lookup"><span data-stu-id="4d901-121">The first line declares that we are passing in an `Album` as our model, exactly the same model statement found in the Create view.</span></span> <span data-ttu-id="4d901-122">接下來的幾行是**標籤**協助程式標記。</span><span class="sxs-lookup"><span data-stu-id="4d901-122">The next few lines are the **Label** helper markup.</span></span> <span data-ttu-id="4d901-123">下一行是**DropDownList** helper 呼叫，與原始 [建立] 視圖中的完全相同。</span><span class="sxs-lookup"><span data-stu-id="4d901-123">The next line is the **DropDownList** helper call, exactly the same as in the original Create view.</span></span> <span data-ttu-id="4d901-124">下一行會加入名稱為 `Add New Genre`的連結，並將其樣式與按鈕類似。</span><span class="sxs-lookup"><span data-stu-id="4d901-124">The next line adds a link with the name `Add New Genre`, and styles it like a button.</span></span> <span data-ttu-id="4d901-125">包含 `ValidationMessageFor` 的那一行是直接從 Create view 複製而來的。</span><span class="sxs-lookup"><span data-stu-id="4d901-125">The line containing `ValidationMessageFor` is copied directly from the Create view.</span></span> <span data-ttu-id="4d901-126">下列幾行：</span><span class="sxs-lookup"><span data-stu-id="4d901-126">The following lines:</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

<span data-ttu-id="4d901-127">建立隱藏的 div，其識別碼為 `genreDialog`。</span><span class="sxs-lookup"><span data-stu-id="4d901-127">creates a hidden div, with the ID of `genreDialog`.</span></span> <span data-ttu-id="4d901-128">我們將使用 jQuery 來連接我們的 [**新增**內容類型] 對話方塊，此 div 中的識別碼 `genreDialog`。</span><span class="sxs-lookup"><span data-stu-id="4d901-128">We will use jQuery to hook up our **Add Genre** dialog box with the ID `genreDialog` in this div.</span></span> <span data-ttu-id="4d901-129">最後兩個腳本標記包含將用來執行 [加入新的類型] 功能的 JavaScript 檔案連結。</span><span class="sxs-lookup"><span data-stu-id="4d901-129">The last two script tags contain links to the JavaScript files we will use to implement the add new genre feature.</span></span> <span data-ttu-id="4d901-130">在專案中為您提供 */Scripts/chooseGenre.js*檔案，我們將在稍後的教學課程中加以檢查。</span><span class="sxs-lookup"><span data-stu-id="4d901-130">The */Scripts/chooseGenre.js* file is provided for you in the project, we will examine it later in the tutorial.</span></span>

<span data-ttu-id="4d901-131">執行應用程式，然後按一下 [**加入新**的內容類型] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4d901-131">Run the application and click on the **Add New Genre** button.</span></span> <span data-ttu-id="4d901-132">在 [**新增**內容類型] 對話方塊的 [**名稱**] 輸入方塊中，輸入**Opera** 。</span><span class="sxs-lookup"><span data-stu-id="4d901-132">In the **Add Genre** dialog box, enter **Opera** in the **Name** input box.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

<span data-ttu-id="4d901-133">按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4d901-133">Click the **Save** button.</span></span> <span data-ttu-id="4d901-134">AJAX 呼叫會建立 Opera 分類，然後在下拉式清單中填入 Opera，並將 Opera 設定為選取的類型。</span><span class="sxs-lookup"><span data-stu-id="4d901-134">An AJAX call creates the Opera category and then populates the dropdown list with Opera, and sets Opera as the selected genre.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

<span data-ttu-id="4d901-135">輸入 [演出者]、[標題] 和 [價格]，然後選取 [**建立**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4d901-135">Enter an artist, title and price, then select the **Create** button.</span></span> <span data-ttu-id="4d901-136">如果您輸入的價格小於 $8.99，新的專輯會出現在索引視圖的頂端。</span><span class="sxs-lookup"><span data-stu-id="4d901-136">If you enter a price less than $8.99, the new album will appear at the top of the Index view.</span></span> <span data-ttu-id="4d901-137">確認新的專輯專案已儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="4d901-137">Verify the new album entry was saved in the database.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

<span data-ttu-id="4d901-138">嘗試建立只有一個字母的新內容類型。</span><span class="sxs-lookup"><span data-stu-id="4d901-138">Try creating a new genre with only one letter.</span></span> <span data-ttu-id="4d901-139">*Models\Genre.cs*檔案中的下列程式碼會設定內容類型名稱的最小和最大長度。</span><span class="sxs-lookup"><span data-stu-id="4d901-139">The following code in the *Models\Genre.cs* file sets the minimum and maximum length of the genre name.</span></span>

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

<span data-ttu-id="4d901-140">用戶端驗證報告您必須輸入介於2到20個字元之間的字串。</span><span class="sxs-lookup"><span data-stu-id="4d901-140">Client side validation reports you must enter a string between 2 and 20 characters.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a><span data-ttu-id="4d901-141">檢查新的內容類型如何加入至資料庫和選取清單中。</span><span class="sxs-lookup"><span data-stu-id="4d901-141">Examining How a New Genre is Added to the Database and the Select List.</span></span>

<span data-ttu-id="4d901-142">開啟*Scripts\chooseGenre.js*檔案，並檢查程式碼。</span><span class="sxs-lookup"><span data-stu-id="4d901-142">Open the *Scripts\chooseGenre.js* file and examine the code.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

<span data-ttu-id="4d901-143">第二行使用識別碼 `genreDialog`，在*Views\StoreManager\\_ChooseGenre. cshtml*檔案中的 div 標記上建立對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4d901-143">The second line uses the ID `genreDialog` to create a dialog box on the div tag in the *Views\StoreManager\\_ChooseGenre.cshtml* file.</span></span> <span data-ttu-id="4d901-144">大部分的具名引數都一目了然。</span><span class="sxs-lookup"><span data-stu-id="4d901-144">Most of the named parameters are self explanatory.</span></span> <span data-ttu-id="4d901-145">`autoOpen` 參數設定為 false，選取 [**建立**內容類型] 按鈕將會明確開啟對話（這在中是後面的說明）。</span><span class="sxs-lookup"><span data-stu-id="4d901-145">The `autoOpen` parameter is set to false, selecting the **Create Genre** button will open the dialogue explicitly (this is described latter on).</span></span> <span data-ttu-id="4d901-146">對話方塊有兩個按鈕： [**儲存**] 和 [**取消**]。</span><span class="sxs-lookup"><span data-stu-id="4d901-146">The dialog has two buttons, **Save** and **Cancel**.</span></span> <span data-ttu-id="4d901-147">[**取消**] 按鈕會關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4d901-147">The **Cancel** button closes the dialog.</span></span> <span data-ttu-id="4d901-148">下列程式碼顯示 [**儲存**] 按鈕功能。</span><span class="sxs-lookup"><span data-stu-id="4d901-148">The following code shows the **Save** button function.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

<span data-ttu-id="4d901-149">`var createGenreForm` 是從 `createGenreForm` 識別碼中選取的。</span><span class="sxs-lookup"><span data-stu-id="4d901-149">The `var createGenreForm` is selected from the `createGenreForm` ID.</span></span> <span data-ttu-id="4d901-150">`createGenreForm` 識別碼是在*Views\Genre\\_CreateGenre. cshtml*檔案中找到的下列程式碼中設定。</span><span class="sxs-lookup"><span data-stu-id="4d901-150">The `createGenreForm` ID was set in the following code found in the *Views\Genre\\_CreateGenre.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

<span data-ttu-id="4d901-151">*Views\Genre _CreateGenre\\* 中使用的[html.beginform](https://msdn.microsoft.com/library/dd492714.aspx) helper 多載會產生 html，其中包含含有要提交表單之 URL 的 action 屬性。</span><span class="sxs-lookup"><span data-stu-id="4d901-151">The [Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) helper overload used in the *Views\Genre\\_CreateGenre.cshtml* file generates HTML with an action attribute containing the URL to submit the form.</span></span> <span data-ttu-id="4d901-152">您可以透過在瀏覽器中顯示 [建立專輯] 頁面，然後在瀏覽器中選取 [顯示來源]，來查看這項功能。</span><span class="sxs-lookup"><span data-stu-id="4d901-152">You can see this by displaying the create album page in a browser and selecting show source in the browser.</span></span> <span data-ttu-id="4d901-153">下列標記顯示產生的 HTML，其中包含表單標記。</span><span class="sxs-lookup"><span data-stu-id="4d901-153">The following markup shows the generated HTML containing the form tag.</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

<span data-ttu-id="4d901-154">JQuery `$.post` 行會對 action 屬性（`/StoreManager/Create`）進行 AJAX 呼叫，並傳入 [**建立**內容類型] 對話方塊中的資料。</span><span class="sxs-lookup"><span data-stu-id="4d901-154">The jQuery `$.post` line makes an AJAX call to the action attribute (`/StoreManager/Create`) and passes in the data from the **Create Genre** dialog box.</span></span> <span data-ttu-id="4d901-155">資料包含新內容類型的名稱和選擇性的描述。</span><span class="sxs-lookup"><span data-stu-id="4d901-155">The data consists of the name for the new genre and an optional description.</span></span> <span data-ttu-id="4d901-156">如果 AJAX 呼叫成功，新的內容類型名稱和值會加入至選取標記，而新的內容類型會設定為選取的值。</span><span class="sxs-lookup"><span data-stu-id="4d901-156">If the AJAX call is successful, the new genre name and value are added to the Select markup, and the new genre is set to the selected value.</span></span> <span data-ttu-id="4d901-157">因為這是動態產生的標記，所以您無法在瀏覽器中查看來源來看到新的 [選取] 選項。</span><span class="sxs-lookup"><span data-stu-id="4d901-157">Because this is dynamically generated markup, you can't see the new select option by viewing the source in the browser.</span></span> <span data-ttu-id="4d901-158">您可以使用 IE 9 F12 開發人員工具來查看新的 HTML。</span><span class="sxs-lookup"><span data-stu-id="4d901-158">You can see the new HTML with the IE 9 F12 developer tools.</span></span> <span data-ttu-id="4d901-159">若要在 Internet Explorer 9 中查看新的 [選取] 選項，請按 F12 鍵以啟動 F12 開發人員工具。</span><span class="sxs-lookup"><span data-stu-id="4d901-159">To view the new select option, in Internet Explorer 9, hit the F12 key to start the F12 developer tools.</span></span> <span data-ttu-id="4d901-160">流覽至 [建立] 頁面並加入新的內容類型，以便在 [內容類型] 選取清單中選取新的內容類型。</span><span class="sxs-lookup"><span data-stu-id="4d901-160">Navigate to the Create page and add a new genre so the new genre is selected in the genre select list.</span></span> <span data-ttu-id="4d901-161">在 F12 開發人員工具中：</span><span class="sxs-lookup"><span data-stu-id="4d901-161">In the F12 developer tools:</span></span>

1. <span data-ttu-id="4d901-162">選取 [HTML] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4d901-162">Select the HTML tab.</span></span>
2. <span data-ttu-id="4d901-163">按 [重新整理] 圖示。</span><span class="sxs-lookup"><span data-stu-id="4d901-163">Hit the refresh icon.</span></span>  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. <span data-ttu-id="4d901-164">在搜尋方塊中，輸入 GenreID。</span><span class="sxs-lookup"><span data-stu-id="4d901-164">In the search box, enter GenreID.</span></span>
4. <span data-ttu-id="4d901-165">使用下一個圖示，</span><span class="sxs-lookup"><span data-stu-id="4d901-165">Using the next icon,</span></span>   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   <span data-ttu-id="4d901-166">流覽至下列選取標記：</span><span class="sxs-lookup"><span data-stu-id="4d901-166">navigate to the following select tag:</span></span>

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. <span data-ttu-id="4d901-167">展開最後一個選項值。</span><span class="sxs-lookup"><span data-stu-id="4d901-167">Expand the last option value.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

<span data-ttu-id="4d901-168">*Scripts\chooseGenre.js*檔案中的下列程式碼顯示如何將 [**加入新**的內容類型] 按鈕連接到 click 事件，以及如何建立 [**加入新**的內容類型] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4d901-168">The following code in the *Scripts\chooseGenre.js* file shows the how the **Add New Genre** button gets connected to the click event, and how the **Add New Genre** dialog box is created.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

<span data-ttu-id="4d901-169">第一行會建立附加至 [**加入新**的內容類型] 按鈕的 click 函式。</span><span class="sxs-lookup"><span data-stu-id="4d901-169">The first line creates a click function attached to the **Add New Genre** button.</span></span> <span data-ttu-id="4d901-170">Views\StoreManager\\中的下列標記 _ChooseGenre. cshtml 檔案顯示如何建立 [**加入新**的內容類型] 按鈕：</span><span class="sxs-lookup"><span data-stu-id="4d901-170">The following markup from the Views\StoreManager\\_ChooseGenre.cshtml file shows how the **Add New Genre** button is created:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

<span data-ttu-id="4d901-171">Load 方法會建立並開啟 [加入內容類型] 對話方塊，並呼叫 jQuery `parse` 方法，以便在對話方塊中輸入的資料上進行用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="4d901-171">The load method creates and opens the Add Genre dialog and calls the jQuery `parse` method so client validation occurs on data entered in the dialog.</span></span>

<span data-ttu-id="4d901-172">在本節中，您已瞭解如何建立可用於將新的類別資料加入至選取清單的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4d901-172">In this section you have learned how to create a dialog that can be used to add new category data to a select list.</span></span> <span data-ttu-id="4d901-173">您可以遵循相同的程式來建立 UI，將新的演出者新增至 [演出者] 選取清單。</span><span class="sxs-lookup"><span data-stu-id="4d901-173">You can follow the same procedure to create UI to add a new artist to the artist select list.</span></span> <span data-ttu-id="4d901-174">本教學課程提供使用 ASP.NET MVC HTML helper **DropDownList**的總覽。</span><span class="sxs-lookup"><span data-stu-id="4d901-174">This tutorial has given an overview of working with the ASP.NET MVC HTML helper **DropDownList**.</span></span> <span data-ttu-id="4d901-175">如需有關使用**DropDownList**的詳細資訊，請參閱下面的加法參考一節。</span><span class="sxs-lookup"><span data-stu-id="4d901-175">For additional information on working with the **DropDownList**, see the addition references section below.</span></span> <span data-ttu-id="4d901-176">如果本教學課程有説明，請讓我們知道。</span><span class="sxs-lookup"><span data-stu-id="4d901-176">Please let us know if this tutorial has been helpful.</span></span>

<span data-ttu-id="4d901-177">Rick. Anderson [at] Microsoft .com</span><span class="sxs-lookup"><span data-stu-id="4d901-177">Rick.Anderson[at]Microsoft.com</span></span>

### <a name="additional-references"></a><span data-ttu-id="4d901-178">其他參考</span><span class="sxs-lookup"><span data-stu-id="4d901-178">Additional References</span></span>

- <span data-ttu-id="4d901-179">[ASP.NET MVC –](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)的階層式下拉式清單教學課程</span><span class="sxs-lookup"><span data-stu-id="4d901-179">[ASP.NET MVC–Cascading Dropdown Lists Tutorial](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) by [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span></span>
- <span data-ttu-id="4d901-180">已[選擇](https://harvesthq.github.com/chosen/)支援多重選取和篩選的 JavaScript 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="4d901-180">[Chosen](https://harvesthq.github.com/chosen/) A JavaScript plugin that support multi-select and filtering.</span></span>

### <a name="contributors"></a><span data-ttu-id="4d901-181">參與者</span><span class="sxs-lookup"><span data-stu-id="4d901-181">Contributors</span></span>

- [<span data-ttu-id="4d901-182">Radu Enuca</span><span class="sxs-lookup"><span data-stu-id="4d901-182">Radu Enuca</span></span>](https://weblogs.asp.net/raduenuca/default.aspx)
- <span data-ttu-id="4d901-183">Jean-Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="4d901-183">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="4d901-184">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="4d901-184">Brad Wilson</span></span>](http://bradwilson.typepad.com/)

### <a name="reviewers"></a><span data-ttu-id="4d901-185">檢閱者</span><span class="sxs-lookup"><span data-stu-id="4d901-185">Reviewers</span></span>

- <span data-ttu-id="4d901-186">Jean-Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="4d901-186">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="4d901-187">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="4d901-187">Brad Wilson</span></span>](http://bradwilson.typepad.com/)
- <span data-ttu-id="4d901-188">Mike Pope</span><span class="sxs-lookup"><span data-stu-id="4d901-188">Mike Pope</span></span>
- <span data-ttu-id="4d901-189">Tom 作者: dykstra</span><span class="sxs-lookup"><span data-stu-id="4d901-189">Tom Dykstra</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4d901-190">[[上一步]](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)</span><span class="sxs-lookup"><span data-stu-id="4d901-190">[Previous](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)</span></span>
