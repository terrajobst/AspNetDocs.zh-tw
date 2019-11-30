---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
title: 開發與生產環境間的常見設定差異（VB） |Microsoft Docs
author: rick-anderson
description: 在先前的教學課程中，我們會將所有相關檔案從開發環境複製到生產環境，藉以部署我們的網站。 不過，我 。
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 548e75f6-4d6c-4cb4-8da8-417915eb8393
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
msc.type: authoredcontent
ms.openlocfilehash: cc65af6eb4fca8b3b805e11e26da468a958a4221
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619949"
---
# <a name="common-configuration-differences-between-development-and-production-vb"></a>開發與生產環境間的常見設定差異 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載 PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial05_ConfigDifferences_vb.pdf)

> 在先前的教學課程中，我們會將所有相關檔案從開發環境複製到生產環境，藉以部署我們的網站。 不過，環境之間的設定差異並不常見，因為每個環境都有唯一的 Web.config 檔案。 本教學課程會檢查一般設定差異，並查看維護個別設定資訊的策略。

## <a name="introduction"></a>簡介

最後兩個教學課程逐步解說如何部署簡單的 web 應用程式。 [*使用 FTP 用戶端部署您的網站*](deploying-your-site-using-an-ftp-client-vb.md)教學課程示範如何使用獨立的 FTP 用戶端，將所需的檔案從開發環境複製到生產環境。 先前的教學課程[*使用 Visual Studio 部署您的網站*](deploying-your-site-using-visual-studio-vb.md)，並使用 Visual Studio 的複製網站工具和發佈選項來進行部署。 在兩個教學課程中，生產環境中的每個檔案都是開發環境上的檔案複本。 不過，實際執行環境中的設定檔與開發環境中的不同，並不罕見。 Web 應用程式的設定會儲存在 `Web.config` 檔案中，而且通常包含外部資源的相關資訊，例如資料庫、web 和電子郵件伺服器。 在某些情況下，它也會說明應用程式的行為，例如在未處理的例外狀況發生時所採取的動作。

部署 web 應用程式時，正確的設定資訊必須在生產環境中結束。 在大多數情況下，開發環境中的 `Web.config` 檔案無法依原樣複製到生產環境。 而是必須將自訂版本的 `Web.config` 上傳到生產環境。 本教學課程簡要回顧一些較常見的設定差異;它也會摘要說明在環境之間維護不同設定資訊的一些技術。

## <a name="typical-configuration-differences-between-the-development-and-production-environments"></a>開發與生產環境之間的一般設定差異

`Web.config` 檔案包含 ASP.NET 應用程式的各種設定資訊。 無論環境為何，這項設定資訊都是相同的。 比方說，不論環境為何，在 `Web.config` 檔案的 `<authentication>` 和 `<authorization>` 元素中拼出的驗證設定和 URL 授權規則通常都相同。 但是其他設定資訊（例如外部資源的相關資訊）通常會因環境而有所不同。

