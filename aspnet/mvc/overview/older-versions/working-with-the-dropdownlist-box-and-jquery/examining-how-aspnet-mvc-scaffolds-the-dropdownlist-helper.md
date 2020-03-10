---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: 檢查 ASP.NET MVC 如何 scaffold DropDownList Helper |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 275b20ad964b3e8ddc272a7448f0740ed0891eff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614902"
---
# <a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a><span data-ttu-id="67a45-102">檢查 ASP.NET MVC 如何 Scaffold DropDownList 協助程式</span><span class="sxs-lookup"><span data-stu-id="67a45-102">Examining  how  ASP.NET MVC scaffolds the DropDownList Helper</span></span>

<span data-ttu-id="67a45-103">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="67a45-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="67a45-104">在**方案總管**中，以滑鼠右鍵按一下 [*控制器*] 資料夾，然後選取 [**新增控制器**]。</span><span class="sxs-lookup"><span data-stu-id="67a45-104">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span> <span data-ttu-id="67a45-105">將控制器命名為**StoreManagerController**。</span><span class="sxs-lookup"><span data-stu-id="67a45-105">Name the controller **StoreManagerController**.</span></span> <span data-ttu-id="67a45-106">設定 [**新增控制器**] 對話方塊的選項，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="67a45-106">Set the options for the **Add Controller** dialog as shown in the image below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

<span data-ttu-id="67a45-107">編輯 [ *StoreManager\Index.cshtml* ] 視圖，並移除 `AlbumArtUrl`。</span><span class="sxs-lookup"><span data-stu-id="67a45-107">Edit the *StoreManager\Index.cshtml* view and remove `AlbumArtUrl`.</span></span> <span data-ttu-id="67a45-108">移除 `AlbumArtUrl` 會使簡報更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="67a45-108">Removing `AlbumArtUrl` will make the presentation more readable.</span></span> <span data-ttu-id="67a45-109">已完成的程式碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="67a45-109">The completed code is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

<span data-ttu-id="67a45-110">開啟*Controllers\StoreManagerController.cs*檔案，並尋找 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="67a45-110">Open the *Controllers\StoreManagerController.cs* file and find the `Index` method.</span></span> <span data-ttu-id="67a45-111">新增 `OrderBy` 子句，讓專輯依價格排序。</span><span class="sxs-lookup"><span data-stu-id="67a45-111">Add the `OrderBy` clause so the albums will be sorted by price.</span></span> <span data-ttu-id="67a45-112">完整的程式碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="67a45-112">The complete code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

<span data-ttu-id="67a45-113">依價格排序可讓您更輕鬆地測試資料庫的變更。</span><span class="sxs-lookup"><span data-stu-id="67a45-113">Sorting by price will make it easier to test changes to the database.</span></span> <span data-ttu-id="67a45-114">當您測試編輯和建立方法時，您可以使用低價，讓儲存的資料先出現。</span><span class="sxs-lookup"><span data-stu-id="67a45-114">When you are testing the edit and create methods, you can use a low price so the saved data will appear first.</span></span>

<span data-ttu-id="67a45-115">開啟*StoreManager\Edit.cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="67a45-115">Open the *StoreManager\Edit.cshtml* file.</span></span> <span data-ttu-id="67a45-116">在圖例標記之後加入下面這一行。</span><span class="sxs-lookup"><span data-stu-id="67a45-116">Add the following line just after the legend tag.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

<span data-ttu-id="67a45-117">下列程式碼顯示這項變更的內容：</span><span class="sxs-lookup"><span data-stu-id="67a45-117">The following code shows the context of this change:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

<span data-ttu-id="67a45-118">需要 `AlbumId` 才能對專輯記錄進行變更。</span><span class="sxs-lookup"><span data-stu-id="67a45-118">The `AlbumId` is required to make changes to an album record.</span></span>

