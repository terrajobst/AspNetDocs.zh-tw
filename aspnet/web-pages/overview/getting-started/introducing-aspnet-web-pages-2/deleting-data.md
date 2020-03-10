---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: ASP.NET Web Pages 簡介-刪除資料庫資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程會示範如何刪除個別的資料庫專案。 它假設您已透過更新 ASP.NET Web Pa 中的資料庫資料來完成數列 。
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: c8620fc1abc61d514bdc039c66f7a84e67e89abe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629035"
---
# <a name="introducing-aspnet-web-pages---deleting-database-data"></a>ASP.NET Web Pages 簡介-刪除資料庫資料

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程會示範如何刪除個別的資料庫專案。 它假設您已透過[更新 ASP.NET Web Pages 中的資料庫資料](updating-data.md)來完成數列。
> 
> 您將學到什麼：
> 
> - 如何從記錄清單中選取個別記錄。
> - 如何從資料庫中刪除單一記錄。
> - 如何檢查表單中是否已按一下特定按鈕。
>   
> 
> 討論的功能/技術：
> 
> - `WebGrid` helper。
> - SQL `Delete` 命令。
> - 執行 SQL `Delete` 命令的 `Database.Execute` 方法。

## <a name="what-youll-build"></a>您要建置的內容

在上一個教學課程中，您已瞭解如何更新現有的資料庫記錄。 本教學課程很類似，不同之處在于您會將它刪除，而不是更新記錄。 這些程式都是一樣的，不同之處在于刪除作業較簡單，因此本教學課程將會簡短。

在 [*電影*] 頁面中，您將更新 `WebGrid` 協助程式，讓它顯示每個電影旁的 [**刪除**] 連結，以伴隨您稍早新增的**編輯**連結。

![顯示每個電影之刪除連結的電影頁面](deleting-data/_static/image1.png)

如同編輯，當您按一下 [**刪除**] 連結時，它會將您帶到不同的頁面，其中電影資訊已經在表單中：

![刪除顯示電影的電影頁面](deleting-data/_static/image2.png)

然後，您可以按一下按鈕來永久刪除記錄。

## <a name="adding-a-delete-link-to-the-movie-listing"></a>新增電影清單的刪除連結

您將從新增 `WebGrid` helper 的**刪除**連結開始。 此連結類似于您在上一個教學課程中新增的 [**編輯**] 連結。

開啟 [*電影*] 檔案。

藉由新增資料行來變更頁面主體中的 `WebGrid` 標記。 以下是修改過的標記：

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

新的資料行是這一項：

[!code-html[Main](deleting-data/samples/sample2.html)]

方格的設定方式，[**編輯**] 資料行會在方格中最左邊，而 [**刪除**] 資料行則最右邊。 （現在在 [`Year`] 資料行後面有一個逗號，以免您發現）。這些連結資料行的位置並沒有什麼特殊之處，您可以輕鬆地將它們放在彼此旁。 在此情況下，它們是分開的，使它們更難以進行混合。

![已標記 [編輯] 和 [詳細資料] 連結的電影頁面，顯示它們不在彼此旁邊](deleting-data/_static/image3.png)

新的資料行會顯示其文字顯示為 "Delete" 的連結（`<a>` 元素）。 連結的目標（其 `href` 屬性）是最後解析成類似此 URL 的程式碼，每個電影的 `id` 值都不同：

[!code-css[Main](deleting-data/samples/sample3.css)]

此連結將會叫用名為*DeleteMovie*的頁面，並將您所選電影的識別碼傳遞給它。

本教學課程將不會詳細說明如何建立此連結，因為它與上一個教學課程中的 [**編輯**] 連結（[更新 ASP.NET Web Pages 中的資料庫資料](updating-data.md)）幾乎相同。

## <a name="creating-the-delete-page"></a>建立 [刪除] 頁面

現在您可以建立將做為方格中 [**刪除**] 連結目標的頁面。

> [!NOTE] 
> 
> **重要事項**第一次選取要刪除的記錄，然後使用個別的頁面和按鈕來確認程式對於安全性非常重要的技巧。 如同您在先前的教學課程中所閱讀，對您的網站進行*任何*變更時，應該*一律*使用表單 &mdash; 也就是使用 HTTP POST 作業來完成。 如果您只要按一下連結（也就是使用「取得」作業）來變更網站，人們就可以對您的網站提出簡單的要求，並刪除您的資料。 即使是索引網站的搜尋引擎編目程式，也可能會因為下列連結而不小心刪除資料。
> 
> 當您的應用程式可讓使用者變更記錄時，您必須將記錄呈現給使用者，才能進行編輯。 但您可能會想要略過此步驟來刪除記錄。 不過，請勿略過該步驟。 （這也有助於使用者查看記錄，並確認他們正在刪除其所需的記錄）。
> 
> 在後續的教學課程設定中，您將瞭解如何新增登入功能，讓使用者在刪除記錄之前必須先登入。

建立名為*DeleteMovie*的頁面，並以下列標記取代檔案中的內容：

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

此標記類似于*EditMovie*頁面，不同之處在于，標記包含 `<span>` 元素，而不是使用文字方塊（`<input type="text">`）。 這裡沒有任何要編輯的東西。 您只需要顯示電影詳細資料，讓使用者可以確定他們刪除的是正確的電影。

