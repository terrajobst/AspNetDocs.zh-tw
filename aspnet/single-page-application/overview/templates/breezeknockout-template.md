---
uid: single-page-application/overview/templates/breezeknockout-template
title: 輕鬆/挖的範本 |Microsoft Docs
author: madskristensen
description: 輕鬆/挖以單一頁面應用程式範本
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 3bd94827-3c59-448f-abc3-36e6df4858db
msc.legacyurl: /single-page-application/overview/templates/breezeknockout-template
msc.type: authoredcontent
ms.openlocfilehash: 5bb9ee8f758a25afa6baf3ccbaf7d5864754c7df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558188"
---
# <a name="breezeknockout-template"></a>Breeze/Knockout 範本

依[Mads Kristensen](https://github.com/madskristensen)

> 輕鬆/挖加上的 MVC 範本是由 Ward 鐘撰寫的
> 
> [下載輕鬆/挖的 MVC 範本](https://go.microsoft.com/fwlink/?LinkId=282649)

您聽說過「單頁應用程式」（SPA），並想知道它是什麼。 雖然您可以閱讀這方面的資訊，但還是可以親自體驗。 但誰有時間下載範例？ 如果您有 Visual Studio，就會有一個在60秒內啟動並執行的 SPA 範例，其中包含 ASP.NET MVC 4 「輕鬆/挖使單一頁面應用程式」範本。

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

## <a name="what-is-the-breezeknockout-spa-template"></a>什麼是「輕鬆/挖空的 SPA」範本？

大部分的專案範本都會產生應用程式基本架構。 您可以藉由新增程式碼，並最終提供可運作的應用程式，來為這些骨骼加上充實。 「輕鬆/挖的 SPA」範本不同。 它會產生一個範例應用程式，供您進行研究。 它示範了 SPA 應用程式設計，以及許多用來建立 SPA 的技術。

「輕鬆/挖加」範本是 ASP.NET 和 Web 工具2012.2 更新中所包含的[KNOCKOUTJS SPA 範本](../introduction/knockoutjs-template.md)的變化。 「輕而易舉的 SPA」範本會產生具有相同使用者體驗的應用程式，但它有不同的執行方式，使用輕鬆進行資料管理。

KnockoutJS SPA 範本會使用原始 jQuery AJAX 提出服務要求，這對簡單的應用程式而言是足夠的。 但是更複雜的應用程式會有更嚴苛的資料管理需求。 例如，大部分的應用程式：

- 在擴充的使用者會話期間查詢和重新查詢伺服器。
- 加入查詢篩選、排序和分頁。
- 跨多個畫面共用相同的資料。
- 累積對許多物件所做的變更，然後將其儲存為單一交易。
- 驗證用戶端上的變更，讓使用者可以在將變更認可到資料庫之前更正錯誤。

BreezeJS 程式庫會為您處理這些工作，讓您能夠開發出最重要的應用程式邏輯和使用者體驗。

「簡單[ **」是一種開放**](http://www.breezejs.com/?utm_source=ms-spa)原始碼程式庫，可用於以 JAVASCRIPT 和 HTML 建立豐富的資料應用程式，這類應用程式在過去是以獨立桌面應用程式的形式提供。

輕鬆/挖使範本可協助您將第一個重要的步驟帶往更穩固的資料管理基礎結構。 它會產生一個與 KnockoutJS SPA 範本相同的範例待辦事項應用程式外表。 在內部，它會以輕鬆的方式取代 AJAX 資料層，因此您可以並排比較這兩個方法。 當然，它幾乎不會觸及應用程式的潛能。 但是，您將會看到多麼簡單，以及需要多少時間才能進行轉換。

我們現在就開始吧。

## <a name="create-a-breezeknockout-template-project"></a>建立輕鬆/挖的範本專案

按一下上方的 [下載] 按鈕，以下載並安裝範本。 此範本會封裝為 Visual Studio 擴充功能（VSIX）檔案。 您可能需要重新開機 Visual Studio。

在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。 在 **[ C#視覺效果**] 底下，選取 [ **Web**]。 在專案範本清單中，選取 [ **ASP.NET MVC 4 Web 應用程式**]。 為專案命名，然後按一下 [確定]。

在 [**新增專案**] 中，選取 [**輕鬆挖對 SPA**]。

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeKOSpaTemplate.png)

按下 Ctrl-F5 以建立並執行應用程式，而不進行任何偵測，或按 F5 執行以進行偵錯工具。

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

當應用程式第一次執行時，它會顯示登入畫面。 按一下 [註冊] 連結和新的頁面 glides 至 [觀看]，您可以在其中輸入使用者名稱和密碼。 （登入和註冊頁面會使用 ASP.NET MVC 建立）。當您提交註冊表單時，伺服器會為您的帳戶產生包含兩個專案的 TodoList。 然後，它會以黃色附注呈現給您。

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

現在您已在 SPA 的土地。 您在操作 Todo 時所看到及體驗的所有內容，都是在用戶端上轉譯和管理，並具有挖得的説明。 以使用者身分探索應用程式 。 但是有了開發人員的目光。 使用瀏覽器中的開發人員工具來捕捉網路流量。 （在 Internet Explorer 中：按 F12，選取 [**網路**] 索引標籤，然後按一下 [**開始捕獲**]）。現在請嘗試下列動作：

- 新增待辦事項專案。
- 按一下標籤，然後編輯待辦事項專案標題
- 核取核取方塊，將專案標示為已完成。 請注意，textbox 已停用，因此標題已無法再編輯。
- 按一下標籤右邊的 [x]。 專案會消失，並從資料庫中刪除。
- 挑選另一個專案並清除其標題。 您會收到需要標題的驗證錯誤。 短暫暫停之後，就會還原先前的標題。
- 輸入非常的長標題。 您會收到不同的驗證錯誤，指出標題太長。
- 按一下 [新增待辦事項清單] 按鈕。 新的清單就會出現在先前清單的左邊。
- 播放 TodoList 標題，觸發其必要和長度驗證。
- 按一下 [標題] 文字方塊，以清除錯誤訊息。
- 按一下右上角圓形中的 "x"，以刪除 TodoList 及其 todo。

驗證邏輯會輕鬆地在用戶端執行。 伺服器模型類別上的驗證屬性會傳播至用戶端，並在用戶端聯繫伺服器之前自動執行。

檢查網路流量。 請注意，在簡單偵測到錯誤時，並沒有對伺服器的呼叫。 每個有效的變更都會導致 POST 要求「/api/Todo/SaveChanges」。 輕鬆地將變更組合在一起，並以單一要求傳送至 Web API 控制器的 `SaveChanges` 方法。 這與 KnockoutJS SPA 範本不同，它會針對每個專案個別進行 PUT、POST 和 DELETE 要求。

## <a name="peek-inside"></a>查看內部

此應用程式具有用戶端和伺服器端。 用戶端堆疊包含一些 HTML 和應用程式 JavaScript 模組（在「應用程式」資料夾中）和協力廠商 JavaScript 程式庫（在 [腳本] 資料夾中）的組合。

![](http://www.breezejs.com/sites/all/images/spa-template/ClientArchitecture.png)

如果您已經調查過 KnockoutJS SPA 範本，這看起來應該很熟悉。 將焦點放在藍色方塊上。 UI 架構是 ViewModel （MVVM），在此模式中，視圖的 HTML widget 會與視圖模型中支援的呈現程式碼完全分離。 資料系結系統（在此案例中為「挖式」）會協調視圖和視圖模型，讓每個都可以執行其工作，而不需要深入瞭解另一個。

此模型會封裝 Todo 資料。 模型中的實體是藉由「挖的可觀察屬性」輕鬆地建立的，因此可以直接系結至視圖中的小工具。 視圖模型會要求資料內容取得並儲存模型實體。 資料內容會委派大部分的工作，使其變得輕而易舉。

伺服器端堆疊包含一些開發人員程式碼和三個準則 .NET 程式庫： Web API、Entity Framework 和 Breeze.NET：

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

基本架構與 KnockoutJS SPA 範本相同。 不過，這種做法很簡單：已刪除 Dto，而且大部分的 Entity Framework 詳細資料都已委派給 Breeze.NET。

## <a name="next-steps"></a>後續步驟

我們建議您流覽程式碼，並在「輕鬆的」網站上深入[討論](http://www.breezejs.com/spa-template?utm_source=ms-spa)用戶端和伺服器堆疊。

您可以嘗試使用簡單的用戶端查詢來播放;新增一些篩選準則並進行排序。 您可以新增更多模型屬性和更多實體，以便更容易進行端對端 SPA 的開發。 當您確信此設計時，您可以卸載待辦事項功能，並以您自己的方式取代它們。

很快地，您就可以開始進行下一個重要步驟：新增用戶端畫面並在其中導覽。 您會將此 SPA 範本留在後方，然後轉變成更完整的 SPA 堆疊，例如[John Papa 的熱門紙巾](https://github.com/johnpapa/HotTowel#readme "熱門紙巾")，這會將 durandal 等架構新增至輕鬆且挖加上的混合。
