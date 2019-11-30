---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
title: 搭配驗證控制項使用 TextBoxWatermark （C#） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 TextBoxWatermark 控制項會擴充一個文字方塊，讓文字顯示在方塊中。 當使用者按一下方塊時，我 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d49940cb-d38c-456a-b800-5f0eb705d09f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: bc9498b1c5ba2f38b90706c9200ffa813a945fa9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74610891"
---
# <a name="using-textboxwatermark-with-validation-controls-c"></a><span data-ttu-id="a32a3-104">使用 TextBoxWatermark 與驗證控制項 (C#)</span><span class="sxs-lookup"><span data-stu-id="a32a3-104">Using TextBoxWatermark With Validation Controls (C#)</span></span>

<span data-ttu-id="a32a3-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a32a3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a32a3-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a32a3-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span></span>

> <span data-ttu-id="a32a3-107">AJAX 控制項工具組中的 TextBoxWatermark 控制項會擴充一個文字方塊，讓文字顯示在方塊中。</span><span class="sxs-lookup"><span data-stu-id="a32a3-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="a32a3-108">當使用者按一下方塊時，就會清空。</span><span class="sxs-lookup"><span data-stu-id="a32a3-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="a32a3-109">如果使用者離開方塊而不輸入文字，預先填入的文字就會重新出現。</span><span class="sxs-lookup"><span data-stu-id="a32a3-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="a32a3-110">這可能會與相同頁面上的 ASP.NET 驗證控制項衝突，但這些問題可能會受到克服。</span><span class="sxs-lookup"><span data-stu-id="a32a3-110">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="overview"></a><span data-ttu-id="a32a3-111">概觀</span><span class="sxs-lookup"><span data-stu-id="a32a3-111">Overview</span></span>

<span data-ttu-id="a32a3-112">AJAX 控制項工具組中的 `TextBoxWatermark` 控制項會擴充一個文字方塊，讓文字顯示在方塊中。</span><span class="sxs-lookup"><span data-stu-id="a32a3-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="a32a3-113">當使用者按一下方塊時，就會清空。</span><span class="sxs-lookup"><span data-stu-id="a32a3-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="a32a3-114">如果使用者離開方塊而不輸入文字，預先填入的文字就會重新出現。</span><span class="sxs-lookup"><span data-stu-id="a32a3-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="a32a3-115">這可能會與相同頁面上的 ASP.NET 驗證控制項衝突，但這些問題可能會受到克服。</span><span class="sxs-lookup"><span data-stu-id="a32a3-115">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="steps"></a><span data-ttu-id="a32a3-116">步驟</span><span class="sxs-lookup"><span data-stu-id="a32a3-116">Steps</span></span>

<span data-ttu-id="a32a3-117">範例的基本設定如下所示：使用 `TextBoxWatermarkExtender` 控制項浮水印 `TextBox` 控制項。</span><span class="sxs-lookup"><span data-stu-id="a32a3-117">The basic setup of the sample is the following: a `TextBox` control is watermarked using a `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="a32a3-118">按鈕會觸發回傳，稍後會用來觸發頁面上的驗證控制項。</span><span class="sxs-lookup"><span data-stu-id="a32a3-118">A button triggers a postback and will later be used to trigger the validation controls on the page.</span></span> <span data-ttu-id="a32a3-119">此外，也需要 `ScriptManager` 控制項來初始化 ASP.NET AJAX：</span><span class="sxs-lookup"><span data-stu-id="a32a3-119">Also, a `ScriptManager` control is required to initialize ASP.NET AJAX:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="a32a3-120">現在加入一個 `RequiredFieldValidator` 控制項，它會在提交表單時，檢查欄位中是否有文字。</span><span class="sxs-lookup"><span data-stu-id="a32a3-120">Now add a `RequiredFieldValidator` control that checks whether there is text in the field when the form is submitted.</span></span> <span data-ttu-id="a32a3-121">驗證程式的 `InitialValue` 屬性必須設定為 `TextBoxWatermarkExtender` 控制項中所使用的相同值：提交表單時，未變更的文字方塊值是其中的浮水印值：</span><span class="sxs-lookup"><span data-stu-id="a32a3-121">The `InitialValue` property of the validator must be set to the same value that is used in the `TextBoxWatermarkExtender` control: When the form is submitted, the value of an unchanged textbox is the watermark value within it:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="a32a3-122">不過，此方法有一個問題：如果用戶端停用 JavaScript，則文字欄位不會預先填入浮水印文字，因此 `RequiredFieldValidator` 不會觸發錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="a32a3-122">However there is one problem with this approach: If the client disables JavaScript, the text field is not prefilled with the watermark text, therefore the `RequiredFieldValidator` does not trigger an error message.</span></span> <span data-ttu-id="a32a3-123">因此，需要第二個 `RequiredFieldValidator` 控制項，以檢查空的文字方塊（省略 `InitialValue` 屬性）。</span><span class="sxs-lookup"><span data-stu-id="a32a3-123">Therefore, a second `RequiredFieldValidator` control is required which checks for an empty text box (omitting the `InitialValue` attribute).</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="a32a3-124">由於這兩個驗證程式都是使用 `Display`=`"Dynamic"`，因此使用者無法區別兩個驗證程式引發的視覺外觀;相反地，它似乎只有其中一個。</span><span class="sxs-lookup"><span data-stu-id="a32a3-124">Since both validators use `Display`=`"Dynamic"`, the end user cannot distinguish from the visual appearance which of the two validators was fired; instead, it looks like there was only one of them.</span></span>

<span data-ttu-id="a32a3-125">最後，新增一些伺服器端程式碼，以便在沒有驗證器發出錯誤訊息時，輸出欄位中的文字：</span><span class="sxs-lookup"><span data-stu-id="a32a3-125">Finally, add some server-side code to output the text in the field if no validator issued an error message:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample4.aspx)]

<span data-ttu-id="a32a3-126">[![驗證程式抱怨欄位中沒有文字](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a32a3-126">[![The validator complains that there is no text in the field](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)</span></span>

<span data-ttu-id="a32a3-127">驗證程式抱怨欄位中沒有文字（[按一下以查看完整大小的影像](using-textboxwatermark-with-validation-controls-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="a32a3-127">The validator complains that there is no text in the field ([Click to view full-size image](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a32a3-128">[上一頁](using-textboxwatermark-in-a-formview-cs.md)
> [下一頁](using-textboxwatermark-in-a-formview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a32a3-128">[Previous](using-textboxwatermark-in-a-formview-cs.md)
[Next](using-textboxwatermark-in-a-formview-vb.md)</span></span>
