---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
title: 搭配使用 DropDownList Helper 與 ASP.NET MVC |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 53767e05-c8ab-42e1-a94b-22d906195200
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 6375bb2be158cea18309ffa71c71ac3e67bc91ed
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457865"
---
# <a name="using-the-dropdownlist-helper-with-aspnet-mvc"></a>使用 DropDownList 協助程式與 ASP.NET MVC

依[Rick Anderson](https://twitter.com/RickAndMSFT)

本教學課程將告訴您在 ASP.NET MVC Web 應用程式中使用[DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) Helper 和[ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) helper 的基本概念。 您可以使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，這是 Microsoft Visual Studio 的免費版本，可遵循本教學課程。 開始之前，請先確定您已安裝下列必要條件。 您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，您可以使用下列連結個別安裝必要條件：

- [Visual Studio Web Developer EXPRESS SP1 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)<a id="post"></a>
- [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）

如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。 本教學課程假設您已完成[ASP.NET mvc](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)教學課程或[ASP.NET MVC 音樂商店](../mvc-music-store/mvc-music-store-part-1.md)教學課程的簡介，或您已熟悉 ASP.NET mvc 開發。 本教學課程從[ASP.NET MVC 音樂存放](../mvc-music-store/mvc-music-store-part-1.md)教學課程中的已修改專案開始。 您可以下載具有下列連結的入門專案[下載C#版本](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829)。

本主題提供具有完成之教學C#課程原始程式碼的 Visual Web Developer 專案。 [下載](https://code.msdn.microsoft.com/Using-the-DropDownList-67f9367d)。

### <a name="what-youll-build"></a>您要建置的內容

您將建立使用[DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) helper 來選取類別目錄的動作方法和視圖。 您也會使用**jQuery**來新增 [插入類別] 對話方塊，以便在需要新的分類（例如內容類型或演出者）時使用。 以下是 [建立] 視圖的螢幕擷取畫面，其中顯示可新增內容類型和加入新演出者的連結。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image1.png)

### <a name="skills-youll-learn"></a>您要學習的技術

以下是您要學習的內容：

- 如何使用[DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) helper 來選取類別目錄資料。
- 如何新增**jQuery**對話方塊來加入新的類別目錄。

### <a name="getting-started"></a>開始使用

首先，使用下列[連結下載入門專案。](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829) 在 Windows Explorer 中，以滑鼠右鍵按一下*DDL\_Starter .zip*檔案，然後選取 [屬性]。 在 [ **DDL\_Starter .Zip 屬性**] 對話方塊中，選取 [解除封鎖]。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image2.png)

以滑鼠右鍵按一下 DDL\_Starter .zip 檔案，然後選取 [**全部解壓縮**] 來解壓縮檔案。 使用 Visual Web Developer 2010 Express （簡稱 "Visual Web Developer" 或 "VWD"）或 Visual Studio 2010 開啟*StartMusicStore .sln*檔案。

按 CTRL + F5 執行應用程式，然後按一下 [**測試**] 連結。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image3.png)

選取 [**選取電影類別目錄（簡單）** ] 連結。 [電影類型] 選取 [清單] 隨即顯示，並喜劇所選的值。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image4.png)

在瀏覽器中按一下滑鼠右鍵，然後選取 [view source]。 網頁的 HTML 隨即顯示。 下列程式碼顯示 select 元素的 HTML。

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample1.html)]

您可以看到選取清單中的每個專案都有值（0代表動作，1代表戲劇，2代表喜劇，3代表科學小說）和顯示名稱（Action、戲劇、喜劇和科學小說）。 上述程式碼是選取清單的標準 HTML。

將選取清單變更為戲劇，然後按 [**提交**] 按鈕。 瀏覽器中的 URL 是 `http://localhost:2468/Home/CategoryChosen?MovieType=1`，而您選取的頁面會顯示 **： 1**。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image5.png)

開啟*Controllers\HomeController.cs*檔案，並檢查 `SelectCategory` 方法。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample2.cs)]