<span data-ttu-id="67a45-119">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="67a45-119">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="67a45-120">選取 [系統**管理員**] 連結，然後選取 [**建立新**的] 連結以建立新的專輯。</span><span class="sxs-lookup"><span data-stu-id="67a45-120">Select to the **Admin** link, then select the **Create New** link to create a new album.</span></span> <span data-ttu-id="67a45-121">確認已儲存專輯資訊。</span><span class="sxs-lookup"><span data-stu-id="67a45-121">Verify the album information was saved.</span></span> <span data-ttu-id="67a45-122">編輯專輯並確認您所做的變更已保存。</span><span class="sxs-lookup"><span data-stu-id="67a45-122">Edit an album and verify the changes you made are persisted.</span></span>

### <a name="the-album-schema"></a><span data-ttu-id="67a45-123">專輯架構</span><span class="sxs-lookup"><span data-stu-id="67a45-123">The Album Schema</span></span>

<span data-ttu-id="67a45-124">MVC 樣板機制所建立的 `StoreManager` 控制器，可以讓 CRUD （建立、讀取、更新、刪除）存取音樂存放區資料庫中的專輯。</span><span class="sxs-lookup"><span data-stu-id="67a45-124">The `StoreManager` controller created by the MVC scaffolding mechanism allows CRUD (Create, Read, Update, Delete) access to the albums in the music store database.</span></span> <span data-ttu-id="67a45-125">專輯資訊的架構如下所示：</span><span class="sxs-lookup"><span data-stu-id="67a45-125">The schema for album information is shown below:</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

<span data-ttu-id="67a45-126">`Albums` 資料表不會儲存專輯內容類型和描述，它會儲存 `Genres` 資料表的外鍵。</span><span class="sxs-lookup"><span data-stu-id="67a45-126">The `Albums` table does not store the album genre and description, it stores a foreign key to the `Genres` table.</span></span> <span data-ttu-id="67a45-127">`Genres` 資料表包含內容類型名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="67a45-127">The `Genres` table contains the genre name and description.</span></span> <span data-ttu-id="67a45-128">同樣地，`Albums` 資料表不會包含專輯演出者名稱，而是 `Artists` 資料表的外鍵。</span><span class="sxs-lookup"><span data-stu-id="67a45-128">Likewise, the `Albums` table doesn't contain the album artists name, but a foreign key to the `Artists` table.</span></span> <span data-ttu-id="67a45-129">`Artists` 資料表包含演出者的名稱。</span><span class="sxs-lookup"><span data-stu-id="67a45-129">The `Artists` table contains the artist's name.</span></span> <span data-ttu-id="67a45-130">如果您檢查 `Albums` 資料表中的資料，您可以看到每個資料列都包含 `Genres` 資料表的外鍵，以及 `Artists` 資料表的外鍵。</span><span class="sxs-lookup"><span data-stu-id="67a45-130">If you examine the data in the `Albums` table, you can see each row contains a foreign key to the `Genres` table and a foreign key to the `Artists` table.</span></span> <span data-ttu-id="67a45-131">下圖顯示 `Albums` 資料表中的一些資料表資料。</span><span class="sxs-lookup"><span data-stu-id="67a45-131">The image below show some table data from the `Albums` table.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a><span data-ttu-id="67a45-132">HTML 選取標記</span><span class="sxs-lookup"><span data-stu-id="67a45-132">The HTML Select Tag</span></span>

