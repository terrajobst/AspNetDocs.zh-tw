---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
title: 使用 IDataErrorInfo 介面（VB）進行驗證 |Microsoft Docs
author: StephenWalther
description: Stephen Walther 將示範如何在模型類別中執行 IDataErrorInfo 介面，以顯示自訂驗證錯誤訊息。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3a8a9d9f-82dd-4959-b7c6-960e9ce95df1
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 8ff3adc5db8114dcca2c66d937e1706f0bac0d30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542501"
---
# <a name="validating-with-the-idataerrorinfo-interface-vb"></a>驗證與 IDataErrorInfo 介面 (VB)

依[Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther 將示範如何在模型類別中執行 IDataErrorInfo 介面，以顯示自訂驗證錯誤訊息。

本教學課程的目的是要說明在 ASP.NET MVC 應用程式中執行驗證的一種方法。 您將瞭解如何防止某人提交 HTML 表單，而不需要為必要的表單欄位提供值。 在本教學課程中，您將瞭解如何使用 IErrorDataInfo 介面來執行驗證。

## <a name="assumptions"></a>假設

在本教學課程中，我將使用 MoviesDB 資料庫和電影資料庫資料表。 這個資料表具有下列資料行：

<a id="0.6_table01"></a>

| **資料行名稱** | **資料類型** | **允許 Null** |
| --- | --- | --- |
| ID | Int | False |
| 標題 | NVarchar （100） | False |
| 導演 | NVarchar （100） | False |
| DateReleased | DateTime | False |

在本教學課程中，我使用 Microsoft Entity Framework 來產生資料庫模型類別。 Entity Framework 所產生的 Movie 類別如 [圖 1] 所示。

[![Movie 實體](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)

**圖 01**： Movie 實體（[按一下以觀看完整大小的影像](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png)）

> [!NOTE] 
> 
> 若要深入瞭解如何使用 Entity Framework 來產生您的資料庫模型類別，請參閱我的教學課程，其標題為使用 Entity Framework 建立模型類別。

## <a name="the-controller-class"></a>控制器類別

我們使用 Home 控制器來列出電影，並建立新的電影。 此類別的程式碼包含在 [清單 1] 中。

**清單 1-Controllers\HomeController.vb**

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample1.vb)]

[清單 1] 中的 Home 控制器類別包含兩個 Create （）動作。 第一個動作會顯示用來建立新電影的 HTML 表單。 第二個 Create （）動作會執行將新電影的實際插入到資料庫中。 當第一個 Create （）動作所顯示的表單提交至伺服器時，會叫用第二個 Create （）動作。

請注意，第二個 Create （）動作包含下列幾行程式碼：

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample2.vb)]

當發生驗證錯誤時，IsValid 屬性會傳回 false。 在此情況下，會重新顯示包含用於建立電影之 HTML 表單的 [建立] 視圖。

## <a name="creating-a-partial-class"></a>建立部分類別

Movie 類別是由 Entity Framework 所產生。 如果您在 [方案總管] 視窗中展開 [MoviesDBModel] 檔案，並在程式碼編輯器中開啟 MoviesDBModel，則可以看到 Movie 類別的程式碼（請參閱 [圖 2]）。

[![Movie 實體的程式碼](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)

**圖 02**： Movie 實體的程式碼（[按一下以觀看完整大小的影像](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png)）

Movie 類別是部分類別。 這表示我們可以加入另一個具有相同名稱的部分類別，以擴充 Movie 類別的功能。 我們會將驗證邏輯新增至新的部分類別。

將 [清單 2] 中的類別新增至 [模型] 資料夾。

**清單 2-Models\Movie.vb**

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample3.vb)]

請注意，[清單 2] 中的類別包含*部分*修飾詞。 您新增至此類別的任何方法或屬性，都會成為 Entity Framework 所產生之 Movie 類別的一部分。

## <a name="adding-onchanging-and-onchanged-partial-methods"></a>新增 OnChanging 和 OnChanged 部分方法

當 Entity Framework 產生實體類別時，Entity Framework 會自動將部分方法新增至類別。 Entity Framework 會產生對應至類別之每個屬性的 OnChanging 和 OnChanged 部分方法。

就 Movie 類別而言，Entity Framework 會建立下列方法：

- OnIdChanging
- OnIdChanged
- OnTitleChanging
- OnTitleChanged
- OnDirectorChanging
- OnDirectorChanged
- OnDateReleasedChanging
- OnDateReleasedChanged

