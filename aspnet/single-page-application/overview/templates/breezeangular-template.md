---
uid: single-page-application/overview/templates/breezeangular-template
title: 輕鬆/角度範本 |Microsoft Docs
author: madskristensen
description: 輕鬆/角度單一頁面應用程式範本
ms.author: riande
ms.date: 03/08/2013
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: 3e4e63d385a56d51d3d08696782b43d6228f6201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578537"
---
# <a name="breezeangular-template"></a>Breeze/Angular 範本

依[Mads Kristensen](https://github.com/madskristensen)

> 以 Ward 鐘撰寫的輕鬆/角度 MVC 範本
> 
> [下載簡單/角度 MVC 範本](https://go.microsoft.com/fwlink/?LinkId=286437)

[AngularJS](http://angularjs.org)是 Google 提供的開放原始碼程式庫，可用於建立單一頁面應用程式（spa）。 它提供資料系結、相依性插入，以及螢幕管理。 將它與[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa)、另一個用於資料模型化和資料管理的開放原始碼程式庫結合，而且您有絕佳的 HTML/JavaScript 用戶端應用程式的基本要素。

「輕鬆/角 SPA」範本是 ASP.NET 和 Web 工具2012.2 更新中所包含的[KNOCKOUTJS SPA 範本](../introduction/knockoutjs-template.md)的變化。 如果您有 Visual Studio，就會有一個在60秒內啟動並執行的 SPA 範例。

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

外表，應用程式看起來與 KnockoutJS SPA 範本非常類似。 但它的幕後也非常不同。 KnockoutJS 範本會使用挖的資料系結和原始 AJAX 來進行資料存取。 「簡單」/「角度」範本會使用角度來進行資料系結，並輕鬆地存取資料。 這些程式庫可啟用額外的功能，包括頁面流覽和記錄。

以下是應用程式的 [關於] 頁面：

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

此頁面會在目前的使用者會話期間顯示執行中的事件記錄，包括：

- 速度. 請注意，在 #2 和 #7 建立的 Todo 控制器。
- 遠端查詢（#3）和本機快取查詢（#7）。
- 儲存新的（#5、#6）和修改的（#4）實體。
- 已在用戶端（#9）上驗證變更，讓使用者可以在將變更認可到資料庫之前更正錯誤。

此範本中有更多的流覽功能，包括：

- 動態載入 HTML 視圖範本。
- 透過角度「指示詞」的自訂資料系結。
- 模組化和相依性插入。
- 查詢篩選、排序、分頁、投射和包含相關實體。
- 跨多個畫面共用資料。
- 將多個變更儲存為單一交易。
- 驗證規則會自動從伺服器傳播至 JavaScript 用戶端。

我們現在就開始吧。

## <a name="create-a-breezeangular-template-project"></a>建立輕而易舉/角度的範本專案

按一下上方的 [下載] 按鈕，以下載並安裝範本。 此範本會封裝為 Visual Studio 擴充功能（VSIX）檔案。 您可能需要重新開機 Visual Studio。

在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。 在 **[ C#視覺效果**] 底下，選取 [ **Web**]。 在專案範本清單中，選取 [ **ASP.NET MVC 4 Web 應用程式**]。 為專案命名，然後按一下 [確定]。

在 [**新增專案**] 中，選取 [**輕鬆角 SPA**]。

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

按下 Ctrl-F5 以建立並執行應用程式，而不進行任何偵測，或按 F5 執行以進行偵錯工具。

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

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
- 按一下右上方的 [關於] 連結，以查看這些活動的記錄。

驗證邏輯會輕鬆地在用戶端執行。 伺服器模型類別上的驗證屬性會傳播至用戶端，並在用戶端聯繫伺服器之前自動執行。

檢查網路流量。 請注意，在簡單偵測到錯誤時，並沒有對伺服器的呼叫。 每個有效的變更都會導致 POST 要求「/api/Todo/SaveChanges」。 輕鬆地將變更組合在一起，並以單一要求傳送至 Web API 控制器的 `SaveChanges` 方法。 這與 KnockoutJS SPA 範本不同，它會針對每個專案個別進行 PUT、POST 和 DELETE 要求。

此外，請注意，當您在 TodoList 與 About 頁面之間切換時，不會有任何網路流量。 這是因為查詢已限制為本機簡單快取。

## <a name="peek-inside"></a>查看內部

此應用程式具有用戶端和伺服器端。 用戶端堆疊包含一些 HTML 和應用程式 JavaScript 模組（在「應用程式」資料夾中）和協力廠商 JavaScript 程式庫（在 [腳本] 資料夾中）的組合。

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

UI 架構會將視圖的 HTML widget 與控制器中支援的呈現程式碼區隔開。 角度資料系結系統會協調視圖和控制器，讓每個都可以執行其作業，而不需要深入瞭解另一個。

控制器會要求資料內容取得並儲存模型實體。 資料內容會將大部分的工作委派給輕鬆，這會從 JSON 查詢結果中，建立自我追蹤模型物件。

伺服器端堆疊包含一些開發人員程式碼和三個準則 .NET 程式庫： Web API、Entity Framework 和 Breeze.NET：

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

基本架構與 KnockoutJS SPA 範本相同。 不過，這種做法很簡單：已刪除 Dto，而且大部分的 Entity Framework 詳細資料都已委派給 Breeze.NET。

## <a name="next-steps"></a>後續步驟

我們建議您流覽程式碼，並在「輕鬆的」網站上深入[討論](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa)用戶端和伺服器堆疊。

您可以嘗試使用簡單的用戶端查詢來播放;新增一些篩選準則並進行排序。 您可以新增更多模型屬性和更多實體，以便更容易進行端對端 SPA 的開發。 當您確信此設計時，您可以卸載待辦事項功能，並以您自己的方式取代它們。

祝各位寫程式愉快！