<span data-ttu-id="67a45-133">HTML `<select>` 專案（由 HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) helper 建立）用來顯示完整的值清單（例如內容清單）。</span><span class="sxs-lookup"><span data-stu-id="67a45-133">The HTML `<select>` element (created by the HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) helper) is used to display a complete list of values (such as the list of genres).</span></span> <span data-ttu-id="67a45-134">針對 [編輯表單]，當目前的值為已知時，選取清單可以顯示目前的值。</span><span class="sxs-lookup"><span data-stu-id="67a45-134">For edit forms, when the current value is known, the select list can display the current value.</span></span> <span data-ttu-id="67a45-135">我們先前在將選取的值設定為**喜劇**時看到這種情況。</span><span class="sxs-lookup"><span data-stu-id="67a45-135">We saw this previously when we set the selected value to **Comedy**.</span></span> <span data-ttu-id="67a45-136">選取清單非常適合用來顯示類別或外鍵資料。</span><span class="sxs-lookup"><span data-stu-id="67a45-136">The select list is ideal for displaying category or foreign key data.</span></span> <span data-ttu-id="67a45-137">[類型] 外鍵的 [`<select>`] 專案會顯示可能的內容類型名稱清單，但當您儲存表單時，[內容類型] 屬性會更新為 [內容類型] 外鍵值，而不是顯示的類型名稱。</span><span class="sxs-lookup"><span data-stu-id="67a45-137">The `<select>` element for the Genre foreign key displays the list of possible genre names, but when you save the form the Genre property is updated with the Genre foreign key value, not the displayed genre name.</span></span> <span data-ttu-id="67a45-138">在下圖中，選取的內容類型是**Disco** ，而演出者是**Donna 夏季**。</span><span class="sxs-lookup"><span data-stu-id="67a45-138">In the image below, the genre selected is **Disco** and the artist is **Donna Summer**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a><span data-ttu-id="67a45-139">檢查 ASP.NET MVC Scaffold 程式碼</span><span class="sxs-lookup"><span data-stu-id="67a45-139">Examining the ASP.NET MVC Scaffolded Code</span></span>

<span data-ttu-id="67a45-140">開啟*Controllers\StoreManagerController.cs*檔案，並尋找 `HTTP GET Create` 方法。</span><span class="sxs-lookup"><span data-stu-id="67a45-140">Open the *Controllers\StoreManagerController.cs* file and find the `HTTP GET Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

<span data-ttu-id="67a45-141">`Create` 方法會在 `ViewBag`中加入兩個[SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx)物件，一個包含內容類型資訊，另一個則包含演出者資訊。</span><span class="sxs-lookup"><span data-stu-id="67a45-141">The `Create` method adds two [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) objects to the `ViewBag`, one to contain the genre information, and one to contain the artist information.</span></span> <span data-ttu-id="67a45-142">上述使用的[SelectList](https://msdn.microsoft.com/library/dd505286.aspx)函式多載會採用三個引數：</span><span class="sxs-lookup"><span data-stu-id="67a45-142">The [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) constructor overload used above takes three arguments:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. <span data-ttu-id="67a45-143">*items*： [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) ，其中包含清單中的專案。</span><span class="sxs-lookup"><span data-stu-id="67a45-143">*items*: An [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) containing the items in the list.</span></span> <span data-ttu-id="67a45-144">在上述範例中，`db.Genres`傳回的內容清單。</span><span class="sxs-lookup"><span data-stu-id="67a45-144">In the example above, the list of genres returned by `db.Genres`.</span></span>
2. <span data-ttu-id="67a45-145">*dataValueField*： **IEnumerable**清單中包含金鑰值的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="67a45-145">*dataValueField*: The name of the property in the **IEnumerable** list that contains the key value.</span></span> <span data-ttu-id="67a45-146">在上述範例中，`GenreId` 和 `ArtistId`。</span><span class="sxs-lookup"><span data-stu-id="67a45-146">In the example above, `GenreId` and `ArtistId`.</span></span>
3. <span data-ttu-id="67a45-147">*dataTextField*： **IEnumerable**清單中包含要顯示之資訊的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="67a45-147">*dataTextField*: The name of the property in the **IEnumerable** list that contains the information to display.</span></span> <span data-ttu-id="67a45-148">在 [演出者] 和 [內容類型] 資料表中，都會使用 [`name`] 欄位。</span><span class="sxs-lookup"><span data-stu-id="67a45-148">In both the artists and genre table, the `name` field is used.</span></span>

<span data-ttu-id="67a45-149">開啟*Views\StoreManager\Create.cshtml*檔案，並檢查 [內容類型] 欄位的 [`Html.DropDownList` helper 標記]。</span><span class="sxs-lookup"><span data-stu-id="67a45-149">Open the *Views\StoreManager\Create.cshtml* file and examine the `Html.DropDownList` helper markup for the genre field.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

<span data-ttu-id="67a45-150">第一行顯示建立視圖會採用 `Album` 模型。</span><span class="sxs-lookup"><span data-stu-id="67a45-150">The first line shows that the create view takes an `Album` model.</span></span> <span data-ttu-id="67a45-151">在上面顯示的 `Create` 方法中，未傳遞任何模型，因此此視圖會取得**null** `Album` 模型。</span><span class="sxs-lookup"><span data-stu-id="67a45-151">In the `Create` method shown above, no model was passed, so the view gets a **null** `Album` model.</span></span> <span data-ttu-id="67a45-152">此時，我們會建立新的專輯，所以沒有任何 `Album` 資料。</span><span class="sxs-lookup"><span data-stu-id="67a45-152">At this point we are creating a new album so we don't have any `Album` data for it.</span></span>

<span data-ttu-id="67a45-153">上面顯示的[DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)多載會採用欄位的名稱來系結至模型。</span><span class="sxs-lookup"><span data-stu-id="67a45-153">The [Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) overload shown above takes the name of the field to bind to the model.</span></span> <span data-ttu-id="67a45-154">它也會使用此名稱來尋找包含[SelectList](https://msdn.microsoft.com/library/dd505286.aspx)物件的**ViewBag**物件。</span><span class="sxs-lookup"><span data-stu-id="67a45-154">It also uses this name to look for a **ViewBag** object containing a [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) object.</span></span> <span data-ttu-id="67a45-155">使用此多載時，您必須將**ViewBag SelectList**物件命名為 `GenreId`。</span><span class="sxs-lookup"><span data-stu-id="67a45-155">Using this overload, you are required to name the **ViewBag SelectList** object `GenreId`.</span></span> <span data-ttu-id="67a45-156">第二個參數（`String.Empty`）是未選取任何專案時所要顯示的文字。</span><span class="sxs-lookup"><span data-stu-id="67a45-156">The second parameter (`String.Empty`) is the text to display when no item is selected.</span></span> <span data-ttu-id="67a45-157">這正是我們在建立新專輯時所要做的。</span><span class="sxs-lookup"><span data-stu-id="67a45-157">This is exactly what we want when creating a new album.</span></span> <span data-ttu-id="67a45-158">如果您移除了第二個參數，並使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="67a45-158">If you removed the second parameter and used the following code:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

<span data-ttu-id="67a45-159">選取清單會預設為第一個元素，或在我們的範例中為 [岩石]。</span><span class="sxs-lookup"><span data-stu-id="67a45-159">The select list would default to the first element, or Rock in our sample.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

<span data-ttu-id="67a45-160">檢查 `HTTP POST Create` 方法。</span><span class="sxs-lookup"><span data-stu-id="67a45-160">Examining the `HTTP POST Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

