---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-vb
title: 將驗證控制項新增至 DataList 的編輯介面（VB） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將瞭解如何輕鬆地將驗證控制項新增至 DataList 的 EditItemTemplate，以便提供更可靠的編輯使用者 int 。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 6b073fc6-524d-453d-be7c-0c30986de391
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: f952a7bb95e956a2ad935f8bdef5c3efa7437ecb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621866"
---
# <a name="adding-validation-controls-to-the-datalists-editing-interface-vb"></a>將驗證控制項新增至 DataList 的編輯介面 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_39_VB.exe)或[下載 PDF](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/datatutorial39vb1.pdf)

> 在本教學課程中，我們將瞭解如何輕鬆地將驗證控制項新增至 DataList 的 EditItemTemplate，以提供更可靠的編輯使用者介面。

## <a name="introduction"></a>簡介

到目前為止，在 DataList 編輯教學課程中，DataLists 編輯介面尚未包含任何主動式使用者輸入驗證，即使不正確使用者輸入（例如遺失的產品名稱或負價）也會造成例外狀況。 在[先前的教學](handling-bll-and-dal-level-exceptions-vb.md)課程中，我們已檢查如何將例外狀況處理常式代碼加入至 DataList s `UpdateCommand` 事件處理常式，以攔截並妥善顯示任何引發之例外狀況的相關資訊。 不過，在理想的情況下，編輯介面會包含驗證控制項，以防止使用者在一開始就輸入這類不正確資料。

在本教學課程中，我們將瞭解如何輕鬆地將驗證控制項新增至 DataList s `EditItemTemplate`，以便提供更可靠的編輯使用者介面。 具體來說，本教學課程會採用在上一個教學課程中建立的範例，並增強編輯介面以包含適當的驗證。

## <a name="step-1-replicating-the-example-fromhandling-bll--and-dal-level-exceptionshandling-bll-and-dal-level-exceptions-vbmd"></a>步驟1：從[處理 BLL 和 DAL 層級的例外](handling-bll-and-dal-level-exceptions-vb.md)狀況複寫範例

在[處理 BLL 和 DAL 層級的例外](handling-bll-and-dal-level-exceptions-vb.md)狀況教學課程中，我們建立了一個頁面，其中列出了兩個數據行、可編輯 DataList 中產品的名稱和價格。 本教學課程的目標是要增加 DataList 的編輯介面，以包含驗證控制項。 特別是，我們的驗證邏輯將會：

- 需要提供產品的名稱
- 請確定為價格輸入的值是有效的貨幣格式
- 請確定輸入的價格值大於或等於零，因為負值的 `UnitPrice` 值不合法

我們必須先從 [`EditDeleteDataList`] 資料夾中的 [`ErrorHandling.aspx`] 頁面，將範例複製到本教學課程 `UIValidation.aspx`的頁面，然後才能查看如何擴充先前的範例以包含驗證。 為了達到此目的，我們必須同時複製 `ErrorHandling.aspx` 頁面的宣告式標記和其原始程式碼。 請執行下列步驟，先複製宣告式標記：

1. 在 Visual Studio 中開啟 [`ErrorHandling.aspx`] 頁面
2. 移至頁面的宣告式標記（按一下頁面底部的 [來源] 按鈕）
3. 複製 `<asp:Content>` 內的文字，然後 `</asp:Content>` 標記（第3行到32），如 [圖 1] 所示。

