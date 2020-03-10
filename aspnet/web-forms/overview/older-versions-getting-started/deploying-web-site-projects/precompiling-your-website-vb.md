---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/precompiling-your-website-vb
title: 先行編譯您的網站（VB） |Microsoft Docs
author: rick-anderson
description: Visual Studio 為 ASP.NET 的開發人員提供兩種類型的專案： Web 應用程式專案（Wap）和網站專案（WSPs）。 其中一個主要差異 betwe 。
ms.author: riande
ms.date: 06/09/2009
ms.assetid: c285dc6f-a1c6-46e6-ac03-3830947f57e3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/precompiling-your-website-vb
msc.type: authoredcontent
ms.openlocfilehash: 1a46870b73f95300ef5bc1f72dda74d7d62ab11f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627845"
---
# <a name="precompiling-your-website-vb"></a>預先編譯您的網站 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_15_VB.zip)或[下載 PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial15_Precompiling_vb.pdf)

> Visual Studio 為 ASP.NET 的開發人員提供兩種類型的專案： Web 應用程式專案（Wap）和網站專案（WSPs）。 這兩種專案類型之間的主要差異之一，是 Wap 必須在部署之前先明確編譯器代碼，而 WSP 中的程式碼可以在 web 伺服器上自動編譯。 不過，您可以先行編譯 WSP，再進行部署。 本教學課程會探索先行編譯的優點，並示範如何從 Visual Studio 和命令列中先行編譯網站。

## <a name="introduction"></a>簡介

Visual Studio 為 ASP.NET 的開發人員提供兩種不同的專案類型： Web 應用程式專案（WAP）和網站專案（WSP）。 這些專案類型之間的其中一個主要差異在於，Wap 需要*明確編譯*，而 WSPs 預設會使用*自動編譯*。 透過 Wap，您可以將 web 應用程式的程式碼編譯成單一元件，並在網站的 [`Bin`] 資料夾中建立。 部署需要複製專案中的標記內容（`.aspx.ascx`和 `.master` 檔案），以及 `Bin` 資料夾中的元件;程式碼後置類別檔案本身不需要部署。 另一方面，您可以將標記頁面及其對應的程式碼後置類別複製到實際執行環境，藉以部署 WSPs。 程式碼後置類別會視需要在網頁伺服器上編譯。

> [!NOTE]
> 請回到[*判斷需要部署哪些*檔案教學](determining-what-files-need-to-be-deployed-vb.md)課程中的「明確編譯與自動編譯」一節，以取得有關專案模型、明確和自動編譯之間的差異，以及編譯模型如何影響部署的背景資訊。

自動編譯選項很容易使用。 沒有明確的編譯步驟，而且只需要部署已修改的檔案，而明確編譯則必須部署已變更的標記頁面和剛剛編譯的元件。 不過，自動部署有兩個可能的缺點：

- 因為頁面必須在第一次造訪時自動編譯，所以在部署後第一次要求 ASP.NET 網頁時，可能會出現短暫但明顯的延遲。
- 自動編譯需要在 web 伺服器上同時存在宣告式標記和原始程式碼。 如果您計畫將 web 應用程式銷售給將在其 web 伺服器上安裝的客戶，這可能是不討喜選項。

如果上述兩個缺點的其中一個是交易斷路器，您可以切換到 WAP 模型，或在部署之前先行*編譯*WSP。 本教學課程會檢查最適合裝載網站的先行編譯選項，並逐步解說先行編譯的網站先行編譯流程和部署。

## <a name="an-overview-of-aspnet-code-generation-and-compilation"></a>ASP.NET 程式碼產生和編譯的總覽

在查看可用的先行編譯選項之前，讓我們先討論第一次要求 ASP.NET 網頁，因為它是在建立或上次更新之後所發生的程式碼產生和編譯。 如您所知，ASP.NET 網頁是由兩個部分組成： `.aspx` 檔案中的宣告式標記;和原始程式碼部分，通常是在不同的程式碼後置類別檔案（`.aspx.vb`）中。 當要求 ASP.NET 網頁時，執行時間所執行的步驟取決於應用程式的編譯模型。

