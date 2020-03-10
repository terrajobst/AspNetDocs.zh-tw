---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: 使用 Entity Framework （C#）建立模型類別 |Microsoft Docs
author: microsoft
description: 在本教學課程中，您將瞭解如何搭配 Microsoft Entity Framework 使用 ASP.NET MVC。 您會瞭解如何使用 Entity Wizard 來建立 ADO.NET Entity Da 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 2e0e365c287fc455015d237ea466301335805d14
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581162"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a>使用 Entity Framework 建立模型類別 (C#)

由[Microsoft](https://github.com/microsoft)

> 在本教學課程中，您將瞭解如何搭配 Microsoft Entity Framework 使用 ASP.NET MVC。 您將瞭解如何使用 Entity Wizard 來建立 ADO.NET 實體資料模型。 在本教學課程中，我們會建立一個 web 應用程式，說明如何使用 Entity Framework 來選取、插入、更新和刪除資料庫資料。

本教學課程的目的是要說明如何在建立 ASP.NET MVC 應用程式時，使用 Microsoft Entity Framework 來建立資料存取類別。 本教學課程假設您先前不知道 Microsoft Entity Framework。 在本教學課程結束時，您將瞭解如何使用 Entity Framework 來選取、插入、更新和刪除資料庫記錄。

Microsoft Entity Framework 是物件關聯式對應（O/RM）工具，可讓您自動從資料庫產生資料存取層。 此 Entity Framework 可讓您以手動方式建立資料存取類別，以避免乏味的工作。

為了說明如何搭配使用 Microsoft Entity Framework 與 ASP.NET MVC，我們將建立一個簡單的範例應用程式。 我們將建立電影資料庫應用程式，讓您可以顯示和編輯電影資料庫記錄。

本教學課程假設您有 Visual Studio 2008 或 Visual Web Developer 2008 （含 Service Pack 1）。 您需要 Service Pack 1，才能使用 Entity Framework。 您可以從下列位址下載 Visual Studio 2008 Service Pack 1 或 Visual Web Developer （含 Service Pack 1）：

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> ASP.NET MVC 與 Microsoft Entity Framework 之間沒有任何必要的連接。 您可以搭配 ASP.NET MVC 使用的 Entity Framework 有數個替代方案。 例如，您可以使用其他 O/RM 工具（例如 Microsoft LINQ to SQL、NHibernate 或 SubSonic）來建立 MVC 模型類別。

## <a name="creating-the-movie-sample-database"></a>建立電影範例資料庫

電影資料庫應用程式會使用名為電影的資料庫資料表，其中包含下列資料行：

| 資料行名稱 | 資料類型 | 允許 Null 嗎？ | 是否為主要金鑰？ |
| --- | --- | --- | --- |
| ID | int | False | True |
| 標題 | NVarchar （100） | False | False |
| 導演 | NVarchar （100） | False | False |

您可以遵循下列步驟，將此資料表新增至 ASP.NET MVC 專案：

1. 在 [方案總管] 視窗中，以滑鼠右鍵按一下應用程式\_[Data] 資料夾，然後選取 [**新增]、[新增專案**] 功能表選項。
2. 從 [**加入新專案**] 對話方塊中，選取 [ **SQL Server 資料庫**]，將資料庫命名為 MoviesDB，然後按一下 [**加入**] 按鈕。
3. 按兩下 [MoviesDB] 檔案以開啟 [伺服器總管/資料庫總管] 視窗。
4. 展開 [MoviesDB] 資料庫連接，以滑鼠右鍵按一下 [資料表] 資料夾，然後選取 [**加入新的資料表**] 功能表選項。
5. 在 資料表設計工具中，新增 識別碼、標題 和 導演 資料行。
6. 按一下 [**儲存**] 按鈕（其具有軟碟圖示）以儲存新的資料表，並將其名稱設為電影。

建立電影資料庫資料表之後，您應該在資料表中加入一些範例資料。 以滑鼠右鍵按一下 [電影] 資料表，然後選取 [**顯示資料表資料**] 功能表選項。 您可以在出現的方格中輸入假電影資料。

## <a name="creating-the-adonet-entity-data-model"></a>建立 ADO.NET 實體資料模型

若要使用 Entity Framework，您需要建立實體資料模型。 您可以利用 Visual Studio*實體資料模型 Wizard* ，自動從資料庫產生實體資料模型。

請依照下列步驟：

1. 以滑鼠右鍵按一下 [方案總管] 視窗中的 [模型] 資料夾，然後選取 [**加入]、[新增專案**] 功能表選項。
2. 在 [**加入新專案**] 對話方塊中，選取 [資料] 類別（請參閱 [圖 1]）。
3. 選取 [ **ADO.NET 實體資料模型**] 範本，將實體資料模型名稱指定為 MoviesDBModel，然後按一下 [**新增**] 按鈕。 按一下 [**新增**] 按鈕即可啟動 [資料模型嚮導]。
4. 在 [**選擇模型內容**] 步驟中，選擇 [**從資料庫產生**] 選項，然後按 [**下一步]** 按鈕（請參閱 [圖 2]）。
5. 在 [**選擇您的資料連線**] 步驟中，選取 [MoviesDB] 資料庫連接，並輸入實體連接設定名稱 MoviesDBEntities，然後按 [**下一步]** 按鈕（請參閱 [圖 3]）。
6. 在 [**選擇您的資料庫物件**] 步驟中，選取 [電影資料庫] 資料表，然後按一下 [**完成]** 按鈕（請參閱 [圖 4]）。

完成這些步驟之後，就會開啟 [ADO.NET 實體資料模型設計工具（Entity Designer）]。

**圖1–建立新的實體資料模型**

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

**圖2–選擇模型內容步驟**

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

**圖3–選擇您的資料連線**

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

**圖4–選擇您的資料庫物件**

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a>修改 ADO.NET 實體資料模型

建立實體資料模型之後，您可以利用 Entity Designer 來修改模型（請參閱 [圖 5]）。 您可以在 [方案總管] 視窗內的 [模型] 資料夾中，按兩下包含的 MoviesDBModel，隨時開啟 Entity Designer。

**[圖 5] – ADO.NET 實體資料模型設計工具**

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

例如，您可以使用 Entity Designer 來變更「實體模型資料嚮導」所產生的類別名稱。 嚮導會建立名為 [電影] 的新資料存取類別。 換句話說，此 Wizard 提供的類別與資料庫資料表的名稱相同。 因為我們將使用此類別來代表特定電影實例，所以我們應該將類別從電影重新命名為 Movie。

如果您想要重新命名實體類別，可以按兩下 Entity Designer 中的類別名稱，然後輸入新的名稱（請參閱 [圖 6]）。 或者，您可以在選取 Entity Designer 中的實體之後，變更屬性視窗中的機構名稱。

**圖6–變更機構名稱**

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

按一下 [儲存] 按鈕（磁片圖示）以進行修改之後，請記得儲存您的實體資料模型。 在幕後，Entity Designer 會產生一組C#類別。 您可以從 [方案總管] 視窗開啟 MoviesDBModel.Designer.cs 檔案，以查看這些類別。

請勿修改 Designer.cs 檔案中的程式碼，因為下次使用 Entity Designer 時，將會覆寫變更。 如果您想要擴充 Designer.cs 檔案中定義之實體類別的功能，您可以在不同的檔案中建立*部分類別*。

#### <a name="selecting-database-records-with-the-entity-framework"></a>使用 Entity Framework 選取資料庫記錄

讓我們開始建立電影資料庫應用程式，方法是建立顯示電影記錄清單的頁面。 [清單 1] 中的 Home 控制器會公開名為 Index （）的動作。 Index （）動作會利用 Entity Framework，從 Movie 資料庫資料表傳回所有電影記錄。

**清單1– Controllers\HomeController.cs**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

請注意，[清單 1] 中的控制器包含一個「函式」。 此函式會初始化名為 \_db 的類別層級欄位。 [\_db] 欄位代表 Microsoft Entity Framework 所產生的資料庫實體。 [\_db] 欄位是由 Entity Designer 產生之 MoviesDBEntities 類別的實例。

若要在 Home 控制器中使用 theMoviesDBEntities 類別，您必須匯入 MovieEntityApp 命名空間（*MVCProjectName*。模型）。

[\_db] 欄位會在 Index （）動作內使用，以從電影資料庫資料表中取出記錄。 運算式 \_db。MovieSet 代表來自電影資料庫資料表的所有記錄。 ToList （）方法可用來將電影組轉換成電影物件的一般集合（清單&lt;電影&gt;）。

電影記錄是透過 LINQ to Entities 的協助抓取。 [清單 1] 中的 Index （）動作會使用 LINQ*方法語法*來抓取一組資料庫記錄。 如果您想要的話，可以改用 LINQ*查詢語法*。 下列兩個語句會執行相同的動作：

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

使用任何 LINQ 語法（方法語法或查詢語法），這是最直覺的方式。 這兩種方法之間的效能不會有任何差異–唯一的差別在於樣式。

[清單 2] 中的視圖會用來顯示電影記錄。

**清單2– Views\Home\Index.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

[清單 2] 中的視圖包含一個**foreach**迴圈，可逐一查看每個電影記錄，並顯示電影記錄的標題和主管屬性的值。 請注意，每個記錄旁都會顯示 [編輯] 和 [刪除] 連結。 此外，[新增電影] 連結會出現在視圖底部（請參閱 [圖 7]）。

**圖7–索引視圖**

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

索引視圖是具*類型的視圖*。 索引視圖包含 &lt;% @ Page%&gt; 指示詞與*Inherits*屬性，可將模型屬性轉換成電影物件的強型別一般清單集合（清單&lt;movie）。

## <a name="inserting-database-records-with-the-entity-framework"></a>使用 Entity Framework 插入資料庫記錄

您可以使用 Entity Framework，讓您輕鬆地將新的記錄插入資料庫資料表。 [清單 3] 包含兩個新的動作，可供您用來將新記錄插入 Movie 資料庫資料表。

**清單3– Controllers\HomeController.cs （新增方法）**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

第一個 Add （）動作只會傳回一個視圖。 此視圖包含一個表單，可用於新增電影資料庫記錄（請參閱 [圖 8]）。 當您提交表單時，會叫用第二個 Add （）動作。

請注意，第二個 Add （）動作會以 AcceptVerbs 屬性裝飾。 只有在執行 HTTP POST 作業時，才可以叫用此動作。 換句話說，只有在張貼 HTML 表單時，才可以叫用此動作。

第二個 Add （）動作會使用 ASP.NET MVC TryUpdateModel （）方法的協助，建立 Entity Framework Movie 類別的新實例。 TryUpdateModel （）方法會接受傳遞至 Add （）方法之 FormCollection 中的欄位，並將這些 HTML 表單欄位的值指派給 Movie 類別。

使用 Entity Framework 時，您必須在使用 TryUpdateModel 或 UpdateModel 方法來更新實體類別的屬性時，提供屬性的「白名單」。

接下來，Add （）動作會執行一些簡單的表單驗證。 動作會確認 Title 和 Director 屬性都有值。 如果發生驗證錯誤，則會將驗證錯誤訊息新增至 ModelState。

如果沒有任何驗證錯誤，則會在 [電影資料庫] 資料表中加入新的電影記錄，並提供 Entity Framework 的協助。 新記錄會使用下列兩行程式碼新增至資料庫：

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

第一行程式碼會將新的 Movie 實體新增至 Entity Framework 追蹤的電影集合。 第二行程式碼會儲存對重新追蹤至基礎資料庫的電影所做的任何變更。

**圖8–新增視圖**

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a>使用 Entity Framework 更新資料庫記錄

您可以遵循幾乎相同的方式，使用 Entity Framework 來編輯資料庫記錄，做為我們剛遵循以插入新資料庫記錄的方法。 [清單 4] 包含兩個名為 Edit （）的新控制器動作。 第一個 Edit （）動作會傳回用於編輯電影記錄的 HTML 表單。 第二個 Edit （）動作會嘗試更新資料庫。

**清單4– Controllers\HomeController.cs （編輯方法）**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

第二個 Edit （）動作一開始會從符合所編輯電影識別碼的資料庫中抓取電影記錄。 下列 LINQ to Entities 語句會抓取符合特定識別碼的第一個資料庫記錄：

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

接下來，TryUpdateModel （）方法是用來將 HTML 表單欄位的值指派給 movie 實體的屬性。 請注意，提供的白名單是用來指定要更新的確切屬性。

接下來，會執行一些簡單的驗證，以確認電影標題和主管屬性都有值。 如果其中一個屬性遺漏值，則會將驗證錯誤訊息新增至 ModelState，而 ModelState 會傳回 false 值。

最後，如果沒有任何驗證錯誤，則會藉由呼叫 SaveChanges （）方法，將基礎電影資料庫資料表更新為任何變更。

編輯資料庫記錄時，您必須將正在編輯的記錄識別碼傳遞至執行資料庫更新的控制器動作。 否則，控制器動作將不會知道要在基礎資料庫中更新哪一筆記錄。 [清單 5] 中包含的編輯檢視包含隱藏的表單欄位，代表正在編輯之資料庫記錄的識別碼。

**清單5– Views\Home\Edit.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>使用 Entity Framework 刪除資料庫記錄

我們在本教學課程中需要處理的最終資料庫作業，是刪除資料庫記錄。 您可以使用 [清單 6] 中的 [控制器] 動作來刪除特定的資料庫記錄。

**清單 6--\Controllers\HomeController.cs （刪除動作）**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

Delete （）動作會先抓取符合傳遞給動作之識別碼的 Movie 實體。 接下來，藉由呼叫 DeleteObject （）方法並接著 SaveChanges （）方法，從資料庫刪除電影。 最後，會將使用者重新導向回到索引視圖。

## <a name="summary"></a>總結

本教學課程的目的是要示範如何利用 ASP.NET MVC 和 Microsoft Entity Framework，來建立資料庫導向的 web 應用程式。 您已瞭解如何建立可讓您選取、插入、更新和刪除資料庫記錄的應用程式。

首先，我們會討論如何使用實體資料模型 Wizard，從 Visual Studio 內產生實體資料模型。 接下來，您將瞭解如何使用 LINQ to Entities 從資料庫資料表中取出一組資料庫記錄。 最後，我們使用 Entity Framework 來插入、更新和刪除資料庫記錄。

> [!div class="step-by-step"]
> [下一個](creating-model-classes-with-linq-to-sql-cs.md)
