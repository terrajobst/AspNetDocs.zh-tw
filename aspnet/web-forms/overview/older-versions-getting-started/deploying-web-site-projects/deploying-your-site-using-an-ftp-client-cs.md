---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-cs
title: 使用 FTP 用戶端部署您的網站C#（） |Microsoft Docs
author: rick-anderson
description: 部署 ASP.NET 應用程式最簡單的方式，就是將必要的檔案從開發環境手動複製到生產環境。 .。
ms.author: riande
ms.date: 04/01/2009
ms.assetid: a3599cf7-8474-4006-954a-3bc693736b66
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-cs
msc.type: authoredcontent
ms.openlocfilehash: a3474650939ee220b3fd712e9f5a6cf3db11db09
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78545588"
---
# <a name="deploying-your-site-using-an-ftp-client-c"></a>使用 FTP 用戶端部署您的網站 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_03_CS.zip)或[下載 PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial03_DeployingViaFTP_cs.pdf)

> 部署 ASP.NET 應用程式最簡單的方式，就是將必要的檔案從開發環境手動複製到生產環境。 本教學課程示範如何使用 FTP 用戶端，將檔案從您的桌面取得到 web 主機提供者。

## <a name="introduction"></a>簡介

先前的教學課程引進了簡單的書籍審核 ASP.NET web 應用程式，其中包含幾個 ASP.NET 網頁、主版頁面、自訂基底 `Page` 類別、許多影像，以及三個 CSS 樣式表單。 我們現在已準備好要將此應用程式部署到 web 主機提供者，而該應用程式將可供連線到網際網路的任何人存取！

