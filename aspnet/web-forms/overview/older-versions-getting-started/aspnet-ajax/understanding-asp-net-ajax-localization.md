---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
title: 瞭解 ASP.NET AJAX 當地語系化 |Microsoft Docs
author: scottcate
description: 當地語系化是將特定語言和文化特性的支援設計和整合到應用程式或應用程式元件的過程。 Mic 。
ms.author: riande
ms.date: 03/14/2008
ms.assetid: c1a35f18-bab9-41f7-8497-15530c37a09d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
msc.type: authoredcontent
ms.openlocfilehash: 003e7939accd7a68dab97441b3d999bca835b85a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566217"
---
# <a name="understanding-aspnet-ajax-localization"></a>了解 ASP.NET AJAX 當地語系化

由[Scott Cate](https://github.com/scottcate)

[下載 PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial04_Localization_cs.pdf)

> 當地語系化是將特定語言和文化特性的支援設計和整合到應用程式或應用程式元件的過程。 Microsoft ASP.NET 平臺藉由整合標準的 .NET 當地語系化模型，針對標準 ASP.NET 應用程式的當地語系化提供廣泛的支援。Microsoft AJAX 架構利用整合式模型來支援可執行當地語系化的各種案例。

## <a name="introduction"></a>簡介

Microsoft 的 ASP.NET 技術引進了物件導向和事件導向的程式設計模型，並將它與已編譯器代碼的優點結合在一起。 不過，其伺服器端處理模型在技術上有一些缺點，其中有許多都可以由 System.web. Web.config 命名空間中包含的新功能來解決，這會在 .NET Framework 中封裝 Microsoft AJAX Services。3.5。 這些延伸模組可提供許多豐富的用戶端功能，先前是 ASP.NET 2.0 AJAX 延伸模組的一部分，但現在是架構基類庫的一部分。 這個命名空間中的控制項和功能包括頁面的部分轉譯，而不需要完整的頁面重新整理、透過用戶端腳本存取 Web 服務的能力（包括 ASP.NET 分析 API），以及專為鏡像許多的應用程式而設計的廣泛用戶端 API在 ASP.NET 伺服器端控制項集中看到的控制項配置。

本白皮書探討 Microsoft AJAX Framework 和 Microsoft AJAX 腳本程式庫中的當地語系化功能，其中包含了當地語系化支援的商務需求，以及針對 web 中的當地語系化所提供的整合式支援.NET Framework 所提供的應用程式。 Microsoft AJAX 腳本程式庫會利用 .NET 應用程式已使用的 .resx 檔案格式，以提供整合式 IDE 支援和可共用的資源類型。

本白皮書是以 Microsoft Visual Studio 2008 的 Beta 2 版本為基礎。 本白皮書也假設您將使用 Visual Studio 2008，而不是 Visual Web Developer Express，而且將會根據 Visual Studio 的使用者介面提供逐步解說。 有些程式碼範例會利用 Visual Web Developer Express 中可能無法使用的專案範本。

## <a name="the-need-for-localization"></a>*當地語系化的需求*

特別是對於企業應用程式開發人員和元件開發人員而言，建立工具以瞭解文化特性與語言之間的差異，已經變得越來越需要。 設計可配合用戶端地區設定功能的元件會提高開發人員的生產力，並減少調整元件以全域運作所需的工作量。

當地語系化是將特定語言和文化特性的支援設計和整合到應用程式或應用程式元件的過程。 Microsoft ASP.NET 平臺藉由整合標準的 .NET 當地語系化模型，針對標準 ASP.NET 應用程式的當地語系化提供廣泛的支援。Microsoft AJAX 架構利用整合式模型來支援可執行當地語系化的各種案例。 透過 Microsoft AJAX Framework，腳本可以藉由部署到附屬元件，或利用靜態檔案系統結構來進行當地語系化。

## <a name="embedding-scripts-with-satellite-assemblies"></a>*使用附屬元件嵌入腳本*

與標準 .NET Framework 當地語系化策略一致，資源可以包含在附屬元件中。 附屬元件提供幾項優於傳統資源包含在二進位檔中的優點-任何指定的當地語系化都可以更新，而不需要更新較大的影像，而只要將附屬元件安裝到，就可以部署額外的當地語系化專案資料夾和附屬元件可以部署，而不會造成主要專案元件的重載。 特別是在 ASP.NET 專案中，這會很有説明，因為它可以大幅減少累加式更新所使用的系統資源量，並最少中斷生產網站的使用量。

腳本會內嵌在元件中，方法是將它們包含在 managed .resx （或編譯的 .resources）檔案中，這些檔案會在編譯時期包含在元件中。 然後透過元件層級屬性，將其資源提供給腳本應用程式

*內嵌腳本檔案的命名慣例*

Microsoft AJAX Framework 腳本管理支援各種選項，可用於部署和測試腳本，並提供指導方針來協助這些選項。

*若要協助進行調試：*

發行（生產）腳本不應在檔案名中包含 `.debug` 限定詞。 針對偵錯工具設計的腳本應該在檔案名中包含 `.debug`。

*為了簡化當地語系化：*

中性文化特性腳本不應在檔案名中包含任何文化特性識別碼。 對於包含當地語系化資源的腳本，應在檔案名中指定 ISO 語言代碼。 例如，`es-CO` 代表西班牙文，哥倫比亞。

下表摘要說明檔案命名慣例與範例：

| Filename | 意義 |
| --- | --- |
| Script .js | 發行版本文化特性中性的腳本。 |
| Script. debug .js | Debug 版本文化特性中性的腳本。 |
| En-US .js | 發行版本英文、美國腳本。 |
| Script.debug.es-CO .js | Debug-版本西班牙文，哥倫比亞腳本。 |

## <a name="walkthrough-create-an-localized-embedded-script"></a>逐步解說：建立當地語系化的內嵌腳本

*請注意：此逐步解說需要使用 Visual Studio 2008，因為 Visual Web Developer Express 並未包含類別庫專案的專案範本。*

1. 建立 ASP.NET AJAX Extensions 整合的新網站專案。 在名為 LocalizingResources 的方案中，建立另一個專案（類別庫專案）。
2. 將名為 VerifyDeletion 的 Jscript 檔案加入至 LocalizingResources 專案，以及名為 DeletionResources 和 DeletionResources 的 .resx 資源檔。 前者會包含文化特性中性的資源;後者將包含西班牙文語言資源。
3. 將下列程式碼新增至 VerifyDeletion：

[!code-javascript[Main](understanding-asp-net-ajax-localization/samples/sample1.js)]

對於不熟悉 JavaScript Regex 語法的人而言，單一正斜線內的文字（在上一個範例中，/FILENAME/是一個範例）代表 RegExp 物件。 MSDN Library 包含廣泛的 JavaScript 參考，而 JavaScript 原生物件上的資源則可以在線上找到。

1. 將下列資源字串新增至 DeletionResources： 

    **VerifyDelete**：您確定要刪除 FILENAME 嗎？

    **已刪除**：已刪除 FILENAME。

1. 將下列資源字串新增至 DeletionResources： 

    **VerifyDelete**： Est seguro que DESEE quitar FILENAME？

    **已刪除**： FILENAME se ha quitado。
2. 將下列幾行程式碼新增至 AssemblyInfo 檔案：

[!code-csharp[Main](understanding-asp-net-ajax-localization/samples/sample2.cs)]

1. 將 LocalizingResources 專案的參考加入至 System.web 和 system.web。
2. 從網站專案加入 LocalizingResources 專案的參考。
3. 在 default.aspx 的網站專案底下，使用下列其他標記來更新 ScriptManager 控制項：

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample3.aspx)]