使用 Wap 時，必須先將頁面的原始程式碼明確編譯成單一元件，然後再進行部署。 在部署期間，會將此元件和各種標記頁面複製到生產環境。 當要求抵達 ASP.NET 網頁的 web 伺服器時，執行時間會建立頁面程式碼後置類別的實例，並叫用它的 `ProcessRequest` 方法，這會啟動頁面生命週期，最後會產生頁面的內容，並傳回給要求者。 執行時間可以與 ASP.NET 網頁的程式碼後置類別搭配使用，因為程式碼後置類別已經在部署之前編譯成元件。

透過 WSPs 和自動編譯，在部署之前，不會有明確的編譯步驟。 相反地，部署牽涉到將宣告式和原始程式碼內容複寫到生產環境。 當要求在網頁建立或上次更新後第一次抵達 web 伺服器以取得 ASP.NET 網頁時，執行時間必須先將程式碼後置類別編譯成元件。 這個已編譯的元件會儲存在 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files`資料夾中，不過這個資料夾的位置可以透過 `Web.config`中的 `<pages>` 元素自訂。 因為元件會儲存至磁片，所以不需要在對相同頁面的後續要求中重新編譯。

> [!NOTE]
> 如您所預期，第一次要求頁面時（或在第一次變更之後）在使用自動編譯的網站中，因為伺服器需要一些時間來編譯頁面的程式碼，並將產生的元件儲存到，所以會有些許延遲硬碟.

簡單地說，使用明確編譯時，您必須在部署之前編譯網站的原始程式碼，讓執行時間不需要執行該步驟。 使用自動編譯時，執行時間會處理頁面原始程式碼的編譯，但從建立或上次更新以來，第一次造訪網頁時，會稍微初始化成本。

但是，ASP.NET 網頁的宣告式部分（`.aspx` 檔案）呢？ 很明顯地，在程式碼後置類別中，`.aspx` 檔案和程式碼之間有關聯性，因為宣告式標記中定義的 Web 控制項可在程式碼中存取。 也很明顯地，`.aspx` 檔案中的內容會大幅影響網頁所產生的轉譯標記。 那麼，執行時間如何搭配 `.aspx` 檔案中定義的文字、HTML 和 Web 控制項語法，來產生要求的網頁轉譯內容呢？

我不想延宕低層級的執行詳細資料，這會因 Wap 和 WSPs 而有所不同，但簡言之，執行時間會自動產生類別檔案，其中包含各種 Web 控制項做為受保護的成員和方法。 這個產生的檔案會實作為對應程式碼後置類別的*部分類別*。 （[部分類別](http://www.dotnet-guide.com/partialclasses.html)允許將單一類別的內容分散到多個檔案）。因此，程式碼後置類別是在兩個地方定義：在您建立的 `.aspx.vb` 檔案中，以及執行時間所建立的這個自動產生的類別中。 這個自動產生的類別會儲存在 [`%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files`] 資料夾中。

這裡的重點是，在執行時間轉譯 ASP.NET 網頁時，其宣告式和原始程式碼部分都必須編譯成元件。 使用 Wap 時，會在部署之前將原始程式碼明確編譯成元件，但是宣告式標記仍然必須轉換成程式碼，並由 web 伺服器上的執行時間編譯。 使用自動編譯的 WSPs，原始程式碼和宣告式標記都必須由 web 伺服器編譯。

您可以搭配使用明確編譯與 WSP 模型。 您可以明確地編譯原始程式碼部分，就像使用 WAP 模型一樣。 此外，您也可以編譯宣告式標記。

## <a name="precompilation-options"></a>先行編譯選項

.NET Framework 隨附[ASP.NET 編譯工具（`aspnet_compiler.exe`）](https://msdn.microsoft.com/library/ms229863.aspx) ，可讓您編譯使用 WSP 模型所建立之 ASP.NET 應用程式的原始程式碼（甚至是內容）。 這項工具是以 .NET Framework 版本2.0 發行，位於 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727` 資料夾中;您可以從命令列使用它，或透過 [建立] 功能表的 [發行網站] 選項，從 Visual Studio 中啟動。

