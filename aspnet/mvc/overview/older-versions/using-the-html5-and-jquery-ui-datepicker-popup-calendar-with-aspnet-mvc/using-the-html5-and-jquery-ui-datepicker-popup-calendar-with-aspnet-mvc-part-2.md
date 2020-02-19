---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: 搭配 ASP.NET MVC 使用 HTML5 和 jQuery UI Datepicker 快顯行事曆-第2部分 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您如何在 ASP.NET MV 中使用編輯器範本、顯示範本和 jQuery UI datepicker 快顯行事曆的基本概念。
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 325cc90eb6e717c47863eda6253e0d48d796386b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455889"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a>搭配 ASP.NET MVC 使用 HTML5 和 jQuery UI Datepicker 快顯行事曆-第2部分

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程將告訴您如何在 ASP.NET MVC Web 應用程式中使用編輯器範本、顯示範本和 jQuery UI datepicker 快顯行事曆的基本概念。

## <a name="adding-an-automatic-datetime-template"></a>新增自動日期時間範本

在本教學課程的第一個部分中，您已瞭解如何將屬性加入至模型以明確指定格式，以及如何明確指定用來呈現模型的範本。 例如，下列程式碼中的[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性會明確指定 `ReleaseDate` 屬性的格式。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

在下列範例中，使用 `Date` 列舉的[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性會指定使用日期範本來呈現模型。 如果您的專案中沒有任何日期範本，則會使用內建的日期範本。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

不過，ASP。MVC 可以藉由尋找符合類型名稱的範本，使用慣例過度設定來執行類型比對。 這可讓您建立自動將資料格式化的範本，而完全不需要使用任何屬性或程式碼。 在本教學課程的這個部分中，您將建立自動套用至[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)類型之模型屬性的範本。 您不需要使用屬性或其他設定來指定範本應該用來呈現[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)類型的所有模型屬性。

您也將學習自訂個別屬性或甚至是個別欄位的顯示方式。

首先，讓我們移除現有的格式資訊，並在應用程式中顯示完整的日期。

開啟*Movie.cs*檔案，並將 `ReleaseDate` 屬性上的 `DataType` 屬性標記為批註：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

按 CTRL+F5 執行應用程式。

請注意，[`ReleaseDate`] 屬性現在會顯示日期和時間，因為這是未提供任何格式資訊時的預設值。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a>加入用來測試新範本的 CSS 樣式

在建立格式化日期的範本之前，您將會新增一些 CSS 樣式規則，以套用至新的範本。 這些會協助您確認轉譯的頁面使用的是新的範本。

開啟*Content\Site.cs*s 檔案，然後將下列 CSS 規則新增至檔案的底部：

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a>加入日期時間顯示範本

現在您可以建立新的範本。 在*Views\Movies*資料夾中，建立*DisplayTemplates*資料夾。

在*Views\Shared*資料夾中，建立*DisplayTemplates*資料夾和*EditorTemplates*資料夾。

所有的控制器都會使用*Views\Shared\DisplayTemplates*資料夾中的顯示範本。 只有 `Movie` 控制器才會使用*Views\Movie\DisplayTemplates*資料夾中的顯示範本。 （如果兩個資料夾中出現相同名稱的範本，則*Views\Movie\DisplayTemplates*資料夾中的範本（也就是較特定的範本）會優先使用 `Movie` 控制器所傳回的視圖）。

在**方案總管**中，展開 [ *Views* ] 資料夾，展開 [ *Shared* ] 資料夾，然後以滑鼠右鍵按一下 [ *Views\Shared\DisplayTemplates* ] 資料夾。

按一下 [**新增**]，然後按一下 [ **View**]。 [**加入視圖**] 對話方塊隨即顯示。

在 [**視圖名稱**] 方塊中，輸入 `DateTime`。 （您必須使用此名稱才能符合類型的名稱）。

選取 [**建立為部分視圖**] 核取方塊。 請確定未選取 [**使用版面配置或主版] 頁面**，並**建立 [強型別視圖**] 核取方塊。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

按一下 [新增]。 *Views\Shared\DisplayTemplates*中會建立*日期時間 cshtml*範本。

下圖顯示 [`DateTime` 顯示] 和 [編輯器] 範本建立後**方案總管**中的 [ *Views* ] 資料夾。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

開啟*Views\Shared\DisplayTemplates\DateTime.cshtml*檔案，並新增下列標記，它會使用[字串. format](https://msdn.microsoft.com/library/system.string.format.aspx)方法將屬性格式化為不含時間的日期。 （`{0:d}` 格式會指定簡短日期格式）。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

重複此步驟，在*Views\Movie\DisplayTemplates*資料夾中建立 `DateTime` 範本。 在*Views\Movie\DisplayTemplates\DateTime.cshtml*檔案中使用下列程式碼。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

`loud-1` CSS 類別會使日期以粗體的紅色文字顯示。 您已將 `loud-1` CSS 類別新增為暫時的量值，因此您可以輕鬆地查看何時使用此特定範本。

您所做的就是建立和自訂範本，ASP.NET 將用來顯示日期。 較一般的範本（在*Views\Shared\DisplayTemplates*資料夾中）會顯示簡單的簡短日期。 特別針對 `Movie` 控制器（在*Views\Movies\DisplayTemplates*資料夾中）的範本會顯示一段簡短的日期，並將其格式化為粗體的紅色文字。

按 CTRL+F5 執行應用程式。 瀏覽器會呈現應用程式的索引視圖。

`ReleaseDate` 屬性現在會以粗體紅色字型顯示不含時間的日期。這可協助您確認已選取 [ *Views\Movies\DisplayTemplates* ] 資料夾中的 `DateTime` 樣板化協助程式，其方式是在共用資料夾中 `DateTime` 樣板化 helper （*Views\Shared\DisplayTemplates*）。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

現在將*Views\Movies\DisplayTemplates\DateTime.cshtml*檔案重新命名為*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*。

按 CTRL+F5 執行應用程式。

此時，`ReleaseDate` 屬性會顯示不含時間且不含粗體紅色字型的日期。 這說明具有資料類型名稱的範本（在此案例中為 `DateTime`）會自動用來顯示該類型的所有模型屬性。 在您將*DateTime. cshtml*檔案重新命名*為 LoudDateTime*之後，ASP.NET 在*Views\Movies\DisplayTemplates*資料夾中找不到範本，因此它使用了 * Views\Movies\Shared\* 資料夾中的*DateTime. cshtml*範本。

（範本比對不區分大小寫，因此您可以使用任何大小寫來建立範本檔案名。 例如， *datetime. cshtml、datetime. cshtml*和*datetime. cshtml*全都符合 `DateTime` 類型）。

若要進行檢查：此時會使用*Views\Movies\DisplayTemplates\DateTime.cshtml*範本來顯示 [`ReleaseDate`] 欄位，這會顯示使用簡短日期格式的資料，但不會新增任何特殊格式。

### <a name="using-uihint-to-specify-a-display-template"></a>使用 UIHint 指定顯示範本

如果您的 web 應用程式有許多 `DateTime` 欄位，而且根據預設，您想要以僅限日期的格式來顯示全部或大部分，則*DateTime. cshtml*範本是不錯的方法。 但是，如果您有幾個想要顯示完整日期和時間的日期呢？ 沒問題。 您可以建立額外的範本，並使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)屬性來指定完整日期和時間的格式。 然後，您可以選擇性地套用該範本。 您可以在模型層級使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)屬性，也可以在視圖內指定範本。 在本節中，您將瞭解如何使用 `UIHint` 屬性，選擇性地變更一些日期時間欄位實例的格式。

開啟*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*檔案，並將現有的程式碼取代為下列內容：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

這會顯示完整的日期和時間，並加入讓文字變成綠色和大的 CSS 類別。

開啟*Movie.cs*檔案，並將[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)屬性新增至 `ReleaseDate` 屬性，如下列範例所示：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

這會告訴 ASP.NET MVC，當它顯示 `ReleaseDate` 屬性（具體而言，而不只是任何 `DateTime` 物件）時，應該使用*LoudDateTime*範本。

按 CTRL+F5 執行應用程式。

請注意，[`ReleaseDate`] 屬性現在會以較大的綠色字型顯示日期和時間。

回到*Movie.cs*檔案中的 `UIHint` 屬性並將它批註，以便不使用*LoudDateTime*範本。 再次執行應用程式。 發行日期不會顯示為 [大] 和 [綠色]。 這會驗證 [索引] 和 [詳細資料] 視圖中是否使用*Views\Shared\DisplayTemplates\DateTime.cshtml*範本。

如先前所述，您也可以在 view 中套用範本，這可讓您將範本套用至某些資料的個別實例。 開啟 [ *Views\Movies\Details.cshtml* ] 視圖。 新增 `"LoudDateTime"` 做為 [`ReleaseDate`] 欄位之[DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)呼叫的第二個參數。 完成的程式碼如下所示：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

這會指定應該使用 `LoudDateTime` 範本來顯示模型屬性，而不論哪些屬性會套用至模型。

按 CTRL+F5 執行應用程式。

確認電影 [索引] 頁面使用的是*Views\Shared\DisplayTemplates\DateTime.cshtml*範本（紅色粗體），而 [ *Movie\Details* ] 頁面使用的是*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*範本（大和綠色）。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

在下一節中，您將建立複雜類型的範本。

> [!div class="step-by-step"]
> [上一頁](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [下一頁](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
