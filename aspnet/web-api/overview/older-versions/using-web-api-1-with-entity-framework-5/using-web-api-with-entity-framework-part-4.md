---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: 第4部分：新增系統管理員視圖 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 664aeb33031e933322886a6d6bdd989277e9fda2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556011"
---
# <a name="part-4-adding-an-admin-view"></a>第4部分：新增系統管理員視圖

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a>新增系統管理員視圖

現在，我們會轉至用戶端，並新增可從管理控制器使用資料的頁面。 此頁面可讓使用者將 AJAX 要求傳送至控制器，以建立、編輯或刪除產品。

在方案總管中，展開 [控制器] 資料夾，然後開啟名為 HomeController.cs 的檔案。 此檔案包含 MVC 控制器。 新增名為 `Admin`的方法：

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

**HttpRouteUrl**方法會建立 WEB API 的 URI，並將其儲存在 view 包中，以便稍後進行。

接下來，將文字游標放在 `Admin` 動作方法內，然後以滑鼠右鍵按一下並選取 [**加入視圖**]。 這會顯示 [**加入視圖**] 對話方塊。

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

在 [**加入視圖**] 對話方塊中，將 view 命名為 "Admin"。 選取標示為 [**建立強型別視圖**] 的核取方塊。 在 [**模型類別**] 下，選取 [產品（ProductStore 模型）]。 將所有其他選項保留為預設值。

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

按一下 [**新增**]，會在 Views/Home 底下新增名為 Admin 的檔案。 開啟此檔案，並新增下列 HTML。 此 HTML 會定義網頁的結構，但尚未啟動任何功能。

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a>建立 [系統管理員] 頁面的連結

在方案總管中，展開 [Views] 資料夾，然後展開 [共用] 資料夾。 開啟名為 \_配置. cshtml 的檔案。 找出 id = "menu" 的**ul**元素，以及 Admin 視圖的動作連結：

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> 在範例專案中，我做了一些其他的表面變更，例如取代「此處的標誌」字串。 這些不會影響應用程式的功能。 您可以下載專案並比較檔案。

執行應用程式，然後按一下出現在首頁頂端的 [Admin] 連結。 [管理] 頁面看起來應該如下所示：

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

目前，此頁面不會執行任何動作。 在下一節中，我們將使用挖的 .js 來建立動態 UI。

## <a name="add-authorization"></a>新增授權

流覽網站的任何人目前都可以存取 [管理] 頁面。 讓我們將此變更為限制系統管理員的許可權。

首先新增「系統管理員」角色和系統管理員使用者。 在方案總管中，展開 [篩選] 資料夾，然後開啟名為 InitializeSimpleMembershipAttribute.cs 的檔案。 找出 `SimpleMembershipInitializer` 的函式。 呼叫**WebSecurity. InitializeDatabaseConnection**之後，新增下列程式碼：

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

這是新增「系統管理員」角色並為角色建立使用者的快速且正常的方式。

在方案總管中，展開 [控制器] 資料夾，然後開啟 HomeController.cs 檔案。 將**授權**屬性新增至 `Admin` 方法。

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

開啟 AdminController.cs 檔案，並將**授權**屬性新增至整個 `AdminController` 類別。

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> MVC 和 Web API 都會在不同的命名空間中定義**授權**屬性。 MVC 會使用**AuthorizeAttribute**，而 Web API 則會使用**AuthorizeAttribute**。

現在只有系統管理員可以看到 [管理] 頁面。 此外，如果您將 HTTP 要求傳送至管理控制器，要求必須包含驗證 cookie。 如果不是，伺服器會傳送 HTTP 401 （未經授權）的回應。 您可以藉由將 GET 要求傳送至 `http://localhost:*port*/api/admin`，在 Fiddler 中看到此情況。

> [!div class="step-by-step"]
> [上一頁](using-web-api-with-entity-framework-part-3.md)
> [下一頁](using-web-api-with-entity-framework-part-5.md)
