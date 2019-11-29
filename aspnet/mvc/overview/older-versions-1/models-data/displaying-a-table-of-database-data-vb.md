---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: 顯示資料庫資料的資料表（VB） |Microsoft Docs
author: microsoft
description: 在本教學課程中，我將示範兩種顯示一組資料庫記錄的方法。 我在 HTML ta 中示範了兩種格式化一組資料庫記錄的方法 。
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: f2e2489ac8455913f55c746dbe05b9fe8272285b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590803"
---
# <a name="displaying-a-table-of-database-data-vb"></a>顯示資料庫資料的資料表 (VB)

由[Microsoft](https://github.com/microsoft)

[下載 PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> 在本教學課程中，我將示範兩種顯示一組資料庫記錄的方法。 我在 HTML 資料表中示範了兩種將一組資料庫記錄格式化的方法。 首先，我會示範如何直接在視圖內格式化資料庫記錄。 接下來，我將示範在格式化資料庫記錄時，您可以如何利用部分。

本教學課程的目的是要說明如何在 ASP.NET MVC 應用程式中顯示資料庫資料的 HTML 表格。 首先，您會瞭解如何使用 Visual Studio 所包含的樣板工具來產生可自動顯示一組記錄的視圖。 接下來，您將瞭解在格式化資料庫記錄時，如何使用部分做為範本。

## <a name="create-the-model-classes"></a>建立模型類別

我們即將顯示電影資料庫資料表中的一組記錄。 電影資料庫資料表包含下列資料行：

<a id="0.4_table01"></a>

| **資料行名稱** | **資料類型** | **允許 Null** |
| --- | --- | --- |
| ID | Int | False |
| 標題 | NVarchar （200） | False |
| Director | NVarchar （50） | False |
| DateReleased | DateTime | False |

為了在 ASP.NET MVC 應用程式中呈現電影資料表，我們需要建立模型類別。 在本教學課程中，我們會使用 Microsoft Entity Framework 來建立我們的模型類別。

> [!NOTE] 
> 
> 在本教學課程中，我們會使用 Microsoft Entity Framework。 不過，請務必瞭解，您可以使用各種不同的技術，從 ASP.NET MVC 應用程式與資料庫互動，包括 LINQ to SQL、NHibernate 或 ADO.NET。

請遵循下列步驟來啟動實體資料模型 Wizard：

1. 以滑鼠右鍵按一下 [方案總管] 視窗中的 [模型] 資料夾，然後選取 [**加入]、[新增專案**] 功能表選項。
2. 選取 [**資料**] 類別，然後選取 [ **ADO.NET 實體資料模型**] 範本。
3. 提供您的資料模型名稱*MoviesDBModel* ，然後按一下 [**新增**] 按鈕。

按一下 [新增] 按鈕之後，[實體資料模型 Wizard] 隨即出現（請參閱 [圖 1]）。 請遵循下列步驟來完成嚮導：

1. 在 [**選擇模型內容**] 步驟中，選取 [**從資料庫產生**] 選項。
2. 在 [**選擇您的資料**連線] 步驟中，使用 [ *MoviesDB* ] 資料連線和 [連線設定] 的名稱*MoviesDBEntities* 。 按 [**下一步]** 按鈕。
3. 在 [**選擇您的資料庫物件**] 步驟中，展開 [資料表] 節點，選取 [電影] 資料表。 輸入命名空間*模型*，然後按一下 [**完成]** 按鈕。

[建立 LINQ to SQL 類別的 ![](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)

**圖 01**：建立 LINQ to SQL 類別（[按一下以觀看完整大小的影像](displaying-a-table-of-database-data-vb/_static/image2.png)）

當您完成實體資料模型 Wizard 之後，實體資料模型設計工具隨即開啟。 設計工具應該會顯示 [電影] 實體（請參閱 [圖 2]）。

[![實體資料模型設計工具](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)

**圖 02**：實體資料模型設計工具（[按一下以查看完整大小的影像](displaying-a-table-of-database-data-vb/_static/image4.png)）

我們需要先進行一項變更，才能繼續進行。 「實體資料」 Wizard 會產生名為「*電影*」的模型類別，代表電影資料庫資料表。 因為我們將使用 Movie 類別來代表特定電影，所以我們需要將類別的名稱修改成*電影*，而不是*電影*（單數而非複數）。

按兩下設計工具介面上的類別名稱，並將類別的名稱從電影變更為 Movie。 進行這項變更之後，請按一下 [**儲存**] 按鈕（磁片磁碟機的圖示）以產生 Movie 類別。

## <a name="create-the-movies-controller"></a>建立電影控制器

既然我們已經有方法可以表示資料庫記錄，我們可以建立一個會傳回電影集合的控制器。 在 [Visual Studio 方案總管] 視窗中，以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [**新增]、[控制器**] 功能表選項（請參閱 [圖 3]）。

[![[新增控制器] 功能表](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)

**圖 03**： [新增控制器] 功能表（[按一下以查看完整大小的影像](displaying-a-table-of-database-data-vb/_static/image6.png)）

當 [**新增控制器**] 對話方塊出現時，請輸入控制器名稱 MovieController （請參閱 [圖 4]）。 按一下 [**新增**] 按鈕以新增新的控制器。

[![[新增控制器] 對話方塊](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)

**圖 04**： [新增控制器] 對話方塊（[按一下以查看完整大小的影像](displaying-a-table-of-database-data-vb/_static/image8.png)）

我們需要修改 Movie controller 所公開的 Index （）動作，讓它傳回一組資料庫記錄。 修改控制器，使其看起來像 [清單 1] 中的控制器。

**清單1– Controllers\MovieController.vb**

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

在 [清單 1] 中，MoviesDBEntities 類別是用來代表 MoviesDB 資料庫。 運算式*實體。MovieSet. ToList （）* 會傳回來自電影資料庫資料表的所有電影集合。

## <a name="create-the-view"></a>建立視圖

在 HTML 資料表中顯示一組資料庫記錄最簡單的方式，就是利用 Visual Studio 所提供的樣板。

選取 [**組建]、** [組建方案] 功能表選項來建立您的應用程式。 您必須先建立應用程式，才能開啟 [**加入視圖**] 對話方塊，否則您的資料類別不會出現在對話方塊中。

以滑鼠右鍵按一下 [索引] （）動作，然後選取 [**新增視圖**] 功能表選項（請參閱 [圖 5]）。

[![新增視圖](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)

**圖 05**：加入視圖（[按一下以觀看完整大小的影像](displaying-a-table-of-database-data-vb/_static/image10.png)）

在 [**加入視圖**] 對話方塊中，核取標示為 [**建立強型別的視圖**] 的核取方塊。 選取 Movie 類別做為**view 資料類別**。 選取 [*清單*] 做為**視圖內容**（請參閱 [圖 6]）。 選取這些選項會產生強型別視圖，以顯示電影清單。

[![[加入視圖] 對話方塊](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)

**圖 06**： [加入視圖] 對話方塊（[按一下以查看完整大小的影像](displaying-a-table-of-database-data-vb/_static/image12.png)）

按一下 [**新增**] 按鈕後，會自動產生 [清單 2] 中的視圖。 此視圖包含逐一查看電影集合，並顯示電影的每個內容所需的程式碼。

**清單2– Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

您可以選取功能表選項 [Debug]、[**開始調試**] （或按 F5 鍵）來執行應用程式。 執行應用程式會啟動 Internet Explorer。 如果您流覽至/Movie URL，則會看到 [圖 7] 中的頁面。

[![電影的資料表](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)

**圖 07**：電影的資料表（[按一下以觀看完整大小的影像](displaying-a-table-of-database-data-vb/_static/image14.png)）

如果您不喜歡 [圖 7] 中資料庫記錄方格外觀的任何內容，就可以直接修改索引視圖。 例如，您可以藉由修改索引視圖，將*DateReleased*標頭變更為 [*發行日期*]。

## <a name="create-a-template-with-a-partial"></a>建立具有部分的範本

當 view 變得太複雜時，最好先將此觀點分解成部分。 使用部分可讓您的觀點更容易瞭解和維護。 我們會建立一個部分，讓我們用來做為範本來設定每個電影資料庫記錄的格式。

請遵循下列步驟來建立部分：

1. 以滑鼠右鍵按一下 [Views\Movie] 資料夾，然後選取 [**新增視圖**] 功能表選項。
2. 選取標示為 *[建立部分視圖（.ascx）* ] 的核取方塊。
3. 將部分*MovieTemplate*命名為。
4. 核取標示為 [**建立強型別的視圖**] 的核取方塊。
5. 選取 [電影] 做為*view 資料類別*。
6. 選取 [空白] 做為 [*視圖內容*]。
7. 按一下 [**新增**] 按鈕，將部分新增至您的專案。

完成這些步驟之後，請修改 MovieTemplate 部分，看起來像 [清單 3]。

**清單3– Views\Movie\MovieTemplate.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

[清單 3] 中的部分包含單一記錄資料列的範本。

[清單 4] 中修改過的索引視圖會使用 MovieTemplate 部分。

**清單4– Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

[清單 4] 中的視圖包含一個 For Each 迴圈，可逐一查看所有電影。 針對每個電影，MovieTemplate 部分是用來格式化電影。 MovieTemplate 是藉由呼叫 RenderPartial （） helper 方法來呈現。

修改過的索引表會呈現資料庫記錄的相同 HTML 資料表。 不過，此視圖已經大幅簡化。

RenderPartial （）方法與大多數其他 helper 方法不同，因為它不會傳回字串。 因此，您必須使用 &lt;% RenderPartial （）%&gt;，而不是 &lt;% = RenderPartial （）%&gt;來呼叫 RenderPartial （）方法。

## <a name="summary"></a>總結

本教學課程的目的是要說明如何在 HTML 資料表中顯示一組資料庫記錄。 首先，您已瞭解如何利用 Microsoft Entity Framework，從控制器動作傳回一組資料庫記錄。 接下來，您已瞭解如何使用 Visual Studio 的架構來產生可自動顯示專案集合的視圖。 最後，您已瞭解如何利用部分來簡化視圖。 您已瞭解如何使用部分做為範本，讓您可以格式化每個資料庫記錄。

> [!div class="step-by-step"]
> [上一頁](creating-model-classes-with-linq-to-sql-vb.md)
> [下一頁](performing-simple-validation-vb.md)
