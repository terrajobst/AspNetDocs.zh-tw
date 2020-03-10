---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
title: 將驗證加入至模型 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教學課程的更新版本可在這裡使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更容易遵循和示範 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 5d9a2999-fcc4-4c45-a018-271fddf74a3b
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: c9f6699c5d3500d4c1fcade9252aeb9dd92983da
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615028"
---
# <a name="adding-validation-to-the-model"></a>將驗證新增至模型

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > 本教學課程的更新版本可在[這裡](../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 它更安全、更容易遵循，並示範更多功能。

在本節中，您會將驗證邏輯新增至 `Movie` 模型，而且您將確保在使用者嘗試使用應用程式建立或編輯電影時，會強制執行驗證規則。

## <a name="keeping-things-dry"></a>讓事情晾乾

ASP.NET MVC 的其中一個核心設計原則是幹（&quot;不重複原則&quot;）。 ASP.NET MVC 鼓勵您只指定一次功能或行為，然後讓它反映在應用程式中的所有位置。 這可減少您需要撰寫的程式碼數量，讓您撰寫的程式碼更容易出錯且更容易維護。

ASP.NET MVC 和 Entity Framework Code First 所提供的驗證支援，是實際運作原則的絕佳範例。 您可以在一個位置以宣告方式指定驗證規則（在模型類別中），而規則會在應用程式的任何位置強制執行。

讓我們看看如何在電影應用程式中利用這項驗證支援。

## <a name="adding-validation-rules-to-the-movie-model"></a>將驗證規則新增至電影模型

首先，將一些驗證邏輯新增至 `Movie` 類別。

開啟 *Movie.cs* 檔案。 在檔案的頂端新增參考[`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間的 `using` 語句：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

請注意，命名空間不包含 `System.Web`。 DataAnnotations 提供一組內建的驗證屬性，您可以將其以宣告方式套用至任何類別或屬性。

現在更新 `Movie` 類別，以利用內建的[`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)、 [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)和[`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)驗證屬性。 使用下列程式碼作為套用屬性的範例。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs?highlight=4,10,13,17)]

執行應用程式，您會再次收到下列執行階段錯誤：

***在建立資料庫之後，支援 ' MovieDBCoNtext ' 內容的模型已經變更。請考慮使用 Code First 移轉來更新資料庫（[https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)）。***

我們將使用「遷移」來更新架構。 建立解決方案，然後開啟 [**套件管理員主控台**] 視窗並輸入下列命令：

[!code-console[Main](adding-validation-to-the-model/samples/sample3.cmd)]

當此命令完成時，Visual Studio 會開啟類別檔案，該檔案會使用指定的名稱（*AddDataAnnotationsMig*）來定義新的 `DbMigration` 衍生類別，而在 `Up` 方法中，您可以看到更新架構條件約束的程式碼。 [`Title`] 和 [`Genre`] 欄位不再是可為 null （也就是說，您必須輸入一個值），而 [`Rating`] 欄位的最大長度為5。

驗證屬性會指定您想要強制執行模型屬性套用的行為。 `Required` 屬性指出屬性必須具有值;在此範例中，電影必須有 `Title`、`ReleaseDate`、`Genre`和 `Price` 屬性的值，才能有效。 `Range` 屬性會將值限制在指定的範圍內。 `StringLength` 屬性可讓您設定字串屬性的最大長度，並選擇性設定其最小長度。 預設需要內部類型（例如 `decimal, int, float, DateTime`），而且不需要 `Required` 屬性。

Code First 可確保在應用程式將變更儲存到資料庫之前，會強制執行您在模型類別上指定的驗證規則。 例如，下列程式碼會在呼叫 `SaveChanges` 方法時擲回例外狀況，因為遺漏了數個必要的 `Movie` 屬性值，而且價格為零（超出有效範圍）。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs?highlight=7-8)]

由 .NET Framework 自動強制執行驗證規則有助於讓應用程式更穩固。 它也確保您不會忘記要驗證某些項目，不小心讓不正確的資料進入資料庫。

以下是已更新之*Movie.cs*檔案的完整程式代碼清單：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC 中的驗證錯誤 UI

重新執行應用程式，並流覽至 */Movies* URL。

按一下 [**建立新**的] 連結以新增電影。 在表單中填寫一些不正確值，然後按一下 [**建立**] 按鈕。

![8_validationErrors](adding-validation-to-the-model/_static/image1.png)

> [!NOTE]
> 若要支援對小數點使用逗號（&quot;，&quot;）之非英文地區設定的 jQuery 驗證，您必須包含全球化 *.js*和您的特定*文化特性/全球化. 文化特性 .js*檔案（從[https://github.com/jquery/globalize](https://github.com/jquery/globalize) ）和 JavaScript，以使用 `Globalize.parseFloat`。 下列程式碼顯示對 Views\Movies\Edit.cshtml 檔案所做的修改，以使用 &quot;fr-fr&quot; 文化特性：

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

請注意表單如何自動使用紅色框線色彩來反白顯示包含無效資料的文字方塊，並且在每個文字旁發出適當的驗證錯誤訊息。 用戶端 (使用 JavaScript 和 jQuery) 與伺服器端 (若使用者已停用 JavaScript 時) 都會強制執行這些錯誤。

真正的好處是，您不需要在 `MoviesController` 類別或*建立. cshtml*視圖中變更一行程式碼，就能啟用此驗證 UI。 您稍早在本教學課程中建立的控制器和檢視會自動拾取您指定的驗證規則 (在 `Movie` 模型類別的屬性 (property) 上使用驗證屬性 (attribute))。

您可能已注意到屬性 `Title` 和 `Genre`，在您提交表單（按下 [**建立**] 按鈕），或在輸入欄位中輸入文字並將它移除之前，不會強制執行必要的屬性。 對於一開始是空的欄位（例如 [建立] 視圖上的欄位），而且只有 [必要] 屬性和其他驗證屬性，您可以執行下列動作來觸發驗證：

1. Tab 鍵放入欄位中。
2. 輸入一些文字。
3. 按下 Tab 鍵切換至下一個欄位。
4. Tab 回到欄位。
5. 移除文字。
6. 按下 Tab 鍵切換至下一個欄位。

上述順序會觸發必要的驗證，而不會按下 [提交] 按鈕。 只要按下 [提交] 按鈕，而不輸入任何欄位，就會觸發用戶端驗證。 直到沒有任何用戶端驗證錯誤後，表單資料才會傳送至伺服器。 您可以藉由將中斷點放在 HTTP Post 方法中，或使用[fiddler 工具](http://fiddler2.com/fiddler2/)或 IE 9 [F12 開發人員工具](https://msdn.microsoft.com/ie/aa740478)來進行測試。

![](adding-validation-to-the-model/_static/image2.png)

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>如何在 Create View 和 Create Action 方法中進行驗證

您可能奇怪如何在不更新控制器或檢視程式碼的狀況下產生驗證 UI。 下一個清單會顯示 `MovieController` 類別中的 `Create` 方法看起來如何。 它們與您稍早在本教學課程中建立它們的方式不一樣。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs?highlight=12,15)]

第一個 (HTTP GET)`Create` 動作方法會顯示初始建立表單。 第二個 (`[HttpPost]`) 版本處理表單張貼。 第二個 `Create` 方法 (`HttpPost` 版本) 會呼叫`ModelState.IsValid` 檢查電影是否有任何驗證錯誤。 呼叫此方法會評估已套用至物件的所有驗證屬性。 如果物件有驗證錯誤，則 `Create` 方法會重新顯示表單。 如果沒有任何錯誤，方法即會將新的電影儲存到資料庫。 在我們使用的電影範例中，**當用戶端偵測到驗證錯誤時，表單不會張貼到伺服器; 第二個**`Create`**方法則**不會被呼叫。 如果您在瀏覽器中停用 JavaScript，則會停用用戶端驗證，而且 HTTP POST `Create` 方法會呼叫 `ModelState.IsValid` 以檢查電影是否有任何驗證錯誤。

您可以在 `HttpPost Create` 方法中設定中斷點，並確認永遠不會呼叫該方法，用戶端驗證就不會在偵測到驗證錯誤時，提交表單資料。 如果您停用瀏覽器的 JavaScript，然後提交有錯誤的表單，就會叫用中斷點。 您仍可使用沒有 JavaScript 的完整驗證。 下圖顯示如何在 Internet Explorer 中停用 JavaScript。

![](adding-validation-to-the-model/_static/image3.png)

![](adding-validation-to-the-model/_static/image4.png)

下圖顯示如何停用 FireFox 瀏覽器的 JavaScript。

![](adding-validation-to-the-model/_static/image5.png)

下圖顯示如何使用 Chrome 瀏覽器停用 JavaScript。

![](adding-validation-to-the-model/_static/image6.png)

以下是您稍早在本教學課程中 scaffold 的*建立. cshtml*視圖範本。 上述動作方法會使用它來顯示初始表單，以及在發生錯誤時重新顯示它。

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample8.cshtml?highlight=22-23,30-31,38-39,46-47)]

請注意程式碼如何使用 `Html.EditorFor` helper 來輸出每個 `Movie` 屬性的 `<input>` 元素。 在此協助程式旁呼叫 `Html.ValidationMessageFor` helper 方法。 這兩個 helper 方法會使用由控制器傳遞至視圖的模型物件（在此案例中為 `Movie` 物件）。 它們會自動尋找在模型上指定的驗證屬性，並適當地顯示錯誤訊息。

這種方法的好處是，控制器或建立視圖範本都無法得知所強制執行的實際驗證規則，或顯示的特定錯誤訊息。 驗證規則和錯誤字串只在 `Movie` 類別中指定。 這些相同的驗證規則會自動套用至編輯檢視，以及您可能會建立以編輯模型的任何其他 views 範本。

如果您稍後想要變更驗證邏輯，您可以在模型中加入驗證屬性（在此範例中為 `movie` 類別），以在一個位置中執行此動作。 您不必擔心應用程式的不同部分會與規則強制執行的方式不一致，所有的驗證邏輯都是在同一個地方定義，用於所有位置。 這會讓程式碼非常整齊乾淨，容易維護及發展。 這表示您會完全接受 DRY 原則。

## <a name="adding-formatting-to-the-movie-model"></a>將格式新增至電影模型

開啟 *Movie.cs* 檔案並檢查 `Movie` 類別。 除了內建的驗證屬性集之外， [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間還會提供格式屬性。 我們已將[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)列舉值套用至發行日期和價格欄位。 下列程式碼顯示具有適當[`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性的 `ReleaseDate` 和 `Price` 屬性。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性不是驗證屬性，而是用來告訴視圖引擎如何呈現 HTML。 在上述範例中，`DataType.Date` 屬性會將電影日期顯示為僅限日期，沒有時間。 例如，下列[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性不會驗證資料的格式：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

以上所列的屬性只會提供 view engine 用來格式化資料的提示（如 &lt;URL 的&gt; 和 &lt;href =&quot;mailto:EmailAddress&quot;電子郵件的屬性。&gt; 您可以使用[RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)屬性來驗證資料的格式。

另一種使用 `DataType` 屬性的方法，您可以明確地設定[`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx)值。 下列程式碼顯示具有日期格式字串（也就是 &quot;d&quot;）的 [發行日期] 屬性。 您會使用此來指定在發行日期中不需要時間。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample11.cs)]

完整的 `Movie` 類別如下所示。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample12.cs)]

執行應用程式，並流覽至 `Movies` 控制器。 發行日期和價格的格式正確。 下圖顯示使用 &quot;fr-fr&quot; 作為文化特性的發行日期和價格。

![8_format_SM](adding-validation-to-the-model/_static/image7.png)

下圖顯示使用預設文化特性（英文 US）所顯示的相同資料。

![](adding-validation-to-the-model/_static/image8.png)

在數列的下一個部分中，我們會檢閱應用程式，並對自動產生的 `Details` 和 `Delete` 方法進行一些改良。

> [!div class="step-by-step"]
> [上一頁](adding-a-new-field-to-the-movie-model-and-table.md)
> [下一頁](examining-the-details-and-delete-methods.md)