[![複製 &lt;asp： Content&gt; 控制項內的文字](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image2.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image1.png)

**圖 2**：複製 `<asp:Content>` 控制項內的文字（[按一下以查看完整大小的影像](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image3.png)）

1. 開啟 [`UIValidation.aspx`] 頁面
2. 移至頁面的宣告式標記
3. 貼上 `<asp:Content>` 控制項內的文字。

若要複製原始碼，請開啟 [`ErrorHandling.aspx.vb`] 頁面，並只複製 `EditDeleteDataList_ErrorHandling` 類別*中*的文字。 將三個事件處理常式（`Products_EditCommand`、`Products_CancelCommand`和 `Products_UpdateCommand`）連同 `DisplayExceptionDetails` 方法**一起複製，但不要複製類別**宣告或 `using` 語句。 將複製的文字貼入 `UIValidation.aspx.vb`的 `EditDeleteDataList_UIValidation`*類別中。*

將內容和程式碼從 `ErrorHandling.aspx` 移至 `UIValidation.aspx`之後，請花點時間在瀏覽器中測試頁面。 您應該會看到相同的輸出，並在這兩個頁面中體驗相同的功能（請參閱 [圖 2]）。

[![UIValidation ErrorHandling 中的功能。](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image5.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image4.png)

**圖 2**： [`UIValidation.aspx`] 頁面會模擬 `ErrorHandling.aspx` 中的功能（[按一下以觀看完整大小的影像](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image6.png)）

## <a name="step-2-adding-the-validation-controls-to-the-datalist-s-edititemtemplate"></a>步驟2：將驗證控制項新增至 DataList s EditItemTemplate

在建立資料輸入表單時，使用者必須輸入任何必要的欄位，而且其提供的所有輸入都是合法的正確格式值。 為了協助確保使用者的輸入有效，ASP.NET 提供五個內建的驗證控制項，其設計目的是要驗證單一輸入 Web 控制項的值：

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx)可確保已提供值
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx)會根據另一個 Web 控制值或常數值來驗證值，或確保值 s 格式對於指定的資料類型是合法的
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx)可確保值在值的範圍內
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx)會根據[正則運算式](http://en.wikipedia.org/wiki/Regular_expression)來驗證值
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx)會根據自訂的使用者定義方法來驗證值

