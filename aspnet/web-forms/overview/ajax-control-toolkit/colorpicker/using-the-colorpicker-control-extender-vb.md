---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: 使用 ColorPicker 控制項擴充項（VB） |Microsoft Docs
author: microsoft
description: ColorPicker 是一種 ASP.NET 的 AJAX 擴充項，可在 popup 控制項中提供 UI 的用戶端色彩挑選功能。 它可以附加至任何 ASP.NET 。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 77e2e3bc61a5e1498570959ca40acff83dc3fc82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554499"
---
# <a name="using-the-colorpicker-control-extender-vb"></a><span data-ttu-id="80b02-104">使用 ColorPicker 控制項擴充項（VB）</span><span class="sxs-lookup"><span data-stu-id="80b02-104">Using the ColorPicker Control Extender (VB)</span></span>

<span data-ttu-id="80b02-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="80b02-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="80b02-106">ColorPicker 是一種 ASP.NET 的 AJAX 擴充項，可在 popup 控制項中提供 UI 的用戶端色彩挑選功能。</span><span class="sxs-lookup"><span data-stu-id="80b02-106">ColorPicker is an ASP.NET AJAX extender that provides client-side color-picking functionality with UI in a popup control.</span></span> <span data-ttu-id="80b02-107">它可以附加至任何 ASP.NET TextBox 控制項。</span><span class="sxs-lookup"><span data-stu-id="80b02-107">It can be attached to any ASP.NET TextBox control.</span></span> <span data-ttu-id="80b02-108">這樣.</span><span class="sxs-lookup"><span data-stu-id="80b02-108">It.</span></span>

<span data-ttu-id="80b02-109">本教學課程的目的是要說明如何使用 AJAX 控制項工具組 ColorPicker 控制項擴充項。</span><span class="sxs-lookup"><span data-stu-id="80b02-109">The goal of this tutorial is to explain how you can use the AJAX Control Toolkit ColorPicker control extender.</span></span> <span data-ttu-id="80b02-110">ColorPicker 控制項擴充項會顯示可讓您選取色彩的快顯對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80b02-110">The ColorPicker control extender displays a popup dialog that enables you to select a color.</span></span> <span data-ttu-id="80b02-111">當您想要提供直覺的使用者介面讓使用者挑選色彩時，ColorPicker 就很有用。</span><span class="sxs-lookup"><span data-stu-id="80b02-111">The ColorPicker is useful whenever you want to provide an intuitive user interface for a user to pick a color.</span></span>

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a><span data-ttu-id="80b02-112">使用 ColorPicker 控制項擴充項延伸 TextBox 控制項</span><span class="sxs-lookup"><span data-stu-id="80b02-112">Extending a TextBox Control with the ColorPicker Control Extender</span></span>

<span data-ttu-id="80b02-113">例如，假設您想要建立可讓訪客建立自訂名片的網站。</span><span class="sxs-lookup"><span data-stu-id="80b02-113">Imagine, for example, that you want to create a website that enables visitors to create customized business cards.</span></span> <span data-ttu-id="80b02-114">訪客可以輸入名片的文字並挑選色彩。</span><span class="sxs-lookup"><span data-stu-id="80b02-114">Visitors can enter the text for a business card and pick the color.</span></span> <span data-ttu-id="80b02-115">[清單 1] 中的 [ASP.NET] 頁面包含兩個名為 txtCardText 和 txtCardColor 的 TextBox 控制項。</span><span class="sxs-lookup"><span data-stu-id="80b02-115">The ASP.NET page in Listing 1 contains two TextBox controls named txtCardText and txtCardColor.</span></span> <span data-ttu-id="80b02-116">當您提交表單時，會顯示選取的值（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="80b02-116">When you submit the form, the selected values are displayed (see Figure 1).</span></span>