用來建立 HTML 選取清單的[DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) Helper 需要**IEnumerable&lt;SelectListItem &gt;** （明確或隱含）。 也就是說，您可以明確地將**ienumerable&lt;SelectListItem &gt;** 傳遞給[DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) helper，也可以使用**SelectListItem**的相同名稱做為模型屬性，將**ienumerable&lt;SelectListItem &gt;** 加入[ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)中。 本教學課程的下一個部分將涵蓋以隱含和明確方式傳入**SelectListItem** 。 上述程式碼顯示建立**IEnumerable&lt;SelectListItem &gt;** 的最簡單方式，並將文字和值填入其中。 請注意，`Comedy`[SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)將[選取](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.selected.aspx)的屬性設定為**true** ，這會導致轉譯的選取清單顯示**喜劇**做為清單中的選取專案。

先前建立的**IEnumerable&lt;SelectListItem &gt;** 會新增至名稱為 MovieType 的[ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 。 這就是我們如何將**IEnumerable&lt;SelectListItem &gt;** 隱含地傳遞給如下所示的[DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) helper。

開啟*Views\Home\SelectCategory.cshtml*檔案，並檢查標記。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample3.cshtml)]

在第三行中，我們將版面配置設定為 Views/Shared/\_Simple\_Layout，這是標準版面配置檔案的簡化版本。 這麼做是為了讓顯示和呈現的 HTML 變得簡單。

在此範例中，我們不會變更應用程式的狀態，因此我們將使用**HTTP GET**而非**HTTP POST**來提交資料。 請參閱 W3C 一節[快速檢查清單，以選擇 HTTP GET 或 POST](http://www.w3.org/2001/tag/doc/whenToUseGet.html#checklist)。 因為我們不會變更應用程式並張貼表單，所以我們會使用[html.beginform](https://msdn.microsoft.com/library/dd460344.aspx)多載，讓我們指定動作方法、控制器和表單方法（**Http POST**或**HTTP GET**）。 Views 通常會包含不採用任何參數的[html.beginform](https://msdn.microsoft.com/library/dd505244.aspx)多載。 [無參數版本] 預設會將表單資料張貼至相同動作方法和控制器的 POST 版本。

下面這行

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample4.cshtml)]

將字串引數傳遞給**DropDownList** helper。 這個字串（在我們的範例中為 "MovieType"）會執行兩項動作：

- 它會提供**DropDownList** helper 的索引鍵，以在**ViewBag**中尋找**IEnumerable&lt;SelectListItem &gt;** 。
- 它會系結至 MovieType form 元素的資料系結。 如果 submit 方法是**HTTP GET**，`MovieType` 將會是查詢字串。 如果 submit 方法是**HTTP POST**，`MovieType` 將會加入訊息本文中。 下圖顯示查詢字串，其值為1。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image6.png)

下列程式碼顯示提交表單的 `CategoryChosen` 方法。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample5.cs)]

流覽回到 [測試] 頁面，然後選取 [ **HTML SelectList** ] 連結。 HTML 網頁會呈現類似于 simple ASP.NET MVC 測試頁面的 select 專案。 以滑鼠右鍵按一下瀏覽器視窗，然後選取 [ **view source**]。 選取清單的 HTML 標籤基本上完全相同。 測試 HTML 網頁，其運作方式類似于我們先前測試過的 ASP.NET MVC 動作方法和 view。

### <a name="improving-the-movie-select-list-with-enums"></a>使用列舉來改善電影選取清單

如果您應用程式中的類別已固定且不會變更，您可以利用列舉，讓您的程式碼更穩定且更容易擴充。 當您加入新的類別時，就會產生正確的類別目錄值。 當您加入新的類別，但忘了更新類別目錄值時，會避免複製和貼上錯誤。

開啟*Controllers\HomeController.cs*檔案，並檢查下列程式碼：

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample6.cs)]

