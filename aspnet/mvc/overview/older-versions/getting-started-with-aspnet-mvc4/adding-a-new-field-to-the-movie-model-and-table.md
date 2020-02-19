---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: 將新欄位新增至電影模型和資料表 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教學課程的更新版本可在這裡使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更容易遵循和示範 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: d966b95163f64b20a17d2327a12c5d6c44a4a66b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457696"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table"></a>將新欄位新增至電影模型和資料表

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > 本教學課程的更新版本可在[這裡](../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 它更安全、更容易遵循，並示範更多功能。

在本節中，您將使用 Entity Framework Code First 移轉來遷移模型類別的某些變更，以便將變更套用至資料庫。

根據預設，當您使用 Entity Framework Code First 自動建立資料庫時（如您稍早在本教學課程中所做的），Code First 會將資料表新增至資料庫，以協助追蹤資料庫的架構是否與其產生的模型類別同步。 如果它們不是同步的，Entity Framework 會擲回錯誤。 這可讓您更輕鬆地在開發期間追蹤問題，而您可能只會在執行時間發現（藉由隱匿錯誤）。

## <a name="setting-up-code-first-migrations-for-model-changes"></a>設定模型變更的 Code First 移轉

如果您使用 Visual Studio 2012，請按兩下方案總管中的 [ *.mdf* ] 檔案，開啟 [資料庫] 工具。 Visual Studio Express for Web 會顯示資料庫總管，Visual Studio 2012 會顯示伺服器總管。 如果您使用 Visual Studio 2010，請使用 SQL Server 物件總管。

在資料庫工具（資料庫總管、伺服器總管或 SQL Server 物件總管）中，以滑鼠右鍵按一下 `MovieDBContext`，然後選取 [**刪除**] 以卸載電影資料庫。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

流覽回到方案總管。 以滑鼠右鍵按一下 [ *.mdf* ] 檔案，然後選取 [**刪除**] 以移除電影資料庫。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

建置應用程式，確定沒有任何錯誤。

在 [工具] 功能表中按一下 [NuGet 套件管理員]，然後按一下 [套件管理員主控台]。

![新增套件手冊](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

在 [**套件管理員主控台**] 視窗的 `PM>` 提示字元中，輸入 "MvcMovie" （MovieDBCoNtext）。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

[**啟用-遷移**] 命令（如上所示）會在新的 [*遷移*] 資料夾中建立*Configuration.cs*檔案。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

Visual Studio 會開啟*Configuration.cs*檔案。 使用下列程式碼取代*Configuration.cs*檔案中的 `Seed` 方法：

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

以滑鼠右鍵按一下 `Movie` 底下的紅色曲線，然後選取 [**解析**]，然後**使用** **MvcMovie。**

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

這麼做會加入下列 using 語句：

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> Code First 移轉會在每次遷移之後呼叫 `Seed` 方法（也就是在套件管理員主控台中呼叫**update-database** ），而這個方法會更新已插入的資料列，如果尚未存在，則會將其插入。

**按下 CTRL-SHIFT-B 以建立專案。** （如果您目前未建立，下列步驟將會失敗）。

下一個步驟是建立初始遷移的 `DbMigration` 類別。 這個遷移會建立新的資料庫，這就是您在上一個步驟中刪除*movie .mdf*檔案的原因。

在 [**套件管理員主控台**] 視窗中，輸入「新增-遷移初始」命令以建立初始遷移。 「初始」名稱是任意的，用來命名所建立的遷移檔案。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

Code First 移轉會在 [*遷移*] 資料夾中建立另一個類別檔案（名稱為 *{DateStamp}\_Initial.cs* ），而此類別包含建立資料庫架構的程式碼。 使用時間戳預先修正遷移檔案名，以協助進行排序。 檢查 *{DateStamp}\_Initial.cs*檔案，其中包含為 Movie DB 建立電影資料表的指示。 當您更新下列指示中的資料庫時，這個 *{DateStamp}\_Initial.cs*檔案將會執行，並建立資料庫架構。 然後，會執行**種子**方法，將測試資料填入資料庫。

在 [**套件管理員主控台**] 中，輸入「更新-資料庫」命令來建立資料庫，並執行**種子**方法。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

如果您收到錯誤訊息，指出資料表已經存在，而且無法建立，可能是因為您在刪除資料庫之後，以及執行 `update-database`之前，已執行應用程式。 在這種情況下，請再次刪除 *.mdf*檔案，然後重試 `update-database` 命令。 如果您仍然收到錯誤，請刪除 [遷移] 資料夾和 [內容]，然後從這個頁面頂端的指示開始（也就是刪除 [ *.mdf* ] 檔案，然後繼續進行 [啟用-遷移]）。

執行應用程式，並流覽至 */Movies* URL。 會顯示種子資料。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>將 Rating 屬性新增至電影模型

首先，將新的 `Rating` 屬性加入至現有的 `Movie` 類別。 開啟*Models\Movie.cs*檔案，然後加入 `Rating` 屬性，如下所示：

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

完整的 `Movie` 類別現在看起來像下列程式碼：

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

使用 [組建] &gt;[**建立電影**] 功能表命令，或按 CTRL SHIFT B**來建立應用**程式。

既然您已更新 `Model` 類別，您也必須更新 *\Views\Movies\Index.cshtml*和 *\Views\Movies\Create.cshtml* view 範本，才能在瀏覽器視圖中顯示新的 `Rating` 屬性。

開啟<em>\Views\Movies\Index.cshtml</em>檔案，然後在 [<strong>價格</strong>] 資料行的正後方加入 `<th>Rating</th>` 欄標題。 然後在範本結尾附近新增 `<td>` 資料行，以轉譯 `@item.Rating` 值。 以下是更新的<em>Index. cshtml</em>視圖範本的樣子：

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

接下來，開啟 *\Views\Movies\Create.cshtml*檔案，並在接近表單結尾處新增下列標記。 這會轉譯一個文字方塊，讓您可以在建立新電影時指定評等。

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

您現已更新應用程式代碼，以支援新的 `Rating` 屬性。

現在執行應用程式，並流覽至 */Movies* URL。 不過，當您這麼做時，您會看到下列其中一個錯誤：

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

您看到這個錯誤是因為應用程式中更新的 `Movie` 模型類別，現在與現有資料庫 `Movie` 資料表的架構不同。 (資料庫資料表中沒有任何 `Rating` 資料行)。

有幾個方法可以解決這個錯誤：

1. 讓 Entity Framework 自動卸除資料庫，並重新依據新的模型類別結構描述來建立資料庫。 在測試資料庫上進行開發時，這個方法非常方便;它可讓您快速地將模型和資料庫架構進化在一起。 不過，缺點是您會遺失資料庫中的現有資料，因此您*不*會想要在生產資料庫上使用此方法！ 使用初始化運算式將測試資料自動植入資料庫，通常是開發應用程式的有效方式。 如需 Entity Framework 資料庫初始化運算式的詳細資訊，請參閱 Tom 作者: dykstra 的[ASP.NET MVC/Entity Framework 教學](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)課程。
2. 您可明確修改現有資料庫的結構描述，使其符合模型類別。 這種方法的優點是可以保留您的資料。 您可以手動方式或藉由建立資料庫變更指令碼來進行這項變更。
3. 使用 Code First 移轉來更新資料庫結構描述。

在本教學課程中，我們將使用 Code First 移轉。

更新種子方法，讓它提供新資料行的值。 開啟 [Migrations\Configuration.cs 檔案]，並將 [評等] 欄位新增至每個 Movie 物件。

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

建立解決方案，然後開啟 [**套件管理員主控台**] 視窗並輸入下列命令：

`add-migration AddRatingMig`

`add-migration` 命令會告訴遷移架構使用目前的 movie DB 架構來檢查目前的電影模型，並建立必要的程式碼來將資料庫移轉至新的模型。 AddRatingMig 是任意的，用來命名遷移檔案。 使用有意義的名稱來進行遷移步驟會很有説明。

當此命令完成時，Visual Studio 會開啟定義新 `DbMigration` 衍生類別的類別檔案，而在 `Up` 方法中，您可以看到建立新資料行的程式碼。

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

建立解決方案，然後在 [**套件管理員主控台**] 視窗中輸入 [更新資料庫] 命令。

下圖顯示 [**套件管理員主控台**] 視窗中的輸出（前面加上 AddRatingMig 的日期戳記會有所不同）。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

重新執行應用程式，並流覽至/Movies URL。 您可以看到新的評等欄位。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

按一下 [**建立新**的] 連結以新增電影。 請注意，您可以加入評等。

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

按一下 **[建立]** 。 新電影（包括評等）現在會顯示在電影清單中：

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

您也應該將 [`Rating`] 欄位加入至 [編輯]、[詳細資料] 和 [SearchIndex] 視圖範本。

您可以再次在 [**套件管理員主控台**] 視窗中輸入「更新資料庫」命令，而且不會進行任何變更，因為架構符合模型。

在本節中，您會看到如何修改模型物件，並讓資料庫與變更保持同步。 您也學到以範例資料填入新建立資料庫的方法，讓您可以試試看案例。 接下來，我們將探討如何將更豐富的驗證邏輯新增至模型類別，並讓某些商務規則得以強制執行。

> [!div class="step-by-step"]
> [上一頁](examining-the-edit-methods-and-edit-view.md)
> [下一頁](adding-validation-to-the-model.md)
