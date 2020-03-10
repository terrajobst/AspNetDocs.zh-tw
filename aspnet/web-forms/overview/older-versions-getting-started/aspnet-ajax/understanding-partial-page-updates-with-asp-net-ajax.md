---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
title: 瞭解使用 ASP.NET AJAX 的部分頁面更新 |Microsoft Docs
author: scottcate
description: ASP.NET AJAX Extensions 最明顯的功能可能是執行部分或累加的頁面更新，而不需執行完整的回傳作業 。
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 54d9df99-1161-4899-b4e8-2679c85915e7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
msc.type: authoredcontent
ms.openlocfilehash: 4b87cb8f58dbd7f27b16bcb0d488ff361770d4fe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78545966"
---
# <a name="understanding-partial-page-updates-with-aspnet-ajax"></a>了解部分頁面更新與 ASP.NET AJAX

由[Scott Cate](https://github.com/scottcate)

[下載 PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial01_Partial_Page_Updates_cs.pdf)

> ASP.NET AJAX 延伸模組最明顯的功能之一，就是能夠執行部分或累加的頁面更新，而不需進行完整的伺服器回傳，而不需要變更程式碼和最少的標記變更。 優點很大–多媒體的狀態（例如 Adobe Flash 或 Windows Media）並未變更，頻寬成本會降低，而且用戶端不會遇到通常與回傳相關聯的閃爍。

## <a name="introduction"></a>簡介

Microsoft 的 ASP.NET 技術引進了物件導向和事件導向的程式設計模型，並將它與已編譯器代碼的優點結合在一起。 不過，它的伺服器端處理模型在技術上有一些固有的缺點：

- 頁面更新需要伺服器的來回行程，這需要重新整理頁面。
- 來回行程不會保存 JAVAscript 或其他用戶端技術（例如 Adobe Flash）所產生的任何效果。
- 在回傳期間，Microsoft Internet Explorer 以外的瀏覽器不支援自動還原捲軸位置。 即使是在 Internet Explorer 中，當頁面重新整理時仍然會有閃爍。
- 回傳可能會涉及大量的頻寬，因為 \_\_VIEWSTATE 表單欄位可能會成長，特別是在處理控制項（例如 GridView 控制項或中繼器）時。
- 沒有透過 JavaScript 或其他用戶端技術來存取 Web 服務的統一模型。

輸入 Microsoft 的 ASP.NET AJAX extensions。 AJAX （代表同步**J** avaScript **a** nd **X** ML）**是一種**整合式架構，可透過跨平臺 JavaScript 提供累加頁面更新，包括組成 microsoft ajax 架構的伺服器端程式碼，以及稱為 microsoft ajax 腳本程式庫的腳本元件。 ASP.NET AJAX extensions 也提供跨平臺的支援，可透過 JavaScript 存取 ASP.NET Web 服務。

本白皮書將探討 ASP.NET AJAX Extensions 的部分頁面更新功能，其中包括 ScriptManager 元件、UpdatePanel 控制項和 UpdateProgress 控制項，並會考慮它們應該或不應成為的案例黑屏.

本白皮書是以 Visual Studio 2008 和 .NET Framework 3.5 的 Beta 2 版本為基礎，它會將 ASP.NET AJAX 延伸模組整合到基類庫（先前為 ASP.NET 2.0 提供的附加元件）。 本白皮書也假設您使用的是 Visual Studio 2008，而不是 Visual Web Developer Express 版;某些參考的專案範本可能無法供 Visual Web Developer Express 使用者使用。

## <a name="partial-page-updates"></a>部分頁面更新

ASP.NET AJAX 延伸模組最明顯的功能之一，就是能夠執行部分或累加的頁面更新，而不需進行完整的伺服器回傳，而不需要變更程式碼和最少的標記變更。 優點很廣泛-多媒體的狀態（例如 Adobe Flash 或 Windows Media）不會變更，頻寬成本會降低，而且用戶端不會遇到通常與回傳相關聯的閃爍。

整合部分頁面轉譯的功能會整合到 ASP.NET 中，並將專案的變更降至最低。

## <a name="walkthrough-integrating-partial-rendering-into-an-existing-project"></a>逐步解說：將部分呈現整合至現有的專案

1. 在 Microsoft Visual Studio 2008 中，前往 [檔案] <em>-&gt; 新</em>的<em>-&gt; 網站</em>，然後從對話方塊中選取 [ASP.NET 網站]，建立新的 ASP.NET 網站專案。 您可以將它命名為任何您喜歡的名稱，而且可以將它安裝到檔案系統或 Internet Information Services （IIS）中。
2. 您會看到具有基本 ASP.NET 標記的空白預設頁面（伺服器端表單和 `@Page` 指示詞）。 卸載名為 `Label1` 的標籤，並將名為 `Button1` 的按鈕放到 form 元素中的頁面上。 您可以將其 text 屬性設定為您喜歡的任何內容。
3. 在設計檢視中，按兩下 `Button1` 以產生程式碼後置事件處理常式。 在此事件處理常式中，將 `Label1.Text` 設定為按一下按鈕！ 。

**清單1：啟用部分呈現之前的 default.aspx 標記**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample1.aspx)]

