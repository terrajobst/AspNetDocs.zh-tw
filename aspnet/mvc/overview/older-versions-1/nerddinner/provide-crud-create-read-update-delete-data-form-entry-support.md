---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: 提供 CRUD （建立、讀取、更新、刪除）資料表單專案支援 |Microsoft Docs
author: microsoft
description: 步驟5顯示如何藉由啟用編輯、建立和刪除 Dinners 的支援，進一步 DinnersController 類別。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: b3123af9a1477bc496a0d229d628510fc202b6d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580553"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>提供 CRUD (建立、讀取、更新、刪除) 資料表單項目支援

由[Microsoft](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟5，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。
> 
> 步驟5顯示如何藉由啟用編輯、建立和刪除 Dinners 的支援，進一步 DinnersController 類別。
> 
> 如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>NerdDinner 步驟5：建立、更新、刪除表單案例

我們引進了控制器和觀點，並涵蓋如何使用它們來在網站上執行 Dinners 的清單/詳細資料體驗。 我們的下一步是進一步讓我們的 DinnersController 類別，並支援編輯、建立和刪除 Dinners。

### <a name="urls-handled-by-dinnerscontroller"></a>DinnersController 處理的 Url

我們先前已將動作方法新增至 DinnersController，以支援兩個 Url： */Dinners*和 */Dinners/Details/[id]* 。

| **URL** | **動詞** | **目的** |
| --- | --- | --- |
| */Dinners/* | GET | 顯示即將推出之 dinners 的 HTML 清單。 |
| */Dinners/Details/[識別碼]* | GET | 顯示特定晚餐的詳細資料。 |

我們現在會新增動作方法來執行三個額外的 Url： */Dinners/Edit/[id]* 、 */Dinners/Create*和 */Dinners/Delete/[id]* 。 這些 Url 可讓您編輯現有的 Dinners、建立新的 Dinners，以及刪除 Dinners。

我們將同時支援 HTTP GET 與 HTTP POST 動詞命令與這些新 Url 的互動。 這些 Url 的 HTTP GET 要求會顯示資料的初始 HTML 視圖（在 "edit" 案例中填入晚餐資料的表單、在 "create" 案例中為空白表單，以及在 "delete" 案例中為刪除確認畫面）。 對這些 Url 的 HTTP POST 要求將會儲存/更新/刪除 DinnerRepository 中的晚餐資料（從該處到資料庫）。

| **URL** | **動詞** | **目的** |
| --- | --- | --- |
| */Dinners/Edit/[識別碼]* | GET | 顯示填入晚餐資料的可編輯 HTML 表單。 |
| POST | 將特定晚餐的表單變更儲存至資料庫。 |
| */Dinners/Create* | GET | 顯示空的 HTML 表單，讓使用者定義新的 Dinners。 |
| POST | 建立新的晚餐，並將其儲存在資料庫中。 |
| */Dinners/Delete/[識別碼]* | GET | 顯示刪除確認畫面。 |
| POST | 從資料庫刪除指定的晚餐。 |

### <a name="edit-support"></a>編輯支援

讓我們從執行「編輯」案例開始。

#### <a name="the-http-get-edit-action-method"></a>HTTP-取得編輯動作方法

我們一開始會先執行編輯動作方法的 HTTP "GET" 行為。 當要求 */Dinners/Edit/[id]* URL 時，將會叫用這個方法。 我們的實現如下所示：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

上述程式碼會使用 DinnerRepository 來取出晚餐物件。 然後，它會使用晚餐物件呈現視圖範本。 因為我們尚未明確地將範本名稱傳遞給*view （）* helper 方法，所以它會使用以慣例為基礎的預設路徑來解析視圖範本：/Views/Dinners/Edit.aspx。

現在讓我們建立這個 view 範本。 若要這麼做，請以滑鼠右鍵按一下 [編輯] 方法，然後選取 [新增視圖] 內容功能表命令：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

在 [新增視圖] 對話方塊中，我們會指示我們將晚餐物件傳遞至我們的 View 範本作為其模型，並選擇自動 scaffold 「編輯」範本：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

當我們按一下 [新增] 按鈕時，Visual Studio 會在 "\Views\Dinners" 目錄中為我們新增 "Edit .aspx" view 範本檔案。 它也會在程式碼編輯器中開啟新的「編輯 .aspx」視圖範本，並以初始的「編輯」 scaffold 執行方式填入，如下所示：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

讓我們對產生的預設 [編輯] scaffold 進行一些變更，並更新編輯檢視範本，使其具有下列內容（這會移除一些我們不想公開的屬性）：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

當我們執行應用程式並要求 *"/Dinners/Edit/1"* URL 時，我們會看到下列頁面：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

我們的視圖所產生的 HTML 標籤如下所示。 這是標準的 HTML –具有 &lt;表單&gt; 元素，可在推送 [儲存] &lt;輸入類型 = "submit"/&gt; 按鈕時，對 */Dinners/Edit/1* URL 執行 HTTP POST。 HTML &lt;輸入類型 = "text"/&gt; 元素已針對每個可編輯的屬性輸出：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html. Html.beginform （）和 Html. TextBox （） Html Helper 方法

我們的 "Edit .aspx" 視圖範本使用數個 "Html Helper" 方法： Html. ValidationSummary （）、Html.beginform （）、Html. TextBox （）和 ValidationMessage （）。 除了為我們產生 HTML 標籤以外，這些 helper 方法還提供內建的錯誤處理和驗證支援。

##### <a name="htmlbeginform-helper-method"></a>Html.beginform （） helper 方法

Html.beginform （） helper 方法是在標記中將 HTML &lt;表單&gt; 元素的輸出。 在我們的編輯 .aspx 視圖範本中，您會發現，使用此C#方法時，我們會套用 "using" 語句。 左大括弧表示 &lt;表單的開頭&gt; 內容，而右大括弧則表示 &lt;/form&gt; 元素的結尾：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

或者，如果您在這類案例中找到 "using" 語句方法非自然，您可以使用 Html.beginform （）和 EndForm （）組合（這會執行相同的動作）：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

呼叫 Html.beginform （）而不使用任何參數，會使其輸出會對目前要求的 URL 執行 HTTP POST 的 form 元素。 這就是為什麼我們的編輯檢視會產生 *&lt;form action = "/Dinners/Edit/1" method = "post"&gt;* 元素。 如果我們想要張貼至不同的 URL，也可以選擇將明確的參數傳遞至 Html.beginform （）。

##### <a name="htmltextbox-helper-method"></a>Html. TextBox （） helper 方法

我們的 Edit .aspx view 會使用 Html. TextBox （） helper 方法來輸出 &lt;輸入類型 = "text"/&gt; 元素：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

上述的 .Html （）方法會採用單一參數，這是用來指定要輸出之 &lt;輸入類型 = "text"/&gt; 元素的 id/name 屬性，以及用來填入 TextBox 值的模型屬性。 例如，我們傳遞至編輯檢視的晚餐物件的「標題」屬性值為「.NET 先期，」，因此我們的 Html. TextBox （"Title"）方法會呼叫 output： *&lt;輸入 id = "title" name = "title" type = "text" value = ". NET 先期，"/&gt;* 。

或者，我們可以使用第一個 Html. TextBox （）參數來指定專案的識別碼/名稱，然後明確地傳入要當做第二個參數使用的值：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

我們通常會想要對輸出的值執行自訂格式。 在這些情況下，內建 .NET 的 String. Format （）靜態方法很有用。 我們的 Edit .aspx view 範本會使用此格式來格式化 EventDate 值（這是 DateTime 類型），因此它不會顯示時間的秒數：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

可以選擇性地使用 Html. TextBox （）的第三個參數來輸出其他 HTML 屬性。 下列程式碼片段示範如何在 &lt;輸入類型 = "text"/&gt; 元素上轉譯額外的 size = "30" 屬性和 class = "mycssclass" 屬性。 請注意，使用「@" character because "類別」來將類別屬性的名稱進行轉義，是中C#保留的關鍵字：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>執行 HTTP POST 編輯動作方法

我們現在已執行編輯動作方法的 HTTP GET 版本。 當使用者要求 */Dinners/Edit/1* URL 時，他們會收到如下所示的 HTML 網頁：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

按 [儲存] 按鈕會導致表單張貼至 */Dinners/Edit/1* URL，並使用 HTTP post 動詞命令提交 HTML &lt;輸入&gt; 的表單值。 現在讓我們來執行編輯動作方法的 HTTP POST 行為–這會處理晚餐的儲存。

首先，我們會將多載的「編輯」動作方法新增至我們的 DinnersController，其上具有 "AcceptVerbs" 屬性，表示它會處理 HTTP POST 案例：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

當 [AcceptVerbs] 屬性套用至多載的動作方法時，ASP.NET MVC 會根據傳入的 HTTP 動詞命令，自動處理分派要求至適當的動作方法。 */Dinners/Edit/[id]* URL 的 HTTP POST 要求將會移至上述的 Edit 方法，而 */Dinners/Edit/[id]* URL 的所有其他 HTTP 動詞要求都會移至我們所實的第一個編輯方法（沒有 `[AcceptVerbs]` 屬性）。

| **側邊主題：為什麼要透過 HTTP 動詞來區分？** |
| --- |
| 您可能會問–為什麼我們要使用單一 URL，並透過 HTTP 指令動詞來區分其行為？ 為什麼不只有兩個不同的 Url 來處理載入和儲存編輯變更？ 例如：/Dinners/Edit/[id] 顯示初始表單，而/Dinners/Save/[id] 則用來處理表單張貼以儲存它嗎？ 發佈兩個不同的 Url 的缺點是，在我們張貼至/Dinners/Save/2，然後因為輸入錯誤而需要重新顯示 HTML 表單的情況下，使用者最後會在其瀏覽器的網址列中擁有/Dinners/Save/2 URL （因為這是表單張貼的 URL）。 如果使用者將此重新顯示頁面的書簽重新顯示到其瀏覽器的 [我的最愛] 清單，或複製/貼上 URL 並以電子郵件傳送給朋友，他們最後會儲存無法在未來使用的 URL （因為該 URL 取決於 post 值）。 藉由公開單一 URL （例如：/Dinners/Edit/[id]）並區分 HTTP 動詞命令的處理方式，使用者可以安全地將編輯頁面加入書簽，並（或）將 URL 傳送給其他人。 |

#### <a name="retrieving-form-post-values"></a>正在抓取表單張貼值

有多種方法可以存取我們的 HTTP POST "Edit" 方法內的張貼表單參數。 一個簡單的方法是只使用控制器基類上的 Request 屬性來存取表單集合，並直接抓取張貼的值：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

上述方法稍加說明，尤其是在我們新增錯誤處理邏輯時。

此案例的更好方法是，在控制器基類上運用內建的*UpdateModel （）* helper 方法。 它支援更新物件的屬性，我們使用傳入的表單參數將其傳遞給它。 它會使用反映來判斷物件上的屬性名稱，然後根據用戶端所提交的輸入值，自動轉換並指派值給它們。

我們可以使用 UpdateModel （）方法，透過下列程式碼來簡化我們的 HTTP POST 編輯動作：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

我們現在可以造訪 */Dinners/Edit/1* URL，並變更晚餐的標題：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

當我們按一下 [儲存] 按鈕時，我們會對編輯動作執行表單張貼，而更新的值將會保存在資料庫中。 接著，我們會將晚餐的詳細資料 URL 重新導向（這會顯示新儲存的值）：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>處理編輯錯誤

我們目前的 HTTP-POST 執行正常運作，除非發生錯誤。

當使用者編輯表單時發生錯誤時，我們必須確定表單會重新顯示，並出現一則資訊性錯誤訊息，引導他們修正此問題。 這包括使用者張貼不正確輸入的情況（例如：格式不正確的日期字串），以及輸入格式有效但有商務規則違規的情況。 發生錯誤時，表單應保留使用者原本輸入的輸入資料，讓他們不需要手動重新填滿變更。 此程式應該在表單成功完成之前，視需要重複多次。

ASP.NET MVC 包含一些好用的內建功能，可讓您輕鬆地進行錯誤處理和表單重新顯示。 若要查看這些功能的作用，讓我們使用下列程式碼來更新編輯動作方法：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

上述程式碼與先前的執行方式類似，不同之處在于我們現在會將 try/catch 錯誤處理區塊包裝在我們的工作周圍。 如果在呼叫 UpdateModel （）時或在嘗試儲存 DinnerRepository 時發生例外狀況（如果我們嘗試儲存的晚餐物件因為在我們的模型中違反規則而無效，則會引發例外狀況），我們的 catch 錯誤處理區塊將會執行. 在此期間，我們會迴圈處理晚餐物件中存在的任何規則違規，並將其新增至 ModelState 物件（我們將在稍後討論）。 然後重新顯示此視圖。

若要查看此工作，讓我們重新執行應用程式、編輯晚餐，然後將它變更為空白標題、EventDate 為「假」，並使用國家/地區值為 USA 的英國電話號碼。 當我們按下 [儲存] 按鈕時，我們的 HTTP POST 編輯方法將無法儲存晚餐（因為有錯誤），並會重新顯示表單：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

我們的應用程式具有適當的錯誤體驗。 具有無效輸入的文字元素會以紅色反白顯示，並向使用者顯示驗證錯誤訊息。 表單也會保留使用者原先輸入的輸入資料，使其不需要重填任何專案。

您可能會問，這是發生的嗎？ [Title]、[EventDate] 和 [ContactPhone] 文字方塊會以紅色反白顯示其本身，並知道要輸出原先輸入的使用者值嗎？ 錯誤訊息如何顯示在頂端的清單中？ 好消息是，這並不是因為神奇而發生，因為我們使用一些內建的 ASP.NET MVC 功能，讓輸入驗證和錯誤處理案例變得很容易。

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>瞭解 ModelState 和驗證 HTML Helper 方法

控制器類別具有 "ModelState" 屬性集合，可提供一種方法來指出與傳遞給視圖的模型物件存在錯誤。 ModelState 集合內的錯誤專案會識別具有問題的模型屬性名稱（例如： "Title"、"EventDate" 或 "ContactPhone"），並允許指定人為易記的錯誤訊息（例如：「需要標題」）。

*UpdateModel （）* helper 方法會在嘗試將表單值指派給模型物件上的屬性時，自動填入 ModelState 集合。 例如，我們晚餐物件的 EventDate 屬性是 DateTime 類型。 當 UpdateModel （）方法在上述案例中無法將字串值「假」指派給它時，UpdateModel （）方法會將專案新增至 ModelState 集合，指出該屬性發生指派錯誤。

開發人員也可以撰寫程式碼，以明確地將錯誤專案新增至 ModelState 集合，如同我們在「catch」錯誤處理區塊內執行的動作，它會根據中的作用中規則違規，將專案填入 ModelState 集合。晚餐物件：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>Html Helper 與 ModelState 的整合

HTML helper 方法-like Html. TextBox （）-在轉譯輸出時檢查 ModelState 集合。 如果專案的錯誤存在，則會轉譯使用者輸入的值和 CSS 錯誤類別。

例如，在我們的「編輯」視圖中，我們會使用 Html. TextBox （） helper 方法來呈現晚餐物件的 EventDate：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

當此視圖在錯誤案例中呈現時，Html. TextBox （）方法會檢查 ModelState 集合，以查看是否有任何與晚餐物件的 "EventDate" 屬性相關聯的錯誤。 當它判定發生錯誤時，它會將提交的使用者輸入（「假」）轉譯為值，並將 css 錯誤類別新增至它所產生的 &lt;輸入類型 = "textbox"/&gt; 標記：

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

您可以自訂 css 錯誤類別的外觀，以尋找您想要的樣子。 預設的 CSS 錯誤類別-「輸入-驗證-錯誤」–定義于 *\content\site.css*樣式表單中，如下所示：

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

此 CSS 規則會導致不正確輸入元素反白顯示，如下所示：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>ValidationMessage （） Helper 方法

ValidationMessage （） helper 方法可以用來輸出與特定模型屬性相關聯的 ModelState 錯誤訊息：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

上述程式碼會輸出： *&lt;span class = "field-驗證-error"&gt; 值 ' 假 '&lt;/span 無效&gt;*

ValidationMessage （） helper 方法也支援第二個參數，可讓開發人員覆寫顯示的錯誤文字訊息：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

上述程式碼會輸出： *&lt;span class = "欄位驗證-錯誤"&gt;\*&lt;/span&gt;* 而不是 EventDate 屬性出現錯誤時的預設錯誤文字。

##### <a name="htmlvalidationsummary-helper-method"></a>ValidationSummary （） Helper 方法

ValidationSummary （） helper 方法可用來轉譯摘要錯誤訊息，伴隨 &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; ModelState 集合中所有詳細錯誤訊息的清單：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

ValidationSummary （） helper 方法會接受選擇性的 string 參數，它會定義摘要錯誤訊息，以顯示在詳細錯誤清單上方：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

您可以選擇性地使用 CSS 來覆寫 [錯誤清單] 的樣子。

#### <a name="using-a-addruleviolations-helper-method"></a>使用 AddRuleViolations Helper 方法

初始的 HTTP POST 編輯執行會使用其 catch 區塊內的 foreach 語句來迴圈晚餐物件的規則違規，並將其新增至控制器的 ModelState 集合：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

我們可以將 "ControllerHelpers" 類別新增至 NerdDinner 專案，並在其中執行「AddRuleViolations」擴充方法，將 helper 方法新增至 ASP.NET MVC ModelStateDictionary 類別，讓這段程式碼更簡潔。 這個擴充方法可以封裝在 ModelStateDictionary 中填入 RuleViolation 錯誤清單所需的邏輯：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

然後，我們可以更新我們的 HTTP POST 編輯動作方法，以使用此延伸模組方法，在 ModelState 集合中填入晚餐規則違規。

#### <a name="complete-edit-action-method-implementations"></a>完成編輯動作方法的執行

下列程式碼會執行編輯案例所需的所有控制器邏輯：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

我們的編輯執行的好處在於，控制器類別和我們的 View 範本都不需要知道晚餐模型所強制執行的特定驗證或商務規則。 我們未來可以在模型中加入其他規則，而不需要對我們的控制器或視圖進行任何程式碼變更，就能加以支援。 如此一來，我們就能彈性地在未來輕鬆開發我們的應用程式需求，並變更最少的程式碼。

### <a name="create-support"></a>建立支援

我們已完成執行 DinnersController 類別的「編輯」行為。 現在讓我們繼續執行它的「建立」支援–這可讓使用者加入新的 Dinners。

#### <a name="the-http-get-create-action-method"></a>HTTP-GET Create 動作方法

我們一開始會先執行建立動作方法的 HTTP 「GET」行為。 當有人造訪 */Dinners/Create* URL 時，將會呼叫這個方法。 我們的執行如下所示：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

上述程式碼會建立新的晚餐物件，並將其 EventDate 屬性指派為未來的一周。 然後，它會呈現以新晚餐物件為基礎的視圖。 因為我們尚未明確地將名稱傳遞給*view （）* helper 方法，所以它會使用以慣例為基礎的預設路徑來解析視圖範本：/Views/Dinners/Create.aspx。

現在讓我們建立這個 view 範本。 若要這麼做，請在 [建立動作] 方法中按一下滑鼠右鍵，然後選取 [新增視圖] 內容功能表命令。 在 [新增視圖] 對話方塊中，我們會指出我們要將晚餐物件傳遞至 View 範本，並選擇自動 scaffold 「建立」範本：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

當我們按一下 [新增] 按鈕時，Visual Studio 會將以 scaffold 為基礎的新 "Create .aspx" 視圖儲存至 "\Views\Dinners" 目錄，並在 IDE 中開啟它：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

讓我們對為我們產生的預設「建立」 scaffold 檔案進行一些變更，並加以修改，如下所示：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

現在當我們執行應用程式並在瀏覽器中存取 *"/Dinners/Create"* URL 時，它會從我們的建立動作執行轉譯如下所示的 UI：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>執行 HTTP POST 建立動作方法

我們已實現建立動作方法的 HTTP GET 版本。 當使用者按一下 [儲存] 按鈕時，它會執行表單張貼至 */Dinners/Create* URL，並使用 HTTP post 動詞命令提交 HTML &lt;輸入&gt; 的表單值。

現在讓我們來執行 create action 方法的 HTTP POST 行為。 我們一開始會先將多載的「建立」動作方法新增至我們的 DinnersController，其上具有 "AcceptVerbs" 屬性，表示它會處理 HTTP POST 案例：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

有多種方式可以在啟用 HTTP POST 的「建立」方法中存取張貼的表單參數。

其中一種方法是建立新的晚餐物件，然後使用*UpdateModel （）* helper 方法（如同我們對 [編輯] 動作所做的），將已張貼的表單值填入其中。 然後，我們可以將它新增至 DinnerRepository、將它保存在資料庫中，然後將使用者重新導向至 [詳細資料] 動作，以使用下列程式碼來顯示新建立的晚餐：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

或者，我們可以使用一種方法，讓我們的 Create （）動作方法接受晚餐物件作為方法參數。 ASP.NET MVC 接著會自動為我們產生新的晚餐物件，並使用表單輸入填入其屬性，然後將它傳遞給我們的動作方法：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

上述動作方法會藉由檢查 ModelState 屬性，確認晚餐物件是否已成功填入表單張貼值。 如果有輸入轉換問題（例如，EventDate 屬性的字串為 "假"），這會傳回 false，而如果有任何問題，則動作方法會重新出現表單。

如果輸入值有效，則動作方法會嘗試新增新晚餐並將其儲存至 DinnerRepository。 它會在 try/catch 區塊中包裝這項工作，並在有任何商務規則違規時重新出現表單（這會造成 dinnerRepository （）方法引發例外狀況）。

若要查看作用中的這個錯誤處理行為，我們可以要求 */Dinners/Create* URL，並填寫新晚餐的詳細資料。 不正確的輸入或值會導致建立表單重新顯示，並醒目提示如下所示的錯誤：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

請注意，我們的建立表單如何接受與編輯表單完全相同的驗證和商務規則。 這是因為我們在模型中定義了驗證和商務規則，而不是內嵌在應用程式的 UI 或控制器中。 這表示我們稍後可以在單一位置變更/發展我們的驗證或商務規則，並將其套用至整個應用程式。 我們不需要變更我們的編輯或建立動作方法內的任何程式碼，就能自動接受任何新規則或對現有的修改。

當我們修正輸入值，然後再按一下 [儲存] 按鈕時，我們對 DinnerRepository 的新增將會成功，而且新的晚餐會新增至資料庫。 接著，我們會將您重新導向至 */Dinners/Details/[id]* URL-，我們會在其中看到新建立的晚餐的詳細資料：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>刪除支援

現在讓我們將「刪除」支援新增至我們的 DinnersController。

#### <a name="the-http-get-delete-action-method"></a>HTTP-GET Delete 動作方法

我們一開始會先執行刪除動作方法的 HTTP GET 行為。 當有人造訪 */Dinners/Delete/[id]* URL 時，就會呼叫這個方法。 以下是實作為：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

動作方法會嘗試取出要刪除的晚餐。 如果晚餐存在，則會根據晚餐物件呈現視圖。 如果物件不存在（或已被刪除），它會傳回一個呈現我們稍早為「詳細資料」動作方法所建立之「NotFound」視圖範本的視圖。

我們可以在 [刪除動作] 方法中按一下滑鼠右鍵，然後選取 [新增視圖] 內容功能表命令，以建立 [刪除] 視圖範本。 在 [新增視圖] 對話方塊中，我們會指出我們會將晚餐物件傳遞至我們的 View 範本作為其模型，並選擇建立空的範本：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

當我們按一下 [新增] 按鈕時，Visual Studio 會在 "\Views\Dinners" 目錄中為我們新增 "Delete .aspx" 視圖範本檔案。 我們會將一些 HTML 和程式碼新增至範本，以執行如下所示的刪除確認畫面：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

上述程式碼會顯示要刪除的晚餐標題，並輸出 &lt;表單&gt; 元素，該專案會在使用者按一下其中的 [刪除] 按鈕時，對/Dinners/Delete/[id] URL 執行 POST。

當我們執行應用程式並存取有效晚餐物件的 *"/Dinners/Delete/[id]"* URL 時，它會呈現如下所示的 UI：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **側邊主題：為什麼要進行貼文？** |
| --- |
| 您可能會問–為什麼我們要在刪除確認畫面中&gt; 建立 &lt;表單的工作？ 為什麼不直接使用標準超連結來連結至執行實際刪除作業的動作方法？ 這是因為我們想要小心預防 web 編目和搜尋引擎探索我們的 Url，並在追蹤這些連結時不小心造成資料被刪除。 以 HTTP 為基礎的 Url 會被視為「安全」，讓它們存取/編目，而且它們應該不會遵循 HTTP POST。 理想的規則是確保您一律將破壞性或資料修改作業放在 HTTP POST 要求後面。 |

#### <a name="implementing-the-http-post-delete-action-method"></a>執行 HTTP POST 刪除動作方法

我們現在已執行刪除動作方法的 HTTP GET 版本，它會顯示刪除確認畫面。 當使用者按一下 [刪除] 按鈕時，它會對 */Dinners/Dinner/[id]* URL 執行表單張貼。

現在，讓我們使用下列程式碼，來執行 delete 動作方法的 HTTP "POST" 行為：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

刪除動作方法的 HTTP POST 版本會嘗試抓取晚餐物件以進行刪除。 如果找不到它（因為它已經被刪除），它會呈現我們的 "NotFound" 範本。 如果找到晚餐，則會將其從 DinnerRepository 中刪除。 然後，它會轉譯「已刪除」範本。

若要執行「已刪除」範本，我們會在動作方法中按一下滑鼠右鍵，然後選擇 [加入視圖] 內容功能表。 我們會將我們的觀點命名為「已刪除」，並讓它成為空的範本（而不是採用強型別模型物件）。 接著，我們會在其中新增一些 HTML 內容：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

現在當我們執行應用程式並存取有效晚餐物件的 *"/Dinners/Delete/[id]"* URL 時，它會轉譯晚餐的刪除確認畫面，如下所示：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

當我們按一下 [刪除] 按鈕時，它會對 */Dinners/Delete/[id]* URL 執行 HTTP POST，這會從我們的資料庫刪除晚餐，並顯示我們的「已刪除」視圖範本：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>模型系結安全性

我們討論了兩種不同的方式，可使用 ASP.NET MVC 的內建模型系結功能。 第一個使用 UpdateModel （）方法來更新現有模型物件上的屬性，而第二個使用 ASP.NET MVC 支援在 as 動作方法參數中傳遞模型物件。 這兩種技術都非常強大，而且非常有用。

這種威力也具有 it 責任。 在接受任何使用者輸入時，一定要擇善固執安全性，而且當您將物件系結至表單輸入時，也會發生這種情況。 請務必小心，一律以 HTML 編碼任何使用者輸入的值，以避免 HTML 和 JavaScript 插入式攻擊，並留意 SQL 插入式攻擊（注意：我們會使用應用程式的 LINQ to SQL，這會自動將參數編碼以避免這些攻擊的類型）。 您絕對不應該依賴用戶端驗證，而且一律會採用伺服器端驗證，以防止駭客嘗試傳送假的值給您。

另一個安全性專案，請確定您在使用 ASP.NET MVC 的系結功能時，是您要系結之物件的範圍。 具體而言，您會想要確定您瞭解允許系結之屬性的安全性含意，並確定您只允許使用者可更新的那些屬性確實是可更新的。

根據預設，UpdateModel （）方法會嘗試更新模型物件上符合傳入表單參數值的所有屬性。 同樣地，當做動作方法參數傳遞的物件，也可以透過表單參數來設定其所有屬性。

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>依據每次使用方式鎖定系結

您可以藉由提供可更新的屬性明確「包含清單」，以根據每次使用來鎖定系結原則。 這可以藉由將額外的字串陣列參數傳遞至 UpdateModel （）方法來完成，如下所示：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

當做動作方法參數傳遞的物件也支援 [Bind] 屬性，可讓您指定允許屬性的「包含清單」，如下所示：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>依據類型鎖定系結

您也可以根據每個類型來鎖定系結規則。 這可讓您指定系結規則一次，然後將它們套用到所有控制器和動作方法的所有案例中（包括 UpdateModel 和動作方法參數案例）。

您可以自訂每個類型的系結規則，方法是將 [Bind] 屬性加入至類型，或在應用程式的 global.asax 檔案中註冊（適用于您不擁有該類型的案例）。 接著，您可以使用 Bind 屬性的 Include 和 Exclude 屬性來控制哪些屬性可系結至特定類別或介面。

我們會針對 NerdDinner 應用程式中的晚餐類別使用這項技術，並在其中新增 [Bind] 屬性，將可系結屬性的清單限制如下：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

請注意，我們不允許透過系結來操作 RSVPs 集合，也不允許透過系結設定 DinnerID 或 HostedBy 屬性。 基於安全性理由，我們只會在動作方法內使用明確的程式碼來操作這些特定屬性。

### <a name="crud-wrap-up"></a>CRUD 總結

ASP.NET MVC 包含一些內建功能，可協助您執行表單張貼案例。 我們使用了各種功能，在我們的 DinnerRepository 之上提供 CRUD UI 支援。

我們使用以模型為主的方法來執行我們的應用程式。 這表示我們的所有驗證和商務規則邏輯都是在模型層內定義，而不是在我們的控制器或 views 內。 我們的控制器類別和我們的視圖範本都不知道晚餐模型類別所強制執行的特定商務規則。

這會讓我們的應用程式架構保持整潔，讓測試更容易。 我們可以在未來的模型層中加入額外的商務規則，而不需要對控制器或視圖*進行任何程式碼變更*，就能加以支援。 如此一來，我們就能在未來發展和變更應用程式，提供極大的靈活性。

我們的 DinnersController 現在會啟用晚餐清單/詳細資料，以及建立、編輯和刪除支援。 類別的完整程式碼可以在下面找到：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>後續步驟

我們現在有基本 CRUD （建立、讀取、更新和刪除）支援在我們的 DinnersController 類別中執行。

現在讓我們來看看如何使用 ViewData 和 ViewModel 類別，在我們的表單上啟用更豐富的 UI。

> [!div class="step-by-step"]
> [上一頁](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [下一頁](use-viewdata-and-implement-viewmodel-classes.md)
