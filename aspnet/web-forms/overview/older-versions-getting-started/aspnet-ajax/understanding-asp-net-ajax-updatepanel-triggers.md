---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
title: 瞭解 ASP.NET AJAX UpdatePanel 觸發程式 |Microsoft Docs
author: scottcate
description: 在 Visual Studio 的標記編輯器中工作時，您可能會注意到（從 IntelliSense） UpdatePanel 控制項有兩個子項目。 其中一個 wh 。
ms.author: riande
ms.date: 03/12/2008
ms.assetid: faab8503-2984-48a9-8a40-7728461abc50
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
msc.type: authoredcontent
ms.openlocfilehash: b1cc869f373d4f8283b4d92af74707c3f11fef61
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74588782"
---
# <a name="understanding-aspnet-ajax-updatepanel-triggers"></a>了解 ASP.NET AJAX UpdatePanel 觸發程序

由[Scott Cate](https://github.com/scottcate)

[下載 PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial02_Triggers_cs.pdf)

> 在 Visual Studio 的標記編輯器中工作時，您可能會注意到（從 IntelliSense） UpdatePanel 控制項有兩個子項目。 其中一個是 Trigger 元素，它會指定頁面上的控制項（如果您使用的是使用者控制項，則會觸發專案所在的 UpdatePanel 控制項部分呈現）。

## <a name="introduction"></a>簡介

Microsoft 的 ASP.NET 技術引進了物件導向和事件導向的程式設計模型，並將它與已編譯器代碼的優點結合在一起。 不過，其伺服器端處理模型在技術上有一些缺點，其中有許多都可以由 Microsoft ASP.NET 3.5 AJAX 延伸模組中包含的新功能來解決。 這些延伸模組可啟用許多新的豐富用戶端功能，包括部分呈現頁面，而不需要完整的頁面重新整理、透過用戶端腳本存取 Web 服務的能力（包括 ASP.NET 分析 API），以及廣泛的用戶端 API設計來鏡像 ASP.NET 伺服器端控制項集中所見的許多控制項配置。

本白皮書將探討 ASP.NET AJAX `UpdatePanel` 元件的 XML 觸發程式功能。 XML 觸發程式可讓您更精確地控制可能會對特定 UpdatePanel 控制項造成部分呈現的元件。

本白皮書是以 .NET Framework 3.5 和 Visual Studio 2008 的 Beta 2 版為基礎。 ASP.NET AJAX 延伸模組先前以 ASP.NET 2.0 為目標的附加元件，現在已整合到 .NET Framework 的基類庫。 本白皮書也假設您將使用 Visual Studio 2008，而不是 Visual Web Developer Express，而且將會根據 Visual Studio 的使用者介面提供逐步解說（雖然程式代碼清單完全相容，而不論開發環境）。

## <a name="triggers"></a>*觸發程序*

給定 UpdatePanel 的觸發程式預設會自動包含任何叫用回傳的子控制項，包括（例如）將其 `AutoPostBack` 屬性設為**true**的 TextBox 控制項。 不過，也可以使用標記以宣告方式包含觸發程式;這會在 UpdatePanel 控制項宣告的 `<triggers>` 區段中完成。 雖然可以透過 `Triggers` 集合屬性來存取觸發程式，但建議您在執行時間註冊任何部分呈現觸發程式（例如，如果在設計階段無法使用控制項），方法是在 `Page_Load` 事件內使用網頁的 ScriptManager 物件的 `RegisterAsyncPostBackControl(Control)` 方法。 請記住，頁面是無狀態的，因此您應該在每次建立這些控制項時重新註冊。

自動子觸發套裝程式含也可以停用（如此一來，建立回傳的子控制項不會自動觸發部分轉譯），方法是將 `ChildrenAsTriggers` 屬性設定為**false**。 這可讓您在指派哪些特定控制項可能會叫用頁面轉譯時擁有最大的彈性，並建議讓開發人員加入宣告來回應事件，而不是處理任何可能發生的事件。

請注意，當 UpdatePanel 控制項是 nested 時，當 UpdateMode 設定為**條件**式時，如果子 UpdatePanel 已觸發，但父系不是，則只有子 updatepanel 會重新整理。 不過，如果父 UpdatePanel 重新整理，則子系 UpdatePanel 也會一併更新。

## <a name="the-lttriggersgt-element"></a>*&lt;觸發&gt; 元素*

在 Visual Studio 的標記編輯器中工作時，您可能會注意到（從 IntelliSense） `UpdatePanel` 控制項有兩個子項目。 最常見的元素是 `<ContentTemplate>` 元素，基本上會封裝更新面板所持有的內容（我們要啟用部分呈現的內容）。 另一個元素是 `<Triggers>` 專案，它會指定頁面上的控制項（如果您使用的是使用者控制項，則會觸發&gt; 元素所在 &lt;的 UpdatePanel 控制項的部分轉譯）。

`<Triggers>` 元素可以包含兩個子節點的任何數位： `<asp:AsyncPostBackTrigger>` 和 `<asp:PostBackTrigger>`。 兩者都接受兩個屬性，`ControlID` 和 `EventName`，而且可以在封裝的目前單位中指定任何控制項（例如，如果您的 UpdatePanel 控制項位於 Web 使用者控制項內，則不應該嘗試參考使用者控制項所在頁面上的控制項）。

`<asp:AsyncPostBackTrigger>` 專案特別有用，因為它可以將來自控制項的任何事件當做封裝單位中*任何*updatepanel 控制項的子系，而不只是以此觸發程式為子系的 updatepanel 為目標。 因此，可以建立任何控制項來觸發部分頁面更新。

同樣地，`<asp:PostBackTrigger>` 元素可以用來觸發部分頁面轉譯，但需要對伺服器進行完整往返。 當控制項原本就會觸發部分頁面轉譯（例如，在 UpdatePanel 控制項的 `<ContentTemplate>` 元素中存在 `Button` 控制項）時，這個觸發程式專案也可以用來強制進行完整的頁面呈現。 同樣地，PostBackTrigger 元素可以在目前的封裝單位中，指定任何 UpdatePanel 控制項的子系的控制項。

## <a name="lttriggersgt-element-reference"></a>*&lt;觸發程式&gt; 元素參考*

*標記子代：*

| **標記** | **說明** |
| --- | --- |
| &lt;asp： AsyncPostBackTrigger&gt; | 指定將會對包含此觸發程式參考的 UpdatePanel 引發部分頁面更新的控制項和事件。 |
| &lt;asp： PostBackTrigger&gt; | 指定會導致完整頁面更新（完整頁面重新整理）的控制項和事件。 當控制項會觸發部分呈現時，可以使用此標記來強制執行完整重新整理。 |

## <a name="walkthrough-cross-updatepanel-triggers"></a>*逐步解說：交叉 UpdatePanel 觸發程式*

1. 建立具有 ScriptManager 物件集的新 ASP.NET 網頁，以啟用部分呈現。 將兩個 Updatepanel 加入此頁面-在第一個中，包含標籤控制項（Label1）和兩個按鈕控制項（Button1 和 Button2）。 Button1 應該會說 [按一下以更新] 和 [Button2] 應該會顯示 [按一下以更新此專案]，或在這些行的某個專案上 在第二個 UpdatePanel 中，只包含標籤控制項（Label2），但將其前景屬性設定為預設值以外的專案，以區別它。
2. 將兩個 UpdatePanel 標記的 UpdateMode 屬性設定為 [**條件**式]。

**清單1： default.aspx 的標記：** 

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample1.aspx)]

