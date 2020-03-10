---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
title: 使用 LINQ to SQL （C#）建立模型類別 |Microsoft Docs
author: microsoft
description: 本教學課程的目的是要說明為 ASP.NET MVC 應用程式建立模型類別的其中一個方法。 在本教學課程中，您將瞭解如何建立模型 c 。
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f84b4a16-e8bb-49e8-87a0-1832879a3501
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
msc.type: authoredcontent
ms.openlocfilehash: c27d1ffac3846fe4bc13b32c2ae91a63b2493126
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543537"
---
# <a name="creating-model-classes-with-linq-to-sql-c"></a>使用 LINQ to SQL 建立模型類別 (C#)

由[Microsoft](https://github.com/microsoft)

[下載 PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_CS.pdf)

> 本教學課程的目的是要說明為 ASP.NET MVC 應用程式建立模型類別的其中一個方法。 在本教學課程中，您將瞭解如何建立模型類別，並利用 Microsoft LINQ to SQL 來執行資料庫存取。

本教學課程的目的是要說明為 ASP.NET MVC 應用程式建立模型類別的其中一個方法。 在本教學課程中，您將瞭解如何建立模型類別，並利用 Microsoft LINQ to SQL 來執行資料庫存取

在本教學課程中，我們會建立基本的電影資料庫應用程式。 我們一開始會以最快、最簡單的方式建立電影資料庫應用程式。 我們會直接從控制器動作執行所有資料存取。

接下來，您將瞭解如何使用存放庫模式。 使用存放庫模式需要執行更多工作。 不過，採用此模式的優點是，它可讓您建立可調整的應用程式，並可輕鬆地進行測試。

## <a name="what-is-a-model-class"></a>什麼是模型類別？

MVC 模型包含不包含在 MVC 視圖或 MVC 控制器中的所有應用程式邏輯。 特別是，MVC 模型包含您所有的應用程式商務和資料存取邏輯。

您可以使用各種不同的技術來執行資料存取邏輯。 例如，您可以使用 Microsoft Entity Framework、NHibernate、Subsonic 或 ADO.NET 類別來建立資料存取類別。

在本教學課程中，我使用 LINQ to SQL 來查詢和更新資料庫。 LINQ to SQL 提供與 Microsoft SQL Server 資料庫互動非常簡單的方法。 不過，請務必瞭解，ASP.NET MVC 架構不會以任何方式系結至 LINQ to SQL。 ASP.NET MVC 與任何資料存取技術相容。

## <a name="create-a-movie-database"></a>建立電影資料庫

在本教學課程中，為了說明如何建立模型類別，我們建立了一個簡單的電影資料庫應用程式。 第一個步驟是建立新的資料庫。 在 [方案總管] 視窗中，以滑鼠右鍵按一下應用程式\_[Data] 資料夾，然後選取 [**新增]、[新增專案**] 功能表選項。 選取 [ **SQL Server 資料庫**] 範本，將它命名為 MoviesDB，然後按一下 [**新增**] 按鈕（請參閱 [圖 1]）。

[![加入新的 SQL Server 資料庫](creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)

**圖 01**：加入新的 SQL Server 資料庫（[按一下以觀看完整大小的影像](creating-model-classes-with-linq-to-sql-cs/_static/image3.png)）

建立新的資料庫之後，您可以按兩下應用程式\_Data 資料夾中的 MoviesDB，開啟資料庫。 按兩下 [MoviesDB] 檔案會開啟 [伺服器總管] 視窗（請參閱 [圖 2]）。

使用 Visual Web Developer 時，[伺服器總管] 視窗稱為 [資料庫總管] 視窗。

[使用 [伺服器總管] 視窗 ![](creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)

**圖 02**：使用 [伺服器總管] 視窗（[按一下以查看完整大小的影像](creating-model-classes-with-linq-to-sql-cs/_static/image6.png)）

我們需要在代表電影的資料庫中新增一個資料表。 以滑鼠右鍵按一下 [資料表] 資料夾，然後選取 [**加入新的資料表**] 功能表選項。 選取此功能表選項會開啟 資料表設計工具（請參閱 圖 3）。

[使用 [伺服器總管] 視窗 ![](creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)

**圖 03**：資料表設計工具（[按一下以觀看完整大小的影像](creating-model-classes-with-linq-to-sql-cs/_static/image9.png)）

我們需要將下列資料行加入至資料庫資料表：

| **資料行名稱** | **資料類型** | **允許 Null** |
| --- | --- | --- |
| ID | Int | False |
| 標題 | NVarchar （200） | False |
| 導演 | Nvarchar （50） | False |

您必須對 [識別碼] 資料行執行兩項特殊動作。 首先，您必須選取 資料表設計工具中的資料行，然後按一下索引鍵的圖示，將 識別碼 資料行標示為 主鍵 資料行。 LINQ to SQL 在對資料庫執行插入或更新時，會要求您指定主鍵資料行。

接下來，您必須將 Id 資料行標記為識別欄位，方法是將值為 [是]**標識**屬性（請參閱 [圖 3]）。 識別欄位是當您將新的資料列加入資料表時，會自動指派新數位的資料行。

## <a name="create-linq-to-sql-classes"></a>建立 LINQ to SQL 類別

我們的 MVC 模型將包含代表 tblMovie 資料庫資料表的 LINQ to SQL 類別。 建立這些 LINQ to SQL 類別的最簡單方式是以滑鼠右鍵按一下 [模型] 資料夾、選取 [**加入]、[新增專案**]、選取 [LINQ to SQL 類別] 範本、提供名稱為 [Movie] 的類別，然後按一下 [**新增**] 按鈕（請參閱 [圖 4]）。

[建立 LINQ to SQL 類別的 ![](creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)

**圖 04**：建立 LINQ to SQL 類別（[按一下以查看完整大小的影像](creating-model-classes-with-linq-to-sql-cs/_static/image12.png)）

建立電影 LINQ to SQL 類別之後，就會立即出現物件關聯式設計工具。 您可以將資料庫資料表從 [伺服器總管] 視窗拖曳至 [物件關聯式設計工具]，以建立代表特定資料庫資料表的 LINQ to SQL 類別。 我們需要將 tblMovie 資料庫資料表新增至物件關聯式設計工具（請參閱 [圖 5]）。

[使用物件關聯式設計工具 ![](creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)

**圖 05**：使用物件關聯式設計工具（[按一下以觀看完整大小的影像](creating-model-classes-with-linq-to-sql-cs/_static/image15.png)）

根據預設，物件關聯式設計工具會建立與您拖曳至設計工具的資料庫資料表具有相同名稱的類別。 不過，我們不想要呼叫我們的類別 `tblMovie`。 因此，請在設計工具中按一下類別的名稱，並將類別的名稱變更為 Movie。

最後，請記得按一下 [**儲存**] 按鈕（軟碟的圖片）來儲存 LINQ to SQL 類別。 否則，物件關聯式設計工具不會產生 LINQ to SQL 類別。

## <a name="using-linq-to-sql-in-a-controller-action"></a>在控制器動作中使用 LINQ to SQL

既然我們已經有了 LINQ to SQL 類別，就可以使用這些類別來抓取資料庫中的資料。 在本節中，您將瞭解如何直接在控制器動作內使用 LINQ to SQL 類別。 我們會在 MVC 視圖中顯示來自 tblMovies 資料庫資料表的電影清單。

首先，我們需要修改 HomeController 類別。 您可以在應用程式的 [控制器] 資料夾中找到這個類別。 修改類別，使其看起來像 [清單 1] 中的類別。

**清單1– `Controllers\HomeController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample1.cs)]

[清單 1] 中的 [`Index()`] 動作會使用 LINQ to SQL DataCoNtext 類別（`MovieDataContext`）來代表 `MoviesDB` 資料庫。 `MoveDataContext` 類別是由 Visual Studio 物件關聯式設計工具所產生。

LINQ 查詢會針對 DataCoNtext 執行，以從 `tblMovies` 資料庫資料表中取出所有電影。 電影清單會指派給名為 `movies`的本機變數。 最後，電影清單會透過 view data 傳遞至 view。

為了顯示電影，我們接下來需要修改索引視圖。 您可以在 [`Views\Home\`] 資料夾中找到索引視圖。 更新 [索引] 視圖，使其看起來像 [清單 2] 中的 [視圖]。

**清單2– `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample2.aspx)]

請注意，修改過的索引視圖會在視圖頂端包含一個 `<%@ import namespace %>` 的指示詞。 這個指示詞會匯入 `MvcApplication1.Models namespace`。 我們需要這個命名空間，才能在視圖中使用 `model` 類別（特別是 `Movie` 類別）。

[清單 2] 中的視圖包含一個 `foreach` 迴圈，可逐一查看 `ViewData.Model` 屬性所代表的所有專案。 每個 `movie`都會顯示 [`Title`] 屬性的值。

請注意，`ViewData.Model` 屬性的值會轉換成 `IEnumerable`。 若要對 `ViewData.Model`的內容進行迴圈，這是必要的。 這裡的另一個選項是建立強型別 `view`。 當您建立強型別 `view`時，您會將 `ViewData.Model` 屬性轉換成視圖的程式碼後置類別中的特定型別。

如果您在修改 `HomeController` 類別和索引視圖之後執行應用程式，則會看到空白頁面。 因為 `tblMovies` 資料庫資料表中沒有電影記錄，所以您會看到空白頁面。

若要將記錄加入 `tblMovies` 資料庫資料表，請以滑鼠右鍵按一下 [伺服器總管] 視窗中的 [`tblMovies` 資料庫] 資料表（Visual Web Developer 中的 [資料庫總管] 視窗），然後選取 [顯示資料表資料] 功能表選項。 您可以使用顯示的方格來插入 `movie` 記錄（請參閱 [圖 6]）。

[插入電影 ![](creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)

**圖 06**：插入電影（[按一下以觀看完整大小的影像](creating-model-classes-with-linq-to-sql-cs/_static/image18.png)）

將一些資料庫記錄新增至 `tblMovies` 資料表並執行應用程式後，您會看到 [圖 7] 中的頁面。 所有電影資料庫記錄都會顯示在項目符號清單中。

[![使用索引視圖顯示電影](creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)

**圖 07**：使用索引視圖顯示電影（[按一下以觀看完整大小的影像](creating-model-classes-with-linq-to-sql-cs/_static/image21.png)）

## <a name="using-the-repository-pattern"></a>使用存放庫模式

在上一節中，我們直接使用控制器動作內的 LINQ to SQL 類別。 我們直接從 `Index()` 控制器動作使用了 `MovieDataContext` 類別。 在簡單應用程式的情況下，這麼做不會有任何問題。 不過，當您需要建立更複雜的應用程式時，直接使用控制器類別中的 LINQ to SQL 會造成問題。

在控制器類別內使用 LINQ to SQL，會使未來難以切換資料存取技術。 例如，您可能會決定從使用 Microsoft LINQ to SQL 切換為使用 Microsoft Entity Framework 作為您的資料存取技術。 在這種情況下，您必須重寫應用程式中存取資料庫的每個控制器。

在控制器類別內使用 LINQ to SQL 也很容易為您的應用程式建立單元測試。 一般來說，在執行單元測試時，您不會想要與資料庫互動。 您想要使用單元測試來測試您的應用程式邏輯，而不是您的資料庫伺服器。

若要建立可更適應未來變更並可更輕鬆測試的 MVC 應用程式，您應該考慮使用存放庫模式。 當您使用儲存機制模式時，會建立個別的儲存機制類別，其中包含您所有的資料庫存取邏輯。

當您建立存放庫類別時，您會建立介面來代表存放庫類別所使用的所有方法。 在您的控制器中，您會針對介面（而不是存放庫）撰寫程式碼。 如此一來，您就可以在未來使用不同的資料存取技術來執行存放庫。

[清單 3] 中的介面名為 `IMovieRepository`，它代表名為 `ListAll()`的單一方法。

**清單3– `Models\IMovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample3.cs)]

[清單 4] 中的存放庫類別會執行 `IMovieRepository` 介面。 請注意，它包含名為 `ListAll()` 的方法，其對應于 `IMovieRepository` 介面所需的方法。

**清單4– `Models\MovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample4.cs)]

最後，[清單 5] 中的 `MoviesController` 類別會使用存放庫模式。 它不再直接使用 LINQ to SQL 類別。

**清單5– `Controllers\MoviesController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample5.cs)]

請注意，[清單 5] 中的 `MoviesController` 類別有兩個函式。 當您的應用程式正在執行時，會呼叫第一個函式，也就是無參數的函數。 此函式會建立 `MovieRepository` 類別的實例，並將它傳遞給第二個處理常式。

第二個函式具有單一參數： `IMovieRepository` 參數。 此函式只會將參數的值指派給名為 `_repository`的類別層級欄位。

`MoviesController` 類別利用稱為相依性插入模式的軟體設計模式。 特別是，它會使用稱為「函式相依性插入」的專案。 若要深入瞭解此模式，您可以閱讀下列文章：聖馬丁 Fowler。

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

請注意，`MoviesController` 類別中的所有程式碼（第一個函式除外）都會與 `IMovieRepository` 介面互動，而不是實際的 `MovieRepository` 類別。 程式碼會與抽象介面互動，而不是介面的具體執行。

如果您想要修改應用程式所使用的資料存取技術，則只要使用替代資料庫存取技術的類別，就可以執行 `IMovieRepository` 介面。 例如，您可以建立 `EntityFrameworkMovieRepository` 類別或 `SubSonicMovieRepository` 類別。 因為控制器類別是根據介面進行設計，所以您可以將 `IMovieRepository` 的新執行傳遞至控制器類別，而類別會繼續工作。

此外，如果您想要測試 `MoviesController` 類別，則可以將假的電影存放庫類別傳遞給 `HomeController`。 您可以使用不實際存取資料庫的類別來執行 `IMovieRepository` 類別，但包含 `IMovieRepository` 介面的所有必要方法。 如此一來，您就可以對 `MoviesController` 類別進行單元測試，而不需要實際存取實際的資料庫。

## <a name="summary"></a>總結

本教學課程的目的是要示範如何利用 Microsoft LINQ to SQL，來建立 MVC 模型類別。 我們檢查了兩種在 ASP.NET MVC 應用程式中顯示資料庫資料的策略。 首先，我們建立了 LINQ to SQL 類別，並直接在控制器動作中使用類別。 使用控制器內的 LINQ to SQL 類別，可讓您快速且輕鬆地在 MVC 應用程式中顯示資料庫資料。

接下來，我們探索了稍微比較棘手，但更良性的是顯示資料庫資料的路徑。 我們利用了存放庫模式，並將所有的資料庫存取邏輯放在個別的儲存機制類別中。 在我們的控制器中，我們會針對介面（而不是實體類別）撰寫所有程式碼。 儲存機制模式的優點是，它可讓我們在未來輕鬆地變更資料庫存取技術，讓我們能夠輕鬆地測試控制器類別。

> [!div class="step-by-step"]
> [上一頁](creating-model-classes-with-the-entity-framework-cs.md)
> [下一頁](displaying-a-table-of-database-data-cs.md)