**清單2： default.aspx.cs 中的後置（已修剪）**

[!code-csharp[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample2.cs)]

1. 按 F5 啟動您的網站。 Visual Studio 會提示您新增 web.config 檔案以啟用調試。請這麼做。 當您按一下按鈕時，請注意頁面會重新整理以變更標籤中的文字，而重新繪製頁面時，會有短暫的閃爍。
2. 關閉瀏覽器視窗之後，請回到 Visual Studio 和 標記 頁面。 在 [Visual Studio 工具箱] 中向下滾動，然後尋找標示為 [AJAX Extensions] 的索引標籤。 （如果您沒有此索引標籤，因為您使用的是舊版 AJAX 或塔延伸模組，請參閱本白皮書稍後的註冊 AJAX Extensions 工具箱專案的逐步解說，或使用可下載的 Windows Installer 安裝目前的版本從網站）。

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image2.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image1.png)

（[按一下以查看完整大小的影像](understanding-partial-page-updates-with-asp-net-ajax/_static/image3.png)）

1. <em>已知問題：</em>如果您將 Visual Studio 2008 安裝到已安裝具有 ASP.NET 2.0 AJAX Extensions 的 Visual Studio 2005 的電腦上，Visual Studio 2008 會匯入 AJAX Extensions 工具箱專案。 您可以藉由檢查元件的工具提示，判斷是否為這種情況：他們應該會說出版本3.5.0.0。 如果它們是2.0.0.0 版，則您已匯入舊的工具箱專案，而且必須使用 Visual Studio 中的 [選擇工具箱專案] 對話方塊，以手動方式將其匯入。 您將無法透過設計工具新增第2版的控制項。

2. 開始 `<asp:Label>` 標記之前，請先建立一個空白字元行，然後按兩下 [工具箱] 中的 UpdatePanel 控制項。 請注意，新的 `@Register` 指示詞會包含在頁面頂端，表示應該使用 `asp:` 前置詞來匯入 System.web. UI 命名空間中的控制項。
3. 將結尾的 `</asp:UpdatePanel>` 標籤拖曳到 Button 元素的尾端，讓元素的格式正確，且已包裝的 Label 和 Button 控制項。
4. 在開啟的 `<asp:UpdatePanel>` 標記之後，開始開啟新的標記。 請注意，IntelliSense 會提示您兩個選項。 在此情況下，請建立 `<ContentTemplate>` 標記。 請務必將此標記包裝在標籤和按鈕的周圍，讓標記的格式正確。

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image5.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image4.png)

（[按一下以查看完整大小的影像](understanding-partial-page-updates-with-asp-net-ajax/_static/image6.png)）

1. 在 `<form>` 專案內的任何位置，按兩下 [工具箱] 中的 [`ScriptManager`] 專案，即可包含 ScriptManager 控制項。
2. 編輯 `<asp:ScriptManager>` 標記，使其包含屬性 `EnablePartialRendering= true`。

**清單3：已啟用部分轉譯之 default.aspx 的標記**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample3.aspx)]

1. 開啟您的 web.config 檔案。 請注意，Visual Studio 已自動將編譯參考加入至 System.web。

1. Visual Studio 2008 的新功能： ASP.NET 網站專案範本隨附的 web.config 會自動包含所有必要的 ASP.NET AJAX 延伸模組參考，並包含設定資訊的批註區段，可以是取消批註以啟用其他功能。 安裝 ASP.NET 2.0 AJAX Extensions 時，Visual Studio 2005 具有類似的範本。 不過，在 Visual Studio 2008 中，AJAX 延伸模組預設是退出宣告的（也就是說，預設會參考它們，但是可以移除做為參考）。

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image8.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image7.png)

