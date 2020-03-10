---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 頁面模型 |Microsoft Docs
author: microsoft
description: 在 ASP.NET 1.x 中，開發人員可選擇內嵌程式碼模型和程式碼後置程式碼模型。 程式碼後置可以使用 Src attr 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: bcb71b2b5a484e8756406867e08e8aa699a9024d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547646"
---
# <a name="the-aspnet-20-page-model"></a>ASP.NET 2.0 頁面模型

由[Microsoft](https://github.com/microsoft)

> 在 ASP.NET 1.x 中，開發人員可選擇內嵌程式碼模型和程式碼後置程式碼模型。 程式碼後置可以使用 Src 屬性或 @Page 指示詞的程式碼後置屬性來執行。 在 ASP.NET 2.0 中，開發人員仍然可以選擇內嵌程式碼和程式碼後置，但已大幅增強程式碼後置模型。

在 ASP.NET 1.x 中，開發人員可選擇內嵌程式碼模型和程式碼後置程式碼模型。 程式碼後置可以使用 Src 屬性或 @Page 指示詞的程式碼後置屬性來執行。 在 ASP.NET 2.0 中，開發人員仍然可以選擇內嵌程式碼和程式碼後置，但已大幅增強程式碼後置模型。

## <a name="improvements-in-the-code-behind-model"></a>程式碼後置模型中的改良功能

若要完全瞭解 ASP.NET 2.0 中程式碼後置模型的變更，最好能夠快速地查看 ASP.NET 1.x 中存在的模型。

## <a name="the-code-behind-model-in-aspnet-1x"></a>ASP.NET 1.x 中的程式碼後置模型

在 ASP.NET 1.x 中，程式碼後置模型是由一個 ASPX 檔案（Webform）和一個包含程式碼的程式碼後置檔案所組成。 這兩個檔案是使用 ASPX 檔案中的 @Page 指示詞進行連接。 ASPX 頁面上的每個控制項在程式碼後置檔案中都具有對應的宣告，做為執行個體變數。 程式碼後置檔案也包含事件系結的程式碼，以及 Visual Studio 設計工具所需的產生程式碼。 此模型的運作良好，但因為 ASPX 頁面中的每個 ASP.NET 元素都需要程式碼後置檔案中的對應程式碼，所以不會真正區分程式碼和內容。 例如，如果設計工具已將新的伺服器控制項加入至 Visual Studio IDE 外部的 ASPX 檔案，應用程式將會因為不存在程式碼後置檔案中該控制項的宣告而中斷。

## <a name="the-code-behind-model-in-aspnet-20"></a>ASP.NET 2.0 中的程式碼後置模型

ASP.NET 2.0 在此模型上有大幅改善。 在 ASP.NET 2.0 中，程式碼後置會使用 ASP.NET 2.0 中提供的新*部分類別*來執行。 ASP.NET 2.0 中的程式碼後置類別定義為部分類別，這表示它只包含類別定義的一部分。 類別定義的其餘部分是由 ASP.NET 2.0 在執行時間以動態方式產生，或在網站先行編譯時使用。 程式碼後置檔案與 ASPX 頁面之間的連結，仍然是使用 @ Page 指示詞來建立的。 不過，ASP.NET 2.0 現在會使用 CodeFile 屬性，而不是「後置」或 Src 屬性。 Inherits 屬性也用來指定頁面的類別名稱。

一般的 @ Page 指示詞可能如下所示：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

ASP.NET 2.0 程式碼後置檔案中的一般類別定義看起來可能像這樣：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> C#和 Visual Basic 是目前唯一支援部分類別的 managed 語言。 因此，使用 j # 的開發人員將無法使用 ASP.NET 2.0 中的程式碼後置模型。

新模型會增強程式碼後置模型，因為開發人員現在會擁有只包含其所建立之程式碼的程式碼檔案。 它也提供程式碼和內容的真正分離，因為程式碼後置檔案中沒有任何執行個體變數宣告。

> [!NOTE]
> 因為 ASPX 頁面的部分類別是事件系結髮生的地方，Visual Basic 開發人員可以使用程式碼後置中的 Handles 關鍵字來系結事件，以實現些許的效能提升。 C#沒有對等的關鍵字。

## <a name="new--page-directive-attributes"></a>新的 @ Page 指示詞屬性

ASP.NET 2.0 將許多新的屬性加入 @ Page 指示詞。 下列是 ASP.NET 2.0 中新增的屬性。

## <a name="async"></a>非同步處理

Async 屬性可讓您將頁面設定為以非同步方式執行。 我們將在此課程模組稍後討論非同步頁面。

## <a name="asynctimeout"></a>AsyncTimeout

已指定非同步頁面的超時時間。 預設值為45秒。

## <a name="codefile"></a>CodeFile

CodeFile 屬性是取代 Visual Studio 2002/2003 中的程式碼後置屬性。

### <a name="codefilebaseclass"></a>CodeFileBaseClass

當您想要從單一基類衍生多個頁面時，會使用 CodeFileBaseClass 屬性。 由於 ASP.NET 中部分類別的執行，若沒有此屬性，使用共用通用欄位來參考 ASPX 頁面中宣告之控制項的基類將無法正常運作，因為 ASP. 神經網路編譯引擎會根據頁面中的控制項自動建立新成員。 因此，如果您想要在 ASP.NET 中有兩個或多個頁面的通用基類，就必須在 CodeFileBaseClass 屬性中定義指定基類，然後從該基類衍生每個頁面類別。 使用此屬性時，也需要 CodeFile 屬性。

## <a name="compilationmode"></a>CompilationMode

這個屬性可讓您設定 ASPX 頁面的 CompilationMode 屬性。 CompilationMode 屬性是包含**Always**、 **Auto**和**Never**值的列舉。 預設值**一律**為。 **自動**設定會防止 ASP.NET 在可能的情況下動態編譯頁面。 排除動態編譯中的頁面會增加效能。 不過，如果排除的頁面包含必須編譯的程式碼，則在流覽網頁時，將會擲回錯誤。

## <a name="enableeventvalidation"></a>EnableEventValidation

這個屬性會指定是否要驗證回傳和回呼事件。 啟用此選項時，會檢查回傳或回呼事件的引數，以確保它們源自原先呈現它們的伺服器控制項。

## <a name="enabletheming"></a>EnableTheming

這個屬性會指定是否要在頁面上使用 ASP.NET 主題。 預設值為 **false**。 [模組 10](profiles-themes-and-web-parts.md)中涵蓋了 ASP.NET 主題。

## <a name="linepragmas"></a>LinePragmas

這個屬性會指定是否應該在編譯期間加入行 pragma。 行 pragma 是偵錯工具用來標示特定代碼區段的選項。

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostback

這個屬性會指定是否要將 JavaScript 插入頁面中，以便維護回傳之間的滾動位置。 此屬性預設為**false** 。

當此屬性為**true**時，ASP.NET 會在回傳時加入 &lt;腳本&gt; 區塊，如下所示：

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

請注意，此腳本區塊的 src 是 WebResource。 此資源不是實體路徑。 當要求此腳本時，ASP.NET 會以動態方式建立腳本。

### <a name="masterpagefile"></a>MasterPageFile

這個屬性會指定目前頁面的主版分頁檔案。 路徑可為相對路徑或絕對路徑。 主版頁面涵蓋于[模組 4](master-pages.md)。

## <a name="stylesheettheme"></a>StyleSheetTheme

這個屬性可讓您覆寫 ASP.NET 2.0 主題所定義的使用者介面外觀屬性。 [課程模組 10](profiles-themes-and-web-parts.md)中涵蓋了主題。

## <a name="theme"></a>佈景主題

指定頁面的主題。 如果未指定 StyleSheetTheme 屬性的值，主題屬性會覆寫套用至頁面上之控制項的所有樣式。

## <a name="title"></a>標題

設定頁面的標題。 此處指定的值將會出現在轉譯頁面的 &lt;標題&gt; 元素中。

### <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

設定 ViewStateEncryptionMode 列舉的值。 可用的值**一律**為、 **Auto**和**Never**。 預設值為 [**自動**]。當這個屬性設定為**Auto**的值時，viewstate 會進行加密，因為控制項會藉由呼叫**RegisterRequiresViewStateEncryption**方法來要求它。

## <a name="setting-public-property-values-via-the--page-directive"></a>透過 @ Page 指示詞設定公用屬性值

在 ASP.NET 2.0 中，@ Page 指示詞的另一項新功能是能夠設定基類的公用屬性的起始值。 例如，假設您在基類中有一個稱為**SomeText**的公用屬性，而您想要在載入頁面時將它初始化為**Hello** 。 您只要在 @ Page 指示詞中設定值，就可以完成這項操作，如下所示：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

@ Page 指示詞的**SomeText**屬性會將基類中 SomeText 屬性的初始值設定為*Hello！* 。 以下影片將逐步解說如何使用 @ Page 指示詞，在基類中設定公用屬性的初始值。

![](the-asp-net-2-0-page-model/_static/image1.png)

[開啟全螢幕影片](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a>頁面類別的新公用屬性

下列公用屬性是 ASP.NET 2.0 中的新功能。

## <a name="apprelativetemplatesourcedirectory"></a>AppRelativeTemplateSourceDirectory

傳回頁面或控制項的應用程式相對路徑。 例如，針對位於 http://app/folder/page.aspx的頁面，屬性會傳回 ~/folder/。

## <a name="apprelativevirtualpath"></a>AppRelativeVirtualPath

傳回頁面或控制項的相對虛擬目錄路徑。 例如，針對位於 http://app/folder/page.aspx的頁面，屬性會傳回 ~/folder/page.aspx。

## <a name="asynctimeout"></a>AsyncTimeout

取得或設定非同步網頁處理所使用的超時時間。 （此課程模組稍後會涵蓋非同步頁面。）

## <a name="clientquerystring"></a>ClientQueryString

唯讀屬性，會傳回所要求 URL 的查詢字串部分。 此值為 URL 編碼。 您可以使用 HttpServerUtility 類別的 UrlDecode 方法來對它進行解碼。

## <a name="clientscript"></a>Page.clientscript

這個屬性會傳回 ClientScriptManager 物件，可用來管理 ASP。神經網路發出用戶端腳本。 （此課程模組稍後會涵蓋 ClientScriptManager 類別）。

## <a name="enableeventvalidation"></a>EnableEventValidation

此屬性控制是否啟用回傳和回呼事件的事件驗證。 啟用時，回傳或回呼事件的引數會經過驗證，以確保它們源自原先呈現它們的伺服器控制項。

## <a name="enabletheming"></a>EnableTheming

這個屬性會取得或設定布林值，指定 ASP.NET 2.0 主題是否要套用至頁面。

## <a name="form"></a>表單

這個屬性會以 HtmlForm 物件的形式傳回 ASPX 頁面上的 HTML 表單。

## <a name="header"></a>頁首

這個屬性會傳回包含頁首之 HtmlHead 物件的參考。 您可以使用傳回的 HtmlHead 物件來取得/設定樣式表單、中繼標記等。

## <a name="idseparator"></a>IdSeparator

當 ASP.NET 為頁面上的控制項建立唯一識別碼時，這個唯讀屬性會取得用來分隔控制項識別碼的字元。 但並不是針對直接從程式碼使用而設計。

## <a name="isasync"></a>IsAsync

這個屬性允許非同步頁面。 本課程模組稍後會討論非同步網頁。

## <a name="iscallback"></a>IsCallback

如果頁面是回呼的結果，此唯讀屬性會傳回**true** 。 稍後會在此課程模組中討論電話支援。

## <a name="iscrosspagepostback"></a>IsCrossPagePostBack

如果頁面是跨頁面回傳的一部分，此唯讀屬性會傳回**true** 。 本課程模組稍後會涵蓋跨頁面回傳。

## <a name="items"></a>項目

傳回 IDictionary 實例的參考，其中包含儲存在頁面內容中的所有物件。 您可以將專案新增至此 IDictionary 物件，而且在內容的整個存留期間都可以使用它們。

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostBack

此屬性控制 ASP.NET 是否會發出 JavaScript，以在回傳之後，維護瀏覽器中的頁面滾動位置。 （本課程模組稍早已討論過此屬性的詳細資料）。

## <a name="master"></a>Master

這個唯讀屬性會針對已套用主版頁面的頁面，傳回 MasterPage 實例的參考。

## <a name="masterpagefile"></a>MasterPageFile

取得或設定頁面的主版分頁檔名。 這個屬性只能在 PreInit 方法中設定。

## <a name="maxpagestatefieldlength"></a>MaxPageStateFieldLength

這個屬性會取得或設定頁面狀態的最大長度（以位元組為單位）。 如果屬性設定為正數，網頁檢視狀態將會分成多個隱藏欄位，使其不會超過指定的位元組數。 如果屬性為負數，則檢視狀態將不會分成多個區塊。

## <a name="pageadapter"></a>PageAdapter

傳回對要求的瀏覽器修改頁面的 PageAdapter 物件參考。

## <a name="previouspage"></a>PreviousPage

當伺服器. 傳輸或跨頁面回傳時，傳回前一頁的參考。

## <a name="skinid"></a>SkinID

指定要套用至頁面的 ASP.NET 2.0 面板。

## <a name="stylesheettheme"></a>StyleSheetTheme

這個屬性會取得或設定套用至頁面的樣式表單。

## <a name="templatecontrol"></a>TemplateControl

傳回頁面之包含控制項的參考。

## <a name="theme"></a>佈景主題

取得或設定套用至頁面的 ASP.NET 2.0 主題名稱。 在 PreInit 方法之前，必須先設定此值。

## <a name="title"></a>標題

這個屬性會取得或設定頁面標頭中所取得之網頁的標題。

## <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

取得或設定頁面的 ViewStateEncryptionMode。 請參閱此課程模組稍早的此屬性的詳細討論。

## <a name="new-protected-properties-of-the-page-class"></a>頁面類別的新受保護屬性

以下是 ASP.NET 2.0 中頁面類別的新受保護屬性。

## <a name="adapter"></a>配接器

傳回 ControlAdapter 的參考，它會在要求的裝置上呈現頁面。

## <a name="asyncmode"></a>AsyncMode

這個屬性會指出是否要以非同步方式處理頁面。 它適用于執行時間，而不是直接在程式碼中使用。

## <a name="clientidseparator"></a>ClientIDSeparator

這個屬性會傳回建立控制項的唯一用戶端識別碼時，用來做為分隔符號的字元。 它適用于執行時間，而不是直接在程式碼中使用。

## <a name="pagestatepersister"></a>PageStatePersister

這個屬性會傳回頁面的 PageStatePersister 物件。 這個屬性主要是由 ASP.NET 控制項開發人員使用。

## <a name="uniquefilepathsuffix"></a>UniqueFilePathSuffix

這個屬性會傳回附加至快取瀏覽器之檔案路徑的唯一尾碼。 預設值為 \_\_ufps = 和6位數的數位。

## <a name="new-public-methods-for-the-page-class"></a>Page 類別的新公用方法

下列公用方法是 ASP.NET 2.0 中 Page 類別的新功能。

## <a name="addonprerendercompleteasync"></a>AddOnPreRenderCompleteAsync

這個方法會註冊非同步頁面執行的事件處理常式委派。 本課程模組稍後會討論非同步網頁。

## <a name="applystylesheetskin"></a>ApplyStyleSheetSkin

將頁面樣式表單中的屬性套用至頁面。

## <a name="executeregisteredasynctasks"></a>ExecuteRegisteredAsyncTasks

這個方法是非同步工作。

### <a name="getvalidators"></a>GetValidators

傳回指定之驗證群組的驗證程式集合，如果未指定，則傳回預設的驗證群組。

## <a name="registerasynctask"></a>RegisterAsyncTask

這個方法會註冊新的非同步工作。 此課程模組稍後會涵蓋非同步頁面。

## <a name="registerrequirescontrolstate"></a>RegisterRequiresControlState

這個方法會告訴 ASP.NET，必須保存頁面控制項狀態。

## <a name="registerrequiresviewstateencryption"></a>RegisterRequiresViewStateEncryption

這個方法會告訴 ASP.NET 網頁 viewstate 需要加密。

## <a name="resolveclienturl"></a>ResolveClientUrl

傳回可用於用戶端要求影像等的相對 URL。

## <a name="setfocus"></a>SetFocus

這個方法會將焦點設定為一開始載入頁面時所指定的控制項。

## <a name="unregisterrequirescontrolstate"></a>UnregisterRequiresControlState

這個方法會取消註冊傳遞給它的控制項，因為不再需要控制項狀態持續性。

## <a name="changes-to-the-page-lifecycle"></a>頁面生命週期的變更

ASP.NET 2.0 中的頁面生命週期並未大幅變更，但有一些您應該注意的新方法。 ASP.NET 2.0 頁面生命週期如下所述。

## <a name="preinit-new-in-aspnet-20"></a>PreInit （ASP.NET 2.0 中的新功能）

PreInit 事件是開發人員可以存取之生命週期中的最早階段。 新增此事件可讓您以程式設計方式變更 ASP.NET 2.0 主題、主版頁面、ASP.NET 2.0 設定檔的存取屬性等等。如果您處於回傳狀態，請務必瞭解 Viewstate 在生命週期的這個階段尚未套用到控制項。 因此，如果開發人員在這個階段變更控制項的屬性，稍後在頁面生命週期中可能會遭到覆寫。

## <a name="init"></a>Init

Init 事件尚未從 ASP.NET 1.x 變更。 這是您想要在頁面上讀取或初始化控制項屬性的位置。 在這個階段，主版頁面、主題等已套用至頁面。

## <a name="initcomplete-new-in-20"></a>InitComplete （2.0 中的新功能）

InitComplete 事件會在頁面初始化階段結束時呼叫。 在生命週期的這個階段中，您可以存取頁面上的控制項，但尚未填入其狀態。

## <a name="preload-new-in-20"></a>預先載入（2.0 中的新功能）

在套用所有回傳資料之後，以及在頁面\_載入之前，會呼叫此事件。

## <a name="load"></a>載入

Load 事件尚未從 ASP.NET 1.x 變更。

## <a name="loadcomplete-new-in-20"></a>System.web.ui.page.loadcomplete （2.0 中的新功能）

System.web.ui.page.loadcomplete 事件是頁面載入階段中的最後一個事件。 在這個階段，所有回傳和 viewstate 資料都已套用至頁面。

## <a name="prerender"></a>預

如果您想要針對以動態方式新增至頁面的控制項適當地維護 viewstate，則可呈現的事件是最後一個加入它們的機會。

## <a name="prerendercomplete-new-in-20"></a>PreRenderComplete （2.0 中的新功能）

在 PreRenderComplete 階段，所有控制項都已加入至頁面，而且該頁面已準備好呈現。 PreRenderComplete 事件是儲存頁面 viewstate 之前引發的最後一個事件。

## <a name="savestatecomplete-new-in-20"></a>SaveStateComplete （2.0 中的新功能）

儲存所有頁面 viewstate 和控制項狀態之後，就會立即呼叫 SaveStateComplete 事件。 這是頁面實際轉譯至瀏覽器前的最後一個事件。

## <a name="render"></a>轉譯

Render 方法自 ASP.NET 1.x 以來並未變更。 這就是 HtmlTextWriter 初始化的位置，而且頁面會轉譯至瀏覽器。

## <a name="cross-page-postback-in-aspnet-20"></a>ASP.NET 2.0 中的跨頁面回傳

在 ASP.NET 1.x 中，回傳必須張貼到相同的頁面。 不允許跨頁面回傳。 ASP.NET 2.0 新增了透過 IButtonControl 介面回傳至不同頁面的功能。 除了協力廠商自訂控制項以外，任何會執行新 IButtonControl 介面（Button、LinkButton 和 ImageButton）的控制項，都可以透過使用 PostBackUrl 屬性來利用這項新功能。 下列程式碼顯示會回傳至第二頁的按鈕控制項。

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

當頁面回傳時，可以透過第二頁上的 PreviousPage 屬性來存取起始回傳的網頁。 此功能是透過新的 WebForm\_DoPostBackWithOptions 用戶端函式來執行，當控制項回傳至不同的頁面時，ASP.NET 2.0 會轉譯至頁面。 這個 JavaScript 函數是由向用戶端發出腳本的新 WebResource 處理常式所提供。

以下影片是跨頁面回傳的逐步解說。

![](the-asp-net-2-0-page-model/_static/image2.png)

[開啟全螢幕影片](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a>跨頁面回傳的詳細資訊

### <a name="viewstate"></a>狀態

您可能已經問自己，您已經在跨頁面回傳案例中，從第一頁看到 viewstate 會發生什麼情況。 畢竟，任何未執行 IPostBackDataHandler 的控制項都會透過 viewstate 保存其狀態，因此若要在跨頁面回傳的第二頁上存取該控制項的屬性，您必須能夠存取該頁面的 viewstate。 ASP.NET 2.0 會在第二頁中使用新的隱藏欄位（稱為 \_\_PREVIOUSPAGE）來處理此案例。 [\_\_PREVIOUSPAGE 表單] 欄位包含第一個頁面的 viewstate，讓您可以存取第二頁中所有控制項的屬性。

### <a name="circumventing-findcontrol"></a>規避 FindControl

在跨頁面回傳的影片逐步解說中，我使用 FindControl 方法來取得第一個頁面上 TextBox 控制項的參考。 該方法適用于該用途，但 FindControl 的成本很高，而且需要撰寫額外的程式碼。 幸好，ASP.NET 2.0 針對此用途提供了 FindControl 的替代方案，可在許多案例中使用。 PreviousPageType 指示詞可讓您使用 TypeName 或 VirtualPath 屬性，來擁有上一頁的強型別參考。 TypeName 屬性可讓您指定前一頁的類型，而 VirtualPath 屬性則可讓您使用虛擬路徑來參考前一頁。 設定 PreviousPageType 指示詞之後，您必須接著使用公用屬性來公開控制項等，以允許存取。

## <a name="lab-1-cross-page-postback"></a>實驗室1跨頁面回傳

在此實驗室中，您將建立使用 ASP.NET 2.0 新跨頁面回傳功能的應用程式。

1. 開啟 Visual Studio 2005，並建立新的 ASP.NET 網站。
2. 加入名為 page2 的新 Webform。
3. 在設計檢視中開啟 default.aspx，並新增 [按鈕] 控制項和 [TextBox] 控制項。 

    1. 為按鈕控制項提供**SubmitButton**的識別碼，並將 TextBox 控制項命名為**UserName**。
    2. 將按鈕的 PostBackUrl 屬性設定為 page2。
4. 在原始檔視圖中開啟 page2。
5. 新增 @ PreviousPageType 指示詞，如下所示：
6. 將下列程式碼新增至頁面\_載入 page2 的程式碼後置： 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. 按一下 [建立] 功能表上的 [建立] 來建立專案。
8. 將下列程式碼加入至 default.aspx 的程式碼後置： 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. 將 page2 中的頁面\_載入變更為下列內容： 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. 建置專案。
11. 執行專案。
12. 在文字方塊中輸入您的名稱，然後按一下按鈕。
13. 結果是什麼？

## <a name="asynchronous-pages-in-aspnet-20"></a>ASP.NET 2.0 中的非同步頁面

ASP.NET 中的許多爭用問題是因外部呼叫延遲（例如 Web 服務或資料庫呼叫）、檔案 IO 延遲等所造成。針對 ASP.NET 應用程式提出要求時，ASP.NET 會使用其中一個背景工作執行緒來服務該要求。 該要求會擁有該執行緒，直到要求完成並已傳送回應為止。 ASP.NET 2.0 藉由新增以非同步方式執行頁面的功能，尋求解決這些類型問題的延遲問題。 這表示工作者執行緒可以啟動要求，然後將額外的執行交給另一個執行緒，藉此快速返回可用的執行緒集區。 當檔案 IO、資料庫呼叫等完成時，就會從執行緒集區取得新的執行緒以完成要求。

讓頁面以非同步方式執行的第一個步驟，是設定 page 指示詞的**Async**屬性，如下所示：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

這個屬性會告知 ASP.NET，以執行頁面的 IHttpAsyncHandler。

下一步是在預先呈現之前，在頁面生命週期中的某個點呼叫 AddOnPreRenderCompleteAsync 方法。 （這個方法通常會在頁面\_載入）中呼叫）。AddOnPreRenderCompleteAsync 方法會採用兩個參數：BeginEventHandler 和 EndEventHandler。 BeginEventHandler 會傳回 IAsyncResult，然後將它當做參數傳遞給 EndEventHandler。

以下影片是非同步網頁要求的逐步解說。

![](the-asp-net-2-0-page-model/_static/image3.png)

[開啟全螢幕影片](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> 在 EndEventHandler 完成之前，非同步網頁不會轉譯至瀏覽器。 不確定，有些開發人員會將非同步要求視為類似非同步回呼。 請務必瞭解它們不是。 非同步要求的優點是第一個工作者執行緒可以傳回到執行緒集區來服務新的要求，藉此減少因 IO 系結等而造成的爭用。

## <a name="script-callbacks-in-aspnet-20"></a>ASP.NET 2.0 中的腳本回呼

Web 開發人員一直都在尋求避免與回呼相關聯之閃爍的方式。 在 ASP.NET 1.x 中，SmartNavigation 是避免閃爍的最常見方法，但是 SmartNavigation 會因其在用戶端上的執行複雜度而造成某些開發人員的問題。 ASP.NET 2.0 使用腳本回呼解決了這個問題。 腳本回呼會利用 XMLHttp，透過 JavaScript 對 Web 服務器提出要求。 XMLHttp 要求會傳回可透過瀏覽器的 DOM 操作的 XML 資料。 新的 WebResource 處理常式會向使用者隱藏 XMLHttp 程式碼。

若要在 ASP.NET 2.0 中設定腳本回呼，必須執行幾個步驟。

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>步驟1：執行 ICallbackEventHandler 介面

為了讓 ASP.NET 能夠將您的頁面辨識為參與腳本回呼，您必須執行 ICallbackEventHandler 介面。 您可以在程式碼後置檔案中執行此動作，如下所示：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

您也可以使用 @ Implements 指示詞來執行此動作，如下所示：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

使用內嵌 ASP.NET 程式碼時，您通常會使用 @ Implements 指示詞。

## <a name="step-2--call-getcallbackeventreference"></a>步驟2：呼叫 GetCallbackEventReference

如先前所述，XMLHttp 呼叫會封裝在 WebResource 處理常式中。 當您的頁面呈現時，ASP.NET 會將呼叫新增至 WebForm\_DoCallback，這是 WebResource 所提供的用戶端腳本。 WebForm\_DoCallback 函數會取代回呼的 \_\_doPostBack 函式。 請記住，\_\_doPostBack 以程式設計方式在頁面上提交表單。 在回呼案例中，您想要避免回傳，因此 \_\_doPostBack 將不會足夠。

> [!NOTE]
> 在用戶端腳本回呼案例中，\_\_doPostBack 仍會轉譯至頁面。 不過，它不會用於回呼。

WebForm\_DoCallback 用戶端函式的引數是透過伺服器端函數 GetCallbackEventReference 提供，通常會在頁面\_載入中呼叫。 典型的 GetCallbackEventReference 呼叫可能如下所示：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> 在此情況下，cm 是 ClientScriptManager 的實例。 本課程模組稍後會涵蓋 ClientScriptManager 類別。

GetCallbackEventReference 有數個多載版本。 在此情況下，引數如下所示：

`this`

呼叫 GetCallbackEventReference 之控制項的參考。 在此情況下，它是頁面本身。

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

將從用戶端程式代碼傳遞至伺服器端事件的字串引數。 在此情況下，Im 會傳遞名為 ddlCompany 之下拉式清單的值。

`ShowCompanyName`

用戶端函式的名稱，將接受來自伺服器端回呼事件的傳回值（字串形式）。 只有當伺服器端回呼成功時，才會呼叫這個函式。 因此，為了加強可靠性，通常建議使用 GetCallbackEventReference 的多載版本，它會採用額外的 string 引數來指定在發生錯誤時要執行的用戶端函數名稱。

`null`

代表用戶端函式的字串，該函數會在回呼至伺服器之前起始。 在此情況下，沒有這類腳本，因此引數為 null。

`true`

布林值，指定是否要以非同步方式執行回呼。

在用戶端上對 WebForm\_DoCallback 的呼叫將會傳遞這些引數。 因此，當此頁面在用戶端上呈現時，該程式碼看起來會像這樣：

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

請注意，用戶端上的函數簽章有點不同。 用戶端函式會傳遞5個字串和一個布林值。 其他字串（在上述範例中為 null）包含用戶端函式，會處理來自伺服器端回呼的任何錯誤。

## <a name="step-3--hook-the-client-side-control-event"></a>步驟3：掛上用戶端控制項事件

請注意，上述 GetCallbackEventReference 的傳回值已指派給字串變數。 該字串是用來攔截起始回呼之控制項的用戶端事件。 在此範例中，回呼是由頁面上的下拉式清單起始，所以我想要攔截*OnChange*事件。

若要攔截用戶端事件，只需要將處理常式新增至用戶端標記，如下所示：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

回想一下， *cbRef*是呼叫 GetCallbackEventReference 的傳回值。 它包含對 WebForm\_DoCallback 的呼叫，如上所示。

## <a name="step-4--register-the-client-side-script"></a>步驟4：註冊用戶端腳本

回想一下，GetCallbackEventReference 的呼叫指定當伺服器端回呼成功時，會執行名為**ShowCompanyName**的用戶端腳本。 該腳本必須使用 ClientScriptManager 實例加入至頁面。 （稍後將在此課程模組中討論 ClientScriptManager 類別）。您可以這樣做，如下所示：

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>步驟5：呼叫 ICallbackEventHandler 介面的方法

ICallbackEventHandler 包含兩個您需要在程式碼中執行的方法。 它們是**RaiseCallbackEvent**和**GetCallbackEvent**。

**RaiseCallbackEvent**接受字串做為引數，並不會傳回任何內容。 字串引數會從用戶端呼叫傳遞至 WebForm\_DoCallback。 在此情況下，該值是下拉式清單的*value*屬性，稱為 ddlCompany。 您的伺服器端程式碼應該放在 RaiseCallbackEvent 方法中。 例如，如果您的回呼是對外部資源進行 WebRequest，則該程式碼應該放在 RaiseCallbackEvent 中。

**GetCallbackEvent**負責處理傳回用戶端的回呼。 它不接受任何引數，而且會傳回字串。 其傳回的字串將會當做引數傳遞至用戶端函式，在此案例中為*ShowCompanyName*。

完成上述步驟之後，您就可以開始在 ASP.NET 2.0 中執行腳本回呼。

![](the-asp-net-2-0-page-model/_static/image4.png)

[開啟全螢幕影片](the-asp-net-2-0-page-model/_static/callback1.wmv)

支援進行 XMLHttp 呼叫的任何瀏覽器都支援 ASP.NET 中的腳本回呼。 這包括現今使用的所有新式瀏覽器。 Internet Explorer 會使用 XMLHttp ActiveX 物件，而其他現代化的瀏覽器（包括即將推出的 IE 7）則使用內部 XMLHttp 物件。 若要以程式設計方式判斷瀏覽器是否支援回呼，您可以使用**SupportCallback**屬性。 如果要求的用戶端支援腳本回呼，這個屬性會傳回**true** 。

## <a name="working-with-client-script-in-aspnet-20"></a>在 ASP.NET 2.0 中使用用戶端腳本

ASP.NET 2.0 中的用戶端腳本是透過使用 ClientScriptManager 類別來管理。 ClientScriptManager 類別會使用類型和名稱來追蹤用戶端腳本。 這可防止相同的腳本以程式設計方式在頁面上多次插入。

> [!NOTE]
> 在網頁上成功註冊腳本之後，任何後續嘗試註冊相同的腳本，都只會導致腳本不會第二次註冊。 不會新增重複的腳本，也不會發生例外狀況。 若要避免不必要的計算，您可以使用一些方法來判斷是否已註冊腳本，讓您不會嘗試多次註冊。

所有目前的 ASP.NET 開發人員都應該熟悉 ClientScriptManager 的方法：

## <a name="registerclientscriptblock"></a>RegisterClientScriptBlock

這個方法會將腳本加入轉譯頁面的頂端。 這適用于新增將在用戶端上明確呼叫的函式。

這個方法有兩個多載版本。 四個引數中有三個是常見的。 包括：

`type (string)`

***型***別引數可識別腳本的型別。 通常最好是使用頁面的類型（這個）。類型的 GetType （））。

`key (string)`

***Key***引數是腳本的使用者定義索引鍵。 這對於每個腳本而言都是唯一的。 如果您嘗試加入的腳本具有與已加入之腳本相同的索引鍵和類型，則不會新增它。

`script (string)`

***腳本***引數是一個字串，其中包含要加入的實際腳本。 建議您使用 StringBuilder 來建立腳本，然後在 StringBuilder 上使用 ToString （）方法來指派***腳本***引數。

如果您使用只接受三個引數的多載 RegisterClientScriptBlock，您必須在腳本中包含 script 元素（&lt;腳本&gt; 和 &lt;/script&gt;）。

您可以選擇使用採用第四個引數的 RegisterClientScriptBlock 多載。 第四個引數是布林值，指定 ASP.NET 是否應該為您加入腳本元素。 如果這個引數為**true**，則您的腳本不應明確包含腳本元素。

使用 IsClientScriptBlockRegistered 方法來判斷腳本是否已註冊。 這可讓您避免嘗試重新註冊已註冊的腳本。

### <a name="registerclientscriptinclude-new-in-20"></a>RegisterClientScriptInclude （2.0 中的新功能）

RegisterClientScriptInclude 標記會建立連結至外部腳本檔案的腳本區塊。 它有兩個多載。 其中一個會接受一個金鑰和一個 URL。 第二個會加入指定類型的第三個引數。

例如，下列程式碼會產生一個腳本區塊，它會連結至應用程式之 scripts 資料夾根目錄中的 jsfunctions：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

此程式碼會在呈現的頁面中產生下列程式碼：

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> 腳本區塊會呈現在頁面底部。

使用 IsClientScriptIncludeRegistered 方法來判斷腳本是否已註冊。 這可讓您避免嘗試重新註冊腳本。

## <a name="registerstartupscript"></a>RegisterStartupScript

RegisterStartupScript 方法會採用與 RegisterClientScriptBlock 方法相同的引數。 向 RegisterStartupScript 註冊的腳本會在頁面載入之後，但在 OnLoad 用戶端事件之前執行。 在1.x 中，使用 RegisterStartupScript 註冊的腳本會放在結尾 &lt;/form&gt; 標記之前，而向 RegisterClientScriptBlock 註冊的腳本會緊接在開頭 &lt;表單&gt; 標記之後。 在 ASP.NET 2.0 中，這兩個都會緊接在結尾 &lt;/form&gt; 標記之前。

> [!NOTE]
> 如果您向 RegisterStartupScript 註冊函式，該函式將不會執行，直到您在用戶端程式代碼中明確呼叫它為止。

使用 IsStartupScriptRegistered 方法來判斷腳本是否已註冊，並避免嘗試重新註冊腳本。

## <a name="other-clientscriptmanager-methods"></a>其他 ClientScriptManager 方法

以下是 ClientScriptManager 類別的一些其他實用方法。

|  <strong>GetCallbackEventReference</strong>   |                                                 請參閱稍早在此課程模組中的腳本回呼。                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>GetPostBackClientHyperlink</strong>  |                取得 JavaScript 參考（javascript：&lt;呼叫&gt;），可以用來從用戶端事件回傳。                 |
|  <strong>GetPostBackEventReference</strong>   |                                   取得可用於從用戶端起始回傳的字串。                                    |
|      <strong>GetWebResourceUrl</strong>       | 傳回內嵌于元件中之資源的 URL。 必須與<strong>RegisterClientScriptResource</strong>搭配使用。 |
| <strong>RegisterClientScriptResource</strong> |     向頁面註冊 Web 資源。 這些是內嵌在元件中，並由新的 WebResource 處理常式所處理的資源。      |
|     <strong>RegisterHiddenField</strong>      |                                                 向頁面註冊隱藏的表單欄位。                                                 |
|  <strong>RegisterOnSubmitStatement</strong>   |                                  註冊在提交 HTML 表單時執行的用戶端程式代碼。                                   |
