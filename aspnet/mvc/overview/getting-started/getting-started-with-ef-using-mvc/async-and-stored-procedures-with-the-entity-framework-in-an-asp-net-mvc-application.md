---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教學課程：在 ASP.NET MVC 應用程式中搭配使用非同步和預存程式與 EF
description: 在本教學課程中，您會瞭解如何執行非同步程式設計模型，並瞭解如何使用預存程式。
author: tdykstra
ms.author: riande
ms.date: 01/18/2019
ms.topic: tutorial
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5612f2f25d06feb904a205505ed8f048d2263266
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583437"
---
# <a name="tutorial-use-async-and-stored-procedures-with-ef-in-an-aspnet-mvc-app"></a>教學課程：在 ASP.NET MVC 應用程式中搭配使用非同步和預存程式與 EF

在先前的教學課程中，您已瞭解如何使用同步程式設計模型來讀取和更新資料。 在本教學課程中，您會瞭解如何執行非同步程式設計模型。 非同步程式碼可以協助應用程式的執行效果更好，因為它會更有效地使用伺服器資源。

在本教學課程中，您也會瞭解如何在實體上使用預存程式進行插入、更新和刪除作業。

最後，您會將應用程式重新部署至 Azure，以及您在第一次部署之後所執行的所有資料庫變更。

下列圖例顯示了您將操作的一些頁面。