（[按一下以查看完整大小的影像](understanding-partial-page-updates-with-asp-net-ajax/_static/image9.png)）

1. 按 F5 以啟動您的網站。 請注意，不需要變更原始程式碼，就能支援僅限部分呈現的標記已變更。

當您啟動網站時，您應該會看到部分轉譯現在已啟用，因為當您按一下按鈕時，將不會有任何閃爍，也不會有頁面捲軸位置的任何變更（此範例不會示範）。 當您按一下按鈕之後，如果您要查看頁面的呈現來源，它會確認實際上有回傳尚未發生-原始標籤文字仍然是來源標記的一部分，而且標籤已透過 JavaScript 變更。

Visual Studio 2008 似乎尚未隨附預先定義的範本，適用于已啟用 AJAX 的 ASP.NET 網站。 不過，如果已安裝 Visual Studio 2005 和 ASP.NET 2.0 AJAX Extensions，這類範本就可以在 Visual Studio 2005 內使用。 因此，設定網站並從啟用 AJAX 的網站範本開始，可能會變得更容易，因為範本應該包含完整設定的 web.config 檔案（支援所有的 ASP.NET AJAX 延伸模組，包括 Web 服務存取權）。和 JSON 序列化-JavaScript 物件標記法），而且預設會在主要 Web Forms 網頁內包含 UpdatePanel 和 ContentTemplate。 使用此預設頁面啟用部分轉譯，就像重新開機本逐步解說的步驟10，以及將控制項放在頁面上一樣簡單。

## <a name="the-scriptmanager-control"></a>ScriptManager 控制項

## <a name="scriptmanager-control-reference"></a>ScriptManager 控制項參考

啟用標記的屬性：

| **屬性名稱** | **類型** | **說明** |
| --- | --- | --- |
| AllowCustomErrors-重新導向 | Bool | 指定是否要使用 web.config 檔案的自訂錯誤區段來處理錯誤。 |
| AsyncPostBackError-訊息 | String | 取得或設定當引發錯誤時，傳送至用戶端的錯誤訊息。 |
| AsyncPostBack-Timeout | Int32 | 取得或設定用戶端應該等待非同步要求完成的預設時間量。 |
| Xsltsettings.enablescript-全球化 | Bool | 取得或設定是否啟用腳本全球化。 |
| Xsltsettings.enablescript-當地語系化 | Bool | 取得或設定是否啟用腳本當地語系化。 |
| ScriptLoadTimeout | Int32 | 決定將腳本載入至用戶端所允許的秒數 |
| ScriptMode | Enum （Auto、Debug、Release、Inherit） | 取得或設定是否要呈現腳本的發行版本 |
| ScriptPath | String | 取得或設定要傳送至用戶端之腳本檔案位置的根路徑。 |

僅限程式碼屬性：

| **屬性名稱** | **類型** | **說明** |
| --- | --- | --- |
| AuthenticationService | AuthenticationService-管理員 | 取得將傳送至用戶端之 ASP.NET Authentication 服務 proxy 的詳細資料。 |
| IsDebuggingEnabled | Bool | 取得是否啟用腳本和程式碼偵錯工具。 |
| IsInAsyncPostback | Bool | 取得頁面目前是否在非同步 post 要求中。 |
| ProfileService | ProfileService-管理員 | 取得將傳送至用戶端之 ASP.NET 分析服務 proxy 的詳細資料。 |
| 指令碼 | 集合&lt;腳本-參考&gt; | 取得將傳送至用戶端之腳本參考的集合。 |
| 服務 | 集合&lt;服務參考&gt; | 取得將傳送至用戶端的 Web 服務 proxy 參考集合。 |
| SupportsPartialRendering | Bool | 取得目前的用戶端是否支援部分呈現。 如果此屬性傳回**false**，則所有頁面要求都會是標準回傳。 |

公用程式代碼方法：

| **方法名稱** | **類型** | **說明** |
| --- | --- | --- |
| SetFocus （字串） | Void | 當要求完成時，將用戶端的焦點設定至特定的控制項。 |

標記子代：

