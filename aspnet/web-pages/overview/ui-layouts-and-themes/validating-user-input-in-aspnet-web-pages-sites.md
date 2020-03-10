---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: 在 ASP.NET Web Pages （Razor）網站中驗證使用者輸入 |Microsoft Docs
author: Rick-Anderson
description: 本文討論如何驗證您從使用者取得的資訊 &mdash; 也就是，確保使用者在中以 HTML 表單輸入有效的資訊 。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: e6f8e1051d09d11f1756bfada44a73ba7c2a1db2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563501"
---
# <a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a>在 ASP.NET Web Pages （Razor）網站中驗證使用者輸入

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文討論如何驗證您從使用者取得的資訊 &mdash; 亦即，確保使用者在 ASP.NET Web Pages （Razor）網站中輸入 HTML 表單中的有效資訊。
> 
> 您將學到什麼：
> 
> - 如何檢查使用者的輸入是否符合您定義的驗證準則。
> - 如何判斷是否已通過所有驗證測試。
> - 如何顯示驗證錯誤（以及如何設定其格式）。
> - 如何驗證不是直接來自使用者的資料。
> 
> 以下是文章中引進的 ASP.NET 程式設計概念：
> 
> - `Validation` helper。
> - `Html.ValidationSummary` 和 `Html.ValidationMessage` 方法。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）3
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 2。

本文包含下列章節：