<span data-ttu-id="67a45-161">`Create` 方法的這個多載會採用由 ASP.NET MVC 模型系結系統從張貼的表單值所建立的 `album` 物件。</span><span class="sxs-lookup"><span data-stu-id="67a45-161">This overload of the `Create` method takes an `album` object, created by the ASP.NET MVC model binding system from the form values posted.</span></span> <span data-ttu-id="67a45-162">當您提交新的專輯時，如果模型狀態是有效的，而且沒有資料庫錯誤，則會將新的專輯新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="67a45-162">When you submit a new album, if model state is valid and there are no database errors, the new album is added the database.</span></span> <span data-ttu-id="67a45-163">下圖顯示新專輯的建立。</span><span class="sxs-lookup"><span data-stu-id="67a45-163">The following image shows the creation of a new album.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

<span data-ttu-id="67a45-164">您可以使用[fiddler 工具](http://www.fiddler2.com/fiddler2/)來檢查 ASP.NET MVC 模型系結用來建立專輯物件的已張貼表單值。</span><span class="sxs-lookup"><span data-stu-id="67a45-164">You can use the [fiddler tool](http://www.fiddler2.com/fiddler2/) to examine the posted form values that ASP.NET MVC model binding uses to create the album object.</span></span>

<span data-ttu-id="67a45-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="67a45-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).</span></span>

### <a name="refactoring-the-viewbag-selectlist-creation"></a><span data-ttu-id="67a45-166">重構 ViewBag SelectList 建立</span><span class="sxs-lookup"><span data-stu-id="67a45-166">Refactoring the ViewBag SelectList Creation</span></span>

