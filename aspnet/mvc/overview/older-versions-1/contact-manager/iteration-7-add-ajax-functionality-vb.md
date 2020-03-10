---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
title: '反復專案 #7 –新增 Ajax 功能（VB） |Microsoft Docs'
author: microsoft
description: 在第七次的反復專案中，我們藉由新增 Ajax 的支援來改善應用程式的回應性和效能。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f640e063-150e-453d-8cfc-7e54a6ce0f1e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
msc.type: authoredcontent
ms.openlocfilehash: cee2b6e7c7517a1e03ae26d5233fc438857a030c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601651"
---
# <a name="iteration-7--add-ajax-functionality-vb"></a>反復專案 #7 –新增 Ajax 功能（VB）

由[Microsoft](https://github.com/microsoft)

[下載程式代碼](iteration-7-add-ajax-functionality-vb/_static/contactmanager_7_vb1.zip)

> 在第七次的反復專案中，我們藉由新增 Ajax 的支援來改善應用程式的回應性和效能。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>建立連絡人管理 ASP.NET MVC 應用程式（VB）

在這一系列的教學課程中，我們從一開始就建立了整個連絡人管理應用程式。 連絡人管理員應用程式可讓您儲存連絡人資訊名稱、電話號碼和電子郵件地址，以取得人員清單。

我們會透過多個反復專案來建立應用程式。 在每次反覆運算時，我們會逐漸改善應用程式。 這個多個反復專案方法的目標，是要讓您瞭解每項變更的原因。

- 反復專案 #1-建立應用程式。 在第一個反復專案中，我們會以最簡單的方式建立連絡人管理員。 我們新增對基本資料庫作業的支援：建立、讀取、更新和刪除（CRUD）。

- 反復專案 #2-讓應用程式看起來不錯。 在此反復專案中，我們藉由修改預設的 ASP.NET MVC view 主版頁面和級聯樣式表，來改善應用程式的外觀。

- 反復專案 #3-新增表單驗證。 在第三個反復專案中，我們會新增基本表單驗證。 我們會防止人們提交表單，而不需要完成必要的表單欄位。 我們也會驗證電子郵件地址和電話號碼。

- 反復專案 #4-讓應用程式鬆散結合。 在這第四次的反復專案中，我們會利用數種軟體設計模式，讓您更輕鬆地維護和修改 Contact Manager 應用程式。 例如，我們會重構應用程式，以使用存放庫模式和相依性插入模式。

- 反復專案 #5-建立單元測試。 在第五個反復專案中，我們會藉由新增單元測試，讓應用程式更容易維護和修改。 我們會模擬我們的資料模型類別，並為我們的控制器和驗證邏輯建立單元測試。

- 反復專案 #6-使用以測試為導向的開發。 在此第六個反復專案中，我們會先撰寫單元測試，並針對單元測試撰寫程式碼，以將新功能加入至應用程式。 在此反復專案中，我們會新增連絡人群組。

- 反復專案 #7-新增 Ajax 功能。 在第七次的反復專案中，我們藉由新增 Ajax 的支援來改善應用程式的回應性和效能。

## <a name="this-iteration"></a>這個反復專案

在此「連絡人管理員」應用程式的反復專案中，我們會重構應用程式，以利用 Ajax。 藉由利用 Ajax，我們讓應用程式更具回應性。 當我們需要只更新頁面中的特定區域時，我們可以避免轉譯整個頁面。

我們會重構索引視圖，如此一來，每當有人選取新的連絡人群組時，就不需要重新顯示整個頁面。 相反地，當有人按一下連絡人群組時，我們只會更新連絡人清單，並保留其餘的網頁。

我們也會變更刪除連結的運作方式。 我們不會顯示個別的確認頁面，而是顯示 JavaScript 確認對話方塊。 如果您確認要刪除連絡人，則會針對伺服器執行 HTTP 刪除作業，以從資料庫中刪除連絡人記錄。

此外，我們將利用 jQuery 將動畫效果加入至索引視圖。 當從伺服器提取新的連絡人清單時，我們會顯示動畫。

最後，我們將利用 ASP.NET AJAX framework 支援來管理瀏覽器歷程記錄。 當我們執行 Ajax 呼叫來更新連絡人清單時，我們會建立歷程記錄點。 如此一來，瀏覽器的 [回溯] 和 [下一頁] 按鈕就會生效。

## <a name="why-use-ajax"></a>為何要使用 Ajax？

使用 Ajax 有許多優點。 首先，將 Ajax 功能新增至應用程式會導致更好的使用者體驗。 在一般 web 應用程式中，每次使用者執行動作時，整個頁面都必須回傳至伺服器。 每當您執行動作時，瀏覽器就會鎖定，使用者必須等到整個頁面被提取並重新顯示為止。

在桌面應用程式的情況下，這會是無法接受的體驗。 但是，在傳統上，我們在 web 應用程式的情況下會遇到這種不正確的使用者體驗，因為我們並不知道我們可以做得更好。 我們認為這是 web 應用程式的限制，但實際上，這只是我們 imaginations 的限制。

在 Ajax 應用程式中，您不需要讓使用者體驗只是為了更新頁面而終止。 相反地，您可以在背景執行非同步要求來更新頁面。 您不會在部分頁面更新時強制使用者等待。

藉由利用 Ajax，您也可以改善應用程式的效能。 請考慮 Contact Manager 應用程式目前在沒有 Ajax 功能的情況下的運作方式。 當您按一下連絡人群組時，必須重新顯示整個索引視圖。 連絡人清單和連絡人群組清單必須從資料庫伺服器抓取。 所有的資料都必須從 web 伺服器傳遞到網頁瀏覽器。

不過，在我們將 Ajax 功能新增至應用程式之後，我們可以避免在使用者按一下連絡人群組時重新出現整個頁面。 我們不再需要從資料庫抓取連絡人群組。 我們也不需要在網路上推送整個索引視圖。 藉由利用 Ajax，我們減少了資料庫伺服器必須執行的工作量，並減少應用程式所需的網路流量。

## <a name="don-t-be-afraid-of-ajax"></a>千萬別害怕 Ajax

有些開發人員會避免使用 Ajax，因為他們會擔心舊版瀏覽器。 在不支援 JavaScript 的瀏覽器存取時，他們想要確保其 web 應用程式仍可運作。 由於 Ajax 相依于 JavaScript，因此有些開發人員會避免使用 Ajax。

不過，如果您想要瞭解如何執行 Ajax，則可以建立同時使用上層和下層瀏覽器的應用程式。 我們的連絡人管理員應用程式將會使用支援 JavaScript 的瀏覽器，以及不支援的瀏覽器。

如果您使用 Contact Manager 應用程式搭配支援 JavaScript 的瀏覽器，則會有更好的使用者體驗。 例如，當您按一下連絡人群組時，只會更新顯示連絡人的頁面區域。

另一方面，如果您將 Contact Manager 應用程式與不支援 JavaScript 的瀏覽器搭配使用（或已停用 JavaScript），則您會有稍微不需要的使用者體驗。 例如，當您按一下連絡人群組時，整個索引視圖必須回傳至瀏覽器，才能顯示相符的連絡人清單。

## <a name="adding-the-required-javascript-files"></a>新增必要的 JavaScript 檔案

我們必須使用三個 JavaScript 檔案，將 Ajax 功能新增至我們的應用程式。 這三個檔案都包含在新 ASP.NET MVC 應用程式的 [腳本] 資料夾中。

如果您打算在應用程式的多個頁面中使用 Ajax，則在您的應用程式 s 視圖主版頁面中包含必要的 JavaScript 檔案是合理的。 如此一來，JavaScript 檔案就會自動包含在應用程式的所有頁面中。

在您的視圖主版頁面的 &lt;標頭&gt; 標記中新增下列 JavaScript 包含：

[!code-html[Main](iteration-7-add-ajax-functionality-vb/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>重構索引視圖以使用 Ajax

讓我們從修改索引視圖開始，讓按一下連絡人群組只會更新顯示連絡人的視圖區域。 [圖 1] 中的紅色方塊包含我們想要更新的區域。

[![只更新連絡人](iteration-7-add-ajax-functionality-vb/_static/image1.jpg)](iteration-7-add-ajax-functionality-vb/_static/image1.png)

**圖 01**：僅更新連絡人（[按一下以觀看完整大小的影像](iteration-7-add-ajax-functionality-vb/_static/image2.png)）

第一個步驟是將我們想要以非同步方式更新的視圖部分，分別放在不同的部分（view user control）。 顯示 [連絡人] 資料表的 [索引] 視圖區段已移至 [清單 1] 中的部分。

**清單 1-Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample2.aspx)]

請注意，[清單 1] 中的部分與 [索引] 視圖的模型不同。 &lt;% @ Page%&gt; 指示詞中的*Inherits*屬性指定部分繼承自 ViewUserControl&lt;群組&gt; 類別。

更新的索引視圖包含在 [清單 2] 中。

**清單 2-Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample3.aspx)]

