---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: 建立自訂 HTML 協助程式（VB） |Microsoft Docs
author: microsoft
description: 本教學課程的目的是要示範如何建立可在 MVC 視圖內使用的自訂 HTML 協助程式。 利用 HTML Helper 。
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: aaeadde258a2855343a5bfb1e5ee76000e04f6bd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600272"
---
# <a name="creating-custom-html-helpers-vb"></a>建立自訂的 HTML 協助程式 (VB)

由[Microsoft](https://github.com/microsoft)

[下載 PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> 本教學課程的目的是要示範如何建立可在 MVC 視圖內使用的自訂 HTML 協助程式。 藉由利用 HTML 協助程式，您可以減少在建立標準 HTML 網頁時，必須執行的 HTML 標籤的單調乏味輸入量。

本教學課程的目的是要示範如何建立可在 MVC 視圖內使用的自訂 HTML 協助程式。 藉由利用 HTML 協助程式，您可以減少在建立標準 HTML 網頁時，必須執行的 HTML 標籤的單調乏味輸入量。

在本教學課程的第一個部分中，我將說明 ASP.NET MVC 架構中包含的一些現有 HTML 協助程式。 接下來，我將說明建立自訂 HTML 協助程式的兩種方法：我將說明如何建立共用方法並建立擴充方法，以建立自訂 HTML helper。

## <a name="understanding-html-helpers"></a>瞭解 HTML 協助程式

HTML Helper 只是傳回字串的方法。 字串可以代表您想要的任何類型內容。 例如，您可以使用 HTML helper 來呈現標準 HTML 標籤，例如 HTML `<input>` 和 `<img>` 標記。 您也可以使用 HTML helper 來呈現更複雜的內容，例如索引標籤區域或資料庫資料的 HTML 表格。

ASP.NET MVC 架構包含下列一組標準 HTML 協助程式（這不是完整的清單）：

- .Html （）
- Html.beginform （）
- Html. CheckBox （）
- DropDownList （）
- EndForm （）
- Html. Hidden （）
- Html. ListBox （）
- Html. Password （）
- Html （選項按鈕）（）
- Html. TextArea （）
- Html. TextBox （）

例如，請考慮 [清單 1] 中的表單。 這種表單是透過兩個標準 HTML helper 的協助來呈現的（請參閱 [圖 1]）。 這個表單會使用 `Html.BeginForm()` 和 `Html.TextBox()` Helper 方法。

[使用 HTML 協助程式轉譯的 ![頁面](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)

**圖 01**：以 HTML 協助程式轉譯的頁面（[按一下以觀看完整大小的影像](creating-custom-html-helpers-vb/_static/image3.png)）

**清單1– `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

`Html.BeginForm()` Helper 方法是用來建立開頭和結尾的 HTML `<form>` 標記。 請注意，會在 using 語句中呼叫 `Html.BeginForm()` 方法。 Using 語句可確保在 using 區塊結尾處關閉 `<form>` 標記。

如果您想要，而不是建立 using 區塊，您可以呼叫 EndForm （） Helper 方法來關閉 `<form>` 標記。 您可以使用任何方法來建立開頭和結尾的 `<form>` 標記，這對您而言是最直覺的。

`Html.TextBox()` 的 Helper 方法會在清單1中用來呈現 HTML `<input>` 標記。 如果您在瀏覽器中選取 [view source]，則會在 [清單 2] 中看到 HTML 原始檔。 請注意，來源包含標準 HTML 標籤。

> [!IMPORTANT]
> 請注意，`Html.TextBox()`HTML 協助程式是以 `<%= %>` 標記而非 `<% %>` 標記來呈現。 如果您未包含等號，則不會將任何內容轉譯至瀏覽器。

ASP.NET MVC 架構包含一小部分的協助程式。 最有可能的情況是，您必須使用自訂 HTML 協助程式來擴充 MVC 架構。 在本教學課程的其餘部分，您將瞭解建立自訂 HTML 協助程式的兩種方法。

**清單2– `Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a>使用共用方法建立 HTML 協助程式

建立新 HTML Helper 的最簡單方式，就是建立可傳回字串的共用方法。 例如，假設您決定要建立新的 HTML Helper，以轉譯 HTML `<label>` 標記。 您可以使用 [清單 2] 中的類別來呈現 `<label>`。

**清單2– `Helpers\LabelHelper.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

[清單 2] 中的類別沒有特別的內容。 `Label()` 方法只會傳回字串。

[清單 3] 中修改過的索引視圖會使用 `LabelHelper` 來呈現 HTML `<label>` 標記。 請注意，此視圖包含匯入 Application1 命名空間的 `<%@ imports %>` 指示詞。

**清單2– `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>建立具有擴充方法的 HTML 協助程式

如果您想要建立 HTML 協助程式，其作用就像 ASP.NET MVC 架構中包含的標準 HTML helper，那麼您必須建立擴充方法。 擴充方法可讓您將新的方法加入至現有的類別。 建立 HTML Helper 方法時，您會將新的方法加入至由視圖的 Html 屬性所表示的 `HtmlHelper` 類別。

[清單 3] 中的 [Visual Basic] 模組會將名為 `Label()` 的擴充方法新增至 `HtmlHelper` 類別。 關於此課程模組，您應該注意幾件事。 首先，請注意模組是以 `<Extension()>` 屬性裝飾。 若要使用這個屬性，您必須匯入 `System.Runtime.CompilerServices` 命名空間

第二，請注意，`Label()` 方法的第一個參數代表 `HtmlHelper` 類別。 擴充方法的第一個參數表示擴充方法擴充的類別。

**清單3– `Helpers\LabelExtensions.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

在您建立擴充方法並成功建立應用程式之後，擴充方法會出現在 Visual Studio Intellisense 中，就像類別的所有其他方法一樣（請參閱 [圖 2]）。 唯一的差別在於擴充方法會在其旁邊顯示特殊符號（向下箭號的圖示）。

[使用 Html. Label （）擴充方法 ![](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)

**圖 02**：使用 Html. Label （）擴充方法（[按一下以查看完整大小的影像](creating-custom-html-helpers-vb/_static/image6.png)）

[清單 4] 中修改過的索引視圖會使用 Html. Label （）擴充方法，將其所有的 &lt;標籤轉譯&gt; 標記。

**清單4– `Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a>總結

在本教學課程中，您已瞭解建立自訂 HTML 協助程式的兩種方法。 首先，您已瞭解如何建立一個會傳回字串的共用方法，以建立自訂的 `Label()` HTML Helper。 接下來，您已瞭解如何在 `HtmlHelper` 類別上建立擴充方法，以建立自訂的 `Label()` HTML Helper 方法。

在本教學課程中，我將重點放在建立非常簡單的 HTML Helper 方法。 請注意，HTML Helper 可以像您想要的一樣複雜。 您可以建立 HTML 協助程式來呈現豐富的內容，例如樹狀檢視、功能表或資料庫資料的資料表。

> [!div class="step-by-step"]
> [上一頁](asp-net-mvc-views-overview-vb.md)
> [下一頁](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