| **Tag** | **說明** |
| --- | --- |
| &lt;AuthenticationService&gt; | 提供有關 proxy 至 ASP.NET authentication 服務的詳細資料。 |
| &lt;ProfileService&gt; | 提供有關 ASP.NET 分析服務之 proxy 的詳細資料。 |
| &lt;指令碼&gt; | 提供其他的腳本參考。 |
| &lt;asp： ScriptReference&gt; | 表示特定的腳本參考。 |
| &lt;Service&gt; | 提供會產生 proxy 類別的其他 Web 服務參考。 |
| &lt;asp： ServiceReference&gt; | 表示特定的 Web 服務參考。 |

ScriptManager 控制項是 ASP.NET AJAX 延伸模組的基本核心。 它可讓您存取腳本程式庫（包括廣泛的用戶端腳本類型系統）、支援部分轉譯，並針對額外的 ASP.NET 服務（例如驗證和分析，以及其他 Web 服務）提供廣泛的支援。 ScriptManager 控制項也提供用戶端腳本的全球化和當地語系化支援。

## <a name="providing-alternative-and-supplemental-scripts"></a>提供替代和補充腳本

雖然 Microsoft ASP.NET 2.0 AJAX 延伸模組在 debug 和 release edition 中包含完整的腳本，做為內嵌在參考元件中的資源，但開發人員可以自由地將 ScriptManager 重新導向至自訂的腳本檔案，並註冊其他必要的腳本。

若要覆寫一般內含腳本（例如支援 WebForms 命名空間和自訂類型系統）的預設系結，您可以註冊 ScriptManager 類別的 `ResolveScriptReference` 事件。 呼叫這個方法時，事件處理常式有機會將路徑變更為有問題的腳本檔案;接著，腳本管理員會將不同或自訂的腳本複本傳送到用戶端。

此外，腳本參考（以 `ScriptReference` 類別表示）可以透過程式設計方式或透過標記來包含。 若要這麼做，請以程式設計方式修改 `ScriptManager.Scripts` 集合，或在 `<Scripts>` 標記下包含 `<asp:ScriptReference>` 標記，這是 ScriptManager 控制項的第一個層級子系。

## <a name="custom-error-handling-for-updatepanels"></a>Updatepanel 的自訂錯誤處理

雖然更新是由 UpdatePanel 控制項所指定的觸發程式來處理，但錯誤處理和自訂錯誤訊息的支援是由頁面的 ScriptManager 控制項實例所處理。 這是藉由將事件（`AsyncPostBackError`）公開至頁面，然後可以提供自訂例外狀況處理邏輯。

藉由使用 AsyncPostBackError 事件，您可以指定 `AsyncPostBackErrorMessage` 屬性，這會在完成回呼時引發警示方塊。

您也可以使用用戶端自訂，而不是使用預設的警示方塊;例如，您可能會想要顯示自訂的 `<div>` 元素，而不是預設的瀏覽器強制回應對話方塊。 在此情況下，您可以在用戶端腳本中處理錯誤：

**清單5：顯示自訂錯誤的用戶端腳本**

[!code-html[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample4.html)]

很簡單地說，上述腳本會向用戶端 AJAX 執行時間註冊回呼，以在非同步要求完成時使用。 然後，它會檢查是否已報告錯誤，如果是，則會處理它的詳細資料，最後向執行時間指出錯誤是在自訂腳本中處理。

## <a name="globalization-and-localization-support"></a>全球化和當地語系化支援

ScriptManager 控制項針對腳本字串和使用者介面元件的當地語系化提供廣泛的支援;不過，該主題不在本白皮書的範圍內。 如需詳細資訊，請參閱技術白皮書： ASP.NET AJAX Extensions 中的全球化支援。

## <a name="the-updatepanel-control"></a>UpdatePanel 控制項

## <a name="updatepanel-control-reference"></a>UpdatePanel 控制項參考

啟用標記的屬性：

| **屬性名稱** | **類型** | **說明** |
| --- | --- | --- |
| ChildrenAsTriggers | bool | 指定子控制項是否會在回傳時自動叫用重新整理。 |
| RenderMode | enum （區塊、內嵌） | 指定內容呈現外觀的方式。 |
| UpdateMode | enum （Always，條件式） | 指定 UpdatePanel 是否一律在部分轉譯期間重新整理，或只在遇到觸發程式時重新整理。 |

僅限程式碼屬性：

| **屬性名稱** | **類型** | **說明** |
| --- | --- | --- |
| IsInPartialRendering | bool | 取得 UpdatePanel 是否支援目前要求的部分呈現。 |
| ContentTemplate | ITemplate | 取得更新要求的標記範本。 |
| ContentTemplateContainer | 控制項 | 取得更新要求的程式設計範本。 |
| 「觸發程序」 | UpdatePanel-TriggerCollection | 取得與目前 UpdatePanel 相關聯之觸發程式的清單。 |

