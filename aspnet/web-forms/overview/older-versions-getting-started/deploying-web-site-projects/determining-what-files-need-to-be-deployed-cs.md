---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-cs
title: 判斷需要部署哪些檔案（C#） |Microsoft Docs
author: rick-anderson
description: 需要從開發環境部署到生產環境的檔案，取決於 ASP.NET 應用程式是否已建立我們 。
ms.author: riande
ms.date: 04/01/2009
ms.assetid: f8d78a88-cc91-40d8-bce3-3d7954f6033b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-cs
msc.type: authoredcontent
ms.openlocfilehash: 1dd4a1179d32f776626c08a07205dc9aabed588d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74596428"
---
# <a name="determining-what-files-need-to-be-deployed-c"></a>判斷需要部署哪些檔案 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_02_CS.zip)或[下載 PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial02_FilesToDeploy_cs.pdf)

> 需要從開發環境部署到生產環境的檔案，部分取決於 ASP.NET 應用程式是使用網站模型或 Web 應用程式模型所建立。 深入瞭解這兩個專案模型，以及專案模型如何影響部署。

## <a name="introduction"></a>簡介

部署 ASP.NET web 應用程式需要將 ASP.NET 相關的檔案從開發環境複製到生產環境。 與 ASP.NET 相關的檔案包括 ASP.NET 網頁標記和程式碼，以及用戶端和伺服器端的支援檔案。 用戶端支援檔案是指您的網頁所參考並直接傳送至瀏覽器的檔案，例如。 伺服器端支援檔案包括用來在伺服器端處理要求的檔案。 這包括設定檔案、web 服務、類別檔案、具類型的資料集，以及 LINQ to SQL 檔案，以及其他檔案。

一般來說，所有用戶端支援檔案都應該從開發環境複製到生產環境，但要複製哪些伺服器端支援檔案，取決於您是否要將伺服器端程式碼明確編譯成元件（`.dll` 檔案），還是要自動產生這些元件。 本教學課程會強調將程式碼明確編譯成元件時需要部署哪些檔案，而不會自動執行此編譯步驟。

## <a name="explicit-compilation-versus-automatic-compilation"></a>明確編譯與自動編譯

ASP.NET 的網頁會分成宣告式標記和原始程式碼。 宣告式標記部分包含 HTML、Web 控制項和資料系結語法;程式碼部分包含以 Visual Basic 或C#程式碼撰寫的事件處理常式。 標記和程式碼部分通常會分成不同的檔案： `WebPage.aspx` 包含宣告式標記，同時 `WebPage.aspx.cs` 裝載程式碼。

假設有一個名為 Clock 的 ASP.NET 網頁，其中包含一個標籤控制項，其 Text 屬性會設定為目前頁面載入的日期和時間。 宣告式標記部分（在 `Clock.aspx`中）會包含標籤 Web 控制項`<asp:Label runat="server" id="TimeLabel" />` 的標記，而程式碼部分（在 `Clock.aspx.cs`中）會有含有下列程式碼的 `Page_Load` 事件處理常式：

[!code-csharp[Main](determining-what-files-need-to-be-deployed-cs/samples/sample1.cs)]

為了讓 ASP.NET 引擎服務此頁面的要求，必須先編譯頁面的程式碼部分（`WebPage.aspx.cs` 檔案）。 這種編譯可以明確或自動進行。