<span data-ttu-id="80b02-117">[![簡單的表單建立名片](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="80b02-117">[![Simple form for creating a business card](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span></span>

<span data-ttu-id="80b02-118">**圖 01**：用來建立名片的簡單表單（[按一下以觀看完整大小的影像](using-the-colorpicker-control-extender-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="80b02-118">**Figure 01**: Simple form for creating a business card ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image2.png))</span></span>

<span data-ttu-id="80b02-119">**清單 1-CreateCard .aspx**</span><span class="sxs-lookup"><span data-stu-id="80b02-119">**Listing 1 - CreateCard.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

<span data-ttu-id="80b02-120">[清單 1] 中的表單可運作，但不提供絕佳的使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="80b02-120">The form in Listing 1 works, but it does not provide a great user experience.</span></span> <span data-ttu-id="80b02-121">使用者必須在文字方塊中輸入色彩。</span><span class="sxs-lookup"><span data-stu-id="80b02-121">The user has to type a color into the textbox.</span></span> <span data-ttu-id="80b02-122">如果使用者想要使用特定的色彩（例如，尖峰綠色的適當陰影），則使用者必須找出 HTML 色彩代碼，而不需要任何協助。</span><span class="sxs-lookup"><span data-stu-id="80b02-122">If the user wants a specialized color - for example, just the right shade of pea green - then the user must figure out the HTML color code without any help.</span></span>

<span data-ttu-id="80b02-123">您可以使用 ColorPicker 控制項擴充項來建立更好的使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="80b02-123">You can use the ColorPicker control extender to create a better user experience.</span></span> <span data-ttu-id="80b02-124">當您將焦點移至 TextBox 控制項時，ColorPicker 會顯示色彩對話方塊（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="80b02-124">The ColorPicker displays a color dialog when you move focus to a TextBox control (see Figure 2).</span></span>

<span data-ttu-id="80b02-125">[![ColorPicker 控制項擴充項](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="80b02-125">[![The ColorPicker Control Extender](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span></span>

<span data-ttu-id="80b02-126">**圖 02**： ColorPicker 控制項擴充項（[按一下以查看完整大小的影像](using-the-colorpicker-control-extender-vb/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="80b02-126">**Figure 02**: The ColorPicker Control Extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image4.png))</span></span>

<span data-ttu-id="80b02-127">您需要完成兩個步驟，才能使用 ColorPicker 控制項擴充項搭配清單1中的表單：</span><span class="sxs-lookup"><span data-stu-id="80b02-127">You need to complete two steps to use the ColorPicker control extender with the form in Listing 1:</span></span>

1. <span data-ttu-id="80b02-128">將 ScriptManager 控制項新增至頁面</span><span class="sxs-lookup"><span data-stu-id="80b02-128">Add a ScriptManager control to the page</span></span>
2. <span data-ttu-id="80b02-129">將 ColorPicker 控制項擴充項新增至頁面</span><span class="sxs-lookup"><span data-stu-id="80b02-129">Add the ColorPicker control extender to the page</span></span>

<span data-ttu-id="80b02-130">在您可以使用 ColorPicker 之前，您必須先將 ScriptManager 新增至您的頁面。</span><span class="sxs-lookup"><span data-stu-id="80b02-130">Before you can use the ColorPicker, you must add a ScriptManager to your page.</span></span> <span data-ttu-id="80b02-131">新增 ScriptManager 的最佳位置是在開啟伺服器端 &lt;表單&gt; 標記的正下方。</span><span class="sxs-lookup"><span data-stu-id="80b02-131">A good place to add the ScriptManager is right below the opening server-side &lt;form&gt; tag.</span></span> <span data-ttu-id="80b02-132">您可以從 [工具箱] 將 ScriptManager 拖曳至頁面（ScriptManager 位於 [AJAX 延伸模組] 索引標籤底下）。</span><span class="sxs-lookup"><span data-stu-id="80b02-132">You can drag the ScriptManager onto the page from the toolbox (the ScriptManager is located under the AJAX Extensions tab).</span></span> <span data-ttu-id="80b02-133">或者，您可以在 [起始伺服器端] 表單標籤底下的 [來源] 視圖中輸入下列標記：</span><span class="sxs-lookup"><span data-stu-id="80b02-133">Alternatively, you can type the following tag into Source View beneath the opening server-side form tag:</span></span>

<span data-ttu-id="80b02-134">&lt;asp： ScriptManager ID = "ScriptManager1" runat = "server"/&gt;</span><span class="sxs-lookup"><span data-stu-id="80b02-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span></span>

<span data-ttu-id="80b02-135">將 ColorPicker 控制項擴充項加入至頁面的最簡單方式是在設計檢視中。</span><span class="sxs-lookup"><span data-stu-id="80b02-135">The easiest way to add the ColorPicker control extender to the page is in Design View.</span></span> <span data-ttu-id="80b02-136">如果您將滑鼠停留在 [txtCardColor] 文字方塊上，就會出現 [智慧型工作] 選項，讓您加入擴充項（請參閱 [圖 3]）。</span><span class="sxs-lookup"><span data-stu-id="80b02-136">If you hover your mouse over the txtCardColor TextBox, a smart task option appears the enables you to add an extender (see Figure 3).</span></span> <span data-ttu-id="80b02-137">如果您選擇此選項，則會出現 [擴充性檢查程式] （請參閱 [圖 4]）。</span><span class="sxs-lookup"><span data-stu-id="80b02-137">If you pick this option, the Extender Wizard appears (see Figure 4).</span></span>

<span data-ttu-id="80b02-138">[![加入擴充項](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="80b02-138">[![Adding an extender](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span></span>

<span data-ttu-id="80b02-139">**圖 03**：加入擴充項（[按一下以查看完整大小的影像](using-the-colorpicker-control-extender-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="80b02-139">**Figure 03**: Adding an extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image6.png))</span></span>

<span data-ttu-id="80b02-140">[![選取具有擴充性 Wizard 的控制項擴充項](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="80b02-140">[![Selecting a control extender with the Extender Wizard](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="80b02-141">**圖 04**：使用擴充性檢查程式選取控制項擴充項（[按一下以查看完整大小的影像](using-the-colorpicker-control-extender-vb/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="80b02-141">**Figure 04**: Selecting a control extender with the Extender Wizard ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image8.png))</span></span>

<span data-ttu-id="80b02-142">您可以挑選 ColorPicker 擴充項，使用 ColorPicker 擴充項來延伸 [txtCardColor] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="80b02-142">You can pick the ColorPicker extender to extend the txtCardColor TextBox with the ColorPicker extender.</span></span> <span data-ttu-id="80b02-143">按一下 [確定] 關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80b02-143">Click OK to close the dialog.</span></span>

<span data-ttu-id="80b02-144">在您進行這些變更之後，頁面的來源看起來會像 [清單 2]。</span><span class="sxs-lookup"><span data-stu-id="80b02-144">After you make these changes, the source for the page looks like Listing 2.</span></span>

<span data-ttu-id="80b02-145">**清單 2-CreateCard .aspx （含 ColorPicker）**</span><span class="sxs-lookup"><span data-stu-id="80b02-145">**Listing 2 - CreateCard.aspx (with ColorPicker)**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

<span data-ttu-id="80b02-146">請注意，此頁面現在包含 [txtCardColor TextBox] 控制項正下方的 ColorPickerExtender 控制項。</span><span class="sxs-lookup"><span data-stu-id="80b02-146">Notice that the page now contains a ColorPickerExtender control that appears directly below the txtCardColor TextBox control.</span></span> <span data-ttu-id="80b02-147">ColorPickerExtender 控制項會擴充 txtCardColor 控制項，使其顯示色彩選擇器對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80b02-147">The ColorPickerExtender control extends the txtCardColor control so that it displays a color picker dialog.</span></span>

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a><span data-ttu-id="80b02-148">使用按鈕啟動色彩選擇器對話方塊</span><span class="sxs-lookup"><span data-stu-id="80b02-148">Using a Button to Launch the Color Picker Dialog</span></span>

<span data-ttu-id="80b02-149">ColorPicker 擴充項支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="80b02-149">The ColorPicker extender supports the following properties:</span></span>

- <span data-ttu-id="80b02-150">PopupButtonId-頁面上導致色彩選擇器對話方塊出現的按鈕識別碼。</span><span class="sxs-lookup"><span data-stu-id="80b02-150">PopupButtonId - The ID of a button on the page that causes the color picker dialog to appear.</span></span>
- <span data-ttu-id="80b02-151">PopupPosition-色彩選擇器對話方塊的相對於目標控制項的位置。</span><span class="sxs-lookup"><span data-stu-id="80b02-151">PopupPosition - The position, relative to the target control, of the color picker dialog.</span></span> <span data-ttu-id="80b02-152">可能的值為絕對、中間、BottomLeft、BottomRight、TopLeft、右上、Right 和 Left （預設為 BottomLeft）。</span><span class="sxs-lookup"><span data-stu-id="80b02-152">Possible values are Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right, and Left (the default is BottomLeft).</span></span>
- <span data-ttu-id="80b02-153">SampleControlId-顯示所選取色彩之控制項的識別碼。</span><span class="sxs-lookup"><span data-stu-id="80b02-153">SampleControlId - The ID of a control that displays the selected color.</span></span>
- <span data-ttu-id="80b02-154">SelectedColor-ColorPicker 所選取的初始色彩。</span><span class="sxs-lookup"><span data-stu-id="80b02-154">SelectedColor - The initial color selected by the ColorPicker.</span></span>

<span data-ttu-id="80b02-155">您可以使用這些屬性來自訂色彩選擇器對話方塊的顯示方式，以及選取的色彩顯示方式。</span><span class="sxs-lookup"><span data-stu-id="80b02-155">You can use these properties to customize how the color picker dialog is displayed and how the selected color is displayed.</span></span> <span data-ttu-id="80b02-156">[清單 3] 中的頁面說明您可以如何使用其中幾個屬性。</span><span class="sxs-lookup"><span data-stu-id="80b02-156">The page in Listing 3 illustrates how you can use several of these properties.</span></span>

<span data-ttu-id="80b02-157">**清單 3-CreateCardButton .aspx**</span><span class="sxs-lookup"><span data-stu-id="80b02-157">**Listing 3 - CreateCardButton.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

<span data-ttu-id="80b02-158">[清單 3] 中的頁面包含 [挑選色彩] 按鈕（請參閱 [圖 5]）。</span><span class="sxs-lookup"><span data-stu-id="80b02-158">The page in Listing 3 includes a Pick Color button (see Figure 5).</span></span> <span data-ttu-id="80b02-159">當您按一下此按鈕時，[色彩選擇器] 對話方塊會出現在文字方塊的上方。</span><span class="sxs-lookup"><span data-stu-id="80b02-159">When you click this button, the color picker dialog appears above the TextBox.</span></span> <span data-ttu-id="80b02-160">如果您從對話方塊中選取色彩，則選取的色彩會顯示為 lblSample 標籤控制項的背景色彩。</span><span class="sxs-lookup"><span data-stu-id="80b02-160">If you select a color from the dialog then the selected color appears as the background color of the lblSample Label control.</span></span>

<span data-ttu-id="80b02-161">ColorPicker PopupButtonID 屬性是用來將 [選擇色彩] 按鈕與 ColorPicker 擴充項產生關聯。</span><span class="sxs-lookup"><span data-stu-id="80b02-161">The ColorPicker PopupButtonID property is used to associate the Pick Color button with the ColorPicker extender.</span></span> <span data-ttu-id="80b02-162">當您提供 [PopupButtonID] 屬性的值時，當目標控制項有焦點時，[色彩選擇器] 對話方塊就不會再出現。</span><span class="sxs-lookup"><span data-stu-id="80b02-162">When you supply a value for the PopupButtonID property, the color picker dialog no longer appears when the target control has focus.</span></span> <span data-ttu-id="80b02-163">您必須按一下按鈕，才會顯示對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80b02-163">You must click the button to display the dialog.</span></span>

<span data-ttu-id="80b02-164">SampleControlID 屬性是用來將顯示所選色彩的控制項與 ColorPicker 建立關聯。</span><span class="sxs-lookup"><span data-stu-id="80b02-164">The SampleControlID property is used to associate a control that displays the selected color with the ColorPicker.</span></span> <span data-ttu-id="80b02-165">ColorPicker 會將這個控制項的背景色彩變更為目前選取的色彩。</span><span class="sxs-lookup"><span data-stu-id="80b02-165">The ColorPicker changes the background color of this control to the currently selected color.</span></span>

<span data-ttu-id="80b02-166">[![顯示具有按鈕的色彩選擇器對話方塊](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="80b02-166">[![Displaying the color picker dialog with a button](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span></span>

<span data-ttu-id="80b02-167">**圖 05**：顯示具有按鈕的色彩選擇器對話方塊（[按一下以觀看完整大小的影像](using-the-colorpicker-control-extender-vb/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="80b02-167">**Figure 05**: Displaying the color picker dialog with a button ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image10.png))</span></span>

## <a name="summary"></a><span data-ttu-id="80b02-168">總結</span><span class="sxs-lookup"><span data-stu-id="80b02-168">Summary</span></span>

<span data-ttu-id="80b02-169">在本教學課程中，您已瞭解如何使用 ColorPicker 控制項擴充項來顯示快捷方式色彩選擇器對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80b02-169">In this tutorial, you learned how to use the ColorPicker control extender to display a popup color picker dialog.</span></span> <span data-ttu-id="80b02-170">首先，我們會檢查當焦點移至 TextBox 控制項時，您可以如何顯示對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80b02-170">First, we examined how you can display the dialog when focus is moved to a TextBox control.</span></span> <span data-ttu-id="80b02-171">接下來，您已瞭解如何建立按鈕，在按一下按鈕時顯示色彩選擇器對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80b02-171">Next, you learned how to create a button that displays the color picker dialog when the button is clicked.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="80b02-172">上一篇</span><span class="sxs-lookup"><span data-stu-id="80b02-172">Previous</span></span>](using-the-colorpicker-control-extender-cs.md)