標記已經包含一個連結，可讓使用者回到電影清單頁面。

如同在 [ *EditMovie* ] 頁面中，所選電影的識別碼會儲存在隱藏欄位中。 （它會在第一個位置以查詢字串值的形式傳遞至頁面。）有一個 `Html.ValidationSummary` 呼叫會顯示驗證錯誤。 在此情況下，錯誤可能是未將電影識別碼傳遞至頁面，或電影識別碼無效。 如果有人執行此頁面，而未先在 [*電影*] 頁面中選取電影，就會發生這種情況。

按鈕標題為 [**刪除電影**]，而其 [名稱] 屬性設定為 [`buttonDelete`]。 `name` 屬性將用於程式碼中，以識別提交表單的按鈕。

當第一次顯示網頁時，您必須將程式碼寫入1）讀取電影詳細資料，而2）則會在使用者按一下按鈕時實際刪除電影。

## <a name="adding-code-to-read-a-single-movie"></a>新增程式碼以讀取單一電影

在 [ *DeleteMovie* ] 頁面的頂端，新增下列程式碼區塊：

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

此標記與 [ *EditMovie* ] 頁面中的對應程式碼相同。 它會從查詢字串中取得影片識別碼，並使用識別碼從資料庫讀取記錄。 程式碼包含驗證測試（`IsInt()` 和 `row != null`），以確定傳遞至頁面的電影識別碼是有效的。

請記住，此程式碼應該只在頁面第一次執行時執行。 當使用者按一下 [**刪除電影**] 按鈕時，您不會想要從資料庫重新讀取電影記錄。 因此，*如果要求不是 post 作業（表單提交）* ，則會在測試中顯示用來讀取電影的程式碼，`if(!IsPost)` &mdash;。

## <a name="adding-code-to-delete-the-selected-movie"></a>新增程式碼以刪除選取的電影

若要在使用者按一下按鈕時刪除電影，請在 `@` 區塊的右大括弧內新增下列程式碼：

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

此程式碼類似于更新現有記錄的程式碼，但較簡單。 此程式碼基本上會執行 SQL `Delete` 語句。

 如同在 [ *EditMovie* ] 頁面中，程式碼位於 `if(IsPost)` 區塊中。 這一次，`if()` 條件有點複雜： 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

這裡有兩個條件。 第一種方式是提交頁面，就像您在 &mdash; `if(IsPost)`之前所看到的一樣。

第二個條件是 `!Request["buttonDelete"].IsEmpty()`，表示要求具有名為 `buttonDelete`的物件。 無可否認的，這是測試提交表單之按鈕的間接方式。 如果表單包含多個 [提交] 按鈕，則只會在要求中出現所按下的按鈕名稱。 因此，在邏輯上，如果特定按鈕的名稱出現在要求 &mdash; 中，或如程式碼中所述，如果該按鈕不是空的 &mdash; 這就是提交表單的按鈕。

`&&` 運算子表示 "and" （邏輯 AND）。 因此，整個 `if` 條件為 。

*此要求是 post （不是第一次要求）*  
  
 AND  
  
*[* `buttonDelete`]*按鈕是提交表單的按鈕。*

這個表單（事實上，此頁面）只包含一個按鈕，因此技術上不需要 `buttonDelete` 的額外測試。 但是，您即將執行會永久移除資料的作業。 因此，您想要盡可能確保只有在使用者明確要求作業時才執行作業。 例如，假設您稍後展開此頁面，並將其他按鈕加入其中。 就算如此，刪除影片的程式碼只會在按一下 [`buttonDelete`] 按鈕時執行。

如同在 [ *EditMovie* ] 頁面中，您會從隱藏的欄位取得識別碼，然後執行 SQL 命令。 `Delete` 語句的語法為：

`DELETE FROM table WHERE ID = value`

請務必包含 `WHERE` 子句和識別碼。 如果您省略 WHERE 子句，將會*刪除資料表中的所有記錄*。 如您所見，您可以使用預留位置，將識別碼值傳遞至 SQL 命令。

## <a name="testing-the-movie-delete-process"></a>測試電影刪除流程

現在您可以測試。 執行 [*電影*] 頁面，然後按一下電影旁的 [**刪除**]。 當 [ *DeleteMovie* ] 頁面出現時，按一下 [**刪除電影**]。

![已反白顯示 [刪除電影] 按鈕的 [刪除電影] 頁面](deleting-data/_static/image4.png)

當您按一下按鈕時，程式碼會刪除電影，並返回電影清單。 您可以在這裡搜尋已刪除的電影，並確認它已被刪除。

## <a name="coming-up-next"></a>下一步

下一個教學課程會示範如何為網站上的所有頁面提供常見的外觀和版面配置。

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a>電影頁面的完整清單（以刪除連結更新）

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a>DeleteMovie 頁面的完整清單

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a>其他資源

- [使用 Razor 語法 ASP.NET Web 程式設計的簡介](../introducing-razor-syntax-c.md)
- W3Schools 網站上的[SQL DELETE 子句](http://www.w3schools.com/sql/sql_delete.asp)

> [!div class="step-by-step"]
> [上一頁](updating-data.md)
> [下一頁](layouts.md)