![部門頁面](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![建立部門](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

在本教學課程中，您已：

> [!div class="checklist"]
> * 瞭解非同步程式碼
> * 建立部門控制器
> * 使用預存程式
> * 部署到 Azure

## <a name="prerequisites"></a>Prerequisites

* [更新相關資料](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="why-use-asynchronous-code"></a>為何要使用非同步程式碼

網頁伺服器的可用執行緒數量有限，而且在高負載情況下，可能會使用所有可用的執行緒。 發生此情況時，伺服器將無法處理新的要求，直到執行緒空出來。 使用同步程式碼，許多執行緒可能在實際上並未執行任何工作時受到占用，原因是在等候 I/O 完成。 使用非同步程式碼，處理程序在等候 I/O 完成時，其執行緒將會空出來以讓伺服器處理其他要求。 因此，非同步程式碼可讓伺服器資源更有效率地使用，而伺服器則可以在不延遲的情況下處理更多的流量。

在舊版的 .NET 中，撰寫和測試非同步程式碼既複雜又容易出錯，而且很難進行偵錯工具。 在 .NET 4.5 中，撰寫、測試和偵錯工具的非同步程式碼會更容易，除非您有不這麼做的原因。 非同步程式碼會產生少量的額外負荷，但對於低流量的情況，效能的衝擊是可忽略的，而在高流量的情況下，可能會大幅改善效能。

如需非同步程式設計的詳細資訊，請參閱[使用 .net 4.5 的非同步支援來避免封鎖呼叫](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async)。

## <a name="create-department-controller"></a>建立部門控制器

建立部門控制器的方式與先前的控制器相同，但這次請選取 [**使用非同步控制器動作**] 核取方塊。

下列重點說明如何將 `Index` 方法的同步程式碼加入，使其成為非同步：

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

已套用四個變更，讓 Entity Framework 資料庫查詢能夠以非同步方式執行：

- 方法會以 `async` 關鍵字標示，這會指示編譯器為方法主體的部分產生回呼，並自動建立傳回的 `Task<ActionResult>` 物件。
- 傳回類型已從 `ActionResult` 變更為 `Task<ActionResult>`。 `Task<T>` 類型代表進行中的工作，其類型為 `T`的結果。
- `await` 關鍵字已套用至 web 服務呼叫。 當編譯器看到此關鍵字時，它會在幕後將方法分割成兩個部分。 第一個部分會以非同步方式啟動的作業結尾。 第二個部分會放在作業完成時呼叫的回呼方法中。
- 已呼叫 `ToList` 擴充方法的非同步版本。

為什麼 `departments.ToList` 語句已修改，但不是 `departments = db.Departments` 的語句？ 原因是，只有導致查詢或命令傳送至資料庫的語句會以非同步方式執行。 `departments = db.Departments` 語句會設定查詢，但在呼叫 `ToList` 方法之前，不會執行查詢。 因此，只會以非同步方式執行 `ToList` 方法。

在 `Details` 方法和 `HttpGet` `Edit` 和 `Delete` 方法中，`Find` 方法是讓查詢傳送至資料庫的方法，因此這是非同步執行的方法：

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

在 `Create`、`HttpPost Edit`和 `DeleteConfirmed` 方法中，這是會導致執行命令的 `SaveChanges` 方法呼叫，而不是只會在記憶體中修改實體的語句（例如 `db.Departments.Add(department)`）。

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

開啟*Views\Department\Index.cshtml*，並將範本程式碼取代為下列程式碼：

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

此程式碼會將標題從 [索引] 變更為 [部門]，將系統管理員名稱移至右側，並提供系統管理員的完整名稱。

在 [建立]、[刪除]、[詳細資料] 和 [編輯] 視圖中，將 [`InstructorID`] 欄位的標題變更為 [系統管理員]，如同您在課程視圖中將 [部門名稱] 欄位變更為 [部門] 的相同方式。

在 [建立] 和 [編輯] 視圖中，使用下列程式碼：

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

在 [刪除] 和 [詳細資料] 視圖中，使用下列程式碼：

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

執行應用程式，然後按一下 [**部門**] 索引標籤。

所有專案的運作方式與其他控制器相同，但在此控制器中，所有 SQL 查詢都會以非同步方式執行。

當您使用 Entity Framework 的非同步程式設計時，要注意的一些事項：

- 非同步程式碼不是安全線程。 換句話說，不要嘗試使用相同的內容實例平行執行多個作業。
- 若您想要充分利用非同步程式碼帶來的效能優點，請確保任何您正在使用的程式庫 (例如分頁) 也使用了非同步 (若它們有呼叫任何可能會傳送查詢到資料庫的 Entity Framework 方法的話)。

## <a name="use-stored-procedures"></a>使用預存程式

有些開發人員和 Dba 偏好使用預存程式來存取資料庫。 在舊版的 Entity Framework 您可以藉由[執行原始 SQL 查詢](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)，使用預存程式來抓取資料，但無法指示 EF 使用預存程式進行更新作業。 在 EF 6 中，您可以輕鬆地將 Code First 設定為使用預存程式。

1. 在*DAL\SchoolCoNtext.cs*中，將反白顯示的程式碼新增至 `OnModelCreating` 方法。

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    此程式碼會指示 Entity Framework 在 `Department` 實體上使用預存程式進行插入、更新和刪除作業。
2. 在 [套件管理主控台] 中，輸入下列命令：

    `add-migration DepartmentSP`

    開啟 *[遷移]\\&lt;時間戳記&gt;\_DepartmentSP.cs* ，以在建立 Insert、Update 和 Delete 預存程式的 `Up` 方法中查看程式碼：

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. 在 [套件管理主控台] 中，輸入下列命令：

     `update-database`
4. 在 [debug] 模式中執行應用程式，按一下 [**部門**] 索引標籤，然後按一下 **[新建]。**
5. 輸入新部門的資料，然後按一下 [**建立**]。

6. 在 Visual Studio 中，查看 [**輸出**] 視窗中的記錄，以查看是否已使用預存程式來插入新的部門資料列。

     ![部門插入 SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Code First 會建立預設的預存程式名稱。 如果您使用現有的資料庫，您可能需要自訂預存程式名稱，才能使用已經在資料庫中定義的預存程式。 如需如何執行此動作的詳細資訊，請參閱[Entity Framework Code First 插入/更新/刪除預存程式](https://msdn.microsoft.com/data/dn468673)。

如果您想要自訂產生的預存程式，您可以編輯 scaffold 程式碼來進行遷移 `Up` 方法，以建立預存程式。 如此一來，每當執行遷移時，您的變更就會反映出來，並在部署後於生產環境中自動執行時，套用到您的生產環境資料庫。

如果您想要變更在先前的遷移中建立的現有預存程式，您可以使用 [新增-遷移] 命令來產生空白的遷移，然後手動撰寫呼叫[AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx)方法的程式碼。

## <a name="deploy-to-azure"></a>部署到 Azure

本節要求您已完成此系列的[遷移與部署](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)教學課程中的選擇性將**應用程式部署至 Azure**一節。 如果您已藉由刪除本機專案中的資料庫來解決了遷移錯誤，請略過本節。

1. 在 Visual Studio 的 [方案總管] 中以滑鼠右鍵按一下專案，再選取內容功能表中的 [發佈]。
2. 按一下 [發行]。

    Visual Studio 會將應用程式部署至 Azure，並在您的預設瀏覽器中開啟應用程式，並在 Azure 中執行。
3. 測試應用程式以確認其運作正常。

    當您第一次執行存取資料庫的頁面時，Entity Framework 會執行所有需要的遷移 `Up` 方法，使資料庫與目前的資料模型保持在最新狀態。 您現在可以使用您在上一次部署之後新增的所有網頁，包括您在本教學課程中新增的部門頁面。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他資源

您可以在[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 瞭解非同步程式碼
> * 建立部門控制器
> * 已使用預存程式
> * 已部署至 Azure

前往下一篇文章，以瞭解如何在多位使用者同時更新相同實體時處理衝突。
> [!div class="nextstepaction"]
> [處理並行](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