從我們在[*判斷需要部署哪些*](determining-what-files-need-to-be-deployed-cs.md)檔案教學課程的討論中，我們知道需要將哪些檔案複製到 web 主機提供者。 （回想一下，要複製哪些檔案取決於您的應用程式是明確或自動編譯）。但是，我們要如何從開發環境（桌面）到生產環境（由 web 主機提供者管理的 web 伺服器）取得檔案？ [ **F** Ile **T** ransfer **P** rotocol （FTP）](http://en.wikipedia.org/wiki/File_Transfer_Protocol)是常用的通訊協定，可透過網路將檔案從一部電腦複製到另一部機器。 另一個選項是 FrontPage Server Extensions （FPSE）。 本教學課程著重于使用獨立的 FTP 用戶端軟體，將必要的檔案從開發環境部署到生產環境。

> [!NOTE]
> Visual Studio 包含透過 FTP 發佈網站的工具;下一個教學課程將涵蓋這些工具，以及使用 FPSE 的工具。

若要使用 FTP 複製檔案，我們需要在開發環境上有*FTP 用戶端*。 FTP 用戶端是設計用來將檔案從電腦安裝到執行*FTP 伺服器*之電腦的應用程式。 （如果您的 web 主機提供者支援透過 FTP 的檔案傳輸，那麼就是在其網頁伺服器上執行的 FTP 伺服器）。有許多可用的 FTP 用戶端應用程式。 您的網頁瀏覽器甚至可以兩倍的 FTP 用戶端。 我最愛的 FTP 用戶端，以及我將在本教學課程中使用的是[FileZilla](http://filezilla-project.org/)，這是適用于 Windows、Linux 和 mac 的免費開放原始碼 ftp 用戶端。 不過，所有的 FTP 用戶端都可以使用，因此，您可以隨意使用您最熟悉的任何用戶端。

如果您跟著做，則必須先建立具有 web 主機提供者的帳戶，才能完成本教學課程或後續工作。 如先前的教學課程所述，gaggle 的 web 主機提供者公司有各式各樣的價格、功能和服務品質。 在此教學課程系列中，我將使用 [[折扣 ASP.NET](http://discountasp.net) ] 做為我的 web 主機提供者，但您可以遵循任何 web 主機提供者，只要它們支援您的網站開發所在的 ASP.NET 版本即可。 （這些教學課程是使用 ASP.NET 3.5 所建立）。此外，因為我們會在本教學課程中使用 FTP 將檔案複製到 web 主機提供者，而在未來的版本中，您的 web 主機提供者必須支援對其網頁伺服器的 FTP 存取。 幾乎所有的 web 主機提供者都提供這項功能，但您應該在註冊之前再次檢查。

## <a name="deploying-the-book-review-web-application-project"></a>部署書籍審查 Web 應用程式專案

回想一下，書籍審查 web 應用程式有兩個版本：一個是使用 Web 應用程式專案模型（BookReviewsWAP），另一個是使用網站專案模型（BookReviewsWSP）。 專案類型會影響是否自動或明確編譯網站，而且編譯模型會指示需要部署的檔案。 因此，我們將從 BookReviewsWAP 開始，分別檢查部署 BookReviewsWAP 和 BookReviewsWSP 專案。 如果您還沒這麼做，請花點時間下載這兩個 ASP.NET 應用程式。

流覽至 [`BookReviewsWAP`] 資料夾，然後按兩下 `BookReviewsWAP.sln` 檔案，以啟動 BookReviewsWAP 專案。 在部署專案之前，請務必先建立它，以確保原始程式碼的任何變更都包含在已編譯的元件中。 若要建立專案，請移至 [建立] 功能表，然後選擇 [組建 BookReviewsWAP] 功能表選項。 這樣會將專案中的原始程式碼編譯成單一元件，`BookReviewsWAP.dll`，放在 `Bin` 資料夾中。

我們現在已準備好部署必要的檔案！ 啟動您的 FTP 用戶端，並連接到 web 主機提供者的 web 伺服器。 （當您註冊虛擬主機公司時，他們會以電子郵件傳送如何連接到 FTP 伺服器的相關資訊，包括 FTP 伺服器的位址，以及使用者名稱和密碼）。

將下列檔案從您的桌面複製到 web 主機提供者的根網站資料夾。 當您在 web 主機提供者上 FTP 至 web 伺服器時，您可能會在根網站目錄中。 不過，某些 web 主機提供者會有一個名為 `www` 或 `wwwroot` 的子資料夾，做為您網站檔案的根資料夾。 最後，在 FTPing 檔案時，您可能需要在生產環境中建立對應的資料夾結構-[`Bin`] 資料夾、[`Fiction`] 資料夾、[`Images`] 資料夾等等。

- `~/Default.aspx`
- `~/About.aspx`
- `~/Site.master`
- `~/Web.config`
- `~/Web.sitemap`
- `Styles` 資料夾的完整內容
- `Images` 資料夾（及其子資料夾的完整內容，`BookCovers`）
- `~/Fiction/Default.aspx`
- `~/Fiction/Blaze.aspx`
- `~/Tech/Default.aspx`
- `~/Tech/CYOW.aspx`
- `~/Tech/TYASP35.aspx`
- `~/Bin/BookReviewsWAP.dll`

[圖 1] 顯示覆制必要檔案後的 FileZilla。 FileZilla 會在左側顯示本機電腦上的檔案，以及遠端電腦右邊的檔案。 如 [圖 1] 所示，ASP.NET 原始程式碼檔案（例如 `About.aspx.cs`）位於本機電腦（開發環境），但是不會複製到 web 主機提供者（生產環境），因為使用明確編譯時不需要部署程式碼檔案。

> [!NOTE]
> 在實際伺服器上擁有原始程式碼檔案時，不會有任何傷害，因為它們會被忽略。 ASP.NET 預設會禁止對原始程式碼檔的 HTTP 要求，如此一來，即使原始程式檔存在於實際執行伺服器上，也無法存取您網站的訪客。 （也就是說，如果使用者嘗試造訪 `http://www.yoursite.com/Default.aspx.cs` 他們會收到錯誤頁面，說明這些檔案類型 `.cs` 檔案-是禁止的）。

[![使用 FTP 用戶端，將所需的檔案從桌面複製到 web 主機提供者的 Web 服務器](deploying-your-site-using-an-ftp-client-cs/_static/image2.png)](deploying-your-site-using-an-ftp-client-cs/_static/image1.png)

**圖 1**：使用 FTP 用戶端，將所需的檔案從桌面複製到 Web 主機提供者的 web 伺服器（[按一下以觀看完整大小的影像](deploying-your-site-using-an-ftp-client-cs/_static/image3.png)）

部署網站之後，請花點時間測試網站。 如果您已購買功能變數名稱並正確地設定 DNS 設定，則可以輸入您的功能變數名稱以流覽您的網站。 或者，您的 web 主機服務提供者應提供您網站的 URL，看起來會像*accountname*。*webhostprovider*.com 或*webhostprovider*.com/*accountname*。 例如，[我的帳戶折扣] ASP.NET 的 URL 為： `http://httpruntime.web703.discountasp.net`。

[圖 2] 顯示已部署的書籍評論網站。 請注意，我是在折扣 ASP 上進行觀看。NET 的伺服器，`http://httpruntime.web703.discountasp.net`。 在此時間點，與網際網路連線的任何人都可以看到我的網站！ 如我們所預期，網站的外觀和行為就像在開發環境中測試一樣。

> [!NOTE]
> 如果您在流覽應用程式時收到錯誤，請花一點時間確保您已部署正確的檔案集合。 接下來，請檢查錯誤訊息，以查看是否會顯示問題的任何線索。 接著，您可以前往您的 web 主機公司技術服務人員，或將您的問題張貼到[ASP.NET 論壇](https://forums.asp.net/)的適當論壇。

[![書籍審查網站現在可供具有網際網路連線的任何人存取](deploying-your-site-using-an-ftp-client-cs/_static/image5.png)](deploying-your-site-using-an-ftp-client-cs/_static/image4.png)

**圖 2**：具有網際網路連線的任何人現在都可存取書籍審查網站（[按一下以觀看完整大小的影像](deploying-your-site-using-an-ftp-client-cs/_static/image6.png)）

## <a name="deploying-the-book-review-web-site-project"></a>部署書籍審查網站專案

部署使用自動編譯的 ASP.NET 應用程式（例如 BookReviewsWSP 網站專案）時，`Bin` 資料夾中沒有已編譯的元件。 因此，web 應用程式的原始程式碼檔案必須部署到生產環境。 讓我們逐步執行此程式。

就像 Web 應用程式專案一樣，最好先建立應用程式，然後再進行部署。 建立網站專案時，並不會建立元件，而是會檢查頁面中是否有任何編譯時期錯誤。 更好的方法是立即找出這些錯誤，而不是讓您的網站訪客探索他們！

成功建立專案之後，請使用您的 FTP 用戶端，將下列檔案複製到 web 主機提供者的根網站資料夾。 您可能需要在生產環境中建立對應的資料夾結構。

> [!NOTE]
> 如果您已部署 BookReviewsWAP 專案，但仍想要嘗試部署 BookReviewsWSP 專案，請先刪除在部署 BookReviewsWAP 時所上傳的 web 伺服器上的所有檔案，然後再部署 BookReviewsWSP 的檔案。

- `~/Default.aspx`
- `~/Default.aspx.cs`
- `~/About.aspx`
- `~/About.aspx.cs`
- `~/Site.master`
- `~/Site.master.cs`
- `~/Web.config`
- `~/Web.sitemap`
- `Styles` 資料夾的完整內容
- `Images` 資料夾（及其子資料夾的完整內容，`BookCovers`）
- `~/App_Code/BasePage.cs`
- `~/Fiction/Default.aspx`
- `~/Fiction/Default.aspx.cs`
- `~/Fiction/Blaze.aspx`
- `~/Fiction/Blaze.aspx.cs`
- `~/Tech/Default.aspx`
- `~/Tech/Default.aspx.cs`
- `~/Tech/CYOW.aspx`
- `~/Tech/CYOW.aspx.cs`
- `~/Tech/TYASP35.aspx`
- `~/Tech/TYASP35.aspx.cs`

[圖 3] 顯示覆制必要檔案後的 FileZilla。 如您所見，ASP.NET 原始程式碼檔案（例如 `About.aspx.cs`）存在於本機電腦（開發環境）和 web 主機提供者（生產環境）上，因為在使用自動編譯時需要部署程式碼檔案。

[![使用 FTP 用戶端，將所需的檔案從桌面複製到 web 主機提供者的 Web 服務器](deploying-your-site-using-an-ftp-client-cs/_static/image8.png)](deploying-your-site-using-an-ftp-client-cs/_static/image7.png)

[**圖 3**]：使用 FTP 用戶端，將所需的檔案從桌面複製到 Web 主機提供者的 web 伺服器（[按一下以觀看完整大小的影像](deploying-your-site-using-an-ftp-client-cs/_static/image9.png)）

應用程式的編譯模型不會影響使用者體驗。 不論是使用 Web 應用程式專案模型或網站專案模型建立網站，都可以存取相同的 ASP.NET 網頁，而且它們的外觀和行為都相同。

### <a name="updating-a-web-application-on-production"></a>更新生產環境上的 Web 應用程式

Web 應用程式開發和部署不是一次性的進程。 例如，建立書籍審查網站時，我建立了各種頁面，並在個人電腦上撰寫隨附的程式碼（開發環境）。 達到特定穩定狀態之後，我部署了應用程式，讓其他人可以造訪網站並閱讀我的評論。 但是，部署不會在此網站上標示我的開發結束。 我可以新增更多書籍評論或實行新功能，例如允許我的訪客對書籍進行評分或留下自己的意見。 這類增強功能會在開發環境中開發，完成後必須部署。 因此，開發和部署是迴圈的。 您可以開發應用程式，然後加以部署。 當網站上線且在生產環境中時，會新增新功能，並在一段時間內修正 bug，這會導致重新部署應用程式。 以此類推，依此類推。

如您所料，重新部署 web 應用程式時，您只需要複製新的和變更的檔案。 不需要重新部署未變更的頁面或伺服器或用戶端支援檔案（雖然這樣做並不會有任何傷害）。

> [!NOTE]
> 使用明確編譯時，請記住一件事，就是每當您將新的 ASP.NET 網頁加入至專案或進行任何程式碼相關的變更時，您都必須重建專案，這會更新 `Bin` 資料夾中的元件。 因此，在生產環境中更新 web 應用程式時，您必須將這個更新的元件複製到生產環境（以及其他新的和更新的內容）。

也請瞭解 `Web.config` 或 `Bin` 目錄中的檔案所做的任何變更，都會停止並重新啟動網站的應用程式集區。 如果您的會話狀態是使用 `InProc` 模式儲存（預設值），則每當修改這些金鑰檔案時，您的網站訪客將會失去其會話狀態。 若要避免此缺陷，請考慮使用 `StateServer` 或 `SQLServer` 模式來儲存會話。 如需有關此主題的詳細資訊，請參閱[會話狀態模式](https://msdn.microsoft.com/library/ms178586.aspx)。

最後，請記住，重新部署應用程式可能需要幾秒鐘到幾分鐘的時間，視需要複製到生產環境的檔案數目和大小而定。 在這段期間，造訪您網站的使用者可能會遇到錯誤或奇怪的行為。 您可以「關閉」您的整個應用程式，方法是將名為 `App_Offline.htm` 的頁面新增至應用程式的根目錄，以向使用者說明網站已關閉進行維護（或任何），而且很快就會備份。 當 `App_Offline.htm` 檔案存在時，ASP.NET 執行時間會將所有連入要求重新導向至該頁面。

## <a name="summary"></a>總結

部署 web 應用程式需要將必要的檔案從開發環境複製到生產環境。 透過網路傳送檔案的最常見方式是檔案傳輸通訊協定（FTP），而大部分的 web 主機提供者都支援其網頁伺服器的 FTP 存取。 在本教學課程中，我們已瞭解如何使用 FTP 用戶端，將所需的檔案部署到 web 伺服器。 一旦部署之後，任何具有網際網路連線的人都可以造訪網站！

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [應用程式\_離線的 .htm 和解決「IE 易記錯誤」功能](https://weblogs.asp.net/scottgu/App_5F00_Offline.htm-and-working-around-the-_2200_IE-Friendly-Errors_2200_-feature)
- [會話狀態模式](https://msdn.microsoft.com/library/ms178586.aspx)

> [!div class="step-by-step"]
> [上一頁](determining-what-files-need-to-be-deployed-cs.md)
> [下一頁](deploying-your-site-using-visual-studio-cs.md)