[Enum](https://msdn.microsoft.com/library/sbbt4032(VS.80).aspx) `eMovieCategories` 會捕捉這四種電影類型。 `SetViewBagMovieType` 方法會從 `eMovieCategories`**列舉**建立**IEnumerable&lt;SelectListItem &gt;** ，並從 `Selected` 參數設定 `selectedMovie` 屬性。 `SelectCategoryEnum` 動作方法會使用與 `SelectCategory` 動作方法相同的視圖。

流覽至 [測試] 頁面，然後按一下 [`Select Movie Category (Enum)`] 連結。 這次不會顯示值（數位），而是顯示代表列舉的字串。

### <a name="posting-enum-values"></a>張貼列舉值

HTML 表單通常用來將資料張貼至伺服器。 下列程式碼顯示 `SelectCategoryEnumPost` 方法的 `HTTP GET` 和 `HTTP POST` 版本。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample7.cs)]

藉由將 `eMovieCategories` 列舉傳遞給 `POST` 方法，我們可以將列舉值和列舉字串解壓縮。 執行範例，然後流覽至 [測試] 頁面。 按一下 [`Select Movie Category(Enum Post)`] 連結。 選取電影類型，然後按 [提交] 按鈕。 顯示的畫面會顯示電影類型的值和名稱。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image7.png)

### <a name="creating-a-multiple-section-select-element"></a>建立多個區段的 Select 元素

[清單方塊](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx)html helper 會以 `multiple` 屬性轉譯 HTML `<select>` 專案，讓使用者可以進行多個選擇。 流覽至 [測試] 連結，然後選取 [**多重選取國家/地區**] 連結。 呈現的 UI 可讓您選取多個國家/地區。 在下圖中，已選取 [加拿大] 和 [中國]。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image8.png)

### <a name="examining-the-multiselectcountry-code"></a>檢查 MultiSelectCountry 程式碼

檢查*Controllers\HomeController.cs*檔案中的下列程式碼。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample8.cs)]

`GetCountries` 方法會建立國家/地區的清單，然後將它傳遞給 `MultiSelectList` 的「函式」。 在上述的 `GetCountries` 方法中使用的 `MultiSelectList` 的函式多載會採用四個參數：

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample9.cs)]

1. *items*： [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) ，其中包含清單中的專案。 在上述範例中，國家/地區清單。
2. *dataValueField*： **IEnumerable**清單中包含值的屬性名稱。 在上述範例中，`ID` 屬性。
3. *dataTextField*： **IEnumerable**清單中包含要顯示之資訊的屬性名稱。 在上述範例中，`name` 屬性。
4. *selectedValues*：選取的值清單。

在上述範例中，`MultiSelectCountry` 方法會為選取的國家/地區傳遞 `null` 值，因此在顯示 UI 時不會選取任何國家/地區。 下列程式碼顯示用來呈現 `MultiSelectCountry` 視圖的 Razor 標記。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample10.cshtml)]

上述使用的 HTML helper [ListBox](https://msdn.microsoft.com/library/dd470200.aspx)方法會採用兩個參數，將屬性名稱設為模型系結，以及包含 select 選項和值的[MultiSelectList](https://msdn.microsoft.com/library/system.web.mvc.multiselectlist.aspx) 。 上述的 `ViewBag.YouSelected` 程式碼是用來顯示您提交表單時選取的國家/地區值。 檢查 `MultiSelectCountry` 方法的 HTTP POST 多載。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample11.cs)]

`ViewBag.YouSelected` 動態屬性包含選取的國家/地區，取得表單集合中的 `Countries` 專案。 在此版本中，會將所選國家/地區的清單傳遞給 GetCountries 方法，因此當顯示 [`MultiSelectCountry`] 視圖時，會在 UI 中選取選取的國家/地區。

### <a name="making-a-select-element-friendly-with-the-harvest-chosen-jquery-plugin"></a>使用搜集選擇的 jQuery 外掛程式讓 Select 元素變得易懂

[搜集[選擇](https://harvesthq.github.com/chosen/)的 jQuery 外掛程式] 可以加入至 HTML &lt;選取 [&gt;] 元素，以建立使用者易記的 UI。 下列影像示範使用 `MultiSelectCountry` view 來搜集[選擇](https://harvesthq.github.com/chosen/)的 jQuery 外掛程式。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image9.png)

在下列兩個影像中，已選取 [**加拿大**]。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image10.png)

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image11.png)

在上圖中，已選取 [加拿大]，其中包含**x** ，您可以按一下以移除選取專案。 下圖顯示已選取 [加拿大]、[中國] 和 [日本]。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image12.png)