編譯工具提供兩種一般的編譯形式：就地先行編譯和先行編譯以進行部署。 使用就地先行編譯時，您可以從命令列執行 `aspnet_compiler.exe` 工具，並指定虛擬目錄的路徑或位於電腦上之網站的實體路徑。 然後，編譯工具會編譯專案中的每個 ASP.NET 網頁，將編譯過的版本儲存在 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files` 資料夾中，就像是第一次從瀏覽器造訪每個頁面一樣。 就地先行編譯可以加速對您網站上新部署的 ASP.NET 網頁提出的第一個要求，因為它會減輕執行時間不需要執行此步驟。 不過，對於大部分裝載的網站而言，就地先行編譯並不實用，因為它需要您能夠從 web 伺服器的命令列執行程式。 在共用主控環境中，不允許此層級的存取。

> [!NOTE]
> 如需就地先行編譯的詳細資訊，請參閱如何：[在 ASP.NET 2.0](http://www.odetocode.com/Articles/417.aspx)中先行[編譯 ASP.NET 網站](https://msdn.microsoft.com/library/ms227972.aspx)和先行編譯。

部署的先行編譯不會將網站中的頁面編譯為 `Temporary ASP.NET Files` 資料夾，而是將頁面編譯成您選擇的目錄，並以可部署到生產環境的格式。

我們在本教學課程中探索的部署有兩種先行編譯的類型：使用可更新的使用者介面先行編譯，以及使用不可更新的使用者介面先行編譯。 具有可更新之使用者介面的先行編譯會將宣告式標記保留在 `.aspx`、`.ascx`和 `.master` 檔案中，因此可讓開發人員視需要修改實際伺服器上的宣告式標記。 具有不可更新之使用者介面的先行編譯會產生任何內容的 `.aspx` 頁面，並移除 `.ascx` 和 `.master` 的檔案，藉此隱藏宣告式標記並禁止開發人員從生產環境進行變更。

### <a name="precompiling-for-deployment-with-an-updatable-user-interface"></a>使用可更新的使用者介面進行部署的先行編譯

瞭解部署先行編譯的最佳方式，就是查看作用中的範例。 讓我們先行編譯本書審查 WSP，以使用可更新的使用者介面進行部署。 您可以從 Visual Studio 的 [建立] 功能表或從命令列叫用 ASP.NET 編譯工具。 本節將探討如何在 Visual Studio 中使用此工具;「從命令列先行編譯」一節會查看從命令列執行編譯器工具。

在 Visual Studio 中開啟 [書籍審查] WSP，移至 [建立] 功能表，然後選取 [發行網站] 功能表選項。 這會啟動 [發行網站] 對話方塊（請參閱 [**圖 1**]），您可以在其中指定目標位置、是否可更新先行編譯網站的使用者介面，以及其他編譯器工具選項。 目標位置可以是遠端 web 伺服器或 FTP 伺服器，但現在請選擇您電腦硬碟上的資料夾。 因為我們想要使用可更新的使用者介面先行編譯網站，請勾選 [允許此先行編譯網站成為可更新] 核取方塊，然後按一下 [確定]。

[![](precompiling-your-website-vb/_static/image2.png)](precompiling-your-website-vb/_static/image1.png)

**圖 1**： ASP.NET 編譯工具會將您的網站先行編譯到指定的目標位置  
 （[按一下以查看完整大小的影像](precompiling-your-website-vb/_static/image3.png)）

> [!NOTE]
> Visual Web Developer 無法使用 [建立] 功能表中的 [發行網站] 選項。 如果您使用的是 Visual Web Developer，就必須使用命令列版本的 ASP.NET 編譯工具，其涵蓋于「從命令列先行編譯」一節。

先行編譯網站之後，流覽至您在 [發行網站] 對話方塊中輸入的目標位置。 請花點時間比較此資料夾的內容與您網站的內容。 [**圖 2** ] 顯示書籍審查網站資料夾。 請注意，它同時包含 `.aspx` 和 `.aspx.cs` 檔案。 另請注意，`Bin` 目錄只包含一個檔案，`Elmah.dll`，我們在[上一個教學](logging-error-details-with-elmah-vb.md)課程中新增此檔案

[![](precompiling-your-website-vb/_static/image5.png)](precompiling-your-website-vb/_static/image4.png)

**圖 2**：專案目錄包含 `.aspx` 和 `.aspx.cs` 檔案;[`Bin`] 資料夾僅包含 `Elmah.dll`  
 （[按一下以查看完整大小的影像](precompiling-your-website-vb/_static/image6.png)）

[**圖 3** ] 顯示 ASP.NET 編譯工具所建立之內容的目標位置資料夾。 此資料夾未包含任何程式碼後置檔案。 此外，這個資料夾的 `Bin` 目錄除了 `Elmah.dll` 元件以外，還包含了數個元件和兩個 `.compiled` 檔案。

[![](precompiling-your-website-vb/_static/image8.png)](precompiling-your-website-vb/_static/image7.png)

**圖 3**：目標位置資料夾包含要部署的檔案  
 （[按一下以查看完整大小的影像](precompiling-your-website-vb/_static/image9.png)）

不同于 Wap 中的明確編譯，部署程式的先行編譯不會為整個網站建立一個元件。 相反地，它會將數個頁面分批組成每個元件。 它也會將 `Global.asax` 檔案（如果有的話）編譯成它自己的元件，以及 `App_Code` 資料夾中的任何類別。 保存 ASP.NET 網頁、使用者控制項和主版頁面（分別是`.aspx`、`.ascx`和 `.master` 檔案）之宣告式標記的檔案，會依原樣複製到目標位置目錄。 同樣地，也會直接複製 `Web.config` 檔案，連同任何靜態檔案（例如影像、CSS 類別和 PDF 檔案）。 如需編譯工具如何處理各種檔案類型的更正式描述，請參閱[ASP.NET 先行編譯期間](https://msdn.microsoft.com/library/e22s60h9.aspx)的檔案處理。

> [!NOTE]
> 您可以藉由從 [發行網站] 對話方塊中選取 [已使用的固定命名和單一頁面元件] 核取方塊，指示編譯工具為每個 ASP.NET 網頁、使用者控制項或主版頁面建立一個元件。 將每個 ASP.NET 網頁編譯成自己的元件，可讓您更精細地控制部署。 例如，如果您更新了單一 ASP.NET 網頁，而且需要部署該變更，您只需要將該頁面的 `.aspx` 檔案和相關聯的元件部署到生產環境。 如需詳細資訊，請參閱[如何：使用 ASP.NET 編譯工具產生固定的名稱](https://msdn.microsoft.com/library/ms228040.aspx)。

目標位置目錄也包含不屬於先行編譯 Web 專案的檔案，亦即 `PrecompiledApp.config`。 此檔案會通知 ASP.NET 執行時間，應用程式已先行編譯，以及是否使用可更新或可更新的 UI 先行編譯。

最後，使用 Visual Studio 或您選擇的文字編輯器，花一點時間開啟目標位置中的其中一個 `.aspx` 檔案。 使用可更新的使用者介面進行先行編譯時，目標位置目錄中的 ASP.NET 網頁會包含與網站中對應檔案完全相同的標記。

### <a name="precompiling-for-deployment-with-a-non-updatable-user-interface"></a>使用不可更新的使用者介面進行預先編譯以進行部署

ASP.NET 編譯器工具也可以用來先行編譯網站，以使用無法更新的 UI 進行部署。 使用不可更新的 UI 先行編譯網站，其運作方式很像是使用可更新的 UI 先行編譯，主要差異在於目標目錄中的 ASP.NET 網頁、使用者控制項和主版頁面會移除其標記。 若要使用無法更新的 UI 先行編譯網站以進行部署，請從 [建立] 功能表選擇 [發行網站] 選項，但取消核取 [允許此先行編譯的網站可以更新] 選項（請參閱 [**圖 4**]）。

[![](precompiling-your-website-vb/_static/image11.png)](precompiling-your-website-vb/_static/image10.png)

**圖 4**：取消核取 [允許此先行編譯網站成為可更新的] 選項，以使用無法更新的 UI 進行先行編譯  
 （[按一下以查看完整大小的影像](precompiling-your-website-vb/_static/image12.png)）

[**圖 5** ] 顯示使用不可更新的使用者介面先行編譯之後的目標位置資料夾。

[![](precompiling-your-website-vb/_static/image14.png)](precompiling-your-website-vb/_static/image13.png)

**圖 5**：使用不可更新的 UI 進行部署的目標位置資料夾  
 （[按一下以查看完整大小的影像](precompiling-your-website-vb/_static/image15.png)）

請比較 [**圖 3** ] 到 [**圖 5**]。 雖然兩個資料夾看起來可能完全相同，但請注意，不可更新的 UI 資料夾缺少主版頁面，`Site.master`。 雖然 [**圖 5** ] 包含各種 ASP.NET 網頁，但如果您要查看這些檔案的內容，您會看到它們已移除其宣告式標記，並以預留位置文字取代：「這是先行編譯工具所產生的標記檔案，不應該刪除！」

[![](precompiling-your-website-vb/_static/image17.png)](precompiling-your-website-vb/_static/image16.png)

**圖 5**：已從 ASP.NET 網頁移除宣告式標記

[**圖 3** ] 和 [ **5** ] 中的 [`Bin`] 資料夾明顯不同。 除了元件之外，[**圖 5** ] 中的 [`Bin`] 資料夾還包含每個 ASP.NET 網頁、使用者控制項和主版頁面的 `.compiled` 檔案。

當您不想要在生產環境中安裝或管理網站的人員或公司修改 ASP.NET 網頁的內容時，以不可更新的 UI 先行編譯網站非常有用。 如果您建立一個 ASP.NET web 應用程式來銷售給客戶，以便安裝在自己的網頁伺服器上，您可能會想要確保他們不會藉由直接編輯您寄送的 `.aspx` 頁面來修改網站的外觀與風格。 藉由使用不可更新的 UI 先行編譯您的網站，您會在安裝時將預留位置 `.aspx` 頁面中寄送，藉此防止客戶檢查或修改其內容。

### <a name="precompiling-from-the-command-line"></a>從命令列先行編譯

在幕後，Visual Studio 的 [發行網站] 對話方塊會叫用 ASP.NET 編譯工具（`aspnet_compiler.exe`）以先行編譯網站。 或者，您也可以從命令列叫用此工具。 事實上，如果您使用 Visual Web Developer，就必須從命令列執行編譯器工具，因為 Visual Web Developer 的 [組建] 功能表並未包含 [發行網站] 選項。

若要從命令列使用編譯器工具，請先卸載至命令列，然後流覽至架構目錄，`%WINDIR%\Microsoft.NET\Framework\v2.0.50727`。 接下來，在命令列中輸入下列語句：

`aspnet_compiler -p "physical_path_to_app" -v / -f -u "target_location_folder"`

上述命令會啟動 ASP.NET 編譯器工具（`aspnet_compiler.exe`），並透過 `-p` 參數，指示它將根目錄為*實體\_路徑\_的網站先行編譯成\_應用程式*;這個值會類似 `C:\MySites\BookReviews`，而且應該以引號分隔。

`-v` 參數會指定網站的虛擬目錄。 如果您的網站註冊為 IIS 元資料庫中的預設網站，則您可以省略 `-p` 參數，並只指定應用程式的虛擬目錄。 如果您使用 `-p` 參數，則繼續 `-v` 參數的值會指出網站的根目錄，並且用來解析應用程式根目錄參考。 比方說，如果您指定 `-v /MySite` 的值，則應用程式中的參考將會解析為 `~/MySite/path/file``~/path/file`。 因為書籍審查網站位於我的 web 主控公司的根目錄，所以我使用了參數 `-v /`。

`-f` 參數（如果有的話）會指示編譯工具覆寫*目標\_位置\_資料夾*目錄（如果已經存在）。 如果您省略 `-f` 參數，而且目標位置資料夾已經存在，編譯工具將會結束，並出現錯誤：「錯誤 ASPRUNTIME：目標目錄不是空的。 請手動將其刪除，或選擇不同的目標。」

`-u` 參數（如果有的話）會通知工具建立可更新的使用者介面。 省略此參數，可使用不可更新的使用者介面先行編譯網站。

最後，*目標\_位置\_資料夾*是目標位置目錄的實體路徑;這個值會類似 `C:\MySites\Output\BookReviews`，而且應該以引號分隔。

## <a name="deploying-the-precompiled-website"></a>部署先行編譯的網站

此時，我們已瞭解如何使用 ASP.NET 編譯工具，使用可更新和不可更新的使用者介面選項先行編譯網站。 不過，我們的範例目前已將網站先行編譯到本機資料夾，而不是實際執行環境。 好消息是，部署先行編譯的網站非常簡單，可以透過 Visual Studio 或透過一些其他檔案複製機制來完成，例如從獨立的 FTP 用戶端。

[發行網站] 對話方塊（如 [**圖 1**] 所示）具有 [目標位置] 選項，可指出將先行編譯的網站檔案複製到何處。 這個位置可以是遠端 web 伺服器或 FTP 伺服器。 在此文字方塊中輸入遠端伺服器會在一個步驟中預先編譯並將網站部署至指定的伺服器。 或者，您也可以將網站先行編譯到本機資料夾，然後透過 FTP 或其他方法，手動將該資料夾的內容複寫到生產環境。

透過 Visual Studio 的 [發行網站] 對話方塊自動部署的先行編譯網站，對於開發與生產環境之間沒有任何設定差異的簡單網站很有説明。 不過，如[*開發與生產*教學](common-configuration-differences-between-development-and-production-vb.md)課程的一般設定差異中所述，這類差異並不常見。 例如，書籍審查 web 應用程式在生產環境中使用的資料庫與開發環境中的不同。 當 Visual Studio 將網站發佈到遠端伺服器時，它會在開發環境中將設定檔資訊複製到其中。

對於在開發與生產環境之間有設定差異的網站，最好是將網站先行編譯到本機目錄，再複製實際執行的設定檔案，然後將先行編譯輸出的內容複寫到生產.

如需將檔案從開發環境複製到生產環境的重新整理程式，請參閱[*使用 FTP 用戶端部署您的網站*](deploying-your-site-using-an-ftp-client-vb.md)和使用 Visual Studio 教學課程來[*部署您的網站*](determining-what-files-need-to-be-deployed-vb.md)。

## <a name="summary"></a>總結

ASP.NET 支援兩種編譯模式：自動和明確。 如先前的教學課程所述，Web 應用程式專案（Wap）會使用明確編譯，而網站專案（WSPs）預設會使用自動編譯。 不過，您可以使用 ASP.NET 編譯工具，在部署之前明確編譯 WSP。

本教學課程著重于編譯工具針對部署支援的先行編譯。 當先行編譯部署時，編譯工具會建立目標位置資料夾、編譯指定的 web 應用程式的原始程式碼，並將這些已編譯的元件和內容檔案複製到目標位置資料夾。 您可以設定編譯工具來建立可更新或不可更新的使用者介面。 使用不可更新的使用者介面選項進行先行編譯時，會移除內容檔案中的宣告式標記。 簡言之，預先編譯可讓您部署網站專案型應用程式，而不需要包含任何原始程式碼檔，並視需要移除宣告式標記。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ASP.NET 網站先行編譯](https://msdn.microsoft.com/library/ms228015.aspx)
- [ASP.NET 2.0 中的後置和編譯](https://msdn.microsoft.com/magazine/cc163675.aspx)
- [ASP.NET 中的先行編譯](http://www.odetocode.com/Articles/417.aspx)
- [ASP.NET 中的先行編譯網站選項](http://www.dotnetperls.com/precompiled)

> [!div class="step-by-step"]
> [上一頁](logging-error-details-with-elmah-vb.md)
> [下一頁](users-and-roles-on-the-production-website-vb.md)
