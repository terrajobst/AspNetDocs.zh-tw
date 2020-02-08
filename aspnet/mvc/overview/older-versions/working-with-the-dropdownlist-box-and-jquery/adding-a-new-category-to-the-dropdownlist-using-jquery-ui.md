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
# <a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a>使用 jQuery UI 將新的分類新增至 DropDownList

依[Rick Anderson]((https://twitter.com/RickAndMSFT))

HTML `Select` 標記非常適合用來呈現固定類別目錄資料的清單，但通常需要加入新的類別。 假設我們想要將「Opera」類型新增至資料庫中的類別目錄嗎？ 在本節中，我們將使用 jQuery UI 來加入可用於加入新分類的對話方塊。 下圖顯示 UI 在瀏覽器中的顯示方式。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

當使用者選取 [**加入新**的內容類型] 連結時，快顯視窗對話方塊會提示使用者輸入新的內容類型名稱（並選擇性地顯示描述）。 下圖顯示 [**新增**內容類型] 快顯對話方塊。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

輸入新的內容類型名稱並推送 [**儲存**] 按鈕時，將會發生下列情況：

1. AJAX 呼叫會將資料張貼至內容類型控制器的 Create 方法，以將新的內容類型儲存至資料庫，並以 JSON 形式傳回新的內容類型資訊（類型名稱和識別碼）。
2. JavaScript 會將新的內容類型資料新增至選取清單。
3. JavaScript 讓新的內容類型成為選取的專案。

   在下圖中， **Opera**已加入至資料庫，並已**在 [內容**類型] 下拉式清單中選取。 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

開啟*Views\StoreManager\Create.cshtml*檔案，並以下列程式碼取代內容類型標記：

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

`_ChooseGenre` 部分視圖將包含連結 JavaScript 的所有邏輯，以及用來執行 [加入新的內容類型] 功能的 jQuery。 完成程式碼之後，就可以輕鬆地使用演出者 UI 來執行相同動作。

在方案總管中，以滑鼠右鍵按一下*Views\StoreManager*資料夾，然後依序選取 [**新增**] 和 [**查看**]。 在 [ **View name** ] 輸入中，輸入 `_ChooseGenre` 然後選取 [**新增**]。 以下列內容取代*Views\StoreManager\\_ChooseGenre. cshtml*檔案中的標記：

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

第一行宣告我們以模型的形式傳入 `Album`，與在 Create view 中找到的模型語句完全相同。 接下來的幾行是**標籤**協助程式標記。 下一行是**DropDownList** helper 呼叫，與原始 [建立] 視圖中的完全相同。 下一行會加入名稱為 `Add New Genre`的連結，並將其樣式與按鈕類似。 包含 `ValidationMessageFor` 的那一行是直接從 Create view 複製而來的。 下列幾行：

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

建立隱藏的 div，其識別碼為 `genreDialog`。 我們將使用 jQuery 來連接我們的 [**新增**內容類型] 對話方塊，此 div 中的識別碼 `genreDialog`。 最後兩個腳本標記包含將用來執行 [加入新的類型] 功能的 JavaScript 檔案連結。 在專案中為您提供 */Scripts/chooseGenre.js*檔案，我們將在稍後的教學課程中加以檢查。

執行應用程式，然後按一下 [**加入新**的內容類型] 按鈕。 在 [**新增**內容類型] 對話方塊的 [**名稱**] 輸入方塊中，輸入**Opera** 。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

按一下 [儲存] 按鈕。 AJAX 呼叫會建立 Opera 分類，然後在下拉式清單中填入 Opera，並將 Opera 設定為選取的類型。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

輸入 [演出者]、[標題] 和 [價格]，然後選取 [**建立**] 按鈕。 如果您輸入的價格小於 $8.99，新的專輯會出現在索引視圖的頂端。 確認新的專輯專案已儲存在資料庫中。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

嘗試建立只有一個字母的新內容類型。 *Models\Genre.cs*檔案中的下列程式碼會設定內容類型名稱的最小和最大長度。

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

用戶端驗證報告您必須輸入介於2到20個字元之間的字串。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a>檢查新的內容類型如何加入至資料庫和選取清單中。

開啟*Scripts\chooseGenre.js*檔案，並檢查程式碼。

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

第二行使用識別碼 `genreDialog`，在*Views\StoreManager\\_ChooseGenre. cshtml*檔案中的 div 標記上建立對話方塊。 大部分的具名引數都一目了然。 `autoOpen` 參數設定為 false，選取 [**建立**內容類型] 按鈕將會明確開啟對話（這在中是後面的說明）。 對話方塊有兩個按鈕： [**儲存**] 和 [**取消**]。 [**取消**] 按鈕會關閉對話方塊。 下列程式碼顯示 [**儲存**] 按鈕功能。

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

`var createGenreForm` 是從 `createGenreForm` 識別碼中選取的。 `createGenreForm` 識別碼是在*Views\Genre\\_CreateGenre. cshtml*檔案中找到的下列程式碼中設定。

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

*Views\Genre _CreateGenre\\* 中使用的[html.beginform](https://msdn.microsoft.com/library/dd492714.aspx) helper 多載會產生 html，其中包含含有要提交表單之 URL 的 action 屬性。 您可以透過在瀏覽器中顯示 [建立專輯] 頁面，然後在瀏覽器中選取 [顯示來源]，來查看這項功能。 下列標記顯示產生的 HTML，其中包含表單標記。

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

JQuery `$.post` 行會對 action 屬性（`/StoreManager/Create`）進行 AJAX 呼叫，並傳入 [**建立**內容類型] 對話方塊中的資料。 資料包含新內容類型的名稱和選擇性的描述。 如果 AJAX 呼叫成功，新的內容類型名稱和值會加入至選取標記，而新的內容類型會設定為選取的值。 因為這是動態產生的標記，所以您無法在瀏覽器中查看來源來看到新的 [選取] 選項。 您可以使用 IE 9 F12 開發人員工具來查看新的 HTML。 若要在 Internet Explorer 9 中查看新的 [選取] 選項，請按 F12 鍵以啟動 F12 開發人員工具。 流覽至 [建立] 頁面並加入新的內容類型，以便在 [內容類型] 選取清單中選取新的內容類型。 在 F12 開發人員工具中：

1. 選取 [HTML] 索引標籤。
2. 按 [重新整理] 圖示。  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. 在搜尋方塊中，輸入 GenreID。
4. 使用下一個圖示，   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   流覽至下列選取標記：

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. 展開最後一個選項值。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

*Scripts\chooseGenre.js*檔案中的下列程式碼顯示如何將 [**加入新**的內容類型] 按鈕連接到 click 事件，以及如何建立 [**加入新**的內容類型] 對話方塊。

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

第一行會建立附加至 [**加入新**的內容類型] 按鈕的 click 函式。 Views\StoreManager\\中的下列標記 _ChooseGenre. cshtml 檔案顯示如何建立 [**加入新**的內容類型] 按鈕：

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

Load 方法會建立並開啟 [加入內容類型] 對話方塊，並呼叫 jQuery `parse` 方法，以便在對話方塊中輸入的資料上進行用戶端驗證。

在本節中，您已瞭解如何建立可用於將新的類別資料加入至選取清單的對話方塊。 您可以遵循相同的程式來建立 UI，將新的演出者新增至 [演出者] 選取清單。 本教學課程提供使用 ASP.NET MVC HTML helper **DropDownList**的總覽。 如需有關使用**DropDownList**的詳細資訊，請參閱下面的加法參考一節。 如果本教學課程有説明，請讓我們知道。

Rick. Anderson [at] Microsoft .com

### <a name="additional-references"></a>其他參考

- [ASP.NET MVC –](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)的階層式下拉式清單教學課程
- 已[選擇](https://harvesthq.github.com/chosen/)支援多重選取和篩選的 JavaScript 外掛程式。

### <a name="contributors"></a>參與者

- [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)
- Jean-Sébastien Goupil
- [Brad Wilson](http://bradwilson.typepad.com/)

### <a name="reviewers"></a>檢閱者

- Jean-Sébastien Goupil
- [Brad Wilson](http://bradwilson.typepad.com/)
- Mike Pope
- Tom 作者: dykstra

> [!div class="step-by-step"]
> [[上一步]](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