公用程式代碼方法：

| **方法名稱** | **類型** | **說明** |
| --- | --- | --- |
| Update （） | Void | 以程式設計方式更新指定的 UpdatePanel。 允許伺服器要求觸發另一個 untriggered UpdatePanel 的部分呈現。 |

標記子代：

| **Tag** | **說明** |
| --- | --- |
| &lt;ContentTemplate&gt; | 指定要用來呈現部分呈現結果的標記。 &lt;asp： UpdatePanel&gt;的子系。 |
| &lt;觸發程序&gt; | 指定與更新此 UpdatePanel 相關聯的*n*個控制項集合。 &lt;asp： UpdatePanel&gt;的子系。 |
| &lt;asp： AsyncPostBackTrigger&gt; | 指定觸發程式，以叫用指定 UpdatePanel 的部分頁面呈現。 這不一定是控制項，而是有問題的 UpdatePanel 的子項。 細微于事件名稱。&gt;&lt;觸發程式的子系。 |
| &lt;asp： PostBackTrigger&gt; | 指定讓整個頁面重新整理的控制項。 這不一定是控制項，而是有問題的 UpdatePanel 的子項。 對物件的細微程度。 &gt;&lt;觸發程式的子系。 |

`UpdatePanel` 控制項是用來分隔將會納入 AJAX 延伸模組部分呈現功能之伺服器端內容的控制項。 可以在頁面上的 UpdatePanel 控制項數目沒有限制，而且可以加以嵌套。 每個 UpdatePanel 都是獨立的，因此每一個都可以獨立運作（您可以同時執行兩個 Updatepanel，呈現頁面的不同部分，與頁面的回傳無關）。

UpdatePanel 控制項主要處理控制項觸發程式-根據預設，UpdatePanel 的 `ContentTemplate` 中包含的任何控制項（其會建立回傳）都會註冊為 UpdatePanel 的觸發程式。 這表示 UpdatePanel 可以搭配使用預設資料繫結控制項（例如 GridView）和使用者控制項，而且可以用腳本進行程式設計。

根據預設，當觸發部分頁面轉譯時，會重新整理頁面上的所有 UpdatePanel 控制項，不論 UpdatePanel 控制項是否為這類動作所定義的觸發程式。 例如，如果一個 UpdatePanel 定義了按鈕控制項，而且按一下該按鈕控制項，則預設會重新整理該頁面上的所有 UpdatePanel 控制項。 這是因為 UpdatePanel 的 [`UpdateMode`] 屬性預設會設定為 [`Always`]。 或者，您可以將 UpdateMode 屬性設定為 `Conditional`，這表示只有在遇到特定觸發程式時，才會重新整理 UpdatePanel。

## <a name="custom-control-notes"></a>自訂控制項附注

UpdatePanel 可以加入任何使用者控制項或自訂控制項;不過，包含這些控制項的頁面也必須包含 ScriptManager 控制項，其屬性 EnablePartialRendering 設定為**true**。

使用 Web 自訂控制項時，您可能會考慮這種情況的其中一種方式是覆寫 `CompositeControl` 類別的受保護 `CreateChildControls()` 方法。 如此一來，如果您判斷頁面支援部分轉譯，您可以在控制項的子系和外部世界之間插入 UpdatePanel;否則，您可以只將子控制項分層成容器 `Control` 實例。

## <a name="updatepanel-considerations"></a>UpdatePanel 考慮

UpdatePanel 會以黑箱的方式運作，並在 JavaScript XMLHttpRequest 的內容中包裝 ASP.NET 回傳。 不過，在行為和速度方面，有顯著的效能考慮要謹記在心。 若要瞭解 UpdatePanel 的運作方式，讓您能夠在適當的情況下做出最佳決定，您應該檢查 AJAX exchange。 下列範例會使用現有的網站和 Mozilla Firefox 搭配 Firebug 延伸模組（Firebug 會捕捉 XMLHttpRequest 資料）。

另請考慮一個表單，其中包含的郵遞區號文字方塊應該填入表單或控制項上的 city 和 state 欄位。 這個表單最終會收集成員資格資訊，包括使用者的姓名、位址和連絡人資訊。 根據特定專案的需求，有許多設計考慮需要考慮。

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image11.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image10.png)

