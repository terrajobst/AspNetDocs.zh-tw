---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: 搭配 ASP.NET MVC 使用 HTML5 和 jQuery UI Datepicker 快顯行事曆-第3部分 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您如何在 ASP.NET MV 中使用編輯器範本、顯示範本和 jQuery UI datepicker 快顯行事曆的基本概念。
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: b3249397e54e64538c4dc78e5fe8b94656e8962b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457891"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a>搭配 ASP.NET MVC 使用 HTML5 和 jQuery UI Datepicker 快顯行事曆-第3部分

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程將告訴您如何在 ASP.NET MVC Web 應用程式中使用編輯器範本、顯示範本和 jQuery UI datepicker 快顯行事曆的基本概念。

## <a name="working-with-complex-types"></a>使用複雜類型

在本節中，您將建立一個網址類別別，並瞭解如何建立範本來顯示它。

在 [*模型*] 資料夾中，建立名為*Person.cs*的新類別檔案，您會在其中放置兩個類型： [`Person` 類別] 和 [`Address` 類別]。 `Person` 類別將包含以 `Address`類型的屬性。 `Address` 類型是複雜類型，這表示它不是其中一個內建類型，例如 `int`、`string`或 `double`。 相反地，它有數個屬性。 新類別的程式碼如下所示：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

在 `Movie` 控制器中，新增下列 `PersonDetail` 動作以顯示 person 實例：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

然後將下列程式碼新增至 `Movie` 控制器，以將一些範例資料填入 `Person` 模型：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

開啟*Views\Movies\PersonDetail.cshtml*檔案，並為 `PersonDetail` view 新增下列標記。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

按 Ctrl + F5 執行應用程式，並流覽至 [*電影/PersonDetail*]。

[`PersonDetail`] 視圖並未包含 `Address` 複雜類型，如您在此螢幕擷取畫面中所見。 （不會顯示任何位址）。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

不會顯示 `Address` 的模型資料，因為它是複雜型別。 若要顯示位址資訊，請再次開啟*Views\Movies\PersonDetail.cshtml*檔案，並新增下列標記。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

[`PersonDetail` now] 視圖的完整標記看起來像這樣：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

再次執行應用程式，並顯示 [`PersonDetail`] 視圖。 現在會顯示位址資訊：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a>建立複雜類型的範本

在本節中，您將會建立用來轉譯 `Address` 複雜類型的範本。 當您建立 `Address` 類型的範本時，ASP.NET MVC 可以自動使用它來格式化應用程式中任何位置的位址模型。 如此一來，您就可以從應用程式中的單一位置控制 `Address` 類型的呈現方式。

在*Views\Shared\DisplayTemplates*資料夾中，建立名為**Address**的強型別部分視圖：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

按一下 **[新增]** ，然後開啟新的*Views\Shared\DisplayTemplates\Address.cshtml*檔案。 新的視圖包含下列產生的標記：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

執行應用程式，並顯示 [`PersonDetail`] 視圖。 這次，您剛建立的 `Address` 範本會用來顯示 `Address` 複雜類型，因此顯示如下所示：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a>摘要：指定模型顯示格式和範本的方式

您已看到，您可以使用下列方法來指定模型屬性的格式或範本：

- 將 `DisplayFormat` 屬性套用至模型中的屬性。 例如，下列程式碼會在沒有時間的情況下顯示日期：

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- 將[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性套用至模型中的屬性，並指定資料類型。 例如，下列程式碼會在沒有時間的情況下顯示日期。

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    如果應用程式在*Views\Shared\DisplayTemplates*資料夾或*Views\Movies\DisplayTemplates*資料夾中包含*date. cshtml*範本，則會使用該範本來呈現 `DateTime` 屬性。 否則，內建的 ASP.NET 範本化系統會將屬性顯示為日期。
- 建立*Views\Shared\DisplayTemplates*資料夾或*Views\Movies\DisplayTemplates*資料夾中的顯示範本，其名稱符合您想要格式化的資料類型。 例如，您看到*Views\Shared\DisplayTemplates\DateTime.cshtml*是用來呈現模型中 `DateTime` 屬性，而不需要將屬性加入至模型，也不需要將任何標記加入至 Views。
- 在模型上使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)屬性來指定要顯示模型屬性的範本。
- 在視圖中，將顯示範本名稱明確新增至[DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)呼叫。

您所使用的方法取決於您需要在應用程式中執行的動作。 混用這些方法，以確切取得您所需的格式類型並不常見。

在下一節中，您將會稍微切換齒輪，並從自訂資料的顯示方式移動，以自訂其輸入方式。 您會將 jQuery datepicker 連結至應用程式中的編輯檢視，以提供更巧妙的方式來指定日期。

> [!div class="step-by-step"]
> [上一頁](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [下一頁](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)
