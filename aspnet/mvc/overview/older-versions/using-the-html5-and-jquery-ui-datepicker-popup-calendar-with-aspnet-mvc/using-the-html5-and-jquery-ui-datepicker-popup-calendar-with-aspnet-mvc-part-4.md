---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: 搭配 ASP.NET MVC 使用 HTML5 和 jQuery UI Datepicker 快顯行事曆-第4部分 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您如何在 ASP.NET MV 中使用編輯器範本、顯示範本和 jQuery UI datepicker 快顯行事曆的基本概念。
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: 583e782641efea9a9517edb31f7718b28203d756
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538945"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a>搭配 ASP.NET MVC 使用 HTML5 和 jQuery UI Datepicker 快顯行事曆-第4部分

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程將告訴您如何在 ASP.NET MVC Web 應用程式中使用編輯器範本、顯示範本和 jQuery UI datepicker 快顯行事曆的基本概念。

### <a name="adding-a-template-for-editing-dates"></a>新增用於編輯日期的範本

在本節中，您將會建立編輯日期的範本，當 ASP.NET MVC 顯示 UI 來編輯以 DataType 屬性的**日期**列舉標記的模型屬性時，將會套用這些[資料](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)。 此範本只會轉譯日期;將不會顯示時間。 在範本中，您將使用[JQUERY UI Datepicker](http://jqueryui.com/demos/datepicker/)快顯行事歷來提供編輯日期的方法。

若要開始，請開啟*Movie.cs*檔案，並將具有**Date**列舉的[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性加入至 `ReleaseDate` 屬性，如下列程式碼所示：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

此程式碼會顯示顯示範本和編輯範本中的 [`ReleaseDate`] 欄位，而不會有時間。 如果您的應用程式在*Views\Shared\EditorTemplates*資料夾或*Views\Movies\EditorTemplates*資料夾中包含*date. cshtml*範本，則在編輯時，將會使用該範本來呈現任何 `DateTime` 屬性。 否則，內建的 ASP.NET 範本化系統會將屬性顯示為日期。

按 CTRL+F5 執行應用程式。 選取 [編輯] 連結，以確認 [發行日期] 的輸入欄位只顯示日期。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

在**方案總管**中，展開 [ *Views* ] 資料夾，展開 [ *Shared* ] 資料夾，然後以滑鼠右鍵按一下 [ *Views\Shared\EditorTemplates* ] 資料夾。

按一下 [**新增**]，然後按一下 [ **View**]。 [**加入視圖**] 對話方塊隨即顯示。

在 [**視圖名稱**] 方塊中，輸入 &quot;日期&quot;。

選取 [**建立為部分視圖**] 核取方塊。 請確定未選取 [**使用版面配置或主版] 頁面**，並**建立 [強型別視圖**] 核取方塊。

按一下 [新增]。 隨即建立*Views\Shared\EditorTemplates\Date.cshtml*範本。

將下列程式碼新增至*Views\Shared\EditorTemplates\Date.cshtml*範本。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

第一行會將模型宣告為 `DateTime` 型別。 雖然您不需要在 [編輯] 和 [顯示] 範本中宣告模型類型，但最佳作法是讓您取得要傳遞至視圖之模型的編譯時間檢查。 （另一個好處是，您可以在 Visual Studio 的視圖中取得模型的 IntelliSense）。如果模型類型未宣告，ASP.NET MVC 會將它視為[動態](https://msdn.microsoft.com/library/dd264741.aspx)類型，而且不會有編譯時間類型檢查。 如果您將模型宣告為 `DateTime` 類型，它就會變成強型別。

第二行只是常值 HTML 標籤，會使用日期欄位&quot; 之前的日期範本來顯示 &quot;。 您會暫時使用這一行來驗證此日期範本是否正在使用中。

下一行是[Html. TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx) helper，會呈現文字方塊的 `input` 欄位。 Helper 的第三個參數會使用匿名型別，將文字方塊的類別設定為 `datefield`，以及要 `date`的型別。 （因為 `class` 是中C#保留的，所以您必須使用 `@` 字元來將剖析器中C#的 `class` 屬性。）

`date` 類型是 HTML5 輸入類型，可讓 HTML5 感知瀏覽器呈現 HTML5 行事曆控制項。 稍後您會加入一些 JavaScript，以使用 `datefield` 類別，將 jQuery datepicker 連結到 `Html.TextBox` 元素。

按 CTRL+F5 執行應用程式。 您可以確認 [編輯] 視圖中的 [`ReleaseDate`] 屬性是使用 [編輯範本]，因為範本會使用 [`ReleaseDate` 文字] 輸入方塊前面的 [日期]&quot; 範本來顯示 &quot;，如下圖所示：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

在您的瀏覽器中，查看頁面的來源。 （例如，以滑鼠右鍵按一下頁面，然後選取 [ **View source**]）。下列範例會顯示頁面的部分標記，其中說明轉譯的 HTML 中的 `class` 和 `type` 屬性。

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

返回*Views\Shared\EditorTemplates\Date.cshtml*範本，並使用日期範本&quot; 標記移除 &quot;。 現在完成的範本看起來像這樣：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a>使用 NuGet 新增 jQuery UI Datepicker 快顯行事曆

在本節中，您會將[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)快顯行事曆新增至日期編輯範本。 [JQUERY UI](http://jqueryui.com/)程式庫可支援動畫、先進的效果和可自訂的小工具。 它建置於 jQuery JavaScript 程式庫之上。 Datepicker 快顯行事曆可讓您輕鬆且自然地使用行事曆輸入日期，而不是輸入字串。 快顯行事曆也會將使用者限制為合法日期，日期的一般文字輸入可讓您輸入類似 `2/33/1999` （二月33rd，1999），但[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)快顯行事曆不會允許此作業。

首先，您必須安裝 jQuery UI 程式庫。 若要這麼做，您將使用 NuGet，這是包含在 SP1 版本的 Visual Studio 2010 和 Visual Web Developer 中的套件管理員。

在 Visual Web Developer 中，從 [**工具**] 功能表選取 [ **nuget 套件管理員**]，然後選取 [**管理 nuget 套件**]。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

注意：如果 [**工具**] 功能表未顯示 [ **nuget 套件管理員**] 命令，您必須遵循 Nuget 網站的 [[安裝 nuget](http://docs.nuget.org/docs/start-here/installing-nuget) ] 頁面上的指示來安裝 nuget。   
  
如果您使用 Visual Studio 而非 Visual Web Developer，請從 [**工具**] 功能表中選取 [ **NuGet 套件管理員**]，然後選取 [**新增程式庫套件參考**]。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

在 [ **MVCMovie-管理 NuGet 封裝**] 對話方塊中，按一下左側的 [**線上**] 索引標籤，然後在 [搜尋] 方塊中輸入 &quot;jQuery. UI&quot;。 選取 [j**查詢 UI widget： Datepicker**]，然後選取 [**安裝**] 按鈕。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

NuGet 會將 jQuery UI Core 和 jQuery UI 日期選擇器的這些偵錯工具版本和縮減版本新增至您的專案：

- *jquery. core .js*
- *jquery. core. min .js*
- *jquery. ui. datepicker .js*
- *jquery. datepicker. min .js*

注意： debug 版本（沒有 *. min .js*副檔名的檔案）在進行調試時很有用，但在生產網站中，您只會包含縮減版本。

若要實際使用 jQuery 日期選擇器，您需要建立可將行事曆 widget 連結至編輯範本的 jQuery 腳本。 在**方案總管**中，以滑鼠右鍵按一下 [*腳本*] 資料夾，然後依序選取 [**加入**]、[**新增專案**] 和 [ **JScript**檔案]。 將檔案命名為*DatePickerReady*。

將下列程式碼新增至*DatePickerReady*檔案：

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

如果您不熟悉 jQuery，以下是此功能的簡短說明：第一行是 &quot;jQuery ready&quot; 函式，當頁面中的所有 DOM 元素都已載入時，就會呼叫此函式。 第二行會選取所有具有類別名稱 `datefield`的 DOM 元素，然後針對每個專案叫用 `datepicker` 函式。 （請記住，您稍早在本教學課程中已將 `datefield` 類別新增至*Views\Shared\EditorTemplates\Date.cshtml*範本）。

接下來，開啟*Views\Shared\\_Layout. cshtml*檔案。 您需要新增下列檔案的參考，這些檔案都是必要的，以便您可以使用日期選擇器：

- *Content/主題/base/jquery. .css*
- *Content/主題/base/jquery. datepicker .css*
- *Content/主題/base/jquery. ui. css*
- *jquery. core. min .js*
- *jquery. datepicker. min .js*
- *DatePickerReady .js*

下列範例會顯示您應該在*Views\Shared\\_Layout. cshtml*檔案的 `head` 專案底部加入的實際程式碼。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

完整的 `head` 區段如下所示：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

[URL 內容 helper](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx)方法會將資源路徑轉換為絕對路徑。 當應用程式在 IIS 上執行時，您必須使用 `@URL.Content` 來正確參考這些資源。

按 CTRL+F5 執行應用程式。 選取 [編輯] 連結，然後將插入點放入 [ **ReleaseDate** ] 欄位中。 隨即顯示 jQuery UI 快顯行事曆。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

就像大部分的 jQuery 控制項一樣，datepicker 可讓您廣泛地進行自訂。 如需相關資訊，請參閱[JQUERY ui](http://learn.jquery.com/jquery-ui/getting-started/)網站上的[視覺化自訂：設計 jquery ui 主題](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme)。

### <a name="supporting-the-html5-date-input-control"></a>支援 HTML5 日期輸入控制項

當瀏覽器支援 HTML5 時，您會想要使用原生 HTML5 輸入（例如 `date` input 元素），而不使用 jQuery UI 行事曆。 如果瀏覽器支援，您可以在應用程式中新增邏輯，以自動使用 HTML5 控制項。 若要這麼做，請將*DatePickerReady*的內容取代為下列內容：

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

此腳本的第一行會使用 Modernizr 來驗證是否支援 HTML5 日期輸入。 如果不支援，jQuery UI 日期選擇器會改為連結。 （[Modernizr](http://www.modernizr.com/docs/)是一種開放原始碼 JavaScript 程式庫，可偵測 HTML5 和 CSS3 原生執行的可用性。 Modernizr 會包含在您所建立的任何新 ASP.NET MVC 專案中）。

進行這項變更之後，您可以使用支援 HTML5 的瀏覽器來測試它，例如 Opera 11。 使用與 HTML5 相容的瀏覽器來執行應用程式，並編輯電影專案。 使用 HTML5 日期控制項，而不是 jQuery UI 快顯行事曆：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

因為新版本的瀏覽器會以累加方式來執行 HTML5，所以現在最好的方法是將程式碼新增至您的網站，以容納各種 HTML5 支援。 例如，以下顯示更健全的*DatePickerReady*腳本，可讓您的網站支援僅部分支援 HTML5 日期控制項的瀏覽器。

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

此腳本會選取不完全支援 HTML5 日期控制項 `date` 類型的 HTML5 `input` 元素。 針對這些元素，它會連結 jQuery UI 快顯行事曆，然後將 `type` 屬性從 `date` 變更為 `text`。 藉由將 `type` 屬性從 `date` 變更為 `text`，就會消除部分 HTML5 日期支援。 您可以在[JSFIDDLE](http://jsfiddle.net/XSTK8/15/)中找到更健全的*DatePickerReady*腳本。

### <a name="adding-nullable-dates-to-the-templates"></a>將可為 Null 的日期加入至範本

如果您使用其中一個現有的日期範本並傳遞 null 日期，您會收到執行階段錯誤。 為了讓日期範本更穩固，您會將其變更為處理 null 值。 若要支援可為 null 的日期，請將*Views\Shared\DisplayTemplates\DateTime.cshtml*中的程式碼變更為下列內容：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

當模型為**null**時，此程式碼會傳回空字串。

將*Views\Shared\EditorTemplates\Date.cshtml*檔案中的程式碼變更為下列內容：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

當此程式碼執行時，如果模型不是 null，則會使用模型的 `DateTime` 值。 如果模型是 null，則會改用目前的日期。

### <a name="wrapup"></a>Wrapup

本教學課程涵蓋 ASP.NET 樣板化 helper 的基本概念，並示範如何在 ASP.NET MVC 應用程式中使用 jQuery UI datepicker 快顯行事曆。 如需詳細資訊，請嘗試下列資源：

- 如需當地語系化的詳細資訊，請參閱 Rajeesh 的 blog [JQueryUI Datepicker in ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/)。
- 如需 jQuery UI 的詳細資訊，請參閱[JQUERY ui](http://docs.jquery.com/UI)。
- 如需如何將 datepicker 控制項當地語系化的詳細資訊，請參閱[UI/datepicker/當地語系化](http://docs.jquery.com/UI/Datepicker/Localization)。
- 如需有關 ASP.NET MVC 範本的詳細資訊，請參閱[ASP.NET mvc 2 範本](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)上的 Brad Wilson 的 blog 系列。 雖然此系列是針對 ASP.NET MVC 2 而撰寫的，但該材料仍然適用于目前版本的 ASP.NET MVC。

> [!div class="step-by-step"]
> [上一篇](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
