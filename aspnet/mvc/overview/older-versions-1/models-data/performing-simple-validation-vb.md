---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
title: 執行簡單的驗證（VB） |Microsoft Docs
author: StephenWalther
description: 瞭解如何在 ASP.NET MVC 應用程式中執行驗證。 在本教學課程中，Stephen Walther 會為您介紹模型狀態和驗證 HTML helper 。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: df6cf4b7-0bb3-4c4e-b17a-bd78a759a6bc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 46925f22b7dfc23f2bb89b8d2fff0cbd8ae49062
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542928"
---
# <a name="performing-simple-validation-vb"></a>執行簡單的驗證 (VB)

依[Stephen Walther](https://github.com/StephenWalther)

> 瞭解如何在 ASP.NET MVC 應用程式中執行驗證。 在本教學課程中，Stephen Walther 會為您介紹模型狀態和驗證 HTML 協助程式。

本教學課程的目的是要說明如何在 ASP.NET MVC 應用程式中執行驗證。 例如，您會瞭解如何防止某人提交不包含必要欄位值的表單。 您將瞭解如何使用模型狀態和驗證 HTML 協助程式。

## <a name="understanding-model-state"></a>瞭解模型狀態

您可以使用模型狀態或更精確的模型狀態字典，來表示驗證錯誤。 例如，[清單 1] 中的 Create （）動作會先驗證 Product 類別的屬性，再將 Product 類別加入至資料庫。

我不建議您將驗證或資料庫邏輯新增至控制器。 控制器應該只包含與應用程式流程式控制制相關的邏輯。 我們會帶一個快捷方式，讓事情保持簡單。

**清單 1-Controllers\ProductController.vb**

[!code-vb[Main](performing-simple-validation-vb/samples/sample1.vb)]

在 [清單 1] 中，會驗證 Product 類別的名稱、描述和庫存屬性。 如果其中任何一個屬性無法通過驗證測試，則會將錯誤加入至模型狀態字典（以 Controller 類別的 ModelState 屬性工作表示）。

如果模型狀態中有任何錯誤，則 ModelState 屬性會傳回 false。 在此情況下，會重新顯示用於建立新產品的 HTML 表單。 否則，如果沒有驗證錯誤，就會將新的產品新增至資料庫。

## <a name="using-the-validation-helpers"></a>使用驗證協助程式

ASP.NET MVC 架構包含兩個驗證協助程式： ValidationMessage （）協助程式和 ValidationSummary （） helper。 您會在視圖中使用這兩個協助程式來顯示驗證錯誤訊息。

ValidationMessage （）和 ValidationSummary （） helper 會用於 ASP.NET MVC 樣板自動產生的 Create 和 Edit views。 請遵循下列步驟來產生 Create view：

1. 以滑鼠右鍵按一下產品控制器中的 [建立] （）動作，然後選取 [**新增視圖**] 功能表選項（請參閱 [圖 1]）。
2. 在 [**加入視圖**] 對話方塊中，核取標示為 [**建立強型別的視圖**] 的核取方塊（請參閱 [圖 2]）。
3. 從 [ **View data class** ] 下拉式清單中，選取 [Product] 類別。
4. 從 [**視圖內容**] 下拉式清單中，選取 [建立]。
5. 按一下 [新增] 按鈕。

請確定您已建立應用程式，然後再加入視圖。 否則，類別清單將不會出現在 [ **View data class** ] 下拉式清單中。

[![[新增專案] 對話方塊](performing-simple-validation-vb/_static/image1.jpg)](performing-simple-validation-vb/_static/image1.png)

**圖 01**：加入視圖（[按一下以觀看完整大小的影像](performing-simple-validation-vb/_static/image2.png)）

[![[新增專案] 對話方塊](performing-simple-validation-vb/_static/image2.jpg)](performing-simple-validation-vb/_static/image3.png)

**圖 02**：建立強型別視圖（[按一下以觀看完整大小的影像](performing-simple-validation-vb/_static/image4.png)）

完成這些步驟之後，您會在 [清單 2] 中看到 [建立] 視圖。

**清單 2-Views\Product\Create.aspx**

[!code-aspx[Main](performing-simple-validation-vb/samples/sample2.aspx)]

在 [清單 2] 中，Html. ValidationSummary （） helper 會緊接在 HTML 表單的正上方呼叫。 此 helper 用來顯示驗證錯誤訊息的清單。 ValidationSummary （） helper 會以項目符號清單呈現錯誤。

每個 HTML 表單欄位旁都會呼叫 ValidationMessage （） helper。 此 helper 可用來在表單欄位旁顯示錯誤訊息。 在 [清單 2] 的案例中，ValidationMessage （） helper 會在發生錯誤時顯示星號。

[圖 3] 中的頁面說明當提交表單時，驗證協助程式所呈現的錯誤訊息，其中包含遺漏的欄位和不正確值。

[![[新增專案] 對話方塊](performing-simple-validation-vb/_static/image3.jpg)](performing-simple-validation-vb/_static/image5.png)

**圖 03**：以問題提交的建立視圖（[按一下以查看完整大小的影像](performing-simple-validation-vb/_static/image6.png)）

請注意，當發生驗證錯誤時，HTML 輸入欄位的外觀也會一併修改。 當有與 Html. TextBox （） helper 所呈現之屬性相關聯的驗證錯誤時，Html. TextBox （） helper 會轉譯*class = "input--error"* 屬性。

有三個級聯樣式表類別可用來控制驗證錯誤的外觀：

- 輸入-驗證-錯誤-適用于 Html. TextBox （） helper 所轉譯的 &lt;輸入&gt; 標記。
- 欄位驗證-錯誤-套用至 ValidationMessage （） helper 所呈現的 &lt;範圍&gt; 標記。
- 驗證-摘要-錯誤-適用于 ValidationSummary （） helper 所轉譯的 &lt;ul&gt; 標記。

您可以修改這些級聯樣式表類別，藉由修改位於 Content 資料夾中的 .css 檔案，修改驗證錯誤的外觀。

> [!NOTE] 
> 
> HtmlHelper 類別包含唯讀的靜態屬性，可用於抓取驗證相關的 CSS 類別名稱。 這些靜態屬性的名稱為 ValidationInputCssClassName、ValidationFieldCssClassName 和 ValidationSummaryCssClassName。

## <a name="prebinding-validation-and-postbinding-validation"></a>Prebinding 驗證和 Postbinding 驗證

如果您提交用來建立產品的 HTML 表單，而且您在 [價格] 欄位中輸入不正確值，而且沒有 [庫存] 欄位的值，則您會取得如 [圖 4] 所示的驗證訊息。 這些驗證錯誤訊息來自何處？

[![[新增專案] 對話方塊](performing-simple-validation-vb/_static/image4.jpg)](performing-simple-validation-vb/_static/image7.png)

**圖 04**： Prebinding 驗證錯誤（[按一下以查看完整大小的影像](performing-simple-validation-vb/_static/image8.png)）

實際上有兩種類型的驗證錯誤訊息：在 HTML 表單欄位之前所產生的會系結至類別，以及在表單欄位系結至類別之後所產生的訊息。 換句話說，有 prebinding 的驗證錯誤和 postbinding 驗證錯誤。

[清單 1] 中的產品控制器所公開的 Create （）動作會接受 Product 類別的實例。 Create 方法的簽章看起來像這樣：

[!code-vb[Main](performing-simple-validation-vb/samples/sample3.vb)]

[建立] 表單中的 HTML 表單欄位值會透過稱為「模型系結器」的專案系結至 productToCreate 類別。 預設模型系結器會在無法將表單欄位系結至表單內容時，自動將錯誤訊息新增至模型狀態。

預設的模型系結器無法將字串 "apple" 系結至 Product 類別的 Price 屬性。 您無法將字串指派給 decimal 屬性。 因此，模型系結器會將錯誤新增至模型狀態。

預設的模型系結器也不能將值指定為不接受值任何的屬性。 特別的是，模型系結器無法將值指派給「庫存」屬性。 同樣地，模型系結器會啟動並將錯誤訊息加入至模型狀態。

如果您想要自訂這些 prebinding 錯誤訊息的外觀，則需要建立這些訊息的資源字串。

## <a name="summary"></a>總結

本教學課程的目的是要說明 ASP.NET MVC 架構中驗證的基本機制。 您已瞭解如何使用模型狀態和驗證 HTML 協助程式。 我們也討論了 prebinding 和 postbinding 驗證之間的區別。 在其他教學課程中，我們將討論將您的驗證程式代碼移出控制器和模型類別的各種策略。

> [!div class="step-by-step"]
> [上一頁](displaying-a-table-of-database-data-vb.md)
> [下一頁](validating-with-the-idataerrorinfo-interface-vb.md)