OnChanging 方法會在對應的屬性變更之前呼叫。 OnChanged 方法會在屬性變更之後立即呼叫。

您可以利用這些部分方法，將驗證邏輯新增至 Movie 類別。 [清單 3] 中的 [更新電影] 類別會驗證標題和主管屬性是否指派為非空白值。

> [!NOTE] 
> 
> 部分方法是在類別中定義的方法，而您不需要執行此方法。 如果您未執行部分方法，則編譯器會移除方法簽章和所有對方法的呼叫，因此不會有與部分方法相關聯的執行時間成本。 在 Visual Studio Code 編輯器中，您可以藉由輸入關鍵字*partial*後面加上空格來新增部分方法，以查看要執行的部分清單。

**清單 3-Models\Movie.vb**

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample4.vb)]

例如，如果您嘗試將空字串指派給 Title 屬性，則會將錯誤訊息指派給名為 \_錯誤的字典。

此時，當您將空字串指派給 Title 屬性，而將錯誤加入 [私用 \_錯誤] 欄位時，實際上不會發生任何事。 我們需要執行 IDataErrorInfo 介面，將這些驗證錯誤公開給 ASP.NET MVC 架構。

## <a name="implementing-the-idataerrorinfo-interface"></a>執行 IDataErrorInfo 介面

從第一個版本開始，IDataErrorInfo 介面是 .NET framework 的一部分。 這個介面是非常簡單的介面：

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample5.vb)]

如果類別會實 IDataErrorInfo 介面，則 ASP.NET MVC 架構會在建立類別的實例時使用此介面。 例如，「主控制器建立」（）動作會接受 Movie 類別的實例：

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample6.vb)]

ASP.NET MVC 架構會使用模型系結器（DefaultModelBinder），建立傳遞至 Create （）動作的電影實例。 「模型系結器」負責建立 Movie 物件的實例，方法是將 HTML 表單欄位系結至 Movie 物件的實例。

DefaultModelBinder 會偵測類別是否會實作為 IDataErrorInfo 介面。 如果類別會實作為此介面，則模型系結器會叫用 IDataErrorInfo。此為類別的每個屬性。 如果索引子傳回錯誤訊息，則模型系結器會自動將此錯誤訊息新增至模型狀態。

DefaultModelBinder 也會檢查 IDataErrorInfo 屬性。 這個屬性主要是用來表示與類別相關聯的非屬性特定驗證錯誤。 例如，您可能會想要強制執行取決於 Movie 類別的多個屬性值的驗證規則。 在這種情況下，您會從 Error 屬性傳回驗證錯誤。

清單4中已更新的 Movie 類別會執行 IDataErrorInfo 介面。

**清單 4-Models\Movie.vb （實 IDataErrorInfo）**

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample7.vb)]

在 [清單 4] 中，索引子屬性會檢查 \_錯誤集合，以查看它是否包含對應至傳遞至索引子之屬性名稱的索引鍵。 如果沒有與屬性相關聯的驗證錯誤，則會傳回空字串。

您不需要以任何方式修改 Home 控制器，即可使用修改過的 Movie 類別。 [圖 3] 中所顯示的頁面說明在沒有輸入標題或導演表單欄位的值時，會發生什麼事。

[![自動建立動作方法](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)

**圖 03**：含有遺漏值的表單（[按一下以查看完整大小的影像](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png)）

請注意，系統會自動驗證 DateReleased 值。 因為 DateReleased 屬性不接受 Null 值，所以當這個屬性沒有值時，DefaultModelBinder 會自動產生驗證錯誤。 如果您想要修改 DateReleased 屬性的錯誤訊息，則需要建立自訂模型系結器。

## <a name="summary"></a>總結

在本教學課程中，您已瞭解如何使用 IDataErrorInfo 介面來產生驗證錯誤訊息。 首先，我們建立了部分 Movie 類別，以擴充 Entity Framework 所產生之部分 Movie 類別的功能。 接下來，我們已將驗證邏輯新增至 Movie 類別 OnTitleChanging （）和 OnDirectorChanging （）部分方法。 最後，我們會實 IDataErrorInfo 介面，以便將這些驗證訊息公開給 ASP.NET MVC 架構。

> [!div class="step-by-step"]
> [上一頁](performing-simple-validation-vb.md)
> [下一頁](validating-with-a-service-layer-vb.md)
