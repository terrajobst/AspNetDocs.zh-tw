---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
title: 使用 ColorPicker 控制項擴充項（C#） |Microsoft Docs
author: microsoft
description: ColorPicker 是一種 ASP.NET 的 AJAX 擴充項，可在 popup 控制項中提供 UI 的用戶端色彩挑選功能。 它可以附加至任何 ASP.NET 。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0d86a1e7-a910-4ab2-b85c-7a9ea6906c39
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: ac510ab353878038c1c7a103bfbf6d32fb1b2686
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614041"
---
# <a name="using-the-colorpicker-control-extender-c"></a>使用 ColorPicker 控制項擴充項（C#）

由[Microsoft](https://github.com/microsoft)

> ColorPicker 是一種 ASP.NET 的 AJAX 擴充項，可在 popup 控制項中提供 UI 的用戶端色彩挑選功能。 它可以附加至任何 ASP.NET TextBox 控制項。 這樣.

本教學課程的目的是要說明如何使用 AJAX 控制項工具組 ColorPicker 控制項擴充項。 ColorPicker 控制項擴充項會顯示可讓您選取色彩的快顯對話方塊。 當您想要提供直覺的使用者介面讓使用者挑選色彩時，ColorPicker 就很有用。

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>使用 ColorPicker 控制項擴充項延伸 TextBox 控制項

例如，假設您想要建立可讓訪客建立自訂名片的網站。 訪客可以輸入名片的文字並挑選色彩。 [清單 1] 中的 [ASP.NET] 頁面包含兩個名為 txtCardText 和 txtCardColor 的 TextBox 控制項。 當您提交表單時，會顯示選取的值（請參閱 [圖 1]）。

[![簡單的表單建立名片](using-the-colorpicker-control-extender-cs/_static/image1.jpg)](using-the-colorpicker-control-extender-cs/_static/image1.png)

**圖 01**：用來建立名片的簡單表單（[按一下以觀看完整大小的影像](using-the-colorpicker-control-extender-cs/_static/image2.png)）

**清單 1-CreateCard .aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample1.aspx)]

[清單 1] 中的表單可運作，但不提供絕佳的使用者體驗。 使用者必須在文字方塊中輸入色彩。 如果使用者想要使用特定的色彩（例如，尖峰綠色的適當陰影），則使用者必須找出 HTML 色彩代碼，而不需要任何協助。

您可以使用 ColorPicker 控制項擴充項來建立更好的使用者體驗。 當您將焦點移至 TextBox 控制項時，ColorPicker 會顯示色彩對話方塊（請參閱 [圖 2]）。

[![ColorPicker 控制項擴充項](using-the-colorpicker-control-extender-cs/_static/image2.jpg)](using-the-colorpicker-control-extender-cs/_static/image3.png)

**圖 02**： ColorPicker 控制項擴充項（[按一下以查看完整大小的影像](using-the-colorpicker-control-extender-cs/_static/image4.png)）

您需要完成兩個步驟，才能使用 ColorPicker 控制項擴充項搭配清單1中的表單：

1. 將 ScriptManager 控制項新增至頁面
2. 將 ColorPicker 控制項擴充項新增至頁面

在您可以使用 ColorPicker 之前，您必須先將 ScriptManager 新增至您的頁面。 新增 ScriptManager 的最佳位置是在開啟伺服器端 &lt;表單&gt; 標記的正下方。 您可以從 [工具箱] 將 ScriptManager 拖曳至頁面（ScriptManager 位於 [AJAX 延伸模組] 索引標籤底下）。 或者，您可以在 [起始伺服器端] 表單標籤底下的 [來源] 視圖中輸入下列標記：

&lt;asp： ScriptManager ID = "ScriptManager1" runat = "server"/&gt;

將 ColorPicker 控制項擴充項加入至頁面的最簡單方式是在設計檢視中。 如果您將滑鼠停留在 [txtCardColor] 文字方塊上，就會出現 [智慧型工作] 選項，讓您加入擴充項（請參閱 [圖 3]）。 如果您選擇此選項，則會出現 [擴充性檢查程式] （請參閱 [圖 4]）。