1. 在 Button1 的 Click 事件處理常式中，將 Label1. Text 和 Label2 設定為與時間相關的內容（例如 DateTime. Now. ToLongTimeString （））。 針對 Button2 的 Click 事件處理常式，將 [Label1] 設定為 [與時間相關的值]。

**清單2： default.aspx.cs 中的後置（已修剪）：** 

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample2.cs)]

1. 按 F5 以建立並執行專案。 請注意，當您按一下 [更新兩個面板] 時，這兩個標籤都會變更文字;不過，當您按一下 [更新此面板] 時，只會更新 Label1。

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image2.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image1.png)

（[按一下以查看完整大小的影像](understanding-asp-net-ajax-updatepanel-triggers/_static/image3.png)）

## <a name="under-the-hood"></a>*深入探討*

利用我們剛剛建造的範例，我們可以查看 ASP.NET AJAX 的功能，以及我們的 UpdatePanel 跨面板觸發程式的工作。 若要這麼做，我們將使用所產生的頁面來源 HTML，以及稱為 FireBug 的 Mozilla Firefox 延伸模組，我們可以輕鬆地檢查 AJAX 回傳。 我們也會藉由 Lutz Roeder 來使用 .NET 反映工具。 這兩種工具都可以在線上免費使用，並可透過網際網路搜尋找到。