如果明確地進行編譯，則會將整個應用程式的原始程式碼編譯成位於應用程式 `Bin` 目錄中的一或多個元件（`.dll` 檔案）。 如果編譯自動發生，則產生的自動產生元件預設會放在 [`Temporary ASP.NET` Files] 資料夾中，這可以在 `%WINDOWS%\Microsoft.NET\Framework\` *&lt;版本&gt;* 找到，雖然此位置可透過`<compilation>` 中的[`Web.config`元素](https://msdn.microsoft.com/library/s10awwz0.aspx)來設定。 使用明確編譯時，您必須採取一些動作，將 ASP.NET 應用程式的程式碼編譯成元件，並在部署之前進行此步驟。 使用自動編譯時，會在第一次存取資源時，在 web 伺服器上進行編譯器。

不論您使用何種編譯模型，所有 ASP.NET 網頁（`WebPage.aspx` 檔案）的標記部分都必須複製到生產環境。 使用明確編譯時，您必須複製 `Bin` 資料夾中的元件，但不需要複製 ASP.NET 網頁的程式碼部分（`WebPage.aspx.cs` 檔案）。 使用自動編譯時，您必須複製程式碼部分檔案，以便在流覽網頁時，可以自動編譯器代碼。 每個 ASP.NET 網頁的標記部分都包含一個 `@Page` 指示詞，其中含有指出頁面相關程式碼是否已明確編譯，或是否需要自動編譯的屬性。 因此，生產環境可以順暢地使用任一種編譯模型，而且您不需要套用任何特殊的設定，以表示使用明確或自動編譯。

[表 1] 摘要說明使用明確編譯與自動編譯時要部署的不同檔案。 請注意，不論使用何種編譯模型，如果該資料夾存在，您應該一律將元件部署在 `Bin` 資料夾中。 [`Bin`] 資料夾包含 web 應用程式特定的元件，其中包含使用明確編譯模型時的已編譯原始程式碼。 `Bin` 目錄也包含來自其他專案的元件，以及您可能使用的任何開放原始碼或協力廠商元件，而且這些元件必須在實際執行的伺服器上。 因此，根據一般經驗法則，在部署時，將 `Bin` 資料夾複製到生產環境。 （如果您使用自動編譯模型，而不是使用任何外部元件，那麼您就不會有 `Bin` 目錄-沒問題）。

| **編譯模型** | **要部署標記部分檔案嗎？** | **部署原始程式碼檔？** | **在 `Bin` 目錄中部署元件？** |
| --- | --- | --- | --- |
| 明確編譯 | 是 | 否 | 是 |
| 自動編譯 | 是 | 是 | 是（如果存在的話） |

**表1：** 您部署的檔案取決於所使用的編譯模型。

## <a name="taking-a-trip-down-memory-lane"></a>取得向下行程的記憶體路線

使用的編譯方法，部分取決於如何在 Visual Studio 中管理 ASP.NET 應用程式。 因此.NET 在2000年開始，有四個不同版本的 Visual Studio Visual Studio .NET 2002，Visual Studio .NET 2003、Visual Studio 2005 和 Visual Studio 2008。 使用*Web 應用程式專案模型*，Visual Studio .net 2002 和 2003 managed ASP.NET 應用程式。 Web 應用程式專案模型的主要功能包括：

- 構成專案的檔案會定義在單一專案檔中。 Visual Studio 不會將專案檔中定義的任何檔案視為 web 應用程式的一部分。
- 會使用明確的編譯。 建立專案時，會將專案內的程式碼檔案編譯成放在 `Bin` 資料夾中的單一元件。

當 Microsoft 發行 Visual Studio 2005 時，他們會捨棄對 Web 應用程式專案模型的支援，並將其取代為網站專案模型。 網站專案模型會以下列方式，從 Web 應用程式專案模型中區分其本身：

- 改為使用檔案系統，而不是擁有會將專案檔案拼出的單一專案檔案。 簡單地說，web 應用程式資料夾（或子資料夾）內的任何檔案都會被視為專案的一部分。
- 在 Visual Studio 中建立專案並不會在 `Bin` 目錄中建立元件。 相反地，建立網站專案會報告任何編譯時期錯誤。
- 支援自動編譯。 網站專案通常是藉由將標記和原始程式碼複製到實際執行環境來部署，雖然程式碼可以先行編譯（明確編譯）。

Microsoft 會在發行 Visual Studio 2005 Service Pack 1 時，恢復 Web 應用程式專案模型。 不過，Visual Web Developer 僅繼續支援網站專案模型。 好消息是，Visual Web Developer 2008 Service Pack 1 已捨棄這項限制。 現在您可以使用 Web 應用程式專案模型或網站專案模型，在 Visual Studio （和 Visual Web Developer）中建立 ASP.NET 應用程式。 這兩個模型都有其優缺點。 請參閱[Web 應用程式專案簡介：比較網站專案和 Web 應用程式專案](https://msdn.microsoft.com/library/aa730880.aspx#wapp_topic5)，以比較兩個模型，並協助決定哪一個專案模型最適合您的情況。

## <a name="exploring-the-sample-web-application"></a>探索範例 Web 應用程式

本教學課程的下載內容包含稱為「書籍評論」的 ASP.NET 應用程式。 此網站會模擬某人可能會建立的業餘愛好網站，以與線上社區分享他們的書籍評論。 這個 ASP.NET web 應用程式非常簡單，而且包含下列資源：

- `Web.config`，即應用程式的設定檔。
- 主版頁面（`Site.master`）。
- 七個不同的 ASP.NET 網頁： 

    - ~`/Default.aspx`-網站的首頁。
    - ~`/About.aspx`-「關於網站」頁面。
    - ~`/Fiction/Default.aspx`-一頁，列出已審核的小說書籍。 

        - ~`/Fiction/Blaze.aspx`-Richard Bachman novel *Blaze*的評論。
    - ~/`Tech/Default.aspx`-一頁列出已審核的技術書籍。 

        - ~/`Tech/CYOW.aspx`，請參閱*建立您自己的網站*。
        - ~/`Tech/TYASP35.aspx`-*在24小時內 ASP.NET 3.5*的審查。
- [樣式] 資料夾中有三個不同的 CSS 檔案。
- 四個影像檔案-由 ASP.NET 的標誌和三個已審核的書籍所涵蓋的影像，全都位於 [`Images`] 資料夾中。
- `Web.sitemap` 檔案，會定義網站地圖，並用來顯示根目錄的 `Default.aspx` 頁面中的功能表，以及 `Fiction` 和 `Tech` 資料夾。
- 名為 `BasePage.cs` 的類別檔案，會定義基底 `Page` 類別。 這個類別會根據網站對應中的頁面位置，自動設定 `Title` 屬性，以擴充 `Page` 類別的功能。 簡言之，延伸 `BasePage` （而不是 `System.Web.UI.Page`）的任何 ASP.NET 程式碼後置類別，其標題都會設定為值，視其在網站地圖中的位置而定。 例如，當您在流覽 ~/`Tech/CYOW.aspx` 頁面時，標題會設定為 "Home：技術：建立您自己的網站"。

[圖 1] 顯示透過瀏覽器觀看時，書籍審查網站的螢幕擷取畫面。 在這裡，您會看到頁面 ~/`Tech/TYASP35.aspx`，它會*在24小時內 ASP.NET 3.5*的評論。 橫跨頁面頂端的階層連結和左側資料行中的功能表，是以 `Web.sitemap`中定義的網站地圖結構為基礎。 右上角的影像是位於 [`Images`] 資料夾中的其中一個書籍封面影像。 網站的外觀和風格是透過 樣式 資料夾中的 CSS 檔案所拼出的級聯樣式表規則來定義，而 主要 頁面版面配置則是在主版頁面中定義，`Site.master`。

[![書籍評論網站提供關於標題的評論](determining-what-files-need-to-be-deployed-cs/_static/image2.png)](determining-what-files-need-to-be-deployed-cs/_static/image1.png)

**圖1：** 本書評論網站提供了一種標題的評論（[按一下以觀看完整大小的影像](determining-what-files-need-to-be-deployed-cs/_static/image3.png)）

此應用程式不會使用資料庫;每項審查都會實作為應用程式中的個別網頁。 本教學課程（和接下來的幾個教學課程）會逐步引導您部署沒有資料庫的 web 應用程式。 不過，在未來的教學課程中，我們將增強此應用程式，以在資料庫中儲存評論、讀者批註和其他資訊，並將探索需要執行哪些步驟來正確部署資料驅動 web 應用程式。

> [!NOTE]
> 這些教學課程著重于使用 web 主機提供者裝載 ASP.NET 應用程式，並不會探索如 ASP 的輔助主題。NET 的網站地圖系統，或使用基底 `Page` 類別。 如需這些技術的詳細資訊，以及本教學課程中涵蓋之其他主題的詳細背景，請參閱每個教學課程結尾處的進一步閱讀章節。

本教學課程的下載有兩份 web 應用程式，每個複本都實作為不同的 Visual Studio 專案類型： BookReviewsWAP、Web 應用程式專案和 BookReviewsWSP，也就是網站專案。 這兩個專案都是使用 Visual Web Developer 2008 SP1 所建立，並使用 ASP.NET 3.5 SP1。 若要使用這些專案，請先將內容解壓縮至您的桌面。 若要開啟 Web 應用程式專案（BookReviewsWAP），請流覽至 BookReviewsWAP 資料夾，然後按兩下方案檔，`BookReviewsWAP.sln`。 若要開啟網站專案（BookReviewsWSP），請啟動 Visual Studio，然後從 [檔案] 功能表中，選擇 [開啟網站] 選項，流覽至桌面上的 [`BookReviewsWSP`] 資料夾，然後按一下 [確定]。

本教學課程中的其餘兩節將探討部署應用程式時，您需要將哪些檔案複製到生產環境。 接下來的兩個教學課程- *[使用 FTP 部署您的網站](deploying-your-site-using-an-ftp-client-cs.md)* ，並 *[使用 Visual Studio 來部署您的網站](deploying-your-site-using-visual-studio-cs.md)* -顯示將這些檔案複製到 web 主機提供者的不同方式。

## <a name="determining-the-files-to-deploy-for-the-web-application-project"></a>判斷要為 Web 應用程式專案部署的檔案

Web 應用程式專案模型使用明確編譯-每次建立應用程式時，都會將專案的原始程式碼編譯成單一元件。 此編譯包含 ASP.NET 網頁的程式碼後置檔案（~/`Default.aspx.cs`、~/`About.aspx.cs`等等），以及 `BasePage.cs` 類別。 產生的元件名為 BookReviewsWAP，而且位於應用程式的 `Bin` 目錄中。

[圖 2] 顯示組成書籍審查 Web 應用程式專案的檔案。

[![方案總管列出組成 Web 應用程式專案的檔案](determining-what-files-need-to-be-deployed-cs/_static/image5.png)](determining-what-files-need-to-be-deployed-cs/_static/image4.png)

**圖 2**：方案總管列出組成 Web 應用程式專案的檔案

若要部署使用 Web 應用程式專案模型開發的 ASP.NET 應用程式，請先建立應用程式，以便將最新的原始程式碼明確編譯成元件。 接下來，將下列檔案複製到實際執行環境：

- 包含每個 ASP.NET 網頁之宣告式標記的檔案，例如 ~/`Default.aspx`、~/`About.aspx`等等。 此外，也請複製任何主版頁面和使用者控制項的宣告式標記。
- `Bin` 資料夾中的元件（`.dll` 檔案）。 您不需要複製程式資料庫檔案（`.pdb`）或您可以在 `Bin` 目錄中找到的任何 XML 檔案。

您不需要將 ASP.NET 網頁的原始程式碼檔案複製到生產環境，也不需要複製 `BasePage.cs` 類別檔案。

> [!NOTE]
> 如 [圖 2] 所示，`BasePage` 類別會實作為專案中的類別檔案，放在名為 `HelperClasses`的資料夾中。 當編譯專案時，會將 `BasePage.cs` 檔案中的程式碼連同 ASP.NET 網頁的程式碼後置類別一起編譯成單一元件，`BookReviewsWAP.dll.` ASP.NET 具有一個名為 `App_Code` 的特殊資料夾，其設計目的是要保存網站專案的類別檔案。 [`App_Code`] 資料夾中的程式碼會自動編譯，因此不應該與 Web 應用程式專案一起使用。 相反地，您應該將應用程式的類別檔案放在名為 `HelperClasses`的一般資料夾中，或 `Classes`或類似的專案。 或者，您可以將類別檔案放在不同的類別庫專案中。

除了將 ASP.NET 相關的標記檔案和元件複製到 `Bin` 資料夾中，您還需要複製用戶端支援檔案（影像和 CSS 檔案），以及其他伺服器端支援檔案，`Web.config` 和 `Web.sitemap`。 無論您使用的是明確或自動編譯，都必須將這些用戶端和伺服器端的支援檔案複製到生產環境。

## <a name="determining-the-files-to-deploy-for-the-web-site-project-files"></a>判斷要為網站專案檔案部署的檔案

網站專案模型支援自動編譯，這是使用 Web 應用程式專案模型時無法使用的功能。 使用明確編譯時，您必須將專案的原始程式碼編譯成元件，並將該元件複製到生產環境。 另一方面，使用自動編譯時，您只需將原始程式碼複製到生產環境，它會視需要由執行時間依需求編譯。

Visual Studio 中的 [組建] 功能表選項會出現在 Web 應用程式專案和網站專案中。 建立 Web 應用程式專案會將專案的原始程式碼編譯成位於 `Bin` 目錄中的單一元件;建立網站專案會檢查是否有任何編譯時期錯誤，但不會建立任何元件。 若要部署使用網站專案模型開發的 ASP.NET 應用程式，您只需要將適當的檔案複製到生產環境，但建議您先建立專案，以確保不會發生編譯時期錯誤。

[圖 3] 顯示組成書籍評論網站專案的檔案。

 [![方案總管列出組成網站專案的檔案](determining-what-files-need-to-be-deployed-cs/_static/image7.png)](determining-what-files-need-to-be-deployed-cs/_static/image6.png) 

**圖 3**：方案總管列出組成網站專案的檔案

部署網站專案涉及將所有 ASP.NET 相關檔案複製到生產環境中，包括 ASP.NET 網頁的標記頁面、主版頁面和使用者控制項，以及其程式碼檔案。 您也需要複製任何類別檔案，例如 BasePage.cs。 請注意，`BasePage.cs` 檔案位於 [`App_Code`] 資料夾中，這是在類別檔案的網站專案中使用的特殊 ASP.NET 資料夾。 您也必須在生產環境上建立特殊資料夾，因為開發環境上 [`App_Code`] 資料夾中的類別檔案必須複製到實際執行上的 [`App_Code`] 資料夾。

除了複製 ASP.NET 標記和原始程式碼檔案之外，您還需要複製用戶端支援檔案（影像和 CSS 檔案），以及其他伺服器端支援檔案，`Web.config` 和 `Web.sitemap`。

> [!NOTE]
> 網站專案也可以使用明確的編譯。 未來的教學課程將探討如何明確編譯網站專案。

## <a name="summary"></a>總結

部署 ASP.NET 應用程式需要將必要的檔案從開發環境複製到生產環境。 需要同步處理的一組精確檔案，取決於 ASP.NET 應用程式的程式碼是明確或自動編譯。 所採用的編譯策略會受到 Visual Studio 是否設定為使用 Web 應用程式專案模型或網站專案模型來管理 ASP.NET 應用程式。

Web 應用程式專案模型使用明確編譯，並將專案的程式碼編譯成 `Bin` 資料夾中的單一元件。 部署應用程式時，ASP.NET 網頁的標記部分和 `Bin` 資料夾的內容必須推送至生產環境;應用程式中的原始程式碼（例如程式碼檔案和程式碼後置類別）不需要複製到生產環境。

網站專案模型預設會使用自動編譯，雖然可以明確編譯網站專案，但我們將在未來的教學課程中看到。 部署使用自動編譯的 ASP.NET 應用程式時，必須將標記部分*和*原始程式碼複製到生產環境。 第一次要求時，程式碼會在生產環境中自動編譯。

既然我們已經檢查過哪些檔案需要在開發與生產環境之間同步處理，我們就準備好要將本書審查應用程式部署到 web 主機提供者。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ASP.NET 編譯總覽](https://msdn.microsoft.com/library/ms178466.aspx)
- [ASP.NET 使用者控制項](https://msdn.microsoft.com/library/y6wb1a0e.aspx)
- [檢查 ASP。NET 的網站流覽](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [Web 應用程式專案簡介](https://msdn.microsoft.com/library/aa730880.aspx)
- [主版頁面教學課程](../master-pages/creating-a-site-wide-layout-using-master-pages-cs.md)
- [在頁面之間共用程式碼](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/pages/code.aspx)
- [針對 ASP.NET 網頁的程式碼後置類別使用自訂基類](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)
- [Visual Studio 2005 的網站專案系統：這是什麼？為什麼要這麼做？](https://weblogs.asp.net/scottgu/archive/2005/08/21/423201.aspx)
- [逐步解說：在 Visual Studio 中將網站專案轉換成 Web 應用程式專案](https://msdn.microsoft.com/library/aa983476.aspx)

> [!div class="step-by-step"]
> [上一頁](asp-net-hosting-options-cs.md)
> [下一頁](deploying-your-site-using-an-ftp-client-cs.md)