1. 在 default.aspx 中，于頁面上的任何位置加入此標記：

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample4.aspx)]

1. 按 F5。 若出現提示，請啟用調試。 載入頁面時，請按下 [刪除] 按鈕。 請注意，系統會提示您輸入英文（除非您的電腦預設設定為偏好西班牙文語言資源）以進行確認。
2. 關閉瀏覽器視窗並返回 default.aspx。 在 @Page 標頭指示詞中，將 Culture 和 UICulture 的 auto 取代為 es。 再按一次 F5，即可在瀏覽器中再次啟動 web 應用程式。 這次請注意，系統會提示您以西班牙文刪除檔案：

[![](understanding-asp-net-ajax-localization/_static/image2.png)](understanding-asp-net-ajax-localization/_static/image1.png)

（[按一下以查看完整大小的影像](understanding-asp-net-ajax-localization/_static/image3.png)）

[![](understanding-asp-net-ajax-localization/_static/image5.png)](understanding-asp-net-ajax-localization/_static/image4.png)

（[按一下以查看完整大小的影像](understanding-asp-net-ajax-localization/_static/image6.png)）

請注意，此逐步解說有數個變化。 例如，腳本可以在頁面載入期間，以程式設計方式向 ScriptManager 控制項註冊。

## <a name="including-a-static-script-file-structure"></a>*包含靜態腳本檔案結構*