頁面原始碼的檢查幾乎不會顯示一般的內容;UpdatePanel 控制項會轉譯為 `<div>` 容器，我們可以看到 `<asp:ScriptManager>`提供的腳本資源。 對於 AJAX 用戶端腳本程式庫內部的 PageRequestManager，還有一些新的 AJAX 特定呼叫。 最後，我們會看到兩個 UpdatePanel 容器，一個具有轉譯的 `<input>` 按鈕，並將兩個 `<asp:Label>` 控制項轉譯為 `<span>` 容器。 （如果您檢查 FireBug 中的 DOM 樹狀結構，您會注意到標籤呈暗灰色，表示它們不會產生可見內容）。

按一下 [更新此面板] 按鈕，並注意頂端的 UpdatePanel 會以目前的伺服器時間更新。 在 FireBug 中，選擇 [主控台] 索引標籤，讓您可以檢查要求。 先檢查 POST 要求參數：

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image5.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image4.png)

（[按一下以查看完整大小的影像](understanding-asp-net-ajax-updatepanel-triggers/_static/image6.png)）

請注意，UpdatePanel 已透過 ScriptManager1 參數，精確地指示伺服器端 AJAX 程式碼所引發的控制項樹狀結構： `UpdatePanel1` 控制項的 `Button1`。 現在，按一下 [更新兩個面板] 按鈕。 然後，檢查回應，我們會在字串中看到以管線分隔的變數系列;具體來說，我們看到的是最熱門的 UpdatePanel （`UpdatePanel1`），其 HTML 已傳送到瀏覽器的全部。 AJAX 用戶端腳本程式庫會透過 `.innerHTML` 屬性，以新的內容取代 UpdatePanel 的原始 HTML 內容，因此伺服器會將已變更的內容從伺服器當做 HTML 傳送。

現在，按一下 [更新兩個面板] 按鈕，然後檢查伺服器的結果。 結果非常類似-這兩個 Updatepanel 都會從伺服器接收新的 HTML。 如同先前的回呼，會傳送額外的頁面狀態。

如我們所見，由於未使用任何特殊程式碼來執行 AJAX 回傳，因此 AJAX 用戶端腳本程式庫可以攔截表單回傳，而不需要任何額外的程式碼。 伺服器控制項會自動使用 JavaScript，使其不會自動提交表單-ASP.NET 會自動插入表單驗證和狀態的程式碼，主要是透過自動腳本資源包含（PostBackOptions 類別）來達成。和 ClientScriptManager 類別。

例如，請考慮使用 CheckBox 控制項。檢查 .NET 反映中的類別反組解碼。 若要這麼做，請確定您的 System.web 元件已開啟，並流覽至 `System.Web.UI.WebControls.CheckBox` 類別，並開啟 `RenderInputTag` 方法。 尋找檢查 `AutoPostBack` 屬性的條件：

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image8.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image7.png)

（[按一下以查看完整大小的影像](understanding-asp-net-ajax-updatepanel-triggers/_static/image9.png)）

當 `CheckBox` 控制項上啟用自動回傳時（透過 AutoPostBack 屬性為 true），會因此產生的 `<input>` 標記會以其 `onclick` 屬性中的 ASP.NET 事件處理腳本呈現。 接著，攔截表單的提交，就能讓 ASP.NET AJAX 插入頁面 nonintrusively 中，藉由利用可能不精確的字串取代，協助避免任何可能發生的重大變更。 此外，這可讓*任何*自訂的 ASP.NET 控制項利用 ASP.NET AJAX 的強大功能，而不需要任何額外的程式碼來支援在 UpdatePanel 容器中使用。