如需這五個控制項的詳細資訊，請參閱將[驗證控制項新增至編輯和插入介面](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)教學課程或查看[ASP.NET 快速入門教學](https://quickstarts.asp.net)課程的[驗證控制項一節](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/validation/default.aspx)。

在本教學課程中，我們必須使用 RequiredFieldValidator 來確保已提供產品名稱的值和 CompareValidator，以確保輸入的價格具有大於或等於0的值，並以有效的貨幣格式呈現。

> [!NOTE]
> 雖然 ASP.NET 1.x 具有這五個相同的驗證控制項，但 ASP.NET 2.0 已新增一些改良功能，主要兩個都是除了 Internet Explorer 之外，也是用戶端腳本支援的瀏覽器，而且能夠將頁面上的驗證控制項分割成驗證群組。 如需2.0 中新驗證控制功能的詳細資訊，請參閱[剖析 the ASP.NET 2.0 中的驗證控制項](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)。

首先，將必要的驗證控制項新增至 DataList s `EditItemTemplate`。 這項工作可以透過設計工具執行，方法是按一下 DataList s 智慧標籤中的 [編輯範本] 連結，或透過宣告式語法。 讓我們使用 設計檢視中的 編輯範本 選項來逐步執行進程。 選擇編輯 DataList s `EditItemTemplate`之後，請將它從 [工具箱] 拖曳到範本編輯介面，然後將它放在 [`ProductName`] 文字方塊後面，以加入 RequiredFieldValidator。

[![在 [ProductName] 文字方塊之後將 RequiredFieldValidator 新增至 EditItemTemplate](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image8.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image7.png)

**圖 3**：將 RequiredFieldValidator 新增至 [`ProductName`] 文字方塊 `EditItemTemplate After` （[按一下以查看完整大小的影像](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image9.png)）

所有驗證控制項都可以藉由驗證單一 ASP.NET Web 控制項的輸入來執行。 因此，我們必須指出剛才新增的 RequiredFieldValidator 應該根據 `ProductName` TextBox 進行驗證;做法是將 [驗證控制] [`ControlToValidate` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx)設定為適當 Web 控制項（在此例中為`ProductName`）的 `ID`。 接下來，將[`ErrorMessage` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx)設定為，您必須將產品的名稱和[`Text` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx)提供給 \*。 如果有提供 `Text` 屬性值，就是驗證控制項在驗證失敗時所顯示的文字。 ValidationSummary 控制項會使用所需的 `ErrorMessage` 屬性值;如果省略 `Text` 屬性值，驗證控制項就會在不正確輸入上顯示 `ErrorMessage` 屬性值。

設定 RequiredFieldValidator 的這三個屬性之後，您的畫面看起來應該像 [圖 4]。

[![設定 RequiredFieldValidator s ControlToValidate、ErrorMessage 和 Text 屬性](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image11.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image10.png)

**圖 4**：設定 RequiredFieldValidator 的 `ControlToValidate`、`ErrorMessage`和 `Text` 屬性（[按一下以查看完整大小的影像](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image12.png)）

將 RequiredFieldValidator 新增至 `EditItemTemplate`之後，剩下的工作就是為 [產品的價格] 文字方塊新增必要的驗證。 因為在編輯記錄時，`UnitPrice` 是選擇性的，所以我們不需要新增 RequiredFieldValidator。 不過，我們需要新增 CompareValidator，以確保 `UnitPrice`（如有提供）會正確地格式化為貨幣且大於或等於0。

將 CompareValidator 新增至 `EditItemTemplate`，並將其 [`ControlToValidate`] 屬性設定為 [`UnitPrice`]，其 [`ErrorMessage`] 屬性必須大於或等於零，而且不能包含貨幣符號和其 [`Text`] 屬性為 [\*]。 若要指出 `UnitPrice` 值必須大於或等於0，請將 CompareValidator s [`Operator` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx)設定為 `GreaterThanEqual`、將其[`ValueToCompare` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx)設為0，並將其[`Type` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx)設定為 `Currency`。

加入這兩個驗證控制項之後，DataList s `EditItemTemplate` 的宣告式語法看起來應該如下所示：

[!code-aspx[Main](adding-validation-controls-to-the-datalist-s-editing-interface-vb/samples/sample1.aspx)]

進行這些變更之後，請在瀏覽器中開啟頁面。 如果您嘗試在編輯產品時省略名稱或輸入不正確價格值，則文字方塊旁會出現星號。 如 [圖 5] 所示，包含貨幣符號（例如 $19.95）的價格值會被視為無效。 CompareValidator s `Currency` `Type` 允許數位分隔符號（例如逗號或句號，視文化特性設定而定）和前置加號或負號，但*不允許貨幣*符號。 這種行為可能會 perplex 使用者，因為編輯介面目前使用貨幣格式呈現 `UnitPrice`。

[![星號會出現在具有無效輸入的文字方塊旁邊](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image14.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image13.png)

**圖 5**：具有無效輸入的文字方塊旁邊會出現星號（[按一下以查看完整大小的影像](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image15.png)）

雖然驗證的運作方式不盡相同，但在編輯記錄時，使用者必須手動移除貨幣符號，這是無法接受的。 此外，如果在編輯介面中有不正確輸入，當您按一下時，[更新] 或 [取消] 按鈕都不會叫用回傳。 在理想的情況下，[取消] 按鈕會將 DataList 傳回其預先編輯狀態，而不論使用者的輸入是否有效。 此外，我們必須先確定頁面的資料有效，再更新 DataList s `UpdateCommand` 事件處理常式中的產品資訊，因為瀏覽器不支援 JavaScript 或停用其支援的使用者可能會略過驗證控制項用戶端邏輯。

## <a name="removing-the-currency-symbol-from-the-edititemtemplate-s-unitprice-textbox"></a>從 [EditItemTemplate] 的 [單價] 文字方塊移除貨幣符號

使用 CompareValidator `Currency``Type`時，所驗證的輸入不能包含任何貨幣符號。 這類符號的存在會導致 CompareValidator 將輸入標記為無效。 不過，我們的編輯介面目前在 [`UnitPrice`] 文字方塊中包含貨幣符號，這表示使用者必須明確地移除貨幣符號，才能儲存其變更。 若要解決這個問題，我們有三個選項：

1. 設定 `EditItemTemplate`，讓 `UnitPrice` TextBox 值不會格式化為貨幣。
2. 允許使用者藉由移除 CompareValidator 並以檢查正確格式貨幣值的 RegularExpressionValidator 取代它，來輸入貨幣符號。 這裡的挑戰在於，驗證貨幣值的正則運算式並不像 CompareValidator，而且如果我們想要納入文化特性設定，就需要撰寫程式碼。
3. 完全移除驗證控制項，並依賴 GridView s `RowUpdating` 事件處理常式中的自訂伺服器端驗證邏輯。

讓我們在本教學課程中使用選項1。 目前 `UnitPrice` 的格式為貨幣值，因為 `EditItemTemplate`中 TextBox 的資料系結運算式： `<%# Eval("UnitPrice", "{0:c}") %>`。 將 `Eval` 語句變更為 `Eval("UnitPrice", "{0:n2}")`，將結果格式化為具有兩位數精確度的數位。 這可以直接透過宣告式語法，或從 DataList s `EditItemTemplate`的 [`UnitPrice`] 文字方塊中，按一下 [編輯系結] 連結來完成。

透過這項變更，編輯介面中的格式化價格包括逗號做為群組分隔符號，並將句點當做小數分隔符號，但會保留貨幣符號。

> [!NOTE]
> 從可編輯的介面中移除貨幣格式時，我發現將貨幣符號放在文字方塊外的文字會很有説明。 這是使用者不需要提供貨幣符號的提示。

## <a name="fixing-the-cancel-button"></a>修正 [取消] 按鈕

根據預設，驗證 Web 控制項會發出 JavaScript，以在用戶端上執行驗證。 按一下按鈕、LinkButton 或 ImageButton 時，會先在用戶端上檢查頁面上的驗證控制項，再進行回傳。 如果有任何不正確資料，就會取消回傳。 不過，對於某些按鈕而言，資料的有效性可能會並不重要;在這種情況下，由於不正確資料而取消回傳是一項干擾。

[取消] 按鈕就是範例。 假設使用者輸入不正確資料（例如，省略產品的名稱），然後決定不想要在全部儲存產品後，再按 [取消] 按鈕。 目前，[取消] 按鈕會觸發頁面上的驗證控制項，這會報告產品名稱遺失，並導致無法回傳。 我們的使用者必須在 [`ProductName`] 文字方塊中輸入一些文字，才能取消編輯進程。

幸運的是，按鈕、LinkButton 和 ImageButton 都有一個[`CausesValidation` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.causesvalidation.aspx)，可指出按一下按鈕是否應起始驗證邏輯（預設為 `True`）。 將 [取消] 按鈕的 `CausesValidation` 屬性設定為 `False`。

## <a name="ensuring-the-inputs-are-valid-in-the-updatecommand-event-handler"></a>確保輸入在 UpdateCommand 事件處理常式中有效

由於驗證控制項發出的用戶端腳本，如果使用者輸入不正確輸入，驗證控制項會取消 `CausesValidation` 屬性 `True` （預設值）的 Button、LinkButton 或 ImageButton 控制項所起始的任何回傳。 不過，如果使用者造訪的是 antiquated 瀏覽器，或已停用其 JavaScript 支援的使用者，則不會執行用戶端驗證檢查。

所有的 ASP.NET 驗證控制項都會在回傳時立即重複其驗證邏輯，並透過[`Page.IsValid` 屬性](https://msdn.microsoft.com/library/system.web.ui.page.isvalid.aspx)報告網頁 s 輸入的整體有效性。 不過，根據 `Page.IsValid`的值，頁面流程不會以任何方式中斷或停止。 身為開發人員，我們負責確保 `Page.IsValid` 屬性具有 `True` 的值，然後再繼續採用採用有效輸入資料的程式碼。

如果使用者已停用 JavaScript，請造訪我們的頁面、編輯產品、輸入太昂貴的價格值，然後按一下 [更新] 按鈕，就會略過用戶端驗證，而且會控制發生回傳。 在回傳時，ASP.NET page s `UpdateCommand` 事件處理常式會執行，而當嘗試剖析的 `Decimal`太昂貴時，就會引發例外狀況。 因為我們有例外狀況處理，所以會正常處理這類例外狀況，但如果 `Page.IsValid` 的值為 `True`，則我們可以防止不正確資料在第一個位置 `UpdateCommand` 繼續進行。

將下列程式碼新增至 `UpdateCommand` 事件處理常式的開頭，緊接在 `Try` 區塊之前：

[!code-vb[Main](adding-validation-controls-to-the-datalist-s-editing-interface-vb/samples/sample2.vb)]

透過這種新增，只有當提交的資料有效時，產品才會嘗試更新。 大部分的使用者因為驗證控制項用戶端腳本而無法回傳不正確資料，但瀏覽器不支援 JavaScript 或已停用 JavaScript 支援的使用者，可以略過用戶端檢查並提交不正確資料。

> [!NOTE]
> 精明讀取器會回想一下，當使用 GridView 更新資料時，我們不需要在頁面的程式碼後置類別中明確檢查 `Page.IsValid` 屬性。 這是因為 GridView 會為我們查閱 `Page.IsValid` 屬性，只有在傳回 `True`的值時，才會繼續進行更新。

## <a name="step-3-summarizing-data-entry-problems"></a>步驟3：摘要資料輸入問題

除了五個驗證控制項以外，ASP.NET 還包含[ValidationSummary 控制項](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx)，它會顯示偵測到無效資料之驗證控制項的 `ErrorMessage`。 此摘要資料可顯示為網頁上的文字，或透過強制回應的用戶端 messagebox。 讓我們增強此教學課程，以包含用戶端 messagebox，以摘要說明任何驗證問題。

若要完成此動作，請將 ValidationSummary 控制項從 [工具箱] 拖曳至設計工具。 ValidationSummary 控制項的位置並不重要，因為我們會將它設定為只將摘要顯示為 messagebox。 加入控制項之後，將其 [ [`ShowSummary`] 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx)設為 [`False`]，並將其[`ShowMessageBox` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx)設定為 [`True`]。 透過這項新增功能，任何驗證錯誤都會在用戶端 messagebox 中匯總（請參閱 [圖 6]）。

[在用戶端 Messagebox 中，會摘要說明驗證錯誤 ![](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image17.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image16.png)

**圖 6**：用戶端 Messagebox 中的驗證錯誤摘要（[按一下以觀看完整大小的影像](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image18.png)）

## <a name="summary"></a>總結

在本教學課程中，我們已瞭解如何使用驗證控制項主動確保使用者輸入有效，然後再嘗試在更新工作流程中使用它們，以降低例外狀況的可能性。 ASP.NET 提供五個驗證 Web 控制項，設計用來檢查特定的 Web 控制項 s 輸入，並回報輸入的有效性。 在本教學課程中，我們使用這五個控制項的其中兩個來控制 RequiredFieldValidator 和 CompareValidator，以確保產品的名稱是已提供，而且價格的貨幣格式值大於或等於零。

將驗證控制項新增至 DataList s 編輯介面就像從 [工具箱] 拖曳至 [`EditItemTemplate`]，然後設定幾個屬性一樣簡單。 根據預設，驗證控制項會自動發出用戶端驗證腳本;它們也會在回傳時提供伺服器端驗證，並將累計結果儲存在 `Page.IsValid` 屬性中。 若要在按下按鈕、LinkButton 或 ImageButton 時略過用戶端驗證，請將按鈕的 `CausesValidation` 屬性設定為 [`False`]。 此外，在使用回傳提交的資料執行任何工作之前，請確定 `Page.IsValid` 屬性會傳回 `True`。

到目前為止，我們已檢查過的所有 DataList 編輯教學課程，都有非常簡單的編輯介面，也就是產品名稱的 TextBox，另一個則是價格。 不過，編輯介面可以混合不同的 Web 控制項，例如 Dropdownlist 進行、行事曆、選項按鈕、核取方塊等等。 在下一個教學課程中，我們將探討如何建立使用各種 Web 控制項的介面。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Dennis Patterson、Ken Pespisa 和 Liz Shulok。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](handling-bll-and-dal-level-exceptions-vb.md)
> [下一頁](customizing-the-datalist-s-editing-interface-vb.md)