[![加入擴充項](using-the-colorpicker-control-extender-cs/_static/image3.jpg)](using-the-colorpicker-control-extender-cs/_static/image5.png)

**圖 03**：加入擴充項（[按一下以查看完整大小的影像](using-the-colorpicker-control-extender-cs/_static/image6.png)）

[![選取具有擴充性 Wizard 的控制項擴充項](using-the-colorpicker-control-extender-cs/_static/image4.jpg)](using-the-colorpicker-control-extender-cs/_static/image7.png)

**圖 04**：使用擴充性檢查程式選取控制項擴充項（[按一下以查看完整大小的影像](using-the-colorpicker-control-extender-cs/_static/image8.png)）

您可以挑選 ColorPicker 擴充項，使用 ColorPicker 擴充項來延伸 [txtCardColor] 文字方塊。 按一下 [確定] 關閉對話方塊。

在您進行這些變更之後，頁面的來源看起來會像 [清單 2]。

清單 2-CreateCard .aspx （含 ColorPicker）

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample2.aspx)]

請注意，此頁面現在包含 [txtCardColor TextBox] 控制項正下方的 ColorPickerExtender 控制項。 ColorPickerExtender 控制項會擴充 txtCardColor 控制項，使其顯示色彩選擇器對話方塊。

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>使用按鈕啟動色彩選擇器對話方塊

ColorPicker 擴充項支援下列屬性：

- PopupButtonId-頁面上導致色彩選擇器對話方塊出現的按鈕識別碼。
- PopupPosition-色彩選擇器對話方塊的相對於目標控制項的位置。 可能的值為絕對、中間、BottomLeft、BottomRight、TopLeft、右上、Right 和 Left （預設為 BottomLeft）。
- SampleControlId-顯示所選取色彩之控制項的識別碼。
- SelectedColor-ColorPicker 所選取的初始色彩。

您可以使用這些屬性來自訂色彩選擇器對話方塊的顯示方式，以及選取的色彩顯示方式。 [清單 3] 中的頁面說明您可以如何使用其中幾個屬性。

**清單 3-CreateCardButton .aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample3.aspx)]

[清單 3] 中的頁面包含 [挑選色彩] 按鈕（請參閱 [圖 5]）。 當您按一下此按鈕時，[色彩選擇器] 對話方塊會出現在文字方塊的上方。 如果您從對話方塊中選取色彩，則選取的色彩會顯示為 lblSample 標籤控制項的背景色彩。

ColorPicker PopupButtonID 屬性是用來將 [選擇色彩] 按鈕與 ColorPicker 擴充項產生關聯。 當您提供 [PopupButtonID] 屬性的值時，當目標控制項有焦點時，[色彩選擇器] 對話方塊就不會再出現。 您必須按一下按鈕，才會顯示對話方塊。

SampleControlID 屬性是用來將顯示所選色彩的控制項與 ColorPicker 建立關聯。 ColorPicker 會將這個控制項的背景色彩變更為目前選取的色彩。

[![顯示具有按鈕的色彩選擇器對話方塊](using-the-colorpicker-control-extender-cs/_static/image5.jpg)](using-the-colorpicker-control-extender-cs/_static/image9.png)

**圖 05**：顯示具有按鈕的色彩選擇器對話方塊（[按一下以觀看完整大小的影像](using-the-colorpicker-control-extender-cs/_static/image10.png)）

## <a name="summary"></a>總結

在本教學課程中，您已瞭解如何使用 ColorPicker 控制項擴充項來顯示快捷方式色彩選擇器對話方塊。 首先，我們會檢查當焦點移至 TextBox 控制項時，您可以如何顯示對話方塊。 接下來，您已瞭解如何建立按鈕，在按一下按鈕時顯示色彩選擇器對話方塊。

> [!div class="step-by-step"]
> [下一個](using-the-colorpicker-control-extender-vb.md)