- [使用者輸入驗證的總覽](#Overview_of_User_Input_Validation)
- [驗證使用者輸入](#Validating_User_Input)
- [加入用戶端驗證](#Adding_Client-Side_Validation)
- [格式化驗證錯誤](#Formatting_Validation_Errors)
- [驗證不是直接來自使用者的資料](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a>使用者輸入驗證的總覽

如果您要求使用者在頁面中輸入資訊（例如，在表單中），請務必確定他們輸入的值有效。 例如，您不想要處理遺失重要資訊的表單。

當使用者在 HTML 表單中輸入值時，他們輸入的值就是字串。 在許多情況下，您需要的值是一些其他的資料類型，例如整數或日期。 因此，您也必須確保使用者輸入的值可以正確地轉換成適當的資料類型。

對於這些值，您可能也會有一些限制。 例如，即使使用者正確輸入整數，您可能還是必須確定該值落在特定範圍內。

![使用 CSS 樣式類別的驗證錯誤](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> **重要事項**驗證使用者輸入對於安全性也很重要。 當您限制使用者可以在表單中輸入的值時，您可以減少某人輸入可能會危害網站安全性的值。

<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a>驗證使用者輸入

在 ASP.NET Web Pages 2 中，您可以使用 `Validator` helper 來測試使用者輸入。 基本方法是執行下列動作：

1. 決定您想要驗證的輸入元素（欄位）。

    您通常會驗證表單中 `<input>` 元素的值。 不過，最好是驗證所有輸入，甚至是來自 `<select>` 清單等受限元素的輸入。 這有助於確保使用者不會略過頁面上的控制項並提交表單。
2. 在頁面程式碼中，使用 `Validation` helper 的方法，為每個輸入元素加入個別驗證檢查。

    若要檢查必要的欄位，請使用 `Validation.RequireField(field, [error message])` （適用于個別欄位）或 `Validation.RequireFields(field1, field2, ...))` （適用于欄位清單）。 針對其他類型的驗證，請使用 `Validation.Add(field, ValidationType)`。 針對 `ValidationType`，您可以使用下列選項：

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. 提交頁面時，請檢查 `Validation.IsValid`，以檢查驗證是否已通過：

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    如果發生任何驗證錯誤，您會略過一般頁面處理。 例如，如果頁面的目的是要更新資料庫，除非已修正所有驗證錯誤，否則您不會這麼做。
4. 如果發生驗證錯誤，請使用 `Html.ValidationSummary` 或 `Html.ValidationMessage`或兩者，在頁面的標記中顯示錯誤訊息。

下列範例顯示的頁面會說明這些步驟。

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

若要查看驗證的運作方式，請執行此頁面並故意進行錯誤。 例如，如果您忘記輸入課程名稱、輸入，以及輸入不正確日期，則頁面看起來會像這樣：

![呈現的頁面中的驗證錯誤](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a>加入用戶端驗證

根據預設，使用者輸入會在使用者提交頁面後進行驗證，也就是在伺服器程式碼中執行驗證。 這種方法的缺點是，使用者不知道他們在送出頁面之後就會發生錯誤。 如果表單很長或很複雜，只有在送出頁面之後才報告錯誤，對使用者而言可能不方便。

您可以在用戶端腳本中加入支援以執行驗證。 在這種情況下，當使用者在瀏覽器中工作時，就會執行驗證。 例如，假設您指定值應為整數。 如果使用者輸入非整數值，當使用者離開輸入欄位時，就會回報錯誤。 使用者會收到立即的意見反應，這對他們而言很方便。 以用戶端為基礎的驗證也可以減少使用者提交表單以更正多個錯誤的次數。

> [!NOTE]
> 即使您使用用戶端驗證，也一律會在伺服器程式碼中執行驗證。 如果使用者略過以用戶端為基礎的驗證，在伺服器程式碼中執行驗證就是一種安全性措施。

1. 在頁面中註冊下列 JavaScript 程式庫：  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   其中兩個程式庫可從內容傳遞網路（CDN）載入，因此您不一定要將它們安裝在電腦或伺服器上。 不過，您必須擁有 jquery 的本機複本 *。請驗證.* 不想要的 .js。 如果您還沒有使用包含程式庫的 WebMatrix 範本（例如**入門網站**），請建立以**入門網站**為基礎的 Web 網頁網站。 然後將 *.js*檔案複製到您目前的網站。
2. 在 [標記] 中，針對您要驗證的每個元素，新增對 `Validation.For(field)`的呼叫。 這個方法會發出用戶端驗證所使用的屬性。 （而不是發出實際的 JavaScript 程式碼，方法會發出 `data-val-...`之類的屬性。 這些屬性支援不顯眼的用戶端驗證，使用 jQuery 來執行工作。）

下列頁面顯示如何將用戶端驗證功能新增至稍早所示的範例。

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

並非所有驗證檢查都是在用戶端上執行。 特別的是，資料類型驗證（整數、日期等等）不會在用戶端上執行。 下列檢查同時適用于用戶端和伺服器：

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

在此範例中，有效日期的測試將無法在用戶端程式代碼中使用。 不過，測試將會在伺服器程式碼中執行。

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a>格式化驗證錯誤

您可以藉由定義具有下列保留名稱的 CSS 類別，來控制驗證錯誤的顯示方式：

- `field-validation-error` 定義在顯示錯誤時，`Html.ValidationMessage` 方法的輸出。
- `field-validation-valid` 當沒有錯誤時，定義 `Html.ValidationMessage` 方法的輸出。
- `input-validation-error` 定義當發生錯誤時，如何轉譯 `<input>` 元素。 （例如，您可以使用這個類別，將 &lt;輸入&gt; 元素的背景色彩設定為不同的色彩（如果其值無效）。只有在用戶端驗證期間（在 ASP.NET Web Pages 2 中），才會使用這個 CSS 類別。
- `input-validation-valid` 當沒有錯誤時，定義 `<input>` 元素的外觀。
- `validation-summary-errors` 定義其顯示錯誤清單之 `Html.ValidationSummary` 方法的輸出。
- `validation-summary-valid` 當沒有錯誤時，定義 `Html.ValidationSummary` 方法的輸出。

下列 `<style>` 區塊會顯示錯誤狀況的規則。

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

如果您在本文稍早的範例頁面中包含此樣式區塊，錯誤顯示將如下圖所示：

![使用 CSS 樣式類別的驗證錯誤](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> 如果您不是在 ASP.NET Web Pages 2 中使用用戶端驗證，則 `<input>` 元素（`input-validation-error` 和 `input-validation-valid` 的 CSS 類別不會有任何作用。

### <a name="static-and-dynamic-error-display"></a>靜態和動態錯誤顯示

CSS 規則成對出現，例如 `validation-summary-errors` 和 `validation-summary-valid`。 這些配對可讓您定義這兩種條件的規則：錯誤狀況和「正常」（非錯誤）條件。 請務必瞭解，即使沒有任何錯誤，也一定會轉譯錯誤顯示的標記。 例如，如果頁面在標記中有 `Html.ValidationSummary` 方法，則即使第一次要求頁面時，頁面來源也會包含下列標記：

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

換句話說，即使錯誤清單是空的，`Html.ValidationSummary` 方法一律會呈現 `<div>` 元素和清單。 同樣地，`Html.ValidationMessage` 方法一律會將 `<span>` 元素呈現為個別欄位錯誤的預留位置，即使沒有任何錯誤也一樣。

在某些情況下，顯示錯誤訊息可能會導致頁面重新排列，而且可能會導致頁面上的元素四處移動。 `-valid` 結尾的 CSS 規則可讓您定義有助於防止此問題的版面配置。 例如，您可以定義 `field-validation-error`，`field-validation-valid` 兩者都有相同的固定大小。 如此一來，欄位的顯示區域為靜態，如果顯示錯誤訊息，則不會變更網頁流程。

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a>驗證不是直接來自使用者的資料

有時候，您必須驗證不是直接來自 HTML 表單的資訊。 典型的範例是在查詢字串中傳遞值的頁面，如下列範例所示：

`http://server/myapp/EditClassInformation?classid=1022`

在此情況下，您會想要確定傳遞至頁面的值（在這裡，1022代表 `classid`的值）是有效的。 您無法直接使用 `Validation` helper 來執行這種驗證。 不過，您可以使用驗證系統的其他功能，例如顯示驗證錯誤訊息的能力。

> [!NOTE] 
> 
> **重要事項**一律驗證您從*任何*來源取得的值，包括表單域值、查詢字串值和 cookie 值。 人們很容易就能變更這些值（可能是為了惡意的目的）。 因此，您必須檢查這些值，才能保護您的應用程式。

下列範例會示範如何驗證在查詢字串中傳遞的值。 此程式碼會測試值不是空的，且為整數。

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

請注意，當要求不是提交表單（`if(!IsPost)`）時，就會執行測試。 這項測試會在第一次要求頁面時通過，但不會在要求提交表單時傳遞。

若要顯示此錯誤，您可以藉由呼叫 `Validation.AddFormError("message")`，將錯誤加入至驗證錯誤清單。 如果頁面包含對 `Html.ValidationSummary` 方法的呼叫，就會在該處顯示錯誤，就像使用者輸入驗證錯誤一樣。

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>其他資源

[在 ASP.NET Web Pages 網站中使用 HTML 表單](https://go.microsoft.com/fwlink/?LinkID=202892)
