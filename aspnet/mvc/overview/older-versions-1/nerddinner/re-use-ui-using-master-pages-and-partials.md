---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 使用主版頁面和部分重新使用 UI |Microsoft Docs
author: microsoft
description: 步驟7探討我們可以在我們的視圖範本內套用「幹原則」的方式，使用部分視圖範本和主版頁面來消除程式碼重複。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: 0b17cb6ac14b7f187bf1f175097a37907689d46e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580329"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a>重複使用使用主版頁面和部分頁面的 UI

由[Microsoft](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟7，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。
> 
> 步驟7探討我們可以在我們的視圖範本內套用「幹原則」的方式，使用部分視圖範本和主版頁面來消除程式碼重複。
> 
> 如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。

## <a name="nerddinner-step-7-partials-and-master-pages"></a>NerdDinner 步驟7：部分和主版頁面

MVC 所 ASP.NET 的其中一個設計觀念是「不要自行重複」原則（通常稱為「幹」）。 試設計有助於消除重複的程式碼和邏輯，這最終可讓應用程式更快速地建立及維護。

我們已經看過在數個 NerdDinner 案例中套用的試原則。 一些範例：我們的驗證邏輯會在我們的模型層內執行，讓它在控制器的編輯和建立案例中強制執行;我們會在 [編輯]、[詳細資料] 和 [刪除] 動作方法中重複使用 "NotFound" view 範本;我們在我們的視圖範本中使用慣例命名模式，這樣就不需要在我們呼叫 View （） helper 方法時明確指定名稱。而且我們會針對 [編輯] 和 [建立] 動作案例重複使用 DinnerFormViewModel 類別。

現在讓我們來看一下，我們可以在我們的視圖範本內套用「幹原則」，以避免程式碼重複。

### <a name="re-visiting-our-edit-and-create-view-templates"></a>重新造訪我們的編輯和建立視圖範本

目前我們使用兩個不同的視圖範本– "Edit .aspx" 和 "Create .aspx" –以顯示晚餐表單 UI。 它們的快速視覺化比較會反白顯示其相似之處。 以下是建立表單的樣子：

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

我們的「編輯」表單看起來像這樣：

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

沒有太多差異了嗎？ 除了標題和標題文字之外，表單版面配置和輸入控制項都相同。

如果我們開啟「編輯 .aspx」和「建立 .aspx」視圖範本，我們會發現它們包含相同的表單版面配置和輸入控制項程式碼。 這種重複方式表示，每當我們引進或變更新的晚餐屬性時，都必須進行變更兩次-這不是好的。

### <a name="using-partial-view-templates"></a>使用部分視圖範本

ASP.NET MVC 支援定義「部分視圖」範本的功能，可用來封裝頁面子部分的視圖呈現邏輯。 「部分」提供一個實用的方式來定義 view 轉譯邏輯一次，然後在應用程式的多個位置重複使用它。

為了協助「清理」我們的編輯 .aspx，並建立 .aspx view 範本重複，我們可以建立名為 "DinnerForm" 的部分視圖範本，以封裝兩者通用的表單配置和輸入元素。 若要這麼做，請以滑鼠右鍵按一下/Views/Dinners 目錄，然後選擇 [新增&gt;View] 功能表命令：

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

這會顯示 [新增視圖] 對話方塊。 我們會將新的視圖命名為 [DinnerForm]，選取對話方塊中的 [建立部分視圖] 核取方塊，並指出我們會將 DinnerFormViewModel 類別傳遞給它：

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

當我們按一下 [新增] 按鈕時，Visual Studio 會在 "\Views\Dinners" 目錄中為我們建立新的 "DinnerForm" 視圖範本。

然後，我們可以將重複的表單版面配置/輸入控制項程式碼從編輯 .aspx/Create .aspx view 範本複製/貼上到新的 "DinnerForm" 部分視圖範本：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

然後，我們可以更新編輯和建立視圖範本來呼叫 DinnerForm 部分範本，並消除表單重複。 我們可以在我們的 view 範本內呼叫 RenderPartial （"DinnerForm"）來完成這項操作：

##### <a name="createaspx"></a>建立 .aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>編輯 .aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

呼叫 RenderPartial （例如： ~ Views/Dinners/DinnerForm）時，您可以明確限定所需部分範本的路徑。 不過，在上述程式碼中，我們會利用 ASP.NET MVC 中以慣例為基礎的命名模式，並只將 "DinnerForm" 指定為要轉譯之部分的名稱。 當我們執行此 ASP.NET 時，MVC 會先在以慣例為基礎的 views 目錄中尋找（針對 DinnersController，這會是/Views/Dinners）。 如果找不到部分範本，則會在/Views/Shared 目錄中尋找它。

以部分視圖的名稱呼叫 RenderPartial （）時，ASP.NET MVC 會傳遞給部分視圖，這是呼叫視圖範本所使用的相同模型和 ViewData 字典物件。 或者，還有 RenderPartial （）的多載版本，可讓您傳遞替代模型物件和/或 ViewData 字典，供部分視圖使用。 這適用于您只想要傳遞完整模型/ViewModel 子集的案例。

| **側邊主題：為什麼 &lt;%%&gt;，而不是 &lt;% =%&gt;？** |
| --- |
| 在上述程式碼中，您可能已注意到的其中一項很微妙，就是在呼叫 RenderPartial （）時，使用 &lt;%%&gt; 區塊，而不是 &lt;% =%&gt; 區塊。 &lt;% =%&gt; ASP.NET 中的區塊表示開發人員想要轉譯指定的值（例如： &lt;% = "Hello"%&gt; 會轉譯 "Hello"）。 &lt;%%&gt; 區塊，而不是表示開發人員想要執行程式碼，而且它們內的任何轉譯輸出都必須明確完成（例如： &lt;% Response。 Write （"Hello"）%&gt;。 我們使用 &lt;%%&gt; 區塊的原因是上述的 RenderPartial 程式碼，因為 RenderPartial （）方法不會傳回字串，而是會直接將內容輸出至呼叫視圖範本的輸出資料流程。 這是基於效能效率的理由，這樣做可避免建立（可能非常大）暫存字串物件的需求。 這會減少記憶體使用量，並改善整體應用程式輸送量。 使用 RenderPartial （）時，有一項常見的錯誤是忘了在呼叫結尾處加上分號（當它在 &lt;%%&gt; 區塊內）。 例如，此程式碼會造成編譯器錯誤： &lt;% RenderPartial （"DinnerForm"）%&gt; 您必須寫入： &lt;% Html. RenderPartial （"DinnerForm"）;%&gt; 這是因為 &lt;%%&gt; 區塊是獨立的程式碼語句，而且使用C#程式碼語句時必須以分號結束。 |

### <a name="using-partial-view-templates-to-clarify-code"></a>使用部分視圖範本來澄清程式碼

我們建立了 "DinnerForm" 部分視圖範本，以避免在多個位置複製 view 轉譯邏輯。 這是建立部分視圖範本最常見的原因。

有時候，建立部分視圖還是很合理，即使只是在單一位置呼叫也一樣。 當其 view 轉譯邏輯已解壓縮並分割成一個或多個名稱完整的部分範本時，非常複雜的視圖範本通常會變得更容易閱讀。

例如，請考慮下列網站中的程式碼片段：我們的專案中的主版檔案（我們很快就會看到）。 程式碼相當簡單明瞭，部分是因為在畫面右上方顯示登入/登出連結的邏輯會封裝在 "Logonusercontrol.ascx" 部分中：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

當您發現自己不想要瞭解在視圖範本內的 html/程式碼標記時，請考慮是否要將其中一些元件解壓縮和重構為名稱完整的部分視圖，這樣會變得更清楚。

### <a name="master-pages"></a>主版頁面

除了支援部分視圖以外，ASP.NET MVC 也支援建立「主版頁面」範本的功能，可用來定義網站的一般版面配置和最上層 html。 接著可以將內容預留位置控制項新增至主版頁面，以識別可由 views 覆寫或「填入」的可取代區域。 這提供了一種非常有效率的方法，讓您在應用程式中套用通用版面配置。

根據預設，新的 ASP.NET MVC 專案會自動加入主版頁面範本。 此主版頁面會命名為 "\Views\Shared\"，並存在於下列資料夾中：

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

預設的網站. master 檔案如下所示。 它會定義網站的外部 html，以及頂端導覽的功能表。 其中包含兩個可取代的內容預留位置控制項–一個用於標題，另一個則用於頁面的主要內容取代：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

我們為 NerdDinner 應用程式建立的所有視圖範本（[清單]、[詳細資料]、[編輯]、[建立]、[NotFound] 等等）都是以這個網站為主範本為基礎。 當我們使用 [加入視圖] 對話方塊建立我們的視圖時，會透過預設新增至前 &lt;% @ Page%&gt; 指示詞的 "MasterPageFile" 屬性來表示這種情況：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

這表示我們可以變更網站的內容，並在轉譯任何視圖範本時，自動套用並使用變更。

讓我們更新我們的網站。主要的標頭區段，讓應用程式的標頭是 "NerdDinner"，而不是「我的 MVC 應用程式」。 讓我們也更新導覽功能表，讓第一個索引標籤為「尋找晚餐」（由 HomeController 的 Index （）動作方法處理），並新增名為「主控晚餐」的新索引標籤（由 DinnersController 的 Create （）動作方法處理）：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

當我們儲存網站檔案並重新整理瀏覽器時，我們會看到我們的應用程式內所有視圖的標頭變更會顯示在其中。 例如:

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

並使用 */Dinners/Edit/[id]* URL：

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>後續步驟

部分和主版頁面提供極具彈性的選項，可讓您完全整理視圖。 您會發現它們可協助您避免重複的 view 內容/程式碼，並讓您的視圖範本更容易閱讀和維護。

現在讓我們來回顧我們稍早建立的清單案例，並啟用可調整的分頁支援。

> [!div class="step-by-step"]
> [上一頁](use-viewdata-and-implement-viewmodel-classes.md)
> [下一頁](implement-efficient-data-paging.md)
