---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
title: 將驗證新增至模型（C#） |Microsoft Docs
author: Rick-Anderson
description: 建立控制器
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 9af927e2-1c3b-43d9-917d-1df75be3c482
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 19d86dc0df931a9d135e46209559892b77626cf6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615448"
---
# <a name="adding-validation-to-the-model-c"></a>將驗證新增至模型 (C#)

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > 本教學課程的更新版本可在[這裡](../../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 它更安全、更容易遵循，並示範更多功能。
> 
> 
> 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。 開始之前，請先確定您已安裝下列必要條件。 您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，您可以使用下列連結個別安裝必要條件：
> 
> - [Visual Studio Web Developer Express SP1 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）
> 
> 如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主題提供具有C#原始程式碼的 Visual Web Developer 專案。 [下載C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您偏好 Visual Basic，請切換到本教學課程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。

在本節中，您會將驗證邏輯新增至 `Movie` 模型，而且您將確保在使用者嘗試使用應用程式建立或編輯電影時，會強制執行驗證規則。

## <a name="keeping-things-dry"></a>讓事情晾乾

ASP.NET MVC 的其中一個核心設計原則是試（「不重複原則」）。 ASP.NET MVC 鼓勵您只指定一次功能或行為，然後讓它反映在應用程式中的所有位置。 這可減少您需要撰寫的程式碼數量，讓您撰寫的程式碼更容易維護。

ASP.NET MVC 和 Entity Framework Code First 所提供的驗證支援，是實際運作原則的絕佳範例。 您可以在一個位置以宣告方式指定驗證規則（在模型類別中），然後在應用程式中的任何位置強制執行這些規則。

讓我們看看如何在電影應用程式中利用這項驗證支援。

## <a name="adding-validation-rules-to-the-movie-model"></a>將驗證規則新增至電影模型

首先，將一些驗證邏輯新增至 `Movie` 類別。

開啟 *Movie.cs* 檔案。 在檔案的頂端新增參考[`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間的 `using` 語句：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

命名空間是 .NET Framework 的一部分。 它提供了一組內建的驗證屬性，可讓您以宣告方式套用至任何類別或屬性。

現在更新 `Movie` 類別，以利用內建的[`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)、 [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)和[`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)驗證屬性。 使用下列程式碼作為套用屬性的範例。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs)]

驗證屬性會指定您想要強制執行模型屬性套用的行為。 `Required` 屬性指出屬性必須具有值;在此範例中，電影必須有 `Title`、`ReleaseDate`、`Genre`和 `Price` 屬性的值，才能有效。 `Range` 屬性會將值限制在指定的範圍內。 `StringLength` 屬性可讓您設定字串屬性的最大長度，並選擇性設定其最小長度。

Code First 可確保在應用程式將變更儲存到資料庫之前，會強制執行您在模型類別上指定的驗證規則。 例如，下列程式碼會在呼叫 `SaveChanges` 方法時擲回例外狀況，因為遺漏了數個必要的 `Movie` 屬性值，而且價格為零（超出有效範圍）。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample3.cs)]

由 .NET Framework 自動強制執行驗證規則有助於讓應用程式更穩固。 它也確保您不會忘記要驗證某些項目，不小心讓不正確的資料進入資料庫。

以下是已更新之*Movie.cs*檔案的完整程式代碼清單：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC 中的驗證錯誤 UI

重新執行應用程式，並流覽至 */Movies* URL。

按一下 [**建立電影**] 連結以新增電影。 在表單中填寫一些不正確值，然後按一下 [**建立**] 按鈕。

[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)

請注意表單如何自動使用背景色彩來反白顯示包含無效資料的文字方塊，並且在每個文字旁發出適當的驗證錯誤訊息。 錯誤訊息符合您在批註 `Movie` 類別時所指定的錯誤字串。 用戶端（使用 JavaScript）和伺服器端（如果使用者已停用 JavaScript）都會強制執行錯誤。

真正的好處是，您不需要在 `MoviesController` 類別或*建立. cshtml*視圖中變更一行程式碼，就能啟用此驗證 UI。 您稍早在本教學課程中建立的控制器和視圖，會自動挑選您使用 `Movie` 模型類別上的屬性所指定的驗證規則。

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>如何在 Create View 和 Create Action 方法中進行驗證

您可能奇怪如何在不更新控制器或檢視程式碼的狀況下產生驗證 UI。 下一個清單會顯示 `MovieController` 類別中的 `Create` 方法看起來如何。 它們與您稍早在本教學課程中建立它們的方式不一樣。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

第一個動作方法會顯示初始的建立表單。 第二個處理表單張貼。 第二個 `Create` 方法會呼叫 `ModelState.IsValid`，以檢查電影是否有任何驗證錯誤。 呼叫此方法會評估已套用至物件的所有驗證屬性。 如果物件有驗證錯誤，`Create` 方法就會重新出現表單。 如果沒有任何錯誤，方法即會將新的電影儲存到資料庫。

以下是您稍早在本教學課程中 scaffold 的*建立. cshtml*視圖範本。 上述動作方法會使用它來顯示初始表單，以及在發生錯誤時重新顯示它。

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

請注意程式碼如何使用 `Html.EditorFor` helper 來輸出每個 `Movie` 屬性的 `<input>` 元素。 在此協助程式旁呼叫 `Html.ValidationMessageFor` helper 方法。 這兩個 helper 方法會使用由控制器傳遞至視圖的模型物件（在此案例中為 `Movie` 物件）。 它們會自動尋找在模型上指定的驗證屬性，並適當地顯示錯誤訊息。

這種方法的好處是，控制器或建立視圖範本都無法得知所強制執行的實際驗證規則，或顯示的特定錯誤訊息。 驗證規則和錯誤字串只在 `Movie` 類別中指定。

如果您稍後想要變更驗證邏輯，您可以在一個地方執行此動作。 您不必擔心應用程式的不同部分會與規則強制執行的方式不一致，所有的驗證邏輯都是在同一個地方定義，用於所有位置。 這會讓程式碼非常整齊乾淨，容易維護及發展。 這表示您會完全接受 DRY 原則。

## <a name="adding-formatting-to-the-movie-model"></a>將格式新增至電影模型

開啟 *Movie.cs* 檔案。 除了內建的驗證屬性集之外， [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間還會提供格式屬性。 您會將[`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性和[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)列舉值套用至發行日期和價格欄位。 下列程式碼顯示具有適當[`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性的 `ReleaseDate` 和 `Price` 屬性。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs)]

或者，您可以明確地設定[`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx)值。 下列程式碼顯示具有日期格式字串（也就是 "d"）的 [發行日期] 屬性。 您會使用此來指定在發行日期中不需要時間。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample8.cs)]

下列程式碼會將 `Price` 屬性格式化為貨幣。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

完整的 `Movie` 類別如下所示。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

執行應用程式，並流覽至 `Movies` 控制器。

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

在數列的下一個部分中，我們會檢閱應用程式，並對自動產生的 `Details` 和 `Delete` 方法進行一些改良。

> [!div class="step-by-step"]
> [上一頁](adding-a-new-field.md)
> [下一頁](improving-the-details-and-delete-methods.md)