<span data-ttu-id="67a45-167">`Edit` 方法和 `HTTP POST Create` 方法都有相同的程式碼，可在**ViewBag**中設定**SelectList** 。</span><span class="sxs-lookup"><span data-stu-id="67a45-167">Both the `Edit` methods and the `HTTP POST Create` method have identical code to set up the **SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="67a45-168">在[試](http://en.wikipedia.org/wiki/Don't_repeat_yourself)的精神中，我們會重構這段程式碼。</span><span class="sxs-lookup"><span data-stu-id="67a45-168">In the spirit of [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself), we will refactor this code.</span></span> <span data-ttu-id="67a45-169">我們稍後會使用此重構的程式碼。</span><span class="sxs-lookup"><span data-stu-id="67a45-169">We'll make use of this refactored code later.</span></span>

<span data-ttu-id="67a45-170">建立新的方法，將內容類型和演出者**SelectList**新增至**ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="67a45-170">Create a new method to add a genre and artist **SelectList** to the **ViewBag**.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

<span data-ttu-id="67a45-171">以 `SetGenreArtistViewBag` 方法的呼叫，取代兩行設定每個 `Create` 中的 `ViewBag` 和 `Edit` 方法。</span><span class="sxs-lookup"><span data-stu-id="67a45-171">Replace the two lines setting the `ViewBag` in each of the `Create` and `Edit` methods with a call to the `SetGenreArtistViewBag` method.</span></span> <span data-ttu-id="67a45-172">已完成的程式碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="67a45-172">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

<span data-ttu-id="67a45-173">建立新的專輯並編輯專輯，以確認變更可正常執行。</span><span class="sxs-lookup"><span data-stu-id="67a45-173">Create a new album and edit an album to verify the changes work.</span></span>

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a><span data-ttu-id="67a45-174">將 SelectList 明確地傳遞至 DropDownList</span><span class="sxs-lookup"><span data-stu-id="67a45-174">Explicitly Passing the SelectList to the DropDownList</span></span>

<span data-ttu-id="67a45-175">ASP.NET MVC 樣板所建立的建立和編輯檢視會使用下列**DropDownList**多載：</span><span class="sxs-lookup"><span data-stu-id="67a45-175">The create and edit views created by the ASP.NET MVC scaffolding use the following **DropDownList** overload:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

<span data-ttu-id="67a45-176">[建立] 視圖的 `DropDownList` 標記如下所示。</span><span class="sxs-lookup"><span data-stu-id="67a45-176">The `DropDownList` markup for the create view is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

<span data-ttu-id="67a45-177">因為 `SelectList` 的 `ViewBag` 屬性會命名為 `GenreId`，所以**DropDownList** helper 會使用**ViewBag**中的 `GenreId`**SelectList** 。</span><span class="sxs-lookup"><span data-stu-id="67a45-177">Because the `ViewBag` property for the `SelectList` is named `GenreId`, the **DropDownList** helper will use the `GenreId`**SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="67a45-178">在下列**DropDownList**多載中，會明確傳入 `SelectList`。</span><span class="sxs-lookup"><span data-stu-id="67a45-178">In the following **DropDownList** overload, the `SelectList` is explicitly passed in.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

<span data-ttu-id="67a45-179">開啟*Views\StoreManager\Edit.cshtml*檔案，並使用上述多載，將**DropDownList**呼叫變更為明確傳入**SelectList**。</span><span class="sxs-lookup"><span data-stu-id="67a45-179">Open the *Views\StoreManager\Edit.cshtml* file, and change the **DropDownList** call to explicitly pass in the **SelectList**, using the overload above.</span></span> <span data-ttu-id="67a45-180">針對 [內容類型] 類別執行此動作。</span><span class="sxs-lookup"><span data-stu-id="67a45-180">Do this for the Genre category.</span></span> <span data-ttu-id="67a45-181">完成的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="67a45-181">The completed code is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

<span data-ttu-id="67a45-182">執行應用程式並按一下 [系統**管理**] 連結，然後流覽至 [爵士樂] 專輯並選取 [**編輯**] 連結。</span><span class="sxs-lookup"><span data-stu-id="67a45-182">Run the application and click the **Admin** link, then navigate to a Jazz album and select the **Edit** link.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

<span data-ttu-id="67a45-183">並不會顯示 [爵士樂] 做為目前選取的內容類型，而是顯示 [岩石]。</span><span class="sxs-lookup"><span data-stu-id="67a45-183">Instead of showing Jazz as the currently selected genre, Rock is displayed.</span></span> <span data-ttu-id="67a45-184">當字串引數（要系結的屬性）和**SelectList**物件具有相同的名稱時，不會使用選取的值。</span><span class="sxs-lookup"><span data-stu-id="67a45-184">When the string argument (the property to bind) and the **SelectList** object have the same name, the selected value is not used.</span></span> <span data-ttu-id="67a45-185">未提供任何選取的值時，瀏覽器會預設為**SelectList**中的第一個元素（在上述範例中為「**岩石**」）。</span><span class="sxs-lookup"><span data-stu-id="67a45-185">When there is no selected value provided, browsers default to the first element in the **SelectList**(which is **Rock** in the example above).</span></span> <span data-ttu-id="67a45-186">這是**DropDownList** helper 的已知限制。</span><span class="sxs-lookup"><span data-stu-id="67a45-186">This is a known limitation of the **DropDownList** helper.</span></span>

<span data-ttu-id="67a45-187">開啟*Controllers\StoreManagerController.cs*檔案，並將**SelectList**物件名稱變更為 `Genres` 和 `Artists`。</span><span class="sxs-lookup"><span data-stu-id="67a45-187">Open the *Controllers\StoreManagerController.cs* file and change the **SelectList** object names to `Genres` and `Artists`.</span></span> <span data-ttu-id="67a45-188">完成的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="67a45-188">The completed code is shown below:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

<span data-ttu-id="67a45-189">[名稱] 和 [演出者] 是較好的類別名稱，因為它們包含的不只是每個類別目錄的識別碼。</span><span class="sxs-lookup"><span data-stu-id="67a45-189">The names Genres and Artists are better names for the categories, as they contain more than just the ID of each category.</span></span> <span data-ttu-id="67a45-190">我們先前已付費的重構。</span><span class="sxs-lookup"><span data-stu-id="67a45-190">The refactoring we did earlier paid off.</span></span> <span data-ttu-id="67a45-191">我們的變更會與 `SetGenreArtistViewBag` 方法隔離，而不是變更四種方法中的**ViewBag** 。</span><span class="sxs-lookup"><span data-stu-id="67a45-191">Instead of changing the **ViewBag** in four methods, our changes were isolated to the `SetGenreArtistViewBag` method.</span></span>

<span data-ttu-id="67a45-192">變更 [建立] 和 [編輯] 視圖中的**DropDownList**呼叫，以使用新的**SelectList**名稱。</span><span class="sxs-lookup"><span data-stu-id="67a45-192">Change the **DropDownList** call in the create and edit views to use the new **SelectList** names.</span></span> <span data-ttu-id="67a45-193">編輯檢視的新標記如下所示：</span><span class="sxs-lookup"><span data-stu-id="67a45-193">The new markup for the edit view is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

<span data-ttu-id="67a45-194">建立視圖需要空字串，以防止顯示 SelectList 中的第一個專案。</span><span class="sxs-lookup"><span data-stu-id="67a45-194">The Create view requires an empty string to prevent the first item in the SelectList from being displayed.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

<span data-ttu-id="67a45-195">建立新的專輯並編輯專輯，以確認變更可正常執行。</span><span class="sxs-lookup"><span data-stu-id="67a45-195">Create a new album and edit an album to verify the changes work.</span></span> <span data-ttu-id="67a45-196">選取具有 [岩石] 以外類型的專輯來測試編輯程式碼。</span><span class="sxs-lookup"><span data-stu-id="67a45-196">Test the edit code by selecting an album with a genre other than Rock.</span></span>

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a><span data-ttu-id="67a45-197">搭配 DropDownList Helper 使用視圖模型</span><span class="sxs-lookup"><span data-stu-id="67a45-197">Using a View Model with the DropDownList Helper</span></span>

<span data-ttu-id="67a45-198">在 Viewmodel 資料夾中建立名為 `AlbumSelectListViewModel`的新類別。</span><span class="sxs-lookup"><span data-stu-id="67a45-198">Create a new class in the ViewModels folder named `AlbumSelectListViewModel`.</span></span> <span data-ttu-id="67a45-199">將 `AlbumSelectListViewModel` 類別中的程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="67a45-199">Replace the code in the `AlbumSelectListViewModel` class with the following:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

<span data-ttu-id="67a45-200">`AlbumSelectListViewModel` 的函式會採用專輯、演出者和內容的清單，並建立包含專輯的物件和內容組和演出者的 `SelectList`。</span><span class="sxs-lookup"><span data-stu-id="67a45-200">The `AlbumSelectListViewModel` constructor takes an album, a list of artists and genres and creates an object containing the album and a `SelectList` for genres and artists.</span></span>

<span data-ttu-id="67a45-201">建立專案，以便在下一個步驟中建立視圖時，可以使用 `AlbumSelectListViewModel`。</span><span class="sxs-lookup"><span data-stu-id="67a45-201">Build the project so the `AlbumSelectListViewModel` is available when we create a view in the next step.</span></span>

<span data-ttu-id="67a45-202">將 `EditVM` 方法加入至 `StoreManagerController`。</span><span class="sxs-lookup"><span data-stu-id="67a45-202">Add an `EditVM` method to the `StoreManagerController`.</span></span> <span data-ttu-id="67a45-203">已完成的程式碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="67a45-203">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

<span data-ttu-id="67a45-204">以滑鼠右鍵按一下 `AlbumSelectListViewModel`，選取 [**解析**]，然後**使用 MvcMusicStore. viewmodel;** 。</span><span class="sxs-lookup"><span data-stu-id="67a45-204">Right click `AlbumSelectListViewModel`, select **Resolve**, then **using MvcMusicStore.ViewModels;**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

<span data-ttu-id="67a45-205">或者，您可以新增下列 using 語句：</span><span class="sxs-lookup"><span data-stu-id="67a45-205">Alternatively, you can add the following using statement:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

<span data-ttu-id="67a45-206">以滑鼠右鍵按一下 `EditVM`，然後選取 [**新增視圖**]。</span><span class="sxs-lookup"><span data-stu-id="67a45-206">Right click `EditVM` and select **Add View**.</span></span> <span data-ttu-id="67a45-207">使用如下所示的選項。</span><span class="sxs-lookup"><span data-stu-id="67a45-207">Use the options shown below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

<span data-ttu-id="67a45-208">選取 [**新增**]，然後以下列內容取代*Views\StoreManager\EditVM.cshtml*檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="67a45-208">Select **Add**, then replace the contents of the *Views\StoreManager\EditVM.cshtml* file with the following:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

<span data-ttu-id="67a45-209">`EditVM` 標記與原始的 `Edit` 標記非常類似，但有下列例外狀況。</span><span class="sxs-lookup"><span data-stu-id="67a45-209">The `EditVM` markup is very similar to the original `Edit` markup with the following exceptions.</span></span>

- <span data-ttu-id="67a45-210">[`Edit`] 視圖中的模型屬性的格式為 `model.property`（例如，`model.Title`）。</span><span class="sxs-lookup"><span data-stu-id="67a45-210">Model properties in the `Edit` view are of the form `model.property`(for example, `model.Title` ).</span></span> <span data-ttu-id="67a45-211">[`EditVm`] 視圖中的模型屬性的格式為 `model.Album.property`（例如，`model.Album.Title`）。</span><span class="sxs-lookup"><span data-stu-id="67a45-211">Model properties in the `EditVm` view are of the form `model.Album.property`(for example, `model.Album.Title`).</span></span> <span data-ttu-id="67a45-212">這是因為 `EditVM` 視圖會傳遞 `Album`的容器，而不是 `Edit` 視圖中的 `Album`。</span><span class="sxs-lookup"><span data-stu-id="67a45-212">That's because the `EditVM` view is passed a container for an `Album`, not an `Album` as in the `Edit` view.</span></span>
- <span data-ttu-id="67a45-213">**DropDownList**第二個參數來自視圖模型，而不是**ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="67a45-213">The **DropDownList** second parameter comes from the view model, not the **ViewBag**.</span></span>
- <span data-ttu-id="67a45-214">`EditVM` view 中的**html.beginform** helper 會明確地回傳至 `Edit` 動作方法。</span><span class="sxs-lookup"><span data-stu-id="67a45-214">The **BeginForm** helper in the `EditVM` view explicitly posts back to the `Edit` action method.</span></span> <span data-ttu-id="67a45-215">藉由回傳至 `Edit` 動作，我們不需要撰寫 `HTTP POST EditVM` 動作，而且可以重複使用 `HTTP POST` `Edit` 動作。</span><span class="sxs-lookup"><span data-stu-id="67a45-215">By posting back to the `Edit` action, we don't have to write an `HTTP POST EditVM` action and can reuse the `HTTP POST` `Edit` action.</span></span>

<span data-ttu-id="67a45-216">執行應用程式並編輯專輯。</span><span class="sxs-lookup"><span data-stu-id="67a45-216">Run the application and edit an album.</span></span> <span data-ttu-id="67a45-217">將 URL 變更為使用 `EditVM`。</span><span class="sxs-lookup"><span data-stu-id="67a45-217">Change the URL to use `EditVM`.</span></span> <span data-ttu-id="67a45-218">變更欄位並按 [**儲存**] 按鈕，以確認程式碼是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="67a45-218">Change a field and hit the **Save** button to verify the code is working.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a><span data-ttu-id="67a45-219">您應該使用哪一種方法？</span><span class="sxs-lookup"><span data-stu-id="67a45-219">Which Approach Should You Use?</span></span>

<span data-ttu-id="67a45-220">所有顯示的三種方法都是可接受的。</span><span class="sxs-lookup"><span data-stu-id="67a45-220">All three approaches shown are acceptable.</span></span> <span data-ttu-id="67a45-221">許多開發人員偏好使用 `ViewBag`，將 `SelectList` 明確地傳遞給 `DropDownList`。</span><span class="sxs-lookup"><span data-stu-id="67a45-221">Many developers prefer to explicitly pass the `SelectList` to the `DropDownList` using the `ViewBag`.</span></span> <span data-ttu-id="67a45-222">這種方法有額外的優點，讓您能夠彈性地使用更適當的集合名稱。</span><span class="sxs-lookup"><span data-stu-id="67a45-222">This approach has the added advantage of giving you the flexibility of using a more appropriate name for the collection.</span></span> <span data-ttu-id="67a45-223">要注意的是，您無法將 `ViewBag SelectList` 物件命名為與模型屬性相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="67a45-223">The one caveat is you cannot name the `ViewBag SelectList` object the same name as the model property.</span></span>

<span data-ttu-id="67a45-224">有些開發人員偏好使用 ViewModel 方法。</span><span class="sxs-lookup"><span data-stu-id="67a45-224">Some developers prefer the ViewModel approach.</span></span> <span data-ttu-id="67a45-225">有些人會考慮更詳細的標記，並產生 ViewModel 方法的 HTML 的缺點。</span><span class="sxs-lookup"><span data-stu-id="67a45-225">Others consider the more verbose markup and generated HTML of the ViewModel approach a disadvantage.</span></span>

<span data-ttu-id="67a45-226">在本節中，我們已瞭解使用**DropDownList**與類別目錄資料的三種方法。</span><span class="sxs-lookup"><span data-stu-id="67a45-226">In this section we have learned three approaches to using the **DropDownList** with category data.</span></span> <span data-ttu-id="67a45-227">在下一節中，我們將示範如何加入新的類別。</span><span class="sxs-lookup"><span data-stu-id="67a45-227">In the next section, we'll show how to add a new category.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="67a45-228">[上一頁](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [下一頁](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="67a45-228">[Previous](using-the-dropdownlist-helper-with-aspnet-mvc.md)
[Next](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span></span>
