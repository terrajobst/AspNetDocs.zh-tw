---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: 第3部分：建立管理控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: f39be7a84e85db93487d246e9f8cb59c401fe5ce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556046"
---
# <a name="part-3-creating-an-admin-controller"></a>第3部分：建立管理控制器

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a>新增管理控制器

在本節中，我們將新增 Web API 控制器，以支援產品上的 CRUD （建立、讀取、更新和刪除）作業。 控制器會使用 Entity Framework 來與資料庫層通訊。 只有系統管理員可以使用此控制器。 客戶會透過另一個控制器來存取產品。

在方案總管中，以滑鼠右鍵按一下 [控制器] 資料夾。 依序選取 [**新增**] 和 [**控制器**]。

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

在 [**新增控制器**] 對話方塊中，將控制器命名為 `AdminController`。 在 [**範本**] 下，使用 Entity Framework&quot;選取具有讀取/寫入動作 &quot;API 控制器。 在 [**模型類別**] 下，選取 [產品（ProductStore 模型）]。 在 [**資料內容**] 底下，選取 [&lt;新的資料內容&gt;]。

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> 如果 [**模型類別**] 下拉式按鈕沒有顯示任何模型類別，請確定您已編譯專案。 Entity Framework 使用反映，因此需要已編譯的元件。

選取 [&lt;新的資料內容&gt;] 將會開啟 [**新增資料內容**] 對話方塊。 將資料內容命名 `ProductStore.Models.OrdersContext`。

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

按一下 **[確定]** 以關閉 [**新增資料內容**] 對話方塊。 在 [**新增控制器**] 對話方塊中，按一下 [**新增**]。

以下是已新增至專案的內容：

- 衍生自**DbCoNtext**的類別，名為 `OrdersContext`。 這個類別會提供 POCO 模型與資料庫之間的粘連。
- 名為 `AdminController`的 Web API 控制器。 此控制器支援 `Product` 實例上的 CRUD 作業。 它會使用 `OrdersContext` 類別來與 Entity Framework 通訊。
- Web.config 檔案中的新資料庫連接字串。

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

開啟 OrdersCoNtext.cs 檔案。 請注意，此函式會指定資料庫連接字串的名稱。 這個名稱會參考已加入至 web.config 的連接字串。

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

將下列屬性新增至 `OrdersContext` 類別：

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

**DbSet**代表一組可以查詢的實體。 以下是 `OrdersContext` 類別的完整清單：

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

`AdminController` 類別會定義用來執行基本 CRUD 功能的五種方法。 每個方法都會對應至用戶端可以叫用的 URI：

| 控制器方法 | 說明 | URI | HTTP 方法 |
| --- | --- | --- | --- |
| GetProducts | 取得所有產品。 | api/產品 | GET |
| GetProduct | 依識別碼尋找產品。 | api/產品/*識別碼* | GET |
| PutProduct | 更新產品。 | api/產品/*識別碼* | PUT |
| PostProduct | 建立新的產品。 | api/產品 | POST |
| DeleteProduct | 刪除產品。 | api/產品/*識別碼* | 刪除 |

每個方法都會呼叫 `OrdersContext` 來查詢資料庫。 修改集合（PUT、POST 和 DELETE）呼叫 `db.SaveChanges` 的方法會將變更保存至資料庫。 系統會針對每個 HTTP 要求建立控制器，然後加以處置，因此必須在方法傳回之前保存變更。

## <a name="add-a-database-initializer"></a>加入資料庫初始化運算式

Entity Framework 有一個很好的功能，可讓您在啟動時填入資料庫，並在每次模型變更時自動重新建立資料庫。 這項功能在開發期間很有用，因為您一律會有一些測試資料，即使您變更模型也一樣。

在方案總管中，以滑鼠右鍵按一下 [模型] 資料夾，然後建立名為 `OrdersContextInitializer`的新類別。 貼上下列實作方式：

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

藉由繼承自**DropCreateDatabaseIfModelChanges**類別，我們會在我們每次修改模型類別時，告訴 Entity Framework 卸載資料庫。 當 Entity Framework 建立（或重新建立）資料庫時，它會呼叫**Seed**方法來填入資料表。 我們使用**種子**方法來新增一些範例產品，加上範例訂單。

這項功能非常適合用來測試，但請勿在生產環境中使用**DropCreateDatabaseIfModelChanges**類別，因為如果有人變更了模型類別，您可能會遺失資料。

接下來，開啟 global.asax，然後將下列程式碼新增至**應用程式\_Start**方法：

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a>將要求傳送至控制器

此時，我們尚未撰寫任何用戶端程式代碼，但您可以使用網頁瀏覽器或 HTTP 偵錯工具（例如[Fiddler](http://www.fiddler2.com/fiddler2/)）來叫用 Web API。 在 Visual Studio 中，按 F5 開始進行調試。 您的網頁瀏覽器將會開啟 `http://localhost:*portnum*/`，其中*portnum*是一些埠號碼。

將 HTTP 要求傳送至 "`http://localhost:*portnum*/api/admin`。 第一個要求可能會很慢而無法完成，因為 Entity Framework 需要建立和植入資料庫。 回應應該如下所示：

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> [上一頁](using-web-api-with-entity-framework-part-2.md)
> [下一頁](using-web-api-with-entity-framework-part-4.md)