`<triggers>` 功能會對應至 \_updateControls 的 PageRequestManager 呼叫中所初始化的值（請注意，ASP.NET AJAX 用戶端腳本程式庫會利用以底線開頭的方法、事件和功能變數名稱標示為內部的慣例，而不是用於程式庫本身以外的地方）。 有了它，我們就可以觀察哪些控制項要造成 AJAX 回傳。

例如，讓我們將兩個額外的控制項加入至頁面，將一個控制項完全放在 Updatepanel 外部，並在 UpdatePanel 中保留一個。 我們會在上方的 UpdatePanel 中新增 CheckBox 控制項，並使用清單中定義的多個色彩來卸載 DropDownList。 以下是新的標記：

**清單3：新標記**

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample3.aspx)]

以下是新的程式碼後置：

**清單4：代碼後置**

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample4.cs)]

此頁面背後的構想是，下拉式清單會選取三種色彩的其中一種來顯示第二個標籤，核取方塊會決定是否為粗體，以及標籤是否顯示日期和時間。 此核取方塊不應造成 AJAX 更新，但下拉式清單應為，即使它不是存放在 UpdatePanel 內也一樣。

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image11.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image10.png)

（[按一下以查看完整大小的影像](understanding-asp-net-ajax-updatepanel-triggers/_static/image12.png)）

如上述螢幕擷取畫面所示，按一下 [最新的] 按鈕就會更新此面板，而這會更新與下一時間無關的前幾個時間。 日期也會在按一下時切換，因為日期會顯示在底部標籤中。 最後，重點是底部標籤的色彩：其更新時間比標籤的文字還新，這會示範控制項狀態很重要，而且使用者預期會透過 AJAX 回傳加以保留。 *不過*，時間並未更新。 當控制項在伺服器上重新呈現時，會透過 ASP.NET 執行時間所轉譯之頁面的 [\_\_VIEWSTATE] 欄位的持續性，自動重新擴展時間。 ASP.NET AJAX 伺服器程式碼無法辨識控制項變更狀態的方法;它只會從 view 狀態重新填入，然後執行適當的事件。

但是應該指出，我已初始化頁面中的時間\_載入事件，時間已正確增加。 因此，開發人員應該要小心在適當的事件處理常式期間執行適當的程式碼，並避免在適當的控制項事件處理常式時使用頁面\_載入。

## <a name="summary"></a>總結

ASP.NET AJAX Extensions UpdatePanel 控制項很多功能，而且可以利用多種方法來識別應使其更新的控制項事件。 它支援由其子控制項自動更新，但也可以回應頁面上其他位置的控制項事件。

若要減少伺服器處理負載的可能，建議將 UpdatePanel 的 `ChildrenAsTriggers` 屬性設定為 `false`，並加入宣告而不是預設包含的事件。 這也可避免任何不必要的事件造成潛在不必要的效果，包括驗證和輸入欄位的變更。 這些類型的錯誤可能很難隔離，因為網頁會以透明的方式更新給使用者，因此可能不會立即察覺原因。

藉由檢查 ASP.NET AJAX 表單後攔截模型的內部運作方式，我們可以判斷它是否利用了 ASP.NET 所提供的架構。 在這麼做的情況下，它會保留與使用相同架構設計之控制項的最大相容性，並在針對該頁面撰寫的任何額外 JavaScript 上行程干擾最低。

## <a name="bio"></a>生物

Paveza 是 Terralever （[www.terralever.com](http://www.terralever.com)）的資深 .net 應用程式開發人員，這是 TEMPE，AZ 中的領先互動行銷公司。 他可以在[robpaveza@gmail.com](mailto:robpaveza@gmail.com)觸達，而他的 blog 則位於[http://geekswithblogs.net/robp/](http://geekswithblogs.net/robp/)。

Scott Cate 自1997起開始使用 Microsoft Web 技術，而這是 myKB.com （[www.myKB.com](http://www.myKB.com)）的總裁，他專門撰寫以 ASP.NET 為基礎的應用程式，著重于知識庫軟體解決方案。 Scott 可以透過電子郵件聯絡，位於[scott.cate@myKB.com](mailto:scott.cate@myKB.com)或他的[ScottCate.com](http://ScottCate.com)的 blog

> [!div class="step-by-step"]
> [上一頁](understanding-partial-page-updates-with-asp-net-ajax.md)
> [下一頁](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