使用靜態腳本檔案進行部署時，您會失去使用固有 .NET 當地語系化配置的部分優點。 主要可見的是您遺失從包含腳本資源檔產生的自動類型;例如，在上述逐步解說中，資源是由來自 ScriptManager 控制項且名為 Message 的自動產生類型所公開。

不過，使用靜態腳本檔案結構有一些好處。 更新可以在不需重新編譯和重新部署附屬元件的情況下執行，而且也可以使用靜態檔案結構來覆寫內嵌腳本，以整合元件可能未隨附的次要功能。

Microsoft 建議在專案編譯期間自動產生您的腳本資源，以避免版本控制問題。 維護廣泛的腳本程式碼基底時，可能會變得越來越難以確保程式碼變更反映在每個當地語系化的腳本中。 或者，您可以直接維護一個邏輯腳本和多個當地語系化腳本，在建立專案時合併檔案。

因為沒有以宣告方式包含的資源，所以您應該藉由將 `<asp:ScriptElement>` 專案當做 ScriptManager 控制項之 `<Scripts>` 標記的子系，或以程式設計方式在執行時間將 `ScriptReference` 物件加入至頁面上的 `ScriptManager` 控制項的 `Scripts` 屬性來參考靜態腳本檔案。

## <a name="the-scriptmanager-and-its-role-in-localization"></a>*ScriptManager 和其在當地語系化中的角色*

ScriptManager 針對當地語系化的應用程式啟用數個自動行為：

- 它會根據設定和命名慣例自動尋找腳本檔案;比方說，它會在偵錯工具模式中載入啟用 debug 的腳本，並根據瀏覽器的使用者介面選擇載入當地語系化的腳本。
- 它會啟用文化特性的定義，包括自訂文化特性。
- 它可透過 HTTP 壓縮腳本檔案。
- 它會快取腳本，以有效率地管理許多要求。
- 它會透過加密的 URL 將間接取值層新增至腳本。

您可以透過程式設計方式或宣告式標記，將腳本參考新增至 ScriptManager 控制項。 當您使用內嵌于元件（而非網站專案本身）中的腳本時，宣告式標記特別有用，因為在推送修訂時，腳本的名稱可能不會變更。

## <a name="summary"></a>總結

隨著 web 應用程式成長而接觸到更多物件，必須能夠觸及更廣泛的文化和社區，才能成為商務模型的核心;電子商務 web 應用程式必須能夠處理外部貨幣，內容管理系統必須能夠不僅呈現其內容，也不能提供其他語言的流覽提示和表單欄位，而且公司必須知道這項需求是隨時.

.NET Framework 本質上支援豐富的當地語系化架構，利用附屬元件和 XML 資源（.resx）檔案來呈現統一的方式來查詢資源字串和影像。 ASP.NET AJAX Extensions （包括 Microsoft AJAX Framework 和 Microsoft AJAX 腳本程式庫）可將此程式設計模型的支援提供給用戶端程式代碼，讓您能夠輕鬆地進行資源字串查閱。 附屬元件支援透過 ScriptResource 自動包含腳本資源（實際的 .js 檔案），只要檔案名遵循指定的命名配置即可。 透過這項支援，ASP.NET AJAX 延伸模組簡化了腳本的當地語系化和應用程式的全球化。

## <a name="bio"></a>*生物*

Scott Cate 自1997起開始使用 Microsoft Web 技術，而這是 myKB.com （[www.myKB.com](http://www.myKB.com)）的總裁，他專門撰寫以 ASP.NET 為基礎的應用程式，著重于知識庫軟體解決方案。 Scott 可以透過電子郵件聯絡，位於[scott.cate@myKB.com](mailto:scott.cate@myKB.com)或他的[ScottCate.com](http://ScottCate.com)的 blog

> [!div class="step-by-step"]
> [上一頁](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
> [下一頁](understanding-asp-net-ajax-web-services.md)