在 [清單 2] 中，您應該會注意到已更新的視圖有兩件事。 首先，請注意，移入部分的所有內容都會取代為 RenderPartial （）的呼叫。 第一次要求索引視圖以顯示初始連絡人集時，會呼叫 RenderPartial （）方法。

第二，請注意，用來顯示連絡人群組的 .Html （）已取代為 Html.actionlink （）。 使用下列參數呼叫了 Ajax （）：

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample4.aspx)]

第一個參數表示要顯示的連結文字，第二個參數代表路由值，而第三個參數代表 Ajax 選項。 在此情況下，我們會使用 UpdateTargetId Ajax 選項，指向在 Ajax 要求完成後要更新的 HTML &lt;div&gt; 標記。 我們想要使用新的連絡人清單來更新 &lt;div&gt; 標記。

連絡人控制器的更新索引（）方法包含在 [清單 3] 中。

**清單 3-Controllers\ContactController.vb （Index 方法）**

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample5.vb)]

已更新的 Index （）動作會有條件地傳回兩個專案的其中一個。 如果由 Ajax 要求叫用 Index （）動作，則控制器會傳回部分。 否則，Index （）動作會傳回整個視圖。

請注意，Index （）動作不需要傳回 Ajax 要求所叫用的資料量。 在一般要求的內容中，「索引」動作會傳回所有連絡人群組和所選連絡人群組的清單。 在 Ajax 要求的內容中，Index （）動作只會傳回選取的群組。 Ajax 表示資料庫伺服器上的工作量較少。

