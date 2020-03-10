---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: 使用 ViewData 並執行 ViewModel 類別 |Microsoft Docs
author: microsoft
description: 步驟6顯示如何支援更豐富的表單編輯案例，同時討論兩種可以用來將資料從控制器傳遞至 views 的方法： 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: ca9775417c2e25952511a73096fb76d5d4edaea2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541605"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>使用 ViewData 和實作 ViewModel 類別

由[Microsoft](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟6，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。
> 
> 步驟6顯示如何支援更豐富的表單編輯案例，同時討論兩種可以用來將資料從控制器傳遞至 views 的方法： ViewData 和 ViewModel。
> 
> 如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>NerdDinner 步驟6： ViewData 和 ViewModel

我們已涵蓋數種表單張貼案例，並已討論如何執行建立、更新和刪除（CRUD）支援。 我們現在會進一步進行 DinnersController 的執行，並支援更豐富的表單編輯案例。 這麼做時，我們將討論兩種可用於將資料從控制器傳遞至 views 的方法： ViewData 和 ViewModel。

### <a name="passing-data-from-controllers-to-view-templates"></a>將資料從控制器傳遞至流覽-範本

MVC 模式的其中一個定義特性是嚴格的「關注點分離」，有助於在應用程式的不同元件之間強制執行。 每個模型、控制器和視圖都具有妥善定義的角色和責任，而且它們會以定義完善的方式彼此通訊。 這有助於提升可測試性和重複使用程式碼。

當控制器類別決定將 HTML 回應轉譯回用戶端時，它會負責將轉譯回應所需的所有資料明確地傳遞給視圖範本。 視圖範本絕對不應執行任何資料抓取或應用程式邏輯，而是改為只將呈現程式碼導向至由控制器傳遞給它的模型/資料。

現在，我們的 DinnersController 類別傳遞給我們的視圖範本的模型資料，簡單明瞭明瞭–索引（）案例中的晚餐物件清單，以及在詳細資料（）、編輯（）、建立（）和刪除（）案例中的一個晚餐物件。 當我們在應用程式中新增更多 UI 功能時，我們通常只需要傳遞這種資料，就可以在我們的視圖範本內呈現 HTML 回應。 例如，我們可能會想要將 [編輯] 和 [建立視圖] 中的 [國家/地區] 欄位變更為 dropdownlist 的 HTML 文字方塊。 我們可能會想要以動態方式填入的支援國家/地區清單來產生該清單，而不是以硬式編碼方式在 view 範本中顯示國家/地區名稱的下拉式清單。 我們需要一種方法，將晚餐物件*和*支援的國家/地區清單，從我們的控制器傳遞至我們的視圖範本。

讓我們看一下兩種可以完成此動作的方法。

### <a name="using-the-viewdata-dictionary"></a>使用 ViewData 字典

控制器基類會公開 "ViewData" 字典屬性，可用來將控制器的其他資料項目傳遞給 Views。

例如，若要支援我們想要在編輯檢視中將 [國家/地區] 文字方塊從 HTML 文字方塊變更為 dropdownlist 的案例，我們可以更新編輯（）動作方法來傳遞（除了晚餐物件） SelectList 物件，以作為 m國家/地區 dropdownlist 的 mvc。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

上述 SelectList 的函式會接受用來填入下拉式 downlist 的縣市清單，以及目前選取的值。

然後，我們可以更新編輯 .aspx view 範本，以使用 DropDownList （） helper 方法，而不是我們先前使用的 Html. TextBox （） helper 方法：

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

上述的 DropDownList （） helper 方法會採用兩個參數。 第一個是要輸出的 HTML 表單元素名稱。 第二個是我們透過 ViewData 字典傳遞的「SelectList」模型。 我們使用C# "as" 關鍵字將字典中的類型轉換成 SelectList。

現在當我們執行應用程式並在瀏覽器中存取 */Dinners/Edit/1* URL 時，會看到編輯 UI 已更新為顯示國家/地區 dropdownlist，而不是文字方塊：

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

因為我們也會從 HTTP POST 編輯方法轉譯編輯檢視範本（在發生錯誤的情況下），我們會想要確定我們也會在錯誤案例中轉譯視圖範本時，更新此方法，以將 SelectList 新增至 ViewData：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

現在我們的 DinnersController edit 案例支援 DropDownList。

### <a name="using-a-viewmodel-pattern"></a>使用 ViewModel 模式

ViewData 字典方法具有相當快速且容易執行的優點。 不過，有些開發人員不喜歡使用以字串為基礎的字典，因為輸入錯誤可能會導致不會在編譯時期攔截到的錯誤。 不具類型的 ViewData 字典也需要使用 "as" 運算子，或在使用如C# view 範本的強型別語言時進行轉換。

另一種可以使用的方法，通常稱為「ViewModel」模式。 使用此模式時，我們會建立針對我們的特定視圖案例優化的強型別類別，並針對我們的視圖範本所需的動態值/內容公開屬性。 接著，我們的控制器類別可以填入這些視圖優化的類別，並將其傳遞給我們的 view 範本來使用。 這可讓您在 [視圖] 範本內進行型別安全、編譯時間檢查和編輯器 intellisense。

例如，若要啟用晚餐表單編輯案例，我們可以建立如下所示的 "DinnerFormViewModel" 類別，它會公開兩個強型別屬性：晚餐物件，以及填入國家（地區） dropdownlist 所需的 SelectList 模型：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

然後，我們可以更新編輯（）動作方法，以使用我們從存放庫中抓取的晚餐物件來建立 DinnerFormViewModel，然後將它傳遞至我們的 view 範本：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

接著，我們會更新我們的 view 範本，使其預期會有 "DinnerFormViewModel" 而不是 "晚餐" 物件，方法是變更編輯 .aspx 頁面頂端的 "inherits" 屬性，如下所示：

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

這麼做之後，我們會更新 view 範本內 "Model" 屬性的 intellisense，以反映我們傳遞它的 DinnerFormViewModel 類型的物件模型：

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

然後，我們就可以更新我們的 view 程式碼，使其無法使用。 請注意，我們不會變更我們所建立之輸入元素的名稱（表單元素仍然會命名為「標題」、「國家/地區」），但我們正在更新 HTML Helper 方法，以使用 DinnerFormViewModel 類別來抓取值：

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

我們也會在轉譯錯誤時，更新我們的編輯 post 方法以使用 DinnerFormViewModel 類別：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

我們也可以更新我們的 Create （）動作方法，以重複使用完全相同的*DinnerFormViewModel*類別，以啟用其中的國家/地區 DropDownList。 以下是 HTTP GET 執行：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

以下是 HTTP POST 建立方法的執行：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

現在，我們的編輯和建立畫面都支援下拉式 downlists 來挑選國家/地區。

### <a name="custom-shaped-viewmodel-classes"></a>自訂形狀的 ViewModel 類別

在上述案例中，我們的 DinnerFormViewModel 類別會直接將晚餐模型物件公開為屬性，以及支援的 SelectList 模型屬性。 當我們想要在我們的視圖範本內建立的 HTML UI 相對於我們的領域模型物件時，這種方法會正常運作。

針對不是這種情況的情況，您可以使用的一個選項是建立自訂形狀的 ViewModel 類別，其物件模型較適合供視圖取用，而且看起來可能與基礎領域模型物件完全不同。 例如，它可能會公開從多個模型物件收集而來的不同屬性名稱和/或匯總屬性。

自訂形狀的 ViewModel 類別可以用來將控制器的資料傳遞給 views 來呈現，以及協助處理回傳至控制器動作方法的表單資料。 在此稍後的案例中，您可能會有動作方法以表單張貼的資料更新 ViewModel 物件，然後使用 ViewModel 實例來對應或取出實際的領域模型物件。

自訂形狀的 ViewModel 類別可以提供很大的彈性，而且是在您發現視圖範本內的轉譯程式碼，或動作方法內的表單張貼程式碼開始變得太複雜時，要調查的一些專案。 這通常是您的網域模型不會完全對應至您所產生之 UI 的正負號，而中繼自訂形狀的 ViewModel 類別可以提供協助。

### <a name="next-step"></a>後續步驟

現在讓我們看看如何使用部分和主版頁面，在整個應用程式中重複使用和共用 UI。

> [!div class="step-by-step"]
> [上一頁](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [下一頁](re-use-ui-using-master-pages-and-partials.md)
