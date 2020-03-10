---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
title: 將新欄位新增至影片模型和資料庫資料表（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 28970e1b-1845-4015-86ef-121e52a6c397
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: b2b26b6009c55f02c8a4159bda839fe7aefea4c0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540576"
---
# <a name="adding-a-new-field-to-the-movie-model-and-database-table-vb"></a>將新欄位新增至影片模型和資料庫資料表 (VB)

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。 開始之前，請先確定您已安裝下列必要條件。 您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，您可以使用下列連結個別安裝必要條件：
> 
> - [Visual Studio Web Developer Express SP1 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）
> 
> 如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主題提供具有 VB.NET 原始程式碼的 Visual Web Developer 專案。 [下載 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您想C#要的話，請切換到本教學課程的[ C#版本](../cs/adding-a-new-field.md)。

在本節中，您將對模型類別進行一些變更，並瞭解如何更新資料庫架構，以符合模型的變更。

## <a name="adding-a-rating-property-to-the-movie-model"></a>將 Rating 屬性新增至電影模型

首先，將新的 `Rating` 屬性加入至現有的 `Movie` 類別。 開啟*Movie.cs*檔案，然後加入 `Rating` 屬性，如下所示：

[!code-vb[Main](adding-a-new-field/samples/sample1.vb)]

完整的 `Movie` 類別現在看起來像下列程式碼：

[!code-vb[Main](adding-a-new-field/samples/sample2.vb)]

使用 [ **Debug** &gt;**組建電影**] 功能表命令來重新編譯應用程式。

既然您已更新 `Model` 類別，您也必須更新 *\Views\Movies\Index.vbhtml*和 *\Views\Movies\Create.vbhtml* view 範本，才能支援新的 `Rating` 屬性。

開啟<em>\Views\Movies\Index.vbhtml</em>檔案，然後在 [<strong>價格</strong>] 資料行的正後方加入 `<th>Rating</th>` 欄標題。 然後在範本結尾附近新增 `<td>` 資料行，以轉譯 `@item.Rating` 值。 以下是更新的<em>Index. vbhtml</em>視圖範本看起來像這樣：

[!code-vbhtml[Main](adding-a-new-field/samples/sample3.vbhtml)]

接下來，開啟 *\Views\Movies\Create.vbhtml*檔案，並在接近表單結尾處新增下列標記。 這會轉譯一個文字方塊，讓您可以在建立新電影時指定評等。

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a>管理模型和資料庫架構的差異

您現已更新應用程式代碼，以支援新的 `Rating` 屬性。

現在執行應用程式，並流覽至 */Movies* URL。 不過，當您這麼做時，您會看到下列錯誤：

![](adding-a-new-field/_static/image1.png)

您看到這個錯誤是因為應用程式中更新的 `Movie` 模型類別，現在與現有資料庫 `Movie` 資料表的架構不同。 (資料庫資料表中沒有任何 `Rating` 資料行)。

根據預設，當您使用 Entity Framework Code First 自動建立資料庫時（如您稍早在本教學課程中所做的），Code First 會將資料表新增至資料庫，以協助追蹤資料庫的架構是否與其產生的模型類別同步。 如果它們不是同步的，Entity Framework 會擲回錯誤。 這可讓您更輕鬆地在開發期間追蹤問題，而您可能只會在執行時間發現（藉由隱匿錯誤）。 同步檢查功能會造成您剛才看到的錯誤訊息顯示出來。

有兩種方法可以解決此錯誤：

1. 讓 Entity Framework 自動卸除資料庫，並重新依據新的模型類別結構描述來建立資料庫。 在測試資料庫上進行開發時，這個方法非常方便，因為它可讓您快速地將模型和資料庫架構進化在一起。 不過，缺點是您會遺失資料庫中的現有資料，因此您*不*會想要在生產資料庫上使用此方法！
2. 您可明確修改現有資料庫的結構描述，使其符合模型類別。 這種方法的優點是可以保留您的資料。 您可以手動方式或藉由建立資料庫變更指令碼來進行這項變更。

在本教學課程中，我們將使用第一種方法，您會在模型變更時，讓 Entity Framework Code First 自動重新建立資料庫。

## <a name="automatically-re-creating-the-database-on-model-changes"></a>在模型變更時自動重新建立資料庫

讓我們更新應用程式，如此一來，每當您變更應用程式的模型時，Code First 就會自動卸載並重新建立資料庫。

> [!NOTE] 
> 
> **警告**只有當您使用開發或測試資料庫，而*不*是在包含實際資料的生產資料庫上時，才應該啟用這種方法來自動卸載和重新建立資料庫。 在實際伺服器上使用它可能會導致資料遺失。

在**方案總管**中，以滑鼠右鍵按一下 [*模型*] 資料夾，選取 [**新增**]，然後選取 [**類別**]。

![](adding-a-new-field/_static/image2.png)

將類別命名 &quot;MovieInitializer&quot;。 更新 `MovieInitializer` 類別，以包含下列程式碼：

[!code-vb[Main](adding-a-new-field/samples/sample5.vb)]

`MovieInitializer` 類別指定模型所使用的資料庫應該卸載，並在模型類別變更時自動重新建立。 程式碼包含 `Seed` 方法，可指定在建立（或重新建立）時自動新增至資料庫的一些預設資料。 這可讓您在資料庫中填入一些範例資料，而不需要您在每次進行模型變更時手動填入。

既然您已定義 `MovieInitializer` 類別，您會想要將它連接，以便每次應用程式執行時，它會檢查模型類別是否與資料庫中的架構不同。 如果是，您可以執行初始化運算式來重新建立資料庫，以符合模型，然後在資料庫中填入範例資料。

開啟位於 `MvcMovies` 專案根目錄的*global.asax*檔案：

*Global.asax*檔案包含定義專案之整個應用程式的類別，並且包含在應用程式第一次啟動時執行的 `Application_Start` 事件處理常式。

尋找 `Application_Start` 方法，並在方法的開頭新增對 `Database.SetInitializer` 的呼叫，如下所示：

[!code-vb[Main](adding-a-new-field/samples/sample6.vb)]

您剛才加入的 `Database.SetInitializer` 語句指出，如果架構和資料庫不相符，就應該自動刪除和重新建立 `MovieDBContext` 實例所使用的資料庫。 如您所見，它也會將 `MovieInitializer` 類別中所指定的範例資料填入資料庫中。

關閉*global.asax*檔案。

重新執行應用程式，並流覽至 */Movies* URL。 當應用程式啟動時，它會偵測模型結構不再符合資料庫架構。 它會自動重新建立資料庫，以符合新的模型結構，並在資料庫中填入範例電影：

![7_MyMovieList_SM](adding-a-new-field/_static/image3.png)

按一下 [**建立新**的] 連結以新增電影。 請注意，您可以加入評等。

[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)

按一下 [建立]。 新電影（包括評等）現在會顯示在電影清單中：

![7_ourNewMovie_SM](adding-a-new-field/_static/image6.png)

在本節中，您會看到如何修改模型物件，並讓資料庫與變更保持同步。 您也學到以範例資料填入新建立資料庫的方法，讓您可以試試看案例。 接下來，我們將探討如何將更豐富的驗證邏輯新增至模型類別，並讓某些商務規則得以強制執行。

> [!div class="step-by-step"]
> [上一頁](examining-the-edit-methods-and-edit-view.md)
> [下一頁](adding-validation-to-the-model.md)