在上層和舊版瀏覽器的情況下，我們修改過的索引視圖都適用。 如果您按一下連絡人群組，而且瀏覽器支援 JavaScript，則只會更新包含連絡人清單的視圖區域。 另一方面，如果您的瀏覽器不支援 JavaScript，則會更新整個視圖。

我們更新的索引視圖有一個問題。 當您按一下連絡人群組時，將不會反白顯示選取的群組。 因為群組清單會顯示在 Ajax 要求期間更新的區域之外，所以不會反白顯示正確的群組。 我們將在下一節修正此問題。

## <a name="adding-jquery-animation-effects"></a>新增 jQuery 動畫效果

一般來說，當您按一下網頁中的連結時，可以使用瀏覽器的進度列來偵測瀏覽器是否正在主動提取更新的內容。 另一方面，執行 Ajax 要求時，瀏覽器的進度列不會顯示任何進度。 這可讓使用者擔心。 您如何知道瀏覽器是否已凍結？

有數種方式可讓您向使用者指出執行 Ajax 要求時所執行的工作。 其中一個方法是顯示簡單的動畫。 例如，您可以在 Ajax 要求開始時淡出區域，並在要求完成時淡入區域。

我們將使用 Microsoft ASP.NET MVC 架構隨附的 jQuery 程式庫來建立動畫效果。 更新的索引視圖包含在 [清單 4] 中。

**清單 4-Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample6.aspx)]

請注意，更新的索引視圖包含三個新的 JavaScript 函數。 當您按一下新的連絡人群組時，前兩個函式會使用 jQuery 淡出並淡入連絡人清單。 當 Ajax 要求導致錯誤（例如網路超時）時，第三個函式會顯示錯誤訊息。

第一個函式也會負責反白顯示選取的群組。 Class = selected 屬性會加入至所按元素的父元素（LI 元素）。 同樣地，jQuery 可讓您輕鬆選取正確的專案，並加入 CSS 類別。

這些腳本會透過 AjaxOptions 參數的協助，系結至群組連結。 更新的 Ajax （）方法呼叫看起來像這樣：

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>新增瀏覽器歷程記錄支援

一般來說，當您按一下連結來更新頁面時，您的瀏覽器歷程記錄就會更新。 如此一來，您可以按一下瀏覽器的 [上一頁] 按鈕，將時間移回到頁面的先前狀態。 例如，如果您按一下 [friend 連絡人] 群組，然後按一下 [商務連絡人] 群組，則可以按一下 [瀏覽器上一頁] 按鈕，在選取 [朋友連絡人] 群組時，流覽回頁面的狀態。

可惜的是，執行 Ajax 要求並不會自動更新瀏覽器記錄。 如果您按一下連絡人群組，並使用 Ajax 要求來抓取相符連絡人清單，則不會更新瀏覽器記錄。 選取新的連絡人群組之後，您就無法使用瀏覽器的 [上一頁] 按鈕來流覽回連絡人群組。

如果您想要讓使用者在執行 Ajax 要求之後能夠使用瀏覽器的 [上一頁] 按鈕，則您需要執行更多工作。 您必須利用 ASP.NET AJAX 架構內建的瀏覽器歷程記錄管理功能。

ASP.NET AJAX browser 歷程記錄，您需要做三件事：

1. 將 enableBrowserHistory 屬性設定為 true，以啟用瀏覽器歷程記錄。
2. 當視圖的狀態藉由呼叫 addHistoryPoint （）方法來變更時，儲存歷程記錄點。
3. 當引發導覽事件時，重建視圖的狀態。

更新的索引視圖包含在 [清單 5] 中。

