---
uid: single-page-application/overview/templates/emberjs-template
title: EmberJS 範本 |Microsoft Docs
author: xqiu
description: EmberJS 範本
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 1aefa46dd0841b1b06675409cc8a09f9a218d7ac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578502"
---
# <a name="emberjs-template"></a>EmberJS 範本

依[Xinyang Qiu](https://github.com/xqiu)

> EmberJS MVC 範本是由 Nathan Totten、Thiago Santos 和 Xinyang Qiu 所撰寫。
> 
> [下載 EmberJS MVC 範本](https://go.microsoft.com/fwlink/?LinkId=282647)

EmberJS SPA 範本的設計可讓您開始使用 EmberJS 快速建立互動式用戶端 web 應用程式。

「單頁應用程式」（SPA）是 web 應用程式的一般詞彙，它會載入單一 HTML 頁面，然後動態更新頁面，而不是載入新的頁面。 載入初始頁面之後，SPA 會透過 AJAX 要求與伺服器交談。

![](emberjs-template/_static/image1.png)

AJAX 是新的，但目前有 JavaScript 架構，可讓您更輕鬆地建立和維護大型的 SPA 應用程式。 此外，HTML 5 和 CSS3 可讓您更輕鬆地建立豐富的 Ui。

EmberJS SPA 範本會使用[Ember.js](http://emberjs.com/) JavaScript 程式庫來處理來自 AJAX 要求的頁面更新。 Ember.js 會使用資料系結來同步處理頁面與最新的資料。 如此一來，您就不需要撰寫任何逐步解說 JSON 資料並更新 DOM 的程式碼。 相反地，您會將宣告式屬性放在 HTML 中，告訴 Ember.js 如何呈現資料。

在伺服器端，EmberJS 範本與[KNOCKOUTJS SPA 範本](../introduction/knockoutjs-template.md)幾乎完全相同。 它會使用 ASP.NET MVC 來提供 HTML 檔案，並 ASP.NET Web API 來處理來自用戶端的 AJAX 要求。 如需範本相關層面的詳細資訊，請參閱[KnockoutJS 範本](../introduction/knockoutjs-template.md)檔。 本主題著重于挖的範本與 EmberJS 範本之間的差異。

## <a name="create-an-emberjs-spa-template-project"></a>建立 EmberJS SPA 範本專案

按一下上方的 [下載] 按鈕，以下載並安裝範本。 您可能需要重新開機 Visual Studio。

在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。 在 **[ C#視覺效果**] 底下，選取 [ **Web**]。 在專案範本清單中，選取 [ **ASP.NET MVC 4 Web 應用程式**]。 為專案命名，然後按一下 [確定]。

![](emberjs-template/_static/image2.png)

在 [**新增專案**] 中，選取 [ember.js] [SPA] [**專案**]。

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a>EmberJS SPA 範本總覽

EmberJS 範本使用 jQuery、Ember.js、Handlebars 的組合來建立流暢的互動式 UI。

Ember.js 是使用用戶端 MVC 模式的 JavaScript 程式庫。

- 以 Handlebars 範本化語言撰寫的*範本*會描述應用程式使用者介面。 在發行模式中， [Handlebars 編譯器](https://github.com/Myslik/csharp-ember-handlebars)是用來組合和編譯 Handlebars 範本。
- *模型*會儲存從伺服器取得的應用程式資料（todo 清單和 todo 專案）。
- *控制器*會儲存應用程式狀態。 控制器通常會向對應的範本呈現模型資料。
- 「*視圖*」會從應用程式轉譯基本事件，並將它們傳遞至控制器。
- *路由器*會管理應用程式狀態，讓 url 和範本保持同步。

此外，Ember.js 資料連結庫可以用來同步處理 JSON 物件（透過 RESTful API 從伺服器取得）和用戶端模型。

EmberJS SPA 範本會將腳本組織成八個層級：

- webapi\_adapter、webapi\_序列化程式：擴充 Ember.js 資料連結庫以與 ASP.NET Web API 搭配使用。
- Scripts/helper .js：定義新的 Ember.js Handlebars helper。
- Scripts/node.js：建立應用程式並設定介面卡和序列化程式。
- Scripts/app/模型/\*.js：定義模型。
- Scripts/app/views/\*.js：定義 views。
- 腳本/應用程式/控制器/\*.js：定義控制器。
- Scripts/app/route、Scripts/app/node.js：定義路由。
- Templates/\*. hbs：定義 handlebars 範本。

讓我們更詳細地查看其中一些腳本。

## <a name="models"></a>模型

這些模型定義于 [腳本/應用程式/模型] 資料夾中。 有兩個模型檔案： todoItem 和 todoList。

**todo。 model .js**會定義待辦事項清單的用戶端（瀏覽器）模型。 有兩個模型類別： todoItem 和 todoList。 在 Ember.js 中，模型是 DS 的子類別。模組. 模型可以具有屬性（attribute）：

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

模型可以定義與其他模型的關聯性：

[!code-css[Main](emberjs-template/samples/sample2.css)]

模型可以有系結至其他屬性的計算屬性：

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

模型可以具有觀察者函式，當觀察到的屬性變更時，就會叫用這些函數：

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a>檢視

這些 views 會定義在 Scripts/app/views 資料夾中。 「視圖」會從應用程式 UI 轉譯事件。 事件處理常式可以回呼控制器函式，或直接呼叫資料內容。

例如，下列程式碼來自 views/TodoItemEditView。 它會定義輸入文字欄位的事件處理。

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a>控制器

這些控制器定義于 [腳本/應用程式/控制器] 資料夾中。 若要表示單一模型，請擴充 `Ember.ObjectController`：

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

控制器也可以藉由擴充 `Ember.ArrayController`來代表模型的集合。 例如，Todolistcontroller.cs」代表 `todoList` 物件的陣列。 控制器會依 todoList 識別碼排序（以遞減順序）：

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

控制器會定義名為 `addTodoList`的函式，此函式會建立新的 todoList，並將它新增至陣列。 若要查看如何呼叫此函式，請在 [範本] 資料夾中開啟名為 todoListTemplate 的範本檔案。 下列範本程式碼會將按鈕系結至 `addTodoList` 函式：

[!code-html[Main](emberjs-template/samples/sample8.html)]

控制器也包含一個 `error` 屬性，它會保存一則錯誤訊息。 以下是用來顯示錯誤訊息的範本程式碼（也是在 todoListTemplate 中）：

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a>路由

Node.js 會定義要顯示的路由和預設範本、設定應用程式狀態，以及與路由的 Url 相符：

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

TodoListRoute 會藉由覆寫 setupController 函式來載入 TodoListRoute 的資料：

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

Ember.js 會使用命名慣例來比對 Url、路由名稱、控制器和範本。 如需詳細資訊，請參閱 EmberJS 檔中的[http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) 。

## <a name="templates"></a>範本

Templates 資料夾包含四個範本：

- hbs：啟動應用程式時所呈現的預設範本。
- 關於 hbs： "/about" 路由的範本。
- hbs：根 "/" 路由的範本。
- todoList. hbs： "/todo" 路由的範本。
- \_hbs：範本會定義導覽功能表。

應用程式範本的作用就像主版頁面。 其中包含標頭、頁尾和 "{{輸出口}}"，以根據路由在中插入其他範本。 如需 Ember.js 中應用程式範本的詳細資訊，請參閱[http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/)。

"/TodoList" 範本包含兩個迴圈運算式。 外部迴圈會 `{{#each controller}}`，且 `{{#each todos}}`內的迴圈。 下列程式碼顯示內建的 `Ember.Checkbox` view、自訂的 `App.TodoItemEditView`，以及具有 `deleteTodo` 動作的連結。

[!code-html[Main](emberjs-template/samples/sample12.html)]

在 web.config 檔案中，當**debug**設定為**true**時，在 controller/HtmlHelperExtensions 中定義的 `HtmlHelperExtensions` 類別會定義 helper 函式來快取和插入範本檔案。 此函式是從 Views/Home/App.config 中定義的 ASP.NET MVC view 檔案呼叫：

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

呼叫不含引數的函式時，函式會轉譯 Templates 資料夾中的所有範本檔案。 您也可以指定子資料夾或特定的範本檔案。

當 web.config 中的**debug**為**false**時，應用程式會包含配套專案 "~/bundles/templates"。 使用 Handlebars 編譯器程式庫，在 BundleConfig.cs 中新增此配套專案：

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
