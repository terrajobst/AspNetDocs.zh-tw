---
uid: single-page-application/overview/introduction/knockoutjs-template
title: 單一頁面應用程式： KnockoutJS 範本 |Microsoft Docs
author: MikeWasson
description: 挖的範本
ms.author: riande
ms.date: 01/30/2013
ms.assetid: f9c07af0-4b20-4b08-af8f-47fc3df169a2
msc.legacyurl: /single-page-application/overview/introduction/knockoutjs-template
msc.type: authoredcontent
ms.openlocfilehash: 3a551db1caa9636eb7f2e04c287d3ef371263584
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578691"
---
# <a name="single-page-application-knockoutjs-template"></a>單一頁面應用程式： KnockoutJS 範本

由[Mike Wasson](https://github.com/MikeWasson)

> 挖的 MVC 範本是 ASP.NET 和 Web 工具2012.2 的一部分
> 
> [下載 ASP.NET 和 Web 工具2012。2](https://go.microsoft.com/fwlink/?LinkId=282650)

ASP.NET 和 Web 工具2012.2 更新包含適用于 ASP.NET MVC 4 的單一頁面應用程式（SPA）範本。 此範本的設計目的是讓您快速開始建立互動式用戶端 web 應用程式。

「單頁應用程式」（SPA）是 web 應用程式的一般詞彙，它會載入單一 HTML 頁面，然後動態更新頁面，而不是載入新的頁面。 載入初始頁面之後，SPA 會透過 AJAX 要求與伺服器交談。

![](knockoutjs-template/_static/image1.png)

AJAX 是新的，但目前有 JavaScript 架構，可讓您更輕鬆地建立和維護大型的 SPA 應用程式。 此外，HTML 5 和 CSS3 可讓您更輕鬆地建立豐富的 Ui。

為了讓您開始使用，SPA 範本會建立範例「待辦事項清單」應用程式。 在本教學課程中，我們將引導您進行範本的導覽。 首先，我們將探討待辦事項清單應用程式本身，然後檢查使其正常工作的技術部分。

## <a name="create-a-new-spa-template-project"></a>建立新的 SPA 範本專案

需求：

- 適用于 Web 的 Visual Studio 2012 或 Visual Studio Express 2012
- ASP.NET Web 工具2012.2 更新。 您可以在[這裡](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)安裝更新。

啟動 Visual Studio，然後從 [開始] 頁面選取 [**新增專案**]。 或者，**從 [檔案**] 功能表選取 [**新增**]，然後選取 [**專案**]。

在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。 在 **[ C#視覺效果**] 底下，選取 [ **Web**]。 在專案範本清單中，選取 [ **ASP.NET MVC 4 Web 應用程式**]。 為專案命名，然後按一下 [確定]。

![](knockoutjs-template/_static/image2.png)

在 [**新增專案**] 中，選取 [**單一頁面應用程式**]。

![](knockoutjs-template/_static/image3.png)

按 F5 鍵建置並執行應用程式。 當應用程式第一次執行時，它會顯示登入畫面。

![](knockoutjs-template/_static/image4.png)

按一下 [&quot;註冊&quot;] 連結，並建立新的使用者。

![](knockoutjs-template/_static/image5.png)

在您登入之後，應用程式會建立含有兩個專案的預設待辦事項清單。 您可以按一下 [新增待辦事項清單] 來加入新的清單。

![](knockoutjs-template/_static/image6.png)

重新命名清單、將專案新增至清單，然後將它們簽核。 您也可以刪除專案或刪除整個清單。 這些變更會自動儲存到伺服器上的資料庫（此時會實際為 LocalDB，因為您是在本機執行應用程式）。

![](knockoutjs-template/_static/image7.png)

## <a name="architecture-of-the-spa-template"></a>SPA 範本的架構

下圖顯示應用程式的主要組建區塊。

![](knockoutjs-template/_static/image8.png)

在伺服器端，ASP.NET MVC 會提供 HTML，並處理以表單為基礎的驗證。

ASP.NET Web API 會處理與 ToDoLists 和 ToDoItems 相關的所有要求，包括取得、建立、更新和刪除。 用戶端會使用 JSON 格式的 Web API 來交換資料。

Entity Framework （EF）是 O/RM 層。 它會在 ASP.NET 的物件導向世界和基礎資料庫之間進行協調。 資料庫使用 LocalDB，但是您可以在 web.config 檔案中變更此設定。 通常您會使用 LocalDB 進行本機開發，然後使用 EF code first 的遷移，部署到伺服器上的 SQL database。

在用戶端上，挖的 .js 程式庫會處理來自 AJAX 要求的頁面更新。 [挖加] 會使用資料系結來同步處理頁面與最新的資料。 如此一來，您就不需要撰寫任何逐步解說 JSON 資料並更新 DOM 的程式碼。 相反地，您會將宣告式屬性放在 HTML 中，告訴您如何呈現資料。

此架構的其中一項優點是，它會將展示層與應用程式邏輯隔開。 您可以建立 Web API 部分，而不需要知道網頁的外觀。 在用戶端上，您可以建立「視圖模型」來表示該資料，而視圖模型會使用「挖結」來系結至 HTML。 這可讓您輕鬆地變更 HTML，而不需要變更視圖模型。 （我們稍後會探討挖起來）。

## <a name="models"></a>模型

在 Visual Studio 專案中，[模型] 資料夾包含伺服器端所使用的模型。 （用戶端上也有模型，我們將會取得）。

![](knockoutjs-template/_static/image9.png)

**TodoItem、TodoList**

這些是 Entity Framework Code First 的資料庫模型。 請注意，這些模型具有指向彼此的屬性。 `ToDoList` 包含 ToDoItems 的集合，而且每個 `ToDoItem` 都有其父 ToDoList 的參考。 這些屬性稱為「導覽屬性」，它們代表待辦事項清單和其待辦專案的一對多關聯性。

`ToDoItem` 類別也會使用 **[ForeignKey]** 屬性，指定 `ToDoListId` 是 `ToDoList` 資料表的外鍵。 這會告訴 EF 將外鍵條件約束加入至資料庫。

[!code-csharp[Main](knockoutjs-template/samples/sample1.cs)]

**TodoItemDto, TodoListDto**

這些類別會定義將傳送至用戶端的資料。 「DTO」代表「資料傳輸物件」。 DTO 會定義實體如何序列化為 JSON。 一般來說，使用 Dto 的原因有好幾個：

- 控制要序列化的屬性。 DTO 可以包含來自領域模型的屬性子集。 基於安全性理由，您可能會這麼做（隱藏敏感性資料），或只是要減少您傳送的資料量。
- 若要變更資料的形狀（例如，將更複雜的資料結構壓平合併）。
- 若要將任何商務邏輯從 DTO 中排除（關注點分離）。
- 如果您的網域模型因某些原因而無法序列化。 例如，當您序列化物件時，迴圈參考可能會造成問題，方法是在 Web API 中處理這個問題（請參閱[處理迴圈物件參考](../../../web-api/overview/formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)）。但是，使用 DTO 就完全避免此問題。

在 SPA 範本中，Dto 包含與網域模型相同的資料。 不過，它們仍然很有用，因為它們會避免導覽屬性中的迴圈參考，並示範一般 DTO 模式。

**AccountModels.cs**

此檔案包含網站成員資格的模型。 `UserProfile` 類別會定義成員資格資料庫中使用者設定檔的架構。 （在此案例中，唯一的資訊是使用者識別碼和使用者名稱）。此檔案中的其他模型類別是用來建立使用者註冊和登入表單。

## <a name="entity-framework"></a>Entity Framework

SPA 範本使用 EF Code First。 在 Code First 開發中，您會先在程式碼中定義模型，然後 EF 會使用模型來建立資料庫。 您也可以使用 EF 搭配現有的資料庫（[Database First](https://msdn.microsoft.com/data/jj206878.aspx)）。

[模型] 資料夾中的 `TodoItemContext` 類別衍生自**DbCoNtext**。 這個類別會在模型和 EF 之間提供「粘連」。 `TodoItemContext` 包含 `ToDoItem` 集合和 `TodoList` 集合。 若要查詢資料庫，您只需要針對這些集合撰寫 LINQ 查詢即可。 例如，以下是您可以如何選取使用者 "Alice" 的所有待辦事項清單：

[!code-csharp[Main](knockoutjs-template/samples/sample2.cs)]

您也可以將新的專案加入至集合、更新專案或刪除集合中的專案，並將變更保存至資料庫。

## <a name="aspnet-web-api-controllers"></a>ASP.NET Web API 控制器

在 ASP.NET Web API 中，控制器是處理 HTTP 要求的物件。 如前所述，SPA 範本會使用 Web API 來啟用 `ToDoList` 和 `ToDoItem` 實例上的 CRUD 作業。 控制器位於解決方案的 [控制器] 資料夾中。

![](knockoutjs-template/_static/image10.png)

- `TodoController`：處理待辦事項的 HTTP 要求
- `TodoListController`：處理待辦事項清單的 HTTP 要求。

這些名稱很重要，因為 Web API 會比對 URI 路徑與控制器名稱。 （若要瞭解 Web API 如何將 HTTP 要求路由傳送至控制器，請參閱[ASP.NET Web API 中的路由](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)）。

讓我們看一下 `ToDoListController` 類別。 它包含單一資料成員：

[!code-csharp[Main](knockoutjs-template/samples/sample3.cs)]

如先前所述，`TodoItemContext` 用來與 EF 通訊。 控制器上的方法會執行 CRUD 作業。 Web API 會將來自用戶端的 HTTP 要求對應到控制器方法，如下所示：

| HTTP 要求 | 控制器方法 | 說明 |
| --- | --- | --- |
| GET /api/todo | `GetTodoLists` | 取得待辦事項清單的集合。 |
| 取得/api/todo/*識別碼* | `GetTodoList` | 依識別碼取得待辦事項清單 |
| PUT/api/todo/*id* | `PutTodoList` | 更新待辦事項清單。 |
| POST /api/todo | `PostTodoList` | 建立新的待辦事項清單。 |
| 刪除/api/todo/*識別碼* | `DeleteTodoList` | 刪除待辦事項清單。 |

請注意，某些作業的 Uri 包含識別碼值的預留位置。 例如，若要刪除識別碼為42的清單，URI 為 `/api/todo/42`。

若要深入瞭解如何使用 Web API 進行 CRUD 作業，請參閱[建立支援 Crud 作業的 WEB api](../../../web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations.md)。 此控制器的程式碼相當簡單。 以下是一些有趣的點：

- `GetTodoLists` 方法會使用 LINQ 查詢，依據登入使用者的識別碼來篩選結果。 如此一來，使用者只會看到屬於他或她的資料。 另請注意，Select 語句是用來將 `ToDoList` 實例轉換成 `TodoListDto` 實例。
- PUT 和 POST 方法會先檢查模型狀態，然後再修改資料庫。 如果**ModelState**為 false，則這些方法會傳回 HTTP 400，不正確的要求。 在[模型驗證](../../../web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api.md)中深入瞭解 Web API 中的模型驗證。
- 控制器類別也會以 **[授權]** 屬性裝飾。 這個屬性會檢查 HTTP 要求是否已驗證。 如果要求未通過驗證，用戶端會收到 HTTP 401 （未經授權）。 [在 ASP.NET Web API 中深入瞭解驗證和授權中](../../../web-api/overview/security/authentication-and-authorization-in-aspnet-web-api.md)的驗證。

`TodoController` 類別非常類似 `TodoListController`。 最大的差別在於它不會定義任何 GET 方法，因為用戶端會取得待辦事項，以及每個待辦事項清單。

## <a name="mvc-controllers-and-views"></a>MVC 控制器和 Views

MVC 控制器也位於解決方案的 [控制器] 資料夾中。 `HomeController` 呈現應用程式的主要 HTML。 Home 控制器的視圖定義于 Views/Home/Index. cshtml 中。 主視圖會根據使用者是否登入，呈現不同的內容：

[!code-cshtml[Main](knockoutjs-template/samples/sample4.cshtml)]

當使用者登入時，他們會看到主要 UI。 否則，他們會看到登入面板。 請注意，此條件式轉譯會在伺服器端進行。 永遠不會嘗試在用戶端&#8212;上隱藏機密內容。在此情況中，監看未經處理的 HTTP 訊息的人可以看到您在 HTTP 回應中傳送的任何內容。

## <a name="client-side-javascript-and-knockoutjs"></a>用戶端 JavaScript 和挖式 .js

現在讓我們從應用程式的伺服器端轉換至用戶端。 SPA 範本會結合 jQuery 和挖式 .js 來建立流暢的互動式 UI。 挖式 .js 是 JavaScript 程式庫，可讓您輕鬆地將 HTML 系結至資料。 挖式 .js 會使用稱為「模型-視圖-ViewModel」的模式。

- 此模型是網域資料（ToDo 清單和 ToDo 專案）。
- 此視圖為 HTML 檔案。
- 視圖模型是包含模型資料的 JavaScript 物件。 視圖模型是 UI 的程式碼抽象概念。 它不知道 HTML 標記法。 相反地，它代表視圖的抽象功能，例如「待辦事項清單」。

此視圖會資料系結至視圖模型。 視圖模型的更新會自動反映在視圖中。 系結也適用于另一個方向。 DOM 中的事件（例如按一下）會將資料系結至視圖模型上的函式，以觸發 AJAX 呼叫。

SPA 範本會將用戶端 JavaScript 組織成三個層級：

- todo. datacoNtext：傳送 AJAX 要求。
- todo：定義模型。
- viewmodel .js：定義視圖模型。

![](knockoutjs-template/_static/image11.png)

這些腳本檔案位於解決方案的腳本/應用程式資料夾中。

![](knockoutjs-template/_static/image12.png)

**todo。 datacoNtext**會處理對 Web API 控制器的所有 AJAX 呼叫。 （在 ajaxlogin 中，會在其他位置定義用於登入的 AJAX 呼叫）。

**todo。 model .js**會定義待辦事項清單的用戶端（瀏覽器）模型。 有兩個模型類別： todoItem 和 todoList。

模型類別中的許多屬性都屬於 "ko. 可觀察" 類型。 可預見值是挖的神奇之處。 從[挖空的檔](http://knockoutjs.com/documentation/introduction.html)：可觀察的是可以通知訂閱者有關變更的「JavaScript 物件」。 當可觀察的值變更時，挖的會更新系結至這些可預見值的任何 HTML 元素。 例如，todoItem 具有 title 和作業屬性的可預見值：

[!code-javascript[Main](knockoutjs-template/samples/sample5.js)]

您也可以在程式碼中訂閱可觀察的。 例如，todoItem 類別會訂閱 "作業" 和 "title" 屬性中的變更：

[!code-javascript[Main](knockoutjs-template/samples/sample6.js)]

**視圖模型**

視圖模型會定義在 viewmodel 中。 視圖模型是應用程式將 HTML 網頁元素系結至網域資料的中心點。 在 SPA 範本中，視圖模型包含 todoLists 的可觀察陣列。 視圖模型中的下列程式碼會告訴「挖對」套用系結：

[!code-javascript[Main](knockoutjs-template/samples/sample7.js)]

## <a name="html-and-data-binding"></a>HTML 和資料系結

頁面的主要 HTML 定義于 Views/Home/Index. cshtml 中。 由於我們使用的是資料系結，因此 HTML 只是實際呈現內容的範本。 挖式會使用*宣告*式系結。 您可以藉由將「資料系結」屬性加入至專案，將頁面元素系結至資料。 以下是一個非常簡單的範例，取自挖的檔：

[!code-html[Main](knockoutjs-template/samples/sample8.html)]

在此範例中，「挖加」會以 `myItems.count()`的值更新 **&lt;範圍&gt;** 元素的內容。 每當此值變更時，挖的會更新檔。

挖的會提供數種不同的系結類型。 以下是 SPA 範本中使用的一些系結：

- **foreach**：可讓您逐一查看迴圈，並將相同的標記套用至清單中的每個專案。 這是用來呈現待辦事項清單和待辦事項專案。 在**foreach**中，系結會套用至清單的元素。
- **visible**：用來切換可見度。 當集合是空的，或讓錯誤訊息顯示時，隱藏標記。
- **值**：用來填入表單值。
- **按一下**：將 click 事件系結至視圖模型上的函式。

## <a name="anti-csrf-protection"></a>反 CSRF 保護

跨網站偽造要求（CSRF）是一種攻擊，惡意網站會將要求傳送至使用者目前登入的弱點網站。 為了協助防止 CSRF 攻擊，ASP.NET MVC 會使用*防偽權杖*，也稱為要求驗證權杖。 其概念是伺服器會將隨機產生的權杖放入網頁中。 當用戶端將資料提交至伺服器時，它必須在要求訊息中包含此值。

防偽 token 可以使用，因為由於相同來源的原則，惡意網頁無法讀取使用者的權杖。 （相同來源原則會防止裝載于兩個不同網站的檔存取彼此的內容）。

ASP.NET MVC 透過[AntiForgery](https://msdn.microsoft.com/library/system.web.helpers.antiforgery.aspx)類別和[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute.aspx)屬性，提供反偽造標記的內建支援。 目前，此功能不會內建在 Web API 中。 不過，SPA 範本包含適用于 Web API 的自訂執行。 這段程式碼定義于 [`ValidateHttpAntiForgeryTokenAttribute`] 類別中，位於解決方案的 [篩選] 資料夾中。 若要深入瞭解 Web API 中的反 CSRF，請參閱[防止跨網站偽造要求（CSRF）攻擊](../../../web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks.md)。

## <a name="conclusion"></a>結論

SPA 範本的設計可讓您快速開始撰寫現代化的互動式 web 應用程式。 它會使用挖的 .js 程式庫來分隔資料和應用程式邏輯的呈現（HTML 標籤）。 但是，挖不是您可以用來建立 SPA 的唯一 JavaScript 程式庫。 如果您想要探索一些其他選項，請查看已[建立社區的 SPA 範本](../templates/index.md)。