### <a name="hooking-up-the-harvest-chosen-jquery-plugin"></a>連結到搜集選擇的 jQuery 外掛程式

如果您有 jQuery 的經驗，下一節將更容易遵循。 如果您從未使用過 jQuery，您可能會想要嘗試下列其中一個 jQuery 教學課程。

- [JQuery 如何](http://docs.jquery.com/Tutorials:How_jQuery_Works)由[John Resig](http://ejohn.org/)運作
- [Jörn Zaefferer](http://bassistance.de/)的[jQuery 消費者入門](http://docs.jquery.com/Tutorials:Getting_Started_with_jQuery)
- JQuery by [Cody Lindley](http://codylindley.com/)的[即時範例](http://codylindley.com/blogstuff/js/jquery/#)

所選擇的外掛程式會包含在本教學課程隨附的入門和已完成的範例專案中。 在本教學課程中，您只需要使用 jQuery 將它連結至 UI。 若要在 ASP.NET MVC 專案中使用 [搜集選擇的 jQuery] 外掛程式，您必須：

1. 從[github](https://github.com/harvesthq/chosen/)下載選擇的外掛程式。 已為您完成此步驟。
2. 將選擇的資料夾新增至您的 ASP.NET MVC 專案。 從您在上一個步驟中下載的選擇外掛程式，將資產新增至所選的資料夾。 已為您完成此步驟。
3. 將選擇的外掛程式連結至**DropDownList**或**ListBox** HTML helper。

### <a name="hooking-up-the-chosen-plugin-to-the-multiselectcountry-view"></a>將選擇的外掛程式連結到 MultiSelectCountry 視圖。

開啟*Views\Home\MultiSelectCountry.cshtml*檔案，並將 `htmlAttributes` 參數新增至 `Html.ListBox`。 您要新增的參數會包含選取清單（`@class = "chzn-select"`）的類別名稱。 完成的程式碼如下所示：

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample12.cshtml)]

在上述程式碼中，我們會新增 HTML 屬性和屬性值 `class = "chzn-select"`。 先前類別的 \@ 字元與 Razor view 引擎無關。 `class` 是[ C#關鍵字](https://msdn.microsoft.com/library/x53a06bb.aspx)。 C#關鍵字不能當做識別碼使用，除非它們包含 \@ 做為前置詞。 在上述範例中，`@class` 是有效的識別碼，但**類別**不是，因為**class**是關鍵字。

將參考新增至所*選/選擇的 jquery* ，以及*選擇/選擇的 .css*檔案。 所*選擇/選擇的 jquery* ，並會執行所選外掛程式的功能。 所*選擇/選擇的 .css*檔案提供樣式。 將這些參考新增至*Views\Home\MultiSelectCountry.cshtml*檔案的底部。 下列程式碼示範如何參考所選擇的外掛程式。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample13.cshtml)]

使用**Html. ListBox**程式碼中所使用的類別名稱，啟動所選擇的外掛程式。 在上述範例中，類別名稱為 `chzn-select`。 將下面這一行新增至*Views\Home\MultiSelectCountry.cshtml*視圖檔案的底部。 這一行會啟動所選擇的外掛程式。

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample14.html)]

下面這行是呼叫 jQuery ready 函式的語法，此函式會選取類別名稱 `chzn-select`的 DOM 元素。

[!code-powershell[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample15.ps1)]

然後，從上述呼叫傳回的包裝集合會套用所選的方法（`.chosen();`），這會連結到所選的外掛程式。

下列程式碼顯示已完成的*Views\Home\MultiSelectCountry.cshtml*視圖檔案。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample16.cshtml)]

執行應用程式，並流覽至 [`MultiSelectCountry`] 視圖。 嘗試新增和刪除國家/地區。 所提供的範例下載也包含使用視圖模型（而非**ViewBag**）來執行 MultiSelectCountry 功能的 `MultiCountryVM` 方法和 view。

在下一節中，您將瞭解 ASP.NET MVC 樣板機制如何與**DropDownList** helper 搭配運作。

> [!div class="step-by-step"]
> [下一個](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