資料庫連接字串是根據環境而有所不同之設定資訊的主要範例。 當 web 應用程式與資料庫伺服器通訊時，必須先建立連接，並透過[連接字串](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)來達成此目的。 雖然可以直接在網頁或連接到資料庫的程式碼中硬式編碼資料庫連接字串，但最好將它放在 `Web.config`的[`<connectionStrings>` 元素](https://msdn.microsoft.com/library/bf7sd233.aspx)，以便連接字串資訊位於單一的集中位置。 在開發期間，通常會使用不同的資料庫，而不是在生產環境中使用;因此，每個環境的連接字串資訊都必須是唯一的。

> [!NOTE]
> 未來的教學課程探索如何部署資料驅動應用程式，此時我們將深入探討資料庫連接字串如何儲存在設定檔中的細節。

開發和生產環境的預期行為差異極大。 開發環境中的 web 應用程式是由一小組開發人員所建立、測試及進行調試。 在生產環境中，有許多不同的並行使用者正在造訪相同的應用程式。 ASP.NET 包含一些可協助開發人員測試和偵測應用程式的功能，但在生產環境中，這些功能應該基於效能和安全性理由而停用。 讓我們來看幾個這類的設定。

### <a name="configuration-settings-that-impact-performance"></a>會影響效能的設定

第一次造訪 ASP.NET 網頁時（或第一次變更之後），其宣告式標記必須轉換成類別，而且必須編譯此類別。 如果 web 應用程式使用自動編譯，則也需要編譯頁面的程式碼後置類別。 您可以透過 `Web.config` 檔案的[`<compilation>` 元素](https://msdn.microsoft.com/library/s10awwz0.aspx)來設定各種編譯選項。

Debug 屬性是 `<compilation>` 元素中最重要的屬性之一。 如果 `debug` 屬性設定為 "true"，則編譯的元件會包含在 Visual Studio 中對應用程式進行調試時所需的 debug 符號。 但是，在執行程式碼時，debug 符號會增加元件的大小，並強加額外的記憶體需求。 此外，當 `debug` 屬性設定為 "true" 時，`WebResource.axd` 所傳回的任何內容都不會進行快取，這表示每次使用者造訪頁面時，都必須重新下載 `WebResource.axd`所傳回的靜態內容。

> [!NOTE]
> `WebResource.axd` 是在 ASP.NET 2.0 中引進的內建 HTTP 處理常式，伺服器控制項可用來抓取內嵌的資源，例如腳本檔案、影像、CSS 檔案和其他內容。 如需 `WebResource.axd` 的運作方式，以及如何使用它從自訂伺服器控制項存取內嵌資源的詳細資訊，請參閱[使用 `WebResource.axd`透過 URL 存取內嵌資源](http://aspnet.4guysfromrolla.com/articles/080906-1.aspx)。

在開發環境中，`<compilation>` 元素的 `debug` 屬性通常會設定為 "true"。 事實上，此屬性必須設定為 "true"，才能進行 web 應用程式的偵錯工具。如果您嘗試從 Visual Studio 中偵測到 ASP.NET 應用程式，而且 `debug` 屬性設定為 "false"，Visual Studio 將會顯示一則訊息，說明在 `debug` 屬性設定為 "true" 之前，應用程式無法進行調試，並會提供給您進行這種變更。

您**絕對不**應該在生產環境中將 `debug` 屬性設為 "true"，因為它會對效能造成影響。 如需本主題的更完整討論，請參閱[Scott Guthrie](https://weblogs.asp.net/scottgu/)的 blog 文章，[不要執行生產 ASP.NET 應用程式並啟用 `debug="true"`](https://weblogs.asp.net/scottgu/442448)。

### <a name="custom-errors-and-tracing"></a>自訂錯誤和追蹤

當 ASP.NET 應用程式中發生未處理的例外狀況時，它會反升至執行時間，此時會發生三件事的其中一個：

- 隨即顯示一般執行階段錯誤訊息。 此頁面會通知使用者發生執行階段錯誤，但未提供任何有關錯誤的詳細資料。
- [例外狀況詳細資料] 訊息隨即顯示，其中包含剛剛擲回之例外狀況的資訊。
- [自訂錯誤] 頁面隨即顯示，這是您建立的 ASP.NET 網頁，會顯示您想要的任何訊息。

在發生未處理的例外狀況時，會發生什麼情況，取決於 `Web.config` 檔案的[`<customErrors>` 區段](https://msdn.microsoft.com/library/h0hfz6fc.aspx)。

開發和測試應用程式時，它有助於查看瀏覽器中任何例外狀況的詳細資料。 不過，在生產環境中顯示應用程式的例外狀況詳細資料是潛在的安全性風險。 此外，它也是 unflattering，讓您的網站看起來不夠專業。 在理想情況下，在發生未處理的例外狀況時，開發環境中的 web 應用程式將會顯示例外狀況的詳細資料，而生產環境中的相同應用程式將會顯示自訂錯誤頁面。

> [!NOTE]
> 預設 `<customErrors>` 區段設定只會在網頁透過 localhost 流覽時顯示例外狀況詳細資料訊息，否則會顯示 [一般執行時間錯誤] 頁面。 這不是理想的做法，但要知道預設行為並不會向非本機訪客顯示例外狀況詳細資料。 未來的教學課程會更詳細地檢查 `<customErrors>` 區段，並說明在生產環境中發生錯誤時，如何顯示自訂錯誤頁面。

在開發期間，另一個有用的 ASP.NET 功能是追蹤。 追蹤（啟用時）會記錄每個連入要求的相關資訊，並提供 `Trace.axd`的特殊網頁，以用於查看最近的要求詳細資料。 您可以透過 `Web.config`中的[`<trace>` 元素](https://msdn.microsoft.com/library/6915t83k.aspx)來開啟和設定追蹤。

如果您啟用追蹤，請確定它已在生產環境中停用。 由於追蹤資訊包括 cookie、會話資料和其他潛在的敏感性資訊，因此在生產環境中停用追蹤是很重要的。 好消息是，根據預設，會停用追蹤，而且只能透過 localhost 存取 `Trace.axd` 檔案。 如果您在開發中變更這些預設設定，請確定已在生產環境中將它們關閉。

## <a name="techniques-for-maintaining-separate-configuration-information"></a>維護個別設定資訊的技術

在開發和生產環境中擁有不同的設定，會使部署程式變得更複雜。 在前兩個教學課程中，部署程式牽涉到從開發中將所有必要的檔案複製到生產環境，但這種方法僅適用于這兩種環境中的設定資訊相同。 有各種不同的技術可讓您部署應用程式，並具有各種設定資訊。 讓我們為裝載的 web 應用程式，將其中一些選項分類。

### <a name="manually-deploying-the-production-environment-configuration-file"></a>手動部署生產環境設定檔

最簡單的方法是維護兩個版本的 `Web.config` 檔案：一個用於開發環境，另一個用於生產環境。 將網站部署到生產環境時，需要將所有檔案複製到開發環境中的實際執行伺服器，但 `Web.config` 檔案*除外*。 相反地，生產環境特定 `Web.config` 檔案會複製到生產環境。

這種方法並不複雜，但其實很容易實行，因為設定資訊不常變更。 它最適合具有小型開發小組的應用程式，裝載于單一 web 伺服器上，且其設定資訊不常變更。 當您使用獨立的 FTP 用戶端手動部署應用程式檔時，這是最 tenable 的。 使用 Visual Studio 的 [複製網站] 工具或 [發佈] 選項時，您必須先將部署特定的 `Web.config` 檔案與生產環境特定的檔案交換，然後再進行部署，然後在部署完成之後將它們交換回來。

### <a name="change-the-configuration-during-the-build-or-deployment-process"></a>在組建或部署過程中變更設定

到目前為止，我們已假設有臨機操作組建和部署程式。 許多較大型的軟體專案都有更正規化的程式，利用開放原始碼、家用成長或協力廠商工具。 針對這類專案，您可能會自訂群組建或部署程式，以便在將設定資訊推送至生產環境之前，適當地加以修改。 如果您使用[MSBuild](http://en.wikipedia.org/wiki/MSBuild)、 [NAnt](http://nant.sourceforge.net/)或其他組建工具來建立 web 應用程式，您可能會新增組建步驟來修改 `Web.config` 檔案，以包含生產環境特定的設定。 或者，您的部署工作流程可透過程式設計方式連接到原始檔控制伺服器，並取出適當的 `Web.config` 檔案。

取得適當設定資訊到生產環境的實際方法，會根據您的工具和工作流程而有很大的差異。 因此，我們不會進一步深入探討本主題。 如果您使用的是熱門的組建工具（例如 MSBuild 或 NAnt），您可以透過 web 搜尋找到這些工具的特定部署文章和教學課程。

### <a name="managing-configuration-differences-via-the-web-deployment-project-add-in"></a>透過 Web 部署專案增益集管理設定差異

在2006中，Microsoft 發行了適用于 Visual Studio 2005 的 Web 開發專案增益集。 Visual Studio 2008 的增益集已于2008發行。 此增益集可讓 ASP.NET 開發人員建立個別的 Web 部署專案，以及其 web 應用程式專案（在建立時）明確地編譯 web 應用程式，並複製要部署到本機輸出目錄的檔案。 Web 應用程式專案會在幕後使用 MSBuild。

根據預設，開發環境的 `Web.config` 檔案會複製到輸出目錄，但是您可以設定 Web 部署專案來自訂

以下列方式複製到此目錄的設定資訊：

- 透過 `Web.config` 檔案區段取代，您可以在其中指定要取代的區段，以及包含取代文字的 XML 檔案。
- 提供外部設定來源檔案的路徑。 選取此選項時，Web 部署專案會將特定的 `Web.config` 檔案複製到輸出目錄（而不是開發環境中所使用的 `Web.config` 檔案）。
- 藉由將自訂規則新增至 Web 部署專案所使用的 MSBuild 檔案。

若要部署 web 應用程式，請建立 Web 部署專案，然後將檔案從專案的輸出檔案夾複製到生產環境。

若要深入瞭解使用 Web 部署專案的詳細資訊，請參閱[這篇 Web 部署](https://msdn.microsoft.com/magazine/cc163448.aspx)專案： [MSDN 雜誌](https://msdn.microsoft.com/magazine/default.aspx)的2007年4月問題，或參考本教學課程結尾的進一步閱讀一節中的連結。

> [!NOTE]
> 您無法將 Web 部署專案與 Visual Web Developer 搭配使用，因為 Web 部署專案會實作為 Visual Studio 增益集，而 Visual Studio Express 版本（包括 Visual Web Developer）則不支援增益集。

## <a name="summary"></a>總結

在開發中，web 應用程式的外部資源和行為通常會與在生產環境中的相同應用程式不同。 例如，當未處理的例外狀況發生時，環境之間通常會有不同的資料庫連接字串、編譯選項和行為。 部署程式必須配合這些差異。 如我們在本教學課程中所討論，最簡單的方法是手動將替代的配置檔案複製到生產環境。 當使用 Web 部署專案增益集，或使用更正式的組建或部署程式來容納這類自訂時，可能會有更精緻的解決方案。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [已說明的連接字串](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)
- [資料庫連接字串 @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [請勿在啟用 `debug="true"` 的情況下執行生產 ASP.NET 應用程式](https://weblogs.asp.net/scottgu/Don_1920_t-run-production-ASP.NET-Applications-with-debug_3D001D20_true_1D20_-enabled)
- [正常回應未處理的例外狀況-顯示使用者易記的錯誤頁面](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [如何：使用 Visual Studio 2008 Web 部署專案？](../../../videos/how-do-i/how-do-i-use-a-visual-studio-2008-web-deployment-project.md)
- [部署資料庫時的金鑰設定](http://aspnet.4guysfromrolla.com/articles/121008-1.aspx)
- [Visual Studio 2008 Web 部署專案下載](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) | [Visual Studio 2005 Web 部署專案下載](https://download.microsoft.com/download/9/4/9/9496adc4-574e-4043-bb70-bc841e27f13c/WebDeploymentSetup.msi)
- [Vs 2008 Web 部署](https://weblogs.asp.net/scottgu/archive/2005/11/06/429723.aspx)專案 | [Vs 2008 Web 部署專案支援已發行](https://weblogs.asp.net/scottgu/archive/2008/01/28/vs-2008-web-deployment-project-support-released.aspx)
- [Web 部署專案](https://msdn.microsoft.com/magazine/cc163448.aspx)

> [!div class="step-by-step"]
> [上一頁](deploying-your-site-using-visual-studio-vb.md)
> [下一頁](core-differences-between-iis-and-the-asp-net-development-server-vb.md)