（[按一下以查看完整大小的影像](understanding-partial-page-updates-with-asp-net-ajax/_static/image12.png)）

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image14.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image13.png)

（[按一下以查看完整大小的影像](understanding-partial-page-updates-with-asp-net-ajax/_static/image15.png)）

在此應用程式的原始反復專案中，已建立一個控制項，其中併入了整個使用者註冊資料，包括郵遞區號、城市和州。 整個控制項已包裝在 UpdatePanel 中，並放在 Web 表單上。 當使用者輸入郵遞區號時，UpdatePanel 會藉由指定觸發程式或使用設定為 true 的 ChildrenAsTriggers 屬性，來偵測事件（後端中對應的 TextChanged 事件）。 AJAX 會在 UpdatePanel 中張貼所有欄位（如 FireBug 所捕捉）（請參閱右側的圖表）。

當螢幕擷取畫面顯示時，會傳遞 UpdatePanel 中每個控制項的值（在此案例中，它們全都是空的），以及 ViewState 欄位。 所有告知的資料9kb 都會傳送，而事實上，只需要五個位元組的資料來提出此特定要求。 回應更膨脹： total，57kb 會傳送至用戶端，只是要更新文字欄位和下拉式欄位。

您也可以瞭解 ASP.NET AJAX 如何更新簡報。 UpdatePanel 更新要求的回應部分會顯示在左側的 Firebug 主控台顯示中;這是特殊撰寫的管道分隔字串，由用戶端腳本分解，然後在頁面上進行重組。 具體而言，ASP.NET AJAX 會在代表您 UpdatePanel 的用戶端上設定 HTML 專案的*innerHTML*屬性。 當瀏覽器重新產生 DOM 時，會有稍微的延遲，視需要處理的資訊量而定。

重新產生 DOM 會觸發一些其他問題：

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image17.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image16.png)

（[按一下以查看完整大小的影像](understanding-partial-page-updates-with-asp-net-ajax/_static/image18.png)）

- 如果焦點在 UpdatePanel 中的 HTML 專案，則會失去焦點。 因此，如果使用者按下 Tab 鍵結束 [郵遞區號] 文字方塊，則下一個目的地就會是 [城市] 文字方塊。 不過，當 UpdatePanel 重新整理顯示之後，表單會不再具有焦點，而按 Tab 鍵會開始反白顯示焦點元素（例如連結）。
- 如果有任何類型的自訂用戶端腳本正在使用中存取 DOM 專案，則在部分回傳之後，函式所保存的參考可能會變成無用。

Updatepanel 不適合用來作為全部 catch 解決方案。 相反地，它們會針對某些情況提供快速的解決方案，包括原型化、小型控制項更新，並提供熟悉的介面，以 ASP.NET 可能熟悉 .NET 物件模型但不適用 DOM 的開發人員。 視應用程式案例而定，有許多替代方案可能會產生較佳的效能：

- 請考慮使用 PageMethods 和 JSON （JavaScript 物件標記法），讓開發人員可以在頁面上叫用靜態方法，就像叫用 web 服務呼叫一樣。 因為方法是靜態的，所以不需要任何狀態。腳本呼叫端會提供參數，並以非同步方式傳回結果。
- 如果單一控制項需要在應用程式的多個位置中使用，請考慮使用 Web 服務和 JSON。 這一次只需要極少的特殊工作，而且以非同步方式運作。

透過 Web 服務或頁面方法整合功能也有缺點。 首先和最重要的是，ASP.NET 開發人員通常會在使用者控制項（.ascx 檔案）中建立小型的功能元件。 頁面方法無法裝載于這些檔案中;它們必須裝載在實際的 .aspx 頁面類別內。 同樣地，Web 服務也必須裝載在 .asmx 類別內。 根據應用程式而定，此架構可能會違反單一責任原則，因為單一元件的功能現在散佈在兩個或多個實體元件中，這可能會有很少或沒有一致的結合。

最後，如果應用程式需要使用 Updatepanel，下列指導方針應該可以協助進行疑難排解和維護。

