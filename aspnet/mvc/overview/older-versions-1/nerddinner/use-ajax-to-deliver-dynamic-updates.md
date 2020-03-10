---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: 使用 AJAX 傳遞動態更新 |Microsoft Docs
author: microsoft
description: 步驟10會使用以 Ajax 為基礎的方法（在晚餐詳細資料內整合），將登入使用者的支援回復為出席晚餐的相關資訊 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 3edc02fec546609505b5e085440fa684abe7acd0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600846"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a>使用 AJAX 傳送動態更新

由[Microsoft](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟10，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。
> 
> 步驟10會使用在晚餐詳細資料頁面中整合的以 Ajax 為基礎的方法，來支援已登入的使用者，讓他們有興趣參加晚餐。
> 
> 如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>NerdDinner 步驟10： AJAX 啟用 RSVPs 接受

現在讓我們開始支援已登入的使用者，以在參與晚餐時將其感興趣。 我們會使用在晚餐詳細資料頁面中整合的 AJAX 型方法來啟用此程式。

### <a name="indicating-whether-the-user-is-rsvpd"></a>指出使用者是否為 RSVP

使用者可以造訪 */Dinners/Details/[id*] URL，以查看特定晚餐的詳細資料：

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

Details （）動作方法會實作為，如下所示：

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

執行 RSVP 支援的第一個步驟是將「IsUserRegistered （使用者名稱）」 helper 方法新增至晚餐物件（在我們先前建立的 Dinner.cs 部分類別中）。 此 helper 方法會傳回 true 或 false，取決於使用者目前是否為晚餐的 RSVP：

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

然後，我們可以將下列程式碼加入至 Details view 範本，以顯示適當的訊息，指出是否已針對事件註冊使用者：

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

現在當使用者造訪晚餐時，他們會看到下列訊息：

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

而當他們造訪晚餐時，他們就會看到下列訊息：

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>執行 Register 動作方法

現在讓我們新增必要的功能，讓使用者可以從 [詳細資料] 頁面取得晚餐。

若要執行這項操作，我們將建立新的 "RSVPController" 類別，方法是以滑鼠右鍵按一下 \Controllers 目錄，然後選擇 [新增-&gt;控制器] 功能表命令。

我們會在新的 RSVPController 類別內執行「註冊」動作方法，以取得晚餐的識別碼做為引數、抓取適當的晚餐物件、檢查登入的使用者目前是否在已註冊它的使用者清單中，以及請勿為他們新增 RSVP 物件：

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

請注意，我們如何傳回簡單字串做為動作方法的輸出。 我們可以將此訊息內嵌在視圖範本中，但因為它很小，所以我們只會在控制器基類上使用 Content （） helper 方法，並傳回上述的字串訊息。

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>使用 AJAX 呼叫 RSVPForEvent 動作方法

我們將使用 AJAX，從我們的詳細資料檢視叫用 Register 動作方法。 這麼做非常簡單。 首先，我們要新增兩個腳本程式庫參考：

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

第一個程式庫參考核心 ASP.NET AJAX 用戶端腳本程式庫。 此檔案大約24k 大小（已壓縮），並包含核心用戶端 AJAX 功能。 第二個程式庫包含公用程式函式，這些函式會與 ASP.NET MVC 的內建 AJAX helper 方法整合（我們很快就會用到）。

然後，我們可以更新稍早新增的視圖範本程式碼，讓您不會輸出「您未註冊此事件」訊息，我們會改為轉譯連結，以在推播的情況下執行可在我們的 RSVP 控制器上叫用 RSVPForEvent 動作方法的 AJAX 呼叫並 RSVPs 使用者：

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

上述使用的 Ajax （） helper 方法是內建的 ASP.NET MVC，類似于 Html.actionlink （） helper 方法，不同之處在于，它不會執行標準導覽，而是在按一下連結時，對動作方法進行 AJAX 呼叫。 在上述情況中，我們會在 "RSVP" 控制器上呼叫 "Register" 動作方法，並將 DinnerID 當做 "id" 參數傳遞給它。 我們所傳遞的最後一個 AjaxOptions 參數指出我們想要從動作方法傳回的內容，並更新頁面上的 HTML &lt;div&gt; 元素，其識別碼為 "rsvpmsg"。

現在，當使用者流覽至尚未註冊的晚餐時，他們會看到其 RSVP 的連結：

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

如果他們按一下「此事件的 RSVP」連結，他們會對 RSVP 控制器上的 Register 動作方法進行 AJAX 呼叫，當它完成時，就會看到如下所示的更新訊息：

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

進行此 AJAX 呼叫時，所需的網路頻寬和流量非常輕量。 當使用者按一下「此事件的 RSVP」連結時，會對 */Dinners/Register/1* URL 提出小型的 HTTP POST 網路要求，如下圖所示：

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

而來自我們的 Register 動作方法的回應只是：

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

這個輕量呼叫很快，而且即使在慢速網路也能正常執行。

### <a name="adding-a-jquery-animation"></a>新增 jQuery 動畫

我們所實行的 AJAX 功能既順暢又快速。 不過，有時可能會發生這種情況，因為使用者可能不會注意到 RSVP 連結已被新文字取代。 為了讓結果變得更明顯，我們可以加入簡單的動畫，將注意力吸引更新訊息。

預設 ASP.NET MVC 專案範本包含 jQuery – Microsoft 也支援的絕佳（且非常熱門）開放原始碼 JavaScript 程式庫。 jQuery 提供許多功能，包括美觀的 HTML DOM 選擇和效果程式庫。

若要使用 jQuery，我們會先新增腳本參考。 因為我們會在網站內的各種地方使用 jQuery，所以我們會在網站中新增腳本參考。主版分頁檔案，讓所有頁面都可以使用它。

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*秘訣：請確定您已安裝適用于 VS 2008 SP1 的 JavaScript intellisense，針對 JavaScript 檔案啟用更豐富的 intellisense 支援（包括 jQuery）。您可以從下列下載： http://tinyurl.com/vs2008javascripthotfix*

使用 JQuery 撰寫的程式碼通常會使用全域 "$ （）" JavaScript 方法，以使用 CSS 選取器來抓取一或多個 HTML 元素。 例如， *$ （"#rsvpmsg"）* 會選取識別碼為 rsvpmsg 的任何 HTML 元素，而 *$ （". elements"）* 會選取所有具有 "elements" CSS 類別名稱的專案。 您也可以使用選取器查詢（例如： *$ （"input [@type= 單選] [@checked]"）* ，撰寫更多先進的查詢，例如「傳回所有已核取的選項按鈕」。

選取專案之後，您可以在其上呼叫方法來採取動作，例如隱藏它們： *$ （"#rsvpmsg"）。 hide （）;*

在我們的 RSVP 案例中，我們將定義名為 "AnimateRSVPMessage" 的簡單 JavaScript 函式，以選取 "rsvpmsg" &lt;div&gt; 並以動畫呈現其文字內容的大小。 下列程式碼會啟動小型文字，然後讓它在400毫秒的時間範圍內增加：

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

接著，我們就可以在 AJAX 呼叫成功完成後呼叫這個 JavaScript 函式，方法是將其名稱傳遞至我們的 Ajax （） helper 方法（透過 AjaxOptions "OnSuccess" 事件屬性）：

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

現在，當您按一下「此事件的 RSVP」連結，而我們的 AJAX 呼叫成功完成時，送回的內容訊息會以動畫顯示並成長大：

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

除了提供 "OnSuccess" 事件之外，AjaxOptions 物件也會公開您可以處理的 OnBegin、OnFailure 和 OnComplete 事件（以及各種其他屬性和實用的選項）。

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>清除-重構 RSVP 部分視圖

我們的 details （詳細資料檢視）範本開始變得很長，這會讓您更難瞭解。 為了協助改善程式碼的可讀性，讓我們藉由建立部分視圖– RSVPStatus，封裝詳細資料頁面的所有 RSVP 視圖程式碼來完成。

若要這麼做，請以滑鼠右鍵按一下 [\Views\Dinners] 資料夾，然後選擇 [新增-&gt;View] 功能表命令。 我們會將晚餐物件做為其強型別 ViewModel。 然後，我們可以從詳細資料 .aspx 視圖將 RSVP 內容複寫/貼上到其中。

完成之後，讓我們另外建立另一個部分視圖– EditAndDeleteLinks，用來封裝我們的編輯和刪除連結視圖程式碼。 我們也會將晚餐物件當做其強型別 ViewModel，並將 Edit 和 Delete 邏輯從我們的詳細資料 .aspx 視圖複製/貼上。

然後，我們的詳細資料檢視範本就可以在底部加入兩個 RenderPartial （）方法呼叫：

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

這可讓程式碼更簡潔地進行讀取和維護。

### <a name="next-step"></a>後續步驟

現在讓我們來看看如何進一步使用 AJAX，並在應用程式中加入互動式對應支援。

> [!div class="step-by-step"]
> [上一頁](secure-applications-using-authentication-and-authorization.md)
> [下一頁](use-ajax-to-implement-mapping-scenarios.md)
