---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: 伺服器控制項 |Microsoft Docs
author: microsoft
description: ASP.NET 2.0 以許多方式增強伺服器控制項。 在此課程模組中，我們將探討 ASP.NET 2.0 和 Visual Studio 200 ... 的一些架構變更。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: c02a633013f061c09141d4f98871848c011a799e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641439"
---
# <a name="server-controls"></a>伺服器控制項

由[Microsoft](https://github.com/microsoft)

> ASP.NET 2.0 以許多方式增強伺服器控制項。 在此課程模組中，我們將探討 ASP.NET 2.0 和 Visual Studio 2005 處理伺服器控制項的方式的一些架構變更。

ASP.NET 2.0 以許多方式增強伺服器控制項。 在此課程模組中，我們將探討 ASP.NET 2.0 和 Visual Studio 2005 處理伺服器控制項的方式的一些架構變更。

## <a name="view-state"></a>檢視狀態

ASP.NET 2.0 中檢視狀態的主要變更，大小大幅縮減。 假設有一個頁面上只有一個行事曆控制項。 以下是 ASP.NET 1.1 中的檢視狀態。

[!code-css[Main](server-controls/samples/sample1.css)]

這現在是 ASP.NET 2.0 中相同頁面的檢視狀態。

[!code-css[Main](server-controls/samples/sample2.css)]

這是相當重要的變更，並考慮到該檢視狀態是透過網路來回執行，這種變更可以讓開發人員大幅提升效能。 減少檢視狀態的大小，主要是因為我們在內部處理它的方式。 請記住，檢視狀態是 Base64 編碼的字串。 為了進一步瞭解 ASP.NET 2.0 中 view 狀態的變更，讓我們先看一下上述範例中的解碼值。

以下是已解碼的 1.1 view 狀態：

[!code-css[Main](server-controls/samples/sample3.css)]

這看起來有點像雜亂的內容，但這裡有一個模式。 在 ASP.NET 1.x 中，我們使用了單一字元來識別資料類型，並使用 &lt;的 &gt; 字元來分隔值。 上述檢視狀態範例中的 "t" 代表三元。 三元包含一對 ArrayLists （"l" 代表 ArrayList）。其中一個 ArrayLists 包含 Int32 （"i"），其值為1，另一個則包含另一個三元。 三元包含一對 ArrayLists 等等。要記住的重點是，我們使用包含配對的 Triplet，我們會透過字母來識別資料類型，而我們會使用 &lt; 並 &gt; 字元做為分隔符號。

在 ASP.NET 2.0 中，解碼的檢視狀態看起來有點不同。

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

您應該會注意到解碼檢視狀態的外觀有很大的變化。 這項變更有數個架構結構性支援。 ASP.NET 1.x 中的 View 狀態使用 LosFormatter 來序列化資料。 在2.0 中，我們使用新的 ObjectStateFormatter 類別。 這個類別是特別設計來協助序列化和還原序列化檢視狀態和控制項狀態。 （下一節將涵蓋控制狀態）。藉由變更序列化和還原序列化進行的方法，可以獲得許多好處。 其中一個最顯著的事實是，不同于使用了不正確 LosFormatter，ObjectStateFormatter 會使用 BinaryWriter。 這可讓 ASP.NET 2.0 儲存檢視狀態一系列的位元組，而不是字串。 例如，取得整數。 在 ASP.NET 1.1 中，整數需要4個位元組的檢視狀態。 在 ASP.NET 2.0 中，相同的整數只需要1個位元組。 已進行其他增強，以減少所儲存的檢視狀態量。 例如，日期時間值現在會使用 TickCount （而非字串）來儲存。

就像這樣的一切都不夠，因為1.x 的其中一個最大取用者是 DataGrid 和類似的控制項，所以會特別注意。 控制項的主要缺點，像是 DataGrid 的檢視狀態，其中通常包含大量重複的資訊。 在 ASP.NET 1.x 中，重複的資訊會一次直接儲存，而導致膨脹檢視狀態。 在 ASP.NET 2.0 中，我們使用新的 IndexedString 類別來儲存這類資料。 如果字串重複，我們只會將 IndexedString 的 token 和索引儲存在 IndexedString 物件的執行中資料表內。

## <a name="control-state"></a>控制項狀態

開發人員具有「視圖」狀態的主要傾聽牢騷之一，就是它加入至 HTTP 承載的大小。 如先前所述，檢視狀態的最大取用者之一就是 DataGrid 控制項。 為了避免 DataGrid 產生大量的檢視狀態，許多開發人員只會停用該控制項的檢視狀態。 可惜的是，該解決方案並不一定是一個好用的。 ASP.NET 1.x 中的 View 狀態不僅包含控制項的正確功能所需的資料。 其中也包含有關控制項 UI 狀態的資訊。 這表示如果您想要允許在 DataGrid 上進行分頁，即使您不需要所有檢視狀態包含的 UI 資訊，還是必須啟用 view 狀態。 這是一種全有或全無的案例。

在 ASP.NET 2.0 中，控制狀態會透過引進控制項狀態來解決此問題。 控制項狀態包含控制項適當功能絕對必要的資料。 不同于 view 狀態，控制項狀態無法停用。 因此，請務必小心地控制儲存在控制狀態中的資料。

> [!NOTE]
> 控制項狀態會隨著檢視狀態保存在 [\_\_VIEWSTATE 隱藏的表單] 欄位中。

這段影片是觀看狀態和控制狀態的逐步解說。

![](server-controls/_static/image1.png)

[開啟全螢幕影片](server-controls/_static/state1.wmv)

為了讓伺服器控制項能夠讀取和寫入控制狀態，您必須執行三個步驟。

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>步驟1：呼叫 RegisterRequiresControlState 方法

RegisterRequiresControlState 方法會通知 ASP.NET 控制項需要保存控制項狀態。 它接受一個 type 控制項的引數，也就是要註冊的控制項。

請務必注意，註冊不會從要求中保存。 因此，如果控制項要保存控制項狀態，就必須在每個要求上呼叫這個方法。 建議您在 OnInit 中呼叫方法。

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>步驟2：覆寫 SaveControlState

SaveControlState 方法會在最後一次回傳後，儲存控制項的控制項狀態變更。 它會傳回代表控制項狀態的物件。

## <a name="step-3-override-loadcontrolstate"></a>步驟3：覆寫 LoadControlState

LoadControlState 方法會將儲存的狀態載入控制項。 方法會接受一個型別物件的引數，以保存控制項的儲存狀態。

## <a name="full-xhtml-compliance"></a>完整的 XHTML 合規性

任何 Web 開發人員都知道 Web 應用程式中標準的重要性。 為了維護以標準為基礎的開發環境，ASP.NET 2.0 完全符合 XHTML 標準。 因此，所有標記都是根據瀏覽器中支援 HTML 4.0 或更高版本的 XHTML 標準來呈現。

ASP.NET 1.1 中的 DOCTYPE 定義如下所示：

[!code-html[Main](server-controls/samples/sample6.html)]

在 ASP.NET 2.0 中，預設的 DOCTYPE 定義如下所示：

[!code-html[Main](server-controls/samples/sample7.html)]

如果您選擇，您可以透過設定檔中的 [xhtmlConformance] 節點來改變預設的 XHTML 合規性。 例如，web.config 檔案中的下列節點會將 XHTML 符合性變更為 XHTML 1.0 Strict：

[!code-xml[Main](server-controls/samples/sample8.xml)]

如果您選擇，您也可以將 ASP.NET 設定成使用 ASP.NET 1.x 中使用的舊版設定，如下所示：

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>使用介面卡的自動調整轉譯

在 ASP.NET 1.x 中，設定檔包含已填入 HttpBrowserCapabilities 物件的 &lt;browserCaps&gt; 區段。 此物件可讓開發人員判斷哪個裝置正在進行特定的要求，並適當地轉譯程式碼。 在 ASP.NET 2.0 中，模型已經過改良，現在使用新的 ControlAdapter 類別。 ControlAdapter 類別會覆寫控制項生命週期中的事件，並根據使用者代理程式的功能來控制控制項的呈現。 特定使用者代理程式的功能是由儲存在 c:\windows\microsoft.net\framework\v2.0. 中的瀏覽器定義檔案（副檔名為. 瀏覽器）所定義\*\*\*\*\CONFIG\Browsers 資料夾。

> [!NOTE]
> ControlAdapter 類別是抽象類別。

瀏覽器定義檔與1.x 中的 &lt;browserCaps&gt; 區段非常類似，它會使用正則運算式來剖析使用者代理字串，以識別要求的瀏覽器。 其會定義該使用者代理程式的特定功能。 ControlAdapter 會透過 Render 方法呈現控制項。 因此，如果您覆寫 Render 方法，則不應該在基類上呼叫 Render。 這麼做可能會導致轉譯出現兩次，一次用於介面卡，一次用於控制項本身。

## <a name="developing-a-custom-adapter"></a>開發自訂介面卡

您可以從 ControlAdapter 繼承，以開發自己的自訂介面卡。 此外，您可以在頁面需要介面卡的情況下，從抽象類別 PageAdapter 繼承。 將控制項對應至自訂介面卡，是透過瀏覽器定義檔中的 &lt;controlAdapters&gt; 元素來完成。 例如，瀏覽器定義檔案中的下列 XML 會將 Menu 控制項對應至 MenuAdapter 類別：

[!code-html[Main](server-controls/samples/sample10.html)]

使用此模型，控制項開發人員就會變得相當容易，以特定裝置或瀏覽器為目標。 開發人員也可以完全掌控每個裝置上頁面的呈現方式，這也相當簡單。

## <a name="per-device-rendering"></a>每一裝置轉譯

ASP.NET 2.0 中的伺服器控制項屬性可以使用瀏覽器特定的前置詞來指定給每一裝置。 例如，下列程式碼將會根據用來流覽頁面的裝置，變更標籤的文字。

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

當包含此標籤的頁面從 Internet Explorer 流覽時，標籤會顯示「您是從 Internet Explorer 流覽」文字。 從 Firefox 流覽頁面時，標籤會顯示「您正從 Firefox 流覽」的文字。 當您從任何其他裝置流覽頁面時，它會顯示「您是從未知的裝置流覽」。 您可以使用這個特殊語法來指定任何屬性。

## <a name="setting-focus"></a>設定焦點

ASP.NET 1.x 開發人員經常會詢問如何設定特定控制項的初始焦點。 例如，在登入頁面上，讓 [使用者識別碼] 文字方塊在頁面第一次載入時取得焦點會很有用。 在 ASP.NET 1.x 中，執行這項作業需要撰寫一些用戶端腳本。 雖然這類腳本是一項簡單的工作，但由於 SetFocus 方法，因此在 ASP.NET 2.0 中已不再需要。 SetFocus 方法會採用一個引數，表示應接收焦點的控制項。 這個引數可以是做為字串的控制項的用戶端識別碼，或是做為控制項物件的伺服器控制項名稱。 例如，若要在第一次載入頁面時將初始焦點設定為 TextBox 控制項，請將下列程式碼新增至頁面\_載入：

[!code-csharp[Main](server-controls/samples/sample12.cs)]

--或

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2.0 使用 Webresource 處理常式（先前討論過）來呈現設定焦點的用戶端函式。 用戶端函式的名稱是 WebForm\_自動對焦，如下所示：

[!code-html[Main](server-controls/samples/sample14.html)]

或者，您可以使用控制項的焦點方法，將初始焦點設定為該控制項。 Focus 方法衍生自控制項類別，並可供所有 ASP.NET 2.0 控制項使用。 當發生驗證錯誤時，也可以將焦點設定至特定的控制項。 這將在稍後的課程模組中討論。

## <a name="new-server-controls-in-aspnet-20"></a>ASP.NET 2.0 中的新伺服器控制項

以下是 ASP.NET 2.0 中的新伺服器控制項。 我們將在稍後的課程模組中深入瞭解其中的部分。

## <a name="imagemap-control"></a>ImageMap 控制項

ImageMap 控制項可讓您將作用區新增至可起始回傳或流覽至 URL 的影像。 有三種可用的熱點類型;[Circlehotspot]、RectangleHotSpot 和 PolygonHotSpot。 在 Visual Studio 中或以程式設計方式，透過程式碼來新增熱點。 沒有任何使用者介面可用來在影像上繪製作用區。 作用點的座標和大小或半徑必須以宣告方式指定。 在設計工具中，熱點也沒有視覺標記法。 如果將作用點設定為流覽至 URL，則會透過作用點的 NavigateUrl 屬性來指定 URL。 在回傳後的熱點案例中，PostBackValue 屬性可讓您傳遞回傳中的字串，以便在伺服器端程式碼中抓取。

![Visual Studio 中的作用點集合編輯器](server-controls/_static/image1.jpg)

**圖 1**： Visual Studio 中的作用點集合編輯器

## <a name="bulletedlist-control"></a>BulletedList 控制項

BulletedList 控制項是可輕鬆地系結資料的項目符號清單。 您可以透過 BulletStyle 屬性來排序（編號）或未排序清單。 清單中的每個專案都是以「內容」物件表示。

![Visual Studio 中的 BulletedList 控制項](server-controls/_static/image1.gif)

**圖 2**： Visual Studio 中的 BulletedList 控制項

## <a name="hiddenfield-control"></a>HiddenField 控制項

HiddenField 控制項會將隱藏的表單欄位加入至您的頁面中，其值可在伺服器端程式碼中使用。 隱藏的表單欄位值通常會在 post 備份之間保持不變。 不過，惡意使用者可能會在回傳之前變更值。 如果發生這種情況，HiddenField 控制項將會引發 ValueChanged 事件。 如果您在 HiddenField 控制項中有敏感性資訊，而且想要確保它保持不變，您應該在程式碼中處理 ValueChanged 事件。

## <a name="fileupload-control"></a>FileUpload 控制項

ASP.NET 2.0 中的 FileUpload 控制項可讓您透過 ASP.NET 網頁，將檔案上傳至 Web 服務器。 此控制項與 ASP.NET 1.x HtmlInputFile 類別非常類似，但有一些例外狀況。 在 ASP.NET 1.x 中，建議您檢查 PostedFile 屬性是否為 null，以便判斷您是否有良好的檔案。 ASP.NET 2.0 中的 FileUpload 控制項加入了新的 HasFile 屬性，可讓您用於相同的目的，而且效率更高。

PostedFile 屬性仍可供存取 HttpPostedFile 物件，但 HttpPostedFile 的某些功能現在已可透過 FileUpload 控制項在本質上使用。 例如，若要在 ASP.NET 1.x 中儲存已上傳的檔案，您可以在 HttpPostedFile 物件上呼叫 SaveAs 方法。 使用 ASP.NET 2.0 中的 FileUpload 控制項，您可以在 FileUpload 控制項本身呼叫 SaveAs 方法。

2\.0 行為的另一項重大變更（而且可能是最重要的變更）是不再需要將整個上傳的檔案載入記憶體中，然後再儲存。 在1.x 中，任何已上傳的檔案都會在寫入磁片之前，完全儲存到記憶體中。 此架構會防止上傳大型檔案。

在 ASP.NET 2.0 中，HTTPRuntime 專案的 requestLengthDiskThreshold 屬性可讓您設定在寫入磁片之前，緩衝區中保留的位元組數。

**重要**事項： MSDN 檔（和其他地方的檔）指定這個值是以位元組為單位（不是 kb），而預設值是256。 這個值實際上是以 Kb 指定，而預設值是80。 藉由將預設值設定為80K，我們可以確保緩衝區不會最後出現在大型物件堆積上。

## <a name="wizard-control"></a>Wizard 控制項

當 ASP.NET 的開發人員嘗試使用面板在一系列的「頁面」中收集資訊，或從頁面傳輸到頁面時，這是相當常見的情況。 這項工作通常會令人沮喪，而且非常耗時。 新的 Wizard 控制項可透過在使用者熟悉的 Wizard 介面中允許線性和非線性步驟來解決問題。 Wizard 控制項會以一系列的步驟呈現輸入表單。 每個步驟都是由控制項的 StepType 屬性所指定的特定類型。 可用的步驟類型如下所示：

| **步驟類型** | **說明** |
| --- | --- |
| Auto | Wizard 會根據步驟階層中的位置自動判斷步驟的類型。 |
| 開始 | 第一個步驟，通常用來呈現簡介語句。 |
| 步驟 | 一般步驟。 |
| 完成 | 最後一個步驟，通常用來顯示按鈕以完成嚮導。 |
| 完成 | 顯示訊息成功或失敗。 |

> [!NOTE]
> Wizard 控制項會使用 ASP.NET 控制項狀態來追蹤其狀態。 因此，EnableViewState 屬性可以設定為 false，而不需要任何弊。

這段影片是 Wizard 控制項的逐步解說。

![](server-controls/_static/image2.png)

[開啟全螢幕影片](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a>當地語系化控制項

[當地語系化] 控制項類似于 [常值] 控制項。 不過，[當地語系化] 控制項具有 [**模式]** 屬性，可控制如何呈現加入至它的標記。 Mode 屬性支援下列值：

| **模式** | **說明** |
| --- | --- |
| 轉換 | 標記會根據提出要求之瀏覽器的通訊協定進行轉換。 |
| Ssh | 標記會以-is 呈現。 |
| 編碼 | 加入至控制項的標記會使用 HtmlEncode 進行編碼。 |

## <a name="multiview-and-view-controls"></a>[查看] 和 [視圖] 控制項

多型多型控制項的作用是 View 控制項的容器，而 View 控制項則是做為其他控制項的容器（與面板控制項非常類似）。 同一個視圖控制項中的每個視圖都是由單一 View 控制項表示。 同位查看中的第一個 View 控制項是 view 0，第二個是 view 1 等等。您可以藉由指定 [檢視器] 控制項的 ActiveViewIndex 來切換 views。

## <a name="substitution-control"></a>替代控制項

替代控制項會與 ASP.NET 快取搭配使用。 在您想要利用快取的情況下，您有部分頁面必須在每個要求上更新（換句話說，非快取的頁面部分），替代元件會提供絕佳的解決方案。 控制項實際上不會自行呈現任何輸出。 相反地，它會系結至伺服器端程式碼中的方法。 當要求頁面時，會呼叫方法，並呈現傳回的標記來取代替代控制項。

替代控制項所系結的方法是透過 [**方法名稱**] 屬性來指定。 該方法必須符合下列準則：

- 它必須是靜態（在 VB 中為 shared）方法。
- 它接受一個類型為 HttpCoNtext 的參數。
- 它會傳回代表標記的字串，該標記應取代頁面上的控制項。

替代控制項無法修改頁面上的任何其他控制項，但它可以透過其參數存取目前的 HttpCoNtext。

## <a name="gridview-control"></a>GridView 控制項

GridView 控制項是 DataGrid 控制項的取代。 在稍後的課程模組中，將會更詳細地討論此控制項。

## <a name="detailsview-control"></a>DetailsView 控制項

DetailsView 控制項可讓您從資料來源顯示單一記錄，並加以編輯或刪除。 稍後的課程模組會更詳細地說明。

## <a name="formview-control"></a>FormView 控制項

FormView 控制項是用來在可設定的介面中顯示資料來源中的單一記錄。 稍後的課程模組會更詳細地說明。

## <a name="accessdatasource-control"></a>AccessDataSource 控制項

AccessDataSource 控制項是用來系結 Access 資料庫的資料。 稍後的課程模組會更詳細地說明。

## <a name="objectdatasource-control"></a>ObjectDataSource 控制項

ObjectDataSource 控制項是用來支援三層式架構，因此控制項可以資料系結至中介層商務物件，而不是直接系結至資料來源的兩層式模型。 稍後的課程模組中將會更詳細地討論。

## <a name="xmldatasource-control"></a>XmlDataSource 控制項

XmlDataSource 控制項是用來將資料系結至 XML 資料來源。 稍後的課程模組會更詳細地說明。

## <a name="sitemapdatasource-control"></a>SiteMapDataSource 控制項

SiteMapDataSource 控制項會根據網站地圖提供網站導覽控制項的資料系結。 稍後的課程模組中將會更詳細地討論。

## <a name="sitemappath-control"></a>SiteMapPath 控制項

SiteMapPath 控制項會顯示一系列的導覽連結，通常稱為「階層連結」。 稍後的課程模組會更詳細地說明。

## <a name="menu-control"></a>功能表控制項

功能表控制項會使用 DHTML 顯示動態功能表。 稍後的課程模組會更詳細地說明。

## <a name="treeview-control"></a>TreeView 控制項

TreeView 控制項是用來顯示資料的階層式樹狀檢視。 稍後的課程模組會更詳細地說明。

## <a name="login-control"></a>Login 控制項

Login 控制項提供登入網站的機制。 稍後的課程模組會更詳細地說明。

## <a name="loginview-control"></a>LoginView 控制項

LoginView 控制項可讓您根據使用者的登入狀態來顯示不同的範本。 稍後的課程模組會更詳細地說明。

## <a name="passwordrecovery-control"></a>PasswordRecovery 控制項

PasswordRecovery 控制項是用來抓取 ASP.NET 應用程式的使用者所遺忘的密碼。 稍後的課程模組會更詳細地說明。

## <a name="loginstatus"></a>LoginStatus

LoginStatus 控制項會顯示使用者的登入狀態。 稍後的課程模組會更詳細地說明。

## <a name="loginname"></a>LoginName

LoginName 控制項會在登入 ASP.NET 應用程式後顯示使用者的使用者名稱。 稍後的課程模組會更詳細地說明。

## <a name="createuserwizard"></a>CreateUserWizard

CreateUserWizard 是可設定的 wizard，讓使用者能夠建立 ASP.NET 成員資格帳戶，以便在 ASP.NET 應用程式中使用。 稍後的課程模組會更詳細地說明。

## <a name="changepassword"></a>ChangePassword

ChangePassword 控制項可讓使用者變更 ASP.NET 應用程式的密碼。 稍後的課程模組會更詳細地說明。

## <a name="various-webparts"></a>各種 Webpart

ASP.NET 2.0 隨附各種 Web 組件。 稍後的課程模組中將會詳細說明這些功能。