- **盡可能地嵌套 Updatepanel，而不只是在單元內，也可以跨程式碼單位。** 例如，在包裝控制項的頁面上具有 UpdatePanel，而該控制項也包含 UpdatePanel （其中包含另一個包含 UpdatePanel 的控制項）是跨單位的嵌套。 這有助於清楚瞭解哪些元素應重新整理，並防止未預期的重新整理至子 Updatepanel。
- **將 [ *ChildrenAsTriggers* ] 屬性設定為 [false]，並明確地設定觸發事件。** 利用 `<Triggers>` 集合是處理事件的更清楚方式，而且可能會防止非預期的行為、協助維護工作，以及強制開發人員加入宣告事件。
- **使用最小的可能單位來達到功能。** 如郵遞區號服務的討論中所述，只包裝最少的時間來減少伺服器、總處理，以及用戶端與伺服器交換的使用量，進而提升效能。

## <a name="the-updateprogress-control"></a>UpdateProgress 控制項

## <a name="updateprogress-control-reference"></a>UpdateProgress 控制項參考

啟用標記的屬性：

| **屬性名稱** | **類型** | **說明** |
| --- | --- | --- |
| AssociatedUpdate-PanelID | String | 指定此 UpdateProgress 應該報告的 UpdatePanel 識別碼。 |
| DisplayAfter | Int | 指定在非同步要求開始後顯示此控制項之前的超時（以毫秒為單位）。 |
| DynamicLayout | bool | 指定是否要動態呈現進度。 |

標記子代：

| **Tag** | **說明** |
| --- | --- |
| &lt;ProgressTemplate&gt; | 包含要與此控制項一起顯示之內容集的控制項範本。 |

UpdateProgress 控制項可讓您在執行必要的工作以傳輸到伺服器時，對您的意見進行測量，以保持使用者的關注。 這可協助您的使用者知道您要執行的動作雖然可能不明顯，尤其是因為大部分的使用者都是用來重新整理頁面，並看到狀態列醒目提示。

請注意，UpdateProgress 控制項可以出現在頁面階層上的任何位置。 不過，在從子 UpdatePanel 起始部分回傳的情況下（UpdatePanel 是嵌套在另一個 UpdatePanel 中），觸發子 UpdatePanel 的回傳將會為子系顯示 UpdateProgress 範本UpdatePanel 和父系 UpdatePanel。 但是，如果觸發程式是父 UpdatePanel 的直接子系，則只會顯示與父代相關聯的 UpdateProgress 範本。

## <a name="summary"></a>總結

Microsoft ASP.NET AJAX 延伸模組是一種精密的產品，設計目的是協助讓網頁內容更容易存取，並為您的 web 應用程式提供更豐富的使用者體驗。 做為 ASP.NET AJAX 延伸模組的一部分，部分頁面轉譯控制項（包括 ScriptManager、UpdatePanel 和 UpdateProgress 控制項）是工具組中一些最明顯的元件。

ScriptManager 元件整合了用戶端 JavaScript 的擴充功能，並可讓各種伺服器和用戶端元件搭配最少的開發投資一起運作。

UpdatePanel 控制項是明顯的魔術方塊-UpdatePanel 內的標記可以有伺服器端的程式碼後置，而不會觸發頁面重新整理。 UpdatePanel 控制項可以進行嵌套，而且可以相依于其他 Updatepanel 中的控制項。 根據預設，Updatepanel 會處理其子系控制項所叫用的任何回傳，雖然這項功能可以透過宣告方式或以程式設計方式微調。

使用 UpdatePanel 控制項時，開發人員應該注意可能發生的效能影響。 可能的替代方案包括 web 服務和頁面方法，不過應該考慮應用程式的設計。

UpdateProgress 控制項可讓使用者知道她或他不會被忽略，而且幕後的要求會在頁面不會執行任何動作以回應使用者輸入的情況下繼續進行。 它也包括中止部分呈現結果的功能。

這些工具結合在一起，可讓使用者更容易察覺伺服器的工作，並減少工作流程，以協助建立豐富且順暢的使用者體驗。

## <a name="bio"></a>生物

Scott Cate 自1997起開始使用 Microsoft Web 技術，而這是 myKB.com （[www.myKB.com](http://www.myKB.com)）的總裁，他專門撰寫以 ASP.NET 為基礎的應用程式，著重于知識庫軟體解決方案。 Scott 可以透過電子郵件聯絡，位於[scott.cate@myKB.com](mailto:scott.cate@myKB.com)或他的[ScottCate.com](http://ScottCate.com)的 blog

> [!div class="step-by-step"]
> [下一個](understanding-asp-net-ajax-updatepanel-triggers.md)