**清單 5-Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample8.aspx)]

在 [清單 5] 中，已在 pageInit （）函數中啟用瀏覽器歷程記錄。 PageInit （）函數也用來設定導覽事件的事件處理常式。 每當瀏覽器的 [轉寄] 或 [上一頁] 按鈕導致頁面的狀態變更時，就會引發 [導覽] 事件。

當您按一下連絡人群組時，會呼叫 beginContactList （）方法。 這個方法會藉由呼叫 addHistoryPoint （）方法來建立新的記錄點。 已按下之連絡人群組的識別碼會新增至 [歷程記錄]。

系統會從 contact 群組連結上的 expando 屬性來抓取群組識別碼。 連結會以下列對 Ajax 的呼叫來呈現（）。

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample9.aspx)]

傳遞至 Ajax 的最後一個參數（）會將名為 groupid 的 expando 屬性加入至連結（XHTML 相容性為小寫）。

當使用者點擊瀏覽器的 [上一頁] 或 [下一頁] 按鈕時，就會引發導覽事件並呼叫導覽（）方法。 這個方法會更新頁面中顯示的連絡人，以符合與傳遞至導覽方法之瀏覽器歷程記錄點對應的頁面狀態。

## <a name="performing-ajax-deletes"></a>執行 Ajax 刪除

目前若要刪除連絡人，您必須按一下 [刪除] 連結，然後按一下 [刪除確認] 頁面中顯示的 [刪除] 按鈕（請參閱 [圖 2]）。 這似乎很多頁面要求，可以執行像是刪除資料庫記錄的簡單動作。

[![[刪除確認] 頁面](iteration-7-add-ajax-functionality-vb/_static/image2.jpg)](iteration-7-add-ajax-functionality-vb/_static/image3.png)

**圖 02**：刪除確認頁面（[按一下以查看完整大小的影像](iteration-7-add-ajax-functionality-vb/_static/image4.png)）

略過刪除確認頁面，並直接從索引視圖刪除連絡人是很吸引人的。 您應該避免這個誘惑，因為採取此方法會將您的應用程式開啟至安全性漏洞。 一般來說，您不會想要在叫用修改 web 應用程式狀態的動作時，執行 HTTP GET 作業。 執行刪除時，您會想要執行 HTTP POST，或更好的 HTTP 刪除作業。

[刪除] 連結包含在 ContactList 部分中。 [清單 6] 中包含 ContactList 部分的更新版本。

**清單 6-Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample10.aspx)]

[刪除] 連結會使用下列 ImageActionLink （）方法的呼叫來呈現：

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample11.aspx)]

> [!NOTE] 
> 
> ImageActionLink （）不是 ASP.NET MVC 架構的標準部分。 ImageActionLink （）是包含在 Contact Manager 專案中的自訂 helper 方法。

AjaxOptions 參數有兩個屬性。 首先，Confirm 屬性是用來顯示快捷方式 JavaScript 確認對話方塊。 第二，HttpMethod 屬性是用來執行 HTTP 刪除作業。

[清單 7] 包含新的 AjaxDelete （）動作，已新增至連絡人控制器。

**清單 7-Controllers\ContactController.vb （AjaxDelete）**   

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample12.vb)]

AjaxDelete （）動作會以 AcceptVerbs 屬性裝飾。 除了 HTTP 刪除作業以外的任何 HTTP 作業以外，此屬性可防止叫用動作。 特別是，您無法使用 HTTP GET 叫用此動作。

刪除資料庫記錄之後，您必須顯示未包含已刪除記錄之連絡人的更新清單。 AjaxDelete （）方法會傳回 ContactList 部分和更新的連絡人清單。

## <a name="summary"></a>總結

在此反復專案中，我們已將 Ajax 功能新增至我們的 Contact Manager 應用程式。 我們使用 Ajax 來改善應用程式的回應性和效能。

首先，我們重構了索引視圖，因此按一下連絡人群組並不會更新整個視圖。 相反地，按一下連絡人群組只會更新連絡人清單。

接下來，我們使用 jQuery 動畫效果淡出並淡入連絡人清單中。 將動畫新增至 Ajax 應用程式，可以用來提供應用程式的使用者，使其具有對等的瀏覽器進度列。

我們也將瀏覽器歷程記錄支援新增至我們的 Ajax 應用程式。 我們已讓使用者按一下瀏覽器的 [上一頁] 和 [下一頁] 按鈕，以變更索引視圖的狀態。

最後，我們建立了支援 HTTP 刪除作業的刪除連結。 藉由執行 Ajax delete，我們可以讓使用者刪除資料庫記錄，而不需要使用者要求額外的刪除確認頁面。

> [!div class="step-by-step"]
> [上一篇](iteration-6-use-test-driven-development-vb.md)
