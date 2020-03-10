---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: 建立 JavaScript 用戶端 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 74f2cc4e5e401d690042b05b028dfc0c46ae282a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622343"
---
# <a name="create-the-javascript-client"></a>建立 JavaScript 用戶端

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://github.com/MikeWasson/BookService)

在本節中，您將建立應用程式的用戶端，使用 HTML、JavaScript 和挖的[.js](http://knockoutjs.com/)程式庫。 我們會分階段建立用戶端應用程式：

- 顯示書籍清單。
- 顯示書籍詳細資料。
- 加入新書籍。

挖的程式庫會使用 ViewModel （MVVM）模式：

- **模型**是商業領域中的資料伺服器端標記法（在我們的案例中，也就是書籍和作者）。
- 此**視圖**為展示層（HTML）。
- **視圖模型**是包含模型的 JavaScript 物件。 視圖模型是 UI 的程式碼抽象概念。 它不知道 HTML 標記法。 相反地，它代表視圖的抽象功能，例如 &quot;書籍清單&quot;。

此視圖會資料系結至視圖模型。 視圖模型的更新會自動反映在視圖中。 視圖模型也會從視圖取得事件，例如按一下按鈕。

![](part-6/_static/image1.png)

這種方法可讓您輕鬆地變更應用程式的版面配置和 UI，因為您可以變更系結，而不需要重寫任何程式碼。 例如，您可能會將專案清單顯示為 `<ul>`，然後在稍後將其變更為資料表。

## <a name="add-the-knockout-library"></a>新增挖的程式庫

在 Visual Studio 中，從 [**工具**] 功能表選取 [ **NuGet 套件管理員**]。 接著，選取 [Package Manager 主控台]。 在 [Package Manager Console] 視窗中，輸入下列命令：

[!code-console[Main](part-6/samples/sample1.cmd)]

此命令會將挖的檔案新增至 [腳本] 資料夾。

## <a name="create-the-view-model"></a>建立視圖模型

將名為 app.config 的 JavaScript 檔案新增至 [腳本] 資料夾。 （在方案總管中，以滑鼠右鍵按一下 [腳本] 資料夾，選取 [**新增**]，然後選取 [ **JavaScript**檔案]）。貼上下列程式碼：

[!code-javascript[Main](part-6/samples/sample2.js)]

在挖式中，`observable` 類別會啟用資料系結。 當可觀察的內容變更時，可觀察的會通知所有的資料繫結控制項，以便自行更新。 （`observableArray` 類別是可*觀察*的陣列版本）。首先，我們的視圖模型有兩個可預見值：

- `books` 包含書籍清單。
- 如果 AJAX 呼叫失敗，`error` 會包含錯誤訊息。

`getAllBooks` 方法會進行 AJAX 呼叫，以取得書籍的清單。 然後它會將結果推送至 `books` 陣列。

`ko.applyBindings` 方法是「挖程式庫」的一部分。 它會採用 view 模型做為參數，並設定資料系結。

## <a name="add-a-script-bundle"></a>新增腳本配套

配套是 ASP.NET 4.5 中的一項功能，可讓您輕鬆地將多個檔案結合或組合成單一檔案。 「配套」可減少對伺服器的要求數，進而改善頁面載入時間。

開啟檔案應用程式\_Start/Bundleconfig.json. cs。 將下列程式碼新增至 RegisterBundles 方法。

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> [上一頁](part-5.md)
> [下一頁](part-7.md)
