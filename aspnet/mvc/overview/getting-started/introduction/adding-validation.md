---
uid: mvc/overview/getting-started/introduction/adding-validation
title: 正在新增驗證 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 9f35ca15-e216-4db6-9ebf-24380b0f31b4
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-validation
msc.type: authoredcontent
ms.openlocfilehash: f508d9e38dab5cc4cc44cc5aaa4eae87cf273bd5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615721"
---
# <a name="adding-validation"></a>新增驗證

依[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

在本節中，您會將驗證邏輯新增至 `Movie` 模型，而且您將確保在使用者嘗試使用應用程式建立或編輯電影時，會強制執行驗證規則。

## <a name="keeping-things-dry"></a>讓事情晾乾

ASP.NET MVC 的其中一個核心設計原則是[幹](http://en.wikipedia.org/wiki/Don't_repeat_yourself)（&quot;不重複原則&quot;）。 ASP.NET MVC 鼓勵您只指定一次功能或行為，然後讓它反映在應用程式中的所有位置。 這可減少您需要撰寫的程式碼數量，讓您撰寫的程式碼更容易出錯且更容易維護。

ASP.NET MVC 和 Entity Framework Code First 所提供的驗證支援，是實際運作原則的絕佳範例。 您可以在一個位置以宣告方式指定驗證規則（在模型類別中），而規則會在應用程式的任何位置強制執行。

讓我們看看如何在電影應用程式中利用這項驗證支援。

## <a name="adding-validation-rules-to-the-movie-model"></a>將驗證規則新增至電影模型

首先，將一些驗證邏輯新增至 `Movie` 類別。

開啟 *Movie.cs* 檔案。 請注意， [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間不包含 `System.Web`。 DataAnnotations 提供一組內建的驗證屬性，您可以將其以宣告方式套用至任何類別或屬性。 （它也包含格式屬性（例如[資料類型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)），可協助進行格式設定而不提供任何驗證。）

現在更新 `Movie` 類別，以利用內建的[`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)、 [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)、 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)和[`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)驗證屬性。 將 `Movie` 類別取代為下列內容：

[!code-csharp[Main](adding-validation/samples/sample1.cs?highlight=5,13-15,18-19,22-23)]

[`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)屬性會設定字串的最大長度，並在資料庫上設定這項限制，因此資料庫架構將會變更。 以滑鼠右鍵按一下**伺服器瀏覽器**中的 [**電影**] 資料表，然後按一下 [**開啟資料表定義**]：

![](adding-validation/_static/image1.png)

在上圖中，您可以看到所有的字串欄位都設定為[NVARCHAR （MAX）](https://technet.microsoft.com/library/ms186939.aspx)。 我們將使用「遷移」來更新架構。 建立解決方案，然後開啟 [**套件管理員主控台**] 視窗並輸入下列命令：

[!code-console[Main](adding-validation/samples/sample2.cmd)]

當此命令完成時，Visual Studio 會開啟類別檔案，該檔案會使用指定的名稱（`DataAnnotations`）來定義新的 `DbMigration` 衍生類別，而在 `Up` 方法中，您可以看到更新架構條件約束的程式碼：

[!code-csharp[Main](adding-validation/samples/sample3.cs)]

[`Genre`] 欄位不再是可為 null （也就是您必須輸入值）。 `Rating` 欄位的最大長度為5，`Title` 的最大長度為60。 `Title` 的最小長度為3，而 `Price` 上的範圍未建立架構變更。

檢查電影架構：

![](adding-validation/_static/image2.png)

字串欄位會顯示新的長度限制，且 `Genre` 不再檢查為可為 null。

驗證屬性會指定您想要強制執行模型屬性套用的行為。 `Required` 和 `MinimumLength` 屬性 (attribute) 指出屬性 (property) 必須是值；但無法防止使用者輸入空格以滿足此驗證。 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)屬性是用來限制可輸入的字元。 上述程式碼中的 `Genre` 和 `Rating` 必須只使用字母 (不允許使用空白字元、數字及特殊字元)。 [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)屬性會將值限制在指定的範圍內。 `StringLength` 屬性可讓您設定字串屬性的最大長度，並選擇性設定其最小長度。 實數值型別（例如 `decimal, int, float, DateTime`）原本就是必要的，而且不需要 `Required` 屬性。

Code First 可確保在應用程式將變更儲存到資料庫之前，會強制執行您在模型類別上指定的驗證規則。 例如，下列程式碼會在呼叫 `SaveChanges` 方法時擲回[DbEntityValidationException](https://msdn.microsoft.com/library/system.data.entity.validation.dbentityvalidationexception(v=vs.103).aspx)例外狀況，因為遺漏了數個必要的 `Movie` 屬性值：

[!code-csharp[Main](adding-validation/samples/sample4.cs)]

上述程式碼會擲回下列例外狀況：

*一或多個實體的驗證失敗。如需詳細資訊，請參閱 ' EntityValidationErrors ' 屬性。*

由 .NET Framework 自動強制執行驗證規則有助於讓應用程式更穩固。 它也確保您不會忘記要驗證某些項目，不小心讓不正確的資料進入資料庫。

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC 中的驗證錯誤 UI

執行應用程式，並流覽至 */Movies* URL。

按一下 [**建立新**的] 連結以新增電影。 使用無效值填寫表單。 jQuery 用戶端驗證一偵測到錯誤，就會顯示錯誤訊息。

![8_validationErrors](adding-validation/_static/image3.png)

> [!NOTE]
> 若要針對使用逗號（"，"）作為小數點的非英文地區設定支援 jQuery 驗證，您必須包含此教學課程中先前所述的 NuGet 全球化。

請注意表單如何自動使用紅色框線色彩來反白顯示包含無效資料的文字方塊，並且在每個文字旁發出適當的驗證錯誤訊息。 用戶端 (使用 JavaScript 和 jQuery) 與伺服器端 (若使用者已停用 JavaScript 時) 都會強制執行這些錯誤。

真正的好處是，您不需要在 `MoviesController` 類別或*建立. cshtml*視圖中變更一行程式碼，就能啟用此驗證 UI。 您稍早在本教學課程中建立的控制器和檢視會自動拾取您指定的驗證規則 (在 `Movie` 模型類別的屬性 (property) 上使用驗證屬性 (attribute))。 使用 `Edit` 動作方法測試驗證，即會套用相同的驗證。

直到沒有任何用戶端驗證錯誤後，表單資料才會傳送至伺服器。 您可以使用[fiddler 工具](http://fiddler2.com/fiddler2/)或 IE [F12 開發人員工具](https://msdn.microsoft.com/ie/aa740478)，將中斷點放在 HTTP Post 方法中，藉以確認這點。

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>如何在 Create View 和 Create Action 方法中進行驗證

您可能奇怪如何在不更新控制器或檢視程式碼的狀況下產生驗證 UI。 下一個清單會顯示 `MovieController` 類別中的 `Create` 方法看起來如何。 它們與您稍早在本教學課程中建立它們的方式不一樣。

[!code-csharp[Main](adding-validation/samples/sample5.cs)]

第一個 (HTTP GET)`Create` 動作方法會顯示初始建立表單。 第二個 (`[HttpPost]`) 版本處理表單張貼。 第二個 `Create` 方法（`HttpPost` 版本）會檢查 `ModelState.IsValid` 以查看電影是否有任何驗證錯誤。 取得此屬性會評估已套用至物件的任何驗證屬性。 如果物件有驗證錯誤，`Create` 方法就會重新出現表單。 如果沒有任何錯誤，方法即會將新的電影儲存到資料庫。 在我們的電影範例中，**當用戶端偵測到驗證錯誤時，不會將表單張貼至伺服器; 第二個**`Create`**方法則**不會被呼叫。 如果您在瀏覽器中停用 JavaScript，則會停用用戶端驗證，而 HTTP POST `Create` 方法會 `ModelState.IsValid` 檢查電影是否有任何驗證錯誤。

您可以在 `HttpPost Create` 方法中設定中斷點，並確認永遠不會呼叫該方法，用戶端驗證就不會在偵測到驗證錯誤時，提交表單資料。 如果您停用瀏覽器的 JavaScript，然後提交有錯誤的表單，就會叫用中斷點。 您仍可使用沒有 JavaScript 的完整驗證。 下圖顯示如何在 Internet Explorer 中停用 JavaScript。

![](adding-validation/_static/image5.png)

![](adding-validation/_static/image6.png)

下圖顯示如何停用 FireFox 瀏覽器的 JavaScript。

![](adding-validation/_static/image7.png)

下圖顯示如何停用 Chrome 瀏覽器的 JavaScript。

![](adding-validation/_static/image8.png)

以下是您稍早在本教學課程中 scaffold 的*建立. cshtml*視圖範本。 上述動作方法會使用它來顯示初始表單，以及在發生錯誤時重新顯示它。

[!code-cshtml[Main](adding-validation/samples/sample6.cshtml?highlight=16-17)]

請注意程式碼如何使用 `Html.EditorFor` helper 來輸出每個 `Movie` 屬性的 `<input>` 元素。 在此協助程式旁呼叫 `Html.ValidationMessageFor` helper 方法。 這兩個 helper 方法會使用由控制器傳遞至視圖的模型物件（在此案例中為 `Movie` 物件）。 它們會自動尋找在模型上指定的驗證屬性，並適當地顯示錯誤訊息。

此方法最好的一點在於，控制器和 `Create` 檢視範本對要強制執行的實際驗證規則，或顯示的特定錯誤訊息，全都一無所知。 驗證規則和錯誤字串只在 `Movie` 類別中指定。 這些相同的驗證規則會自動套用到 `Edit` 檢視，以及任何其他您可能建立以編輯模型的檢視範本。

如果您稍後想要變更驗證邏輯，您可以在模型中加入驗證屬性（在此範例中為 `movie` 類別），以在一個位置中執行此動作。 您不必擔心應用程式的不同部分會與規則強制執行的方式不一致，所有的驗證邏輯都是在同一個地方定義，用於所有位置。 這會讓程式碼非常整齊乾淨，容易維護及發展。 這表示您將完全接受這項*試*原則。

## <a name="using-datatype-attributes"></a>使用 DataType 屬性

開啟 *Movie.cs* 檔案並檢查 `Movie` 類別。 除了內建的驗證屬性集之外， [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間還會提供格式屬性。 我們已將[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)列舉值套用至發行日期和價格欄位。 下列程式碼顯示具有適當[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性的 `ReleaseDate` 和 `Price` 屬性。

[!code-csharp[Main](adding-validation/samples/sample7.cs)]

[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性只會提供 view engine 用來格式化資料的提示（並為電子郵件提供 URL 和 `<a href="mailto:EmailAddress.com">` 等屬性，例如 `<a>`。 您可以使用[RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)屬性來驗證資料的格式。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性是用來指定比資料庫內建類型更特定的資料類型，而***不***是驗證屬性。 在此案例中，我們只想要追蹤日期，而非日期和時間。 [DataType 列舉](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)提供許多資料類型，例如*Date、Time、PhoneNumber、Currency、EmailAddress*等等。 `DataType` 屬性也可讓應用程式自動提供類型的特定功能。 例如，您可以建立[EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)的 `mailto:` 連結，而且可以在支援[HTML5](http://html5.org/)的瀏覽器中提供[資料類型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)的日期選擇器。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性會發出 html 5 瀏覽器可以瞭解的[資料](http://ejohn.org/blog/html-5-data-attributes/)（發音*資料虛線*）屬性。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性不會提供任何驗證。

`DataType.Date` 未指定顯示日期的格式。 根據預設，資料欄位會根據伺服器的[CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)，以預設格式顯示。

`DisplayFormat` 屬性用來明確指定日期格式：

[!code-csharp[Main](adding-validation/samples/sample8.cs)]

[`ApplyFormatInEditMode`] 設定可指定在文字方塊中顯示值以供編輯時，也應該套用指定的格式。 （您可能不想針對某些欄位（例如，貨幣值），您可能不希望文字方塊中的貨幣符號進行編輯。）

您可以單獨使用[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性，但是使用[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性也是個不錯的主意。 `DataType` 屬性會傳達資料的*語義*，而不是在螢幕上轉譯的方式，並提供下列您不會在 `DisplayFormat`中取得的優點：

- 瀏覽器可以啟用 HTML5 功能（例如，顯示行事曆控制項、地區設定適當的貨幣符號、電子郵件連結等等）。
- 根據預設，瀏覽器會使用以您的[地區](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)設定為基礎的正確格式來呈現資料。
- [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性可以讓 MVC 選擇正確的欄位範本來轉譯資料（如果單獨使用[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) ，則會使用字串範本）。 如需詳細資訊，請參閱 Brad Wilson 的[ASP.NET MVC 2 範本](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)。 （雖然是針對 MVC 2 而撰寫的，但本文仍適用于目前版本的 ASP.NET MVC）。

如果您使用 `DataType` 屬性搭配日期欄位，您也必須指定 `DisplayFormat` 屬性，才能確保欄位在 Chrome 瀏覽器中正確呈現。 如需詳細資訊，請參閱[這個 StackOverflow 執行緒](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)。

> [!NOTE]
> jQuery 驗證無法與[範圍](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)屬性和[日期時間](https://msdn.microsoft.com/library/system.datetime.aspx)搭配使用。 例如，下列程式碼一律會顯示用戶端驗證錯誤，即使當日期位在指定範圍中也一樣：
> 
> [!code-csharp[Main](adding-validation/samples/sample9.cs)]
> 
> 您將需要停用 jQuery 日期驗證，才能搭配[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)使用[Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)屬性。 在您的模型中編譯硬性日期通常不是很好的作法，因此不建議使用[Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)屬性和[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx) 。

下列程式碼會顯示一行上的結合屬性：

[!code-csharp[Main](adding-validation/samples/sample10.cs?highlight=4,6,10,12)]

在數列的下一個部分中，我們會檢閱應用程式，並對自動產生的 `Details` 和 `Delete` 方法進行一些改良。

> [!div class="step-by-step"]
> [上一頁](adding-a-new-field.md)
> [下一頁](examining-the-details-and-delete-methods.md)
