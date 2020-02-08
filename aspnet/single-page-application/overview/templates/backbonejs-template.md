---
uid: single-page-application/overview/templates/backbonejs-template
title: 骨幹範本 |Microsoft Docs
author: madskristensen
description: 骨幹 SPA 範本
ms.author: riande
ms.date: 04/04/2013
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 7297db7d5b35a53b40f9d9162960e529a167bd12
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074887"
---
# <a name="backbone-template"></a>Backbone 範本

依[Mads Kristensen](https://github.com/madskristensen)

> 骨幹 SPA 範本是由 Kazi Manzur Rashid 所撰寫
> 
> [下載骨幹 SPA 範本](https://go.microsoft.com/fwlink/?LinkId=293631)

骨幹 SPA 範本的設計目的是讓您快速開始使用骨幹來建立互動式用戶端 web 應用程式[。](http://backbonejs.org/)

範本提供在 ASP.NET MVC 中開發骨幹應用程式的初始基本架構。 它提供基本的使用者登入功能，包括使用者註冊、登入、密碼重設，以及使用基本電子郵件範本的使用者確認。

需求：

- [ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a>建立骨幹範本專案

按一下上方的 [下載] 按鈕，以下載並安裝範本。 此範本會封裝為 Visual Studio 擴充功能（VSIX）檔案。 您可能需要重新開機 Visual Studio。

在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。 在 **[ C#視覺效果**] 底下，選取 [ **Web**]。 在專案範本清單中，選取 [ **ASP.NET MVC 4 Web 應用程式**]。 為專案命名，然後按一下 [確定]。

![](backbonejs-template/_static/image1.png)

在 [**新增專案**] 中，選取 [骨幹 SPA 專案]。

![](backbonejs-template/_static/image2.png)

按下 Ctrl-F5 以建立並執行應用程式，而不進行任何偵測，或按 F5 執行以進行偵錯工具。

![](backbonejs-template/_static/image3.png)

按一下 [我的帳戶] 就會顯示登入頁面：

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a>逐步解說：用戶端程式代碼

讓我們從用戶端開始。 用戶端應用程式腳本位於 ~/Scripts/application 資料夾中。 應用程式是以[TypeScript](http://www.typescriptlang.org/) （. ts 檔案）撰寫，並編譯成 JavaScript （.js 檔案）。

**應用程式**

`Application` 是在 application. ts 中定義。 此物件會初始化應用程式，並作為根命名空間。 它會維護應用程式間共用的設定和狀態資訊，例如使用者是否已登入。

`application.start` 方法會建立強制回應視圖，並附加應用層級事件的事件處理常式，例如使用者登入。 接下來，它會建立預設路由器，並檢查是否已指定任何用戶端 URL。 如果不是，它會重新導向至預設 url （#！/）。

**事件**

開發鬆散結合的元件時，事件一律很重要。 應用程式通常會執行多個作業，以回應使用者動作。 骨幹提供內建的事件，包括模型、集合和 View 等元件。 範本會使用「pub/sub」模型，而不是建立這些元件之間的相依性，而是在事件中定義的 `events` 物件，做為用於發佈和訂閱應用程式事件的事件中樞。 `events` 物件是單一的。 下列程式碼顯示如何訂閱事件，然後觸發事件：

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

**傳送**

在骨幹中，路由器會提供方法來路由傳送用戶端頁面，並將它們連接到動作和事件。 此範本會在 [ts] 中定義單一路由器。 路由器會建立 activable views，並在切換 views 時維持狀態。 （Activable views 會在下一節中說明）。一開始，專案有兩個虛擬視圖： Home 和 About。 它也有一個 [NotFound] 視圖，如果路由不是已知的，就會顯示此畫面。

**檢視**

這些觀點定義于 ~/Scripts/application/views。 有兩種類型的視圖： activable views 和強制回應對話方塊視圖。 Activable views 是由路由器叫用。 顯示 activable 視圖時，所有其他 activable 視圖都會變成非作用中。 若要建立 activable 視圖，請使用 `Activable` 物件來擴充此視圖：

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

以 `Activable` 擴充會在視圖中加入兩個新的方法，`activate` 和 `deactivate`。 路由器會呼叫這些方法來啟動和停用此視圖。

強制回應視圖會實作為[Twitter 啟動](https://twitter.github.com/bootstrap/)程式強制回應對話方塊。 [`Membership`] 和 [`Profile`] 視圖是強制回應的視圖。 模型視圖可以由任何應用程式事件叫用。 例如，在 [`Navigation`] 視圖中，按一下 [我的帳戶] 連結會顯示 [`Membership` 視圖] 或 [`Profile`] 視圖，視使用者是否登入而定。 `Navigation` 會將 click 事件處理常式附加至任何具有 `data-command` 屬性的子專案。 以下是 HTML 標籤：

[!code-html[Main](backbonejs-template/samples/sample3.html)]

以下是導覽. ts 中的程式碼，用來連結事件：

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

**模型**

模型定義于 ~/Scripts/application/models。 這些模型都有三個基本事項：預設屬性、驗證規則和伺服器端端點。 以下是典型的範例：

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

**外掛程式**

~/Scripts/application/lib 資料夾包含幾個方便使用的 jQuery 外掛程式. Ts 檔案會定義用來處理表單資料的外掛程式。 您通常需要序列化或還原序列化表單資料，並顯示任何模型驗證錯誤。 Ts 外掛程式的形式包括 `serializeFields`、`deserializeFields`和 `showFieldErrors`等方法。 下列範例示範如何將表單序列化為模型。

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

Flashbar 可為使用者提供各種類型的意見反應訊息。 這些方法是 `$.showSuccessbar`、`$.showErrorbar` 和 `$.showInfobar`。 在幕後，它會使用 Twitter 啟動程式警示來顯示美觀的動畫訊息。

不過，如果 API 有點不同，則 confirm 外掛程式會取代瀏覽器的 [確認] 對話方塊：

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a>逐步解說：伺服器程式碼

現在讓我們來看一下伺服器端。

**控制器**

在單一頁面應用程式中，伺服器只會在使用者介面中播放小型角色。 一般來說，伺服器會轉譯初始頁面，然後傳送和接收 JSON 資料。

範本有兩個 MVC 控制器： `HomeController` 會轉譯初始頁面，而 `SupportsController` 則用來確認新的使用者帳戶及重設密碼。 範本中的其他所有控制器都是 ASP.NET Web API 控制器，其會傳送和接收 JSON 資料。 根據預設，控制器會使用新的 `WebSecurity` 類別來執行使用者相關的工作。 不過，它們也有選擇性的函式，可讓您傳入委派以進行這些工作。 這可讓測試更容易，並可讓您使用 IoC 容器來取代 `WebSecurity` 的其他專案。 範例如下：

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a>檢視

這些觀點設計為模組化：網頁的每個區段都有自己專屬的視圖。 在單一頁面應用程式中，通常會包含沒有任何對應控制器的視圖。 您可以藉由呼叫 `@Html.Partial('myView')`來包含視圖，但這會變得繁瑣。 為了簡化這項作業，範本會定義 helper 方法（`IncludeClientViews`），以呈現指定資料夾中的所有視圖：

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

如果未指定資料夾名稱，預設的資料夾名稱會是 "ClientViews"。 如果您的用戶端視圖也使用部分視圖，請使用底線字元（例如 `_SignUp`）來命名部分視圖。 `IncludeClientViews` 方法會排除名稱以底線開頭的任何 views。 若要在用戶端視圖中包含部分視圖，請呼叫 `Html.ClientView('SignUp')`，而不是 `Html.Partial('_SignUp')`。

**傳送電子郵件**

若要傳送電子郵件，範本會使用 [[郵遞區號](http://aboutcode.net/postal)]。 不過，郵遞區號會從程式碼的其餘部分抽象化 `IMailer` 介面，因此您可以輕鬆地將它取代為另一個實作為。 電子郵件範本位於 Views/Email 資料夾中。 寄件者的電子郵件地址是在 web.config 檔案的**appSettings**區段的 `sender.email` 機碼中指定。 此外，當 web.config 中的 `debug="true"` 時，應用程式不需要確認使用者電子郵件，就能加速開發工作。

## <a name="github"></a>GitHub

您也可以在[GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa)上找到骨幹 SPA 範本。
