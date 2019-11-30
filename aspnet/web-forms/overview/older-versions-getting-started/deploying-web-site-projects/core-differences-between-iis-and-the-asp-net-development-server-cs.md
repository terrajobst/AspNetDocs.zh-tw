---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs
title: IIS 與 ASP.NET 程式開發伺服器之間的核心差異（C#） |Microsoft Docs
author: rick-anderson
description: 在本機測試 ASP.NET 應用程式時，您可能會使用 ASP.NET 開發 Web 服務器。 不過，生產網站很可能 pow 。
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 13a5a423-9235-4dde-b408-2fd10f791d63
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs
msc.type: authoredcontent
ms.openlocfilehash: 7fea3939bd910a052340215c207013e2269f32a2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74617604"
---
# <a name="core-differences-between-iis-and-the-aspnet-development-server-c"></a>IIS 與 ASP.NET 程式開發伺服器間的核心差異 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_06_CS.zip)或[下載 PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial06_WebServerDiff_cs.pdf)

> 在本機測試 ASP.NET 應用程式時，您可能會使用 ASP.NET 開發 Web 服務器。 不過，生產網站很可能是有能力的 IIS。 這些 web 伺服器處理要求的方式有一些差異，而這些差異可能會有重要的後果。 本教學課程將探討一些更無關的差異。

## <a name="introduction"></a>簡介

每當使用者造訪 ASP.NET 應用程式時，他的瀏覽器就會將要求傳送至網站。 Web 服務器軟體會收取該要求，這會與 ASP.NET 執行時間協調，以產生並傳回所要求資源的內容。 [ **I** Nternet **i** nformation (資訊**S** ervices （IIS）](http://en.wikipedia.org/wiki/Internet_Information_Services)是一套服務，可為 Windows 伺服器提供通用的網際網路功能。 IIS 是用來在生產環境中 ASP.NET 應用程式最常用的 web 伺服器;您的 web 主機提供者很可能會使用 web 伺服器軟體來提供您的 ASP.NET 應用程式。 IIS 也可以做為開發環境中的 web 伺服器軟體，不過這牽涉到安裝 IIS 並正確設定它。

ASP.NET 程式開發伺服器是適用于開發環境的替代 web 伺服器選項;它隨附于，並已整合到 Visual Studio 中。 除非 web 應用程式已設定為使用 IIS，否則當您第一次從 Visual Studio 內流覽網頁時，ASP.NET 程式開發伺服器會自動啟動並當做 web 伺服器使用。 我們在[*判斷需要部署哪些*](determining-what-files-need-to-be-deployed-cs.md)檔案教學課程中所建立的示範 web 應用程式，都是以檔案系統為基礎的 web 應用程式，但未設定為使用 IIS。 因此，從 Visual Studio 流覽其中一個網站時，會使用 ASP.NET 程式開發伺服器。

在完美的世界中，開發和生產環境會完全相同。 不過，如同我們在先前的教學課程中所討論的，環境在不同的設定中並不常見。 在環境中使用不同的 web 伺服器軟體，會新增在部署應用程式時必須納入考慮的另一個變數。 本教學課程涵蓋 IIS 與 ASP.NET 程式開發伺服器之間的主要差異。 因為有這些差異，所以在開發環境中執行的程式碼會擲回例外狀況，或在生產時以不同的方式運作。

## <a name="security-context-differences"></a>安全性內容差異

每當 web 伺服器軟體處理傳入要求時，就會將該要求與特定的安全性內容產生關聯。 作業系統會使用此安全性內容資訊來判斷要求所允許的動作。 例如，ASP.NET 網頁可能包含將一些訊息記錄到磁片上檔案的程式碼。 為了讓此 ASP.NET 網頁執行而不發生錯誤，安全性內容必須具有適當的檔案系統層級許可權，亦即該檔案的寫入權限。

ASP.NET 程式開發伺服器會將傳入要求與目前登入之使用者的安全性內容產生關聯。 如果您是以系統管理員身分登入您的桌面，則 ASP.NET 程式開發伺服器所提供的 ASP.NET 網頁將會具有與系統管理員相同的存取權限。 不過，IIS 所處理的 ASP.NET 要求會與特定的電腦帳戶相關聯。 根據預設，IIS 版本6和7會使用 Network Service 電腦帳戶，雖然您的 web 主機提供者可能已為每個客戶設定唯一的帳戶。 更多的是，您的 web 主機服務提供者可能會對此電腦帳戶提供有限的許可權。 最後結果是您可能會在開發環境中有執行的網頁，而不會發生錯誤，但在生產環境中裝載時，會產生與授權相關的例外狀況。

為了顯示這種類型的錯誤動作，我在「書籍評論」網站建立了一個頁面，該檔案會在磁片上建立一個檔案，其中儲存了在*24 小時內 ASP.NET 3.5*的最近一次觀看的日期和時間。 若要跟著做，請開啟 [`~/Tech/TYASP35.aspx`] 頁面，並將下列程式碼新增至 `Page_Load` 事件處理常式：

[!code-csharp[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample1.cs)]

> [!NOTE]
> [`File.WriteAllText` 方法](https://msdn.microsoft.com/library/system.io.file.writealltext.aspx)會建立新的檔案（如果不存在），然後將指定的內容寫入其中。 如果檔案已經存在，則會覆寫現有的內容。

接下來，請造訪使用 ASP.NET 程式開發伺服器在開發環境中，以*24 小時的時間來教您自己的 ASP.NET 3.5* 。 假設您使用具有足夠許可權的帳戶登入您的電腦，以在 web 應用程式的根目錄中建立和修改文字檔，則會顯示與之前相同的書籍，但每次流覽頁面時，會將日期和時間和使用者的 IP 位址儲存在 `LastTYASP35Access.txt` 檔案中。 將瀏覽器指向此檔案;您應該會看到類似 [圖 1] 所示的訊息。

[![文字檔包含流覽書審閱的最後日期和時間](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image2.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image1.png)

**圖 1**：文字檔包含流覽書審閱的最後日期和時間（[按一下以觀看完整大小的影像](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image3.png)）

將 web 應用程式部署至生產環境，然後在24小時的書籍審查頁面中，造訪託管的*教授 ASP.NET 3.5* 。 此時，您應該會看到 [書籍審查] 頁面是正常的，或如 [圖 2] 所示的錯誤訊息。 某些 web 主機提供者會授與寫入權限給匿名 ASP.NET 電腦帳戶，在此情況下，頁面會正常執行而不會發生錯誤。 不過，如果您的 web 主機提供者禁止匿名帳戶的寫入權限，則當 `TYASP35.aspx` 頁面嘗試將目前的日期和時間寫入 `LastTYASP35Access.txt` 檔案時，就會引發[`UnauthorizedAccessException` 的例外](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx)狀況。

[![IIS 所使用的預設電腦帳戶沒有寫入檔案系統的許可權](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image5.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image4.png)

**圖 2**： IIS 所使用的預設電腦帳戶沒有寫入檔案系統的許可權（[按一下以查看完整大小的影像](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image6.png)）

好消息是，大部分的 web 主機提供者都具有某種許可權工具，可讓您在網站中指定檔案系統許可權。 將根目錄的 [寫入] 存取權授與匿名 ASP.NET 帳戶，然後再重新流覽 [書籍審查] 頁面。 （如有需要，請洽詢您的 web 主機提供者，以取得如何將寫入權限授與預設 ASP.NET 帳戶的協助）。此時，頁面應該會載入而不會發生錯誤，而且應該成功建立 `LastTYASP35Access.txt` 檔案。

這就是因為 ASP.NET 程式開發伺服器在不同于 IIS 的安全性內容下運作，所以您可以在檔案系統中讀取或寫入的 ASP.NET 網頁、讀取或寫入 Windows 事件記錄檔，或是讀取或寫入 Windows 登錄會在開發時如預期般運作，但在生產環境中會產生例外狀況。 建立將部署至共用 web 主控環境的 web 應用程式時，請勿讀取或寫入事件記錄檔或 Windows 登錄。 也請記下任何讀取或寫入檔案系統的 ASP.NET 網頁，因為您可能需要在生產環境中對適當的資料夾授與讀取和寫入權限。

## <a name="differences-on-serving-static-content"></a>提供靜態內容的差異

IIS 和 ASP.NET 程式開發伺服器之間的另一個核心差異在於它們如何處理靜態內容的要求。 傳入 ASP.NET 程式開發伺服器的每個要求（不論是 ASP.NET 網頁、影像或 JavaScript 檔案）都是由 ASP.NET 執行時間所處理。 根據預設，IIS 只會在要求傳入 ASP.NET 資源（例如 ASP.NET 網頁、Web 服務等等）時，叫用 ASP.NET 執行時間。 IIS 會抓取靜態內容（影像、CSS 檔案、JavaScript 檔案、PDF 檔案、ZIP 檔案和 like）的要求，而不需要 ASP.NET 執行時間的介入。 （在提供靜態內容時，可以指示 IIS 使用 ASP.NET 執行時間; 如需詳細資訊，請參閱本教學課程中的「以 IIS 7 執行靜態檔案的表單架構驗證和 URL 驗證」一節。）

ASP.NET 執行時間會執行數個步驟來產生要求的內容，包括驗證（識別要求者）和授權（判斷要求者是否有許可權可查看所要求的內容）。 常見的驗證形式是以*表單為基礎的驗證*，使用者可以透過輸入其認證（通常是使用者名稱和密碼）來識別網頁上的文字方塊。 在驗證其認證後，網站會在使用者的瀏覽器上儲存*驗證票證*cookie，並隨著每次後續要求傳送至網站，以及用來驗證使用者。 此外，也可以指定*URL 授權*規則，以指示使用者可以或無法存取特定資料夾的內容。 許多 ASP.NET 網站都使用以表單為基礎的驗證和 URL 授權來支援使用者帳戶，以及定義只能供已驗證的使用者或屬於特定角色之使用者存取的部分網站。

> [!NOTE]
> 以徹底檢查 ASP。NET 的表單架構驗證、URL 授權和其他與使用者帳戶相關的功能，請務必查看我的[網站安全性教學](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)課程。

請考慮使用以表單為基礎的授權來支援使用者帳戶的網站，並將使用 URL 授權的資料夾設定為只允許已驗證的使用者。 假設此資料夾包含 ASP.NET 網頁和 PDF 檔案，而其目的是只有經過驗證的使用者才能看到這些 PDF 檔案。

如果造訪者嘗試直接在他的瀏覽器網址列中輸入 URL 來查看其中一個 PDF 檔案，會發生什麼事？ 若要瞭解，讓我們在書籍審查網站中建立新的資料夾，新增一些 PDF 檔案，並將網站設定為使用 URL 授權，以禁止匿名使用者流覽此資料夾。 如果您下載示範應用程式，就會看到我建立了一個名為 `PrivateDocs` 的資料夾，並從我的[網站安全性教學](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)課程（如何調整！）新增 PDF。 [`PrivateDocs`] 資料夾也包含 `Web.config` 檔案，該檔案會指定要拒絕匿名使用者的 URL 授權規則：

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample2.xml)]

最後，我將 web 應用程式設定為使用以表單為基礎的驗證，方法是更新根目錄中的 `Web.config` 檔案，並取代：

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample3.xml)]

取代成：

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample4.xml)]

使用 ASP.NET 程式開發伺服器，請造訪網站，並在瀏覽器的網址列中輸入其中一個 PDF 檔案的直接 URL。 如果您已下載與本教學課程相關聯的網站，URL 看起來應該像這樣： `http://localhost:portNumber/PrivateDocs/aspnet_tutorial01_Basics_vb.pdf`

在網址列中輸入此 URL，會導致瀏覽器將要求傳送至檔案的 ASP.NET 程式開發伺服器。 ASP.NET 程式開發伺服器將要求交給 ASP.NET 執行時間來處理。 因為我們尚未登入，而且因為 `PrivateDocs` 資料夾中的 `Web.config` 設定為拒絕匿名存取，所以 ASP.NET 執行時間會自動將我們重新導向至登入頁面，`Login.aspx` （請參閱 [圖 3]）。 將使用者重新導向至 [登入] 頁面時，ASP.NET 會包含一個 `ReturnUrl` querystring 參數，指出使用者嘗試查看的頁面。 成功登入之後，使用者可以返回此頁面。

[![未經授權的使用者會自動重新導向至登入頁面](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image8.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image7.png)

**圖 3**：未經授權的使用者會自動重新導向至登[入頁面（按一下以觀看完整大小的影像](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image9.png)）

現在讓我們來看看這在生產環境中的行為。 部署您的應用程式，並在生產環境中的 [`PrivateDocs`] 資料夾中，輸入其中一個 Pdf 的直接 URL。 這會提示您的瀏覽器傳送檔案的要求 IIS。 由於要求的是靜態檔案，因此 IIS 會在不叫用 ASP.NET 執行時間的情況下，抓取並傳回檔案。 因此，不會執行任何 URL 授權檢查;知道檔案的直接 URL 的任何人都可以存取經過的私用 PDF 內容。

[![匿名使用者可以藉由輸入檔案的直接 URL 來下載私人 PDF 檔案](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image11.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image10.png)

**圖 4**：匿名使用者可以藉由輸入檔案的直接 URL （[按一下以查看完整大小的影像](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image12.png)）來下載私人 PDF 檔案

### <a name="performing-forms-based-authentication-and-url-authentication-on-static-files-with-iis-7"></a>在具有 IIS 7 的靜態檔案上執行表單架構驗證和 URL 驗證

有幾種方法可用來保護靜態內容免于未經授權的使用者使用。 IIS 7 引進了*整合式管線*，它會結婚 IIS 的工作流程與 ASP.NET 執行時間的工作流程。 簡言之，您可以指示 IIS 叫用 ASP.NET 執行時間的驗證和授權模組所有傳入的要求（包括如 PDF 檔案的靜態內容）。 請洽詢您的 web 主機提供者，瞭解如何設定您的網站以使用整合式管線。

一旦將 IIS 設定為使用整合式管線，請將下列標記新增至根目錄中的 `Web.config` 檔案：

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample5.xml)]

此標記會指示 IIS 7 使用以 ASP.NET 為基礎的驗證和授權模組。 重新部署您的應用程式，然後重新流覽 PDF 檔案。 這次 IIS 處理要求時，會讓 ASP.NET 執行時間的驗證和授權邏輯有機會檢查要求。 由於只有經過驗證的使用者才有權查看 `PrivateDocs` 資料夾中的內容，因此會自動將匿名訪客重新導向至登入頁面（請參閱 [圖 3]）。

> [!NOTE]
> 如果您的 web 主機提供者仍在使用 IIS 6，則您無法使用整合式管線功能。 其中一個因應措施是將私用檔放在禁止 HTTP 存取的資料夾中（例如 `App_Data`），然後建立頁面來提供這些檔。 此頁面可能會 `GetPDF.aspx`呼叫，而且會透過 querystring 參數傳遞 PDF 的名稱。 [`GetPDF.aspx`] 頁面會先驗證使用者是否有權查看檔案，如果是的話，則會使用[`Response.WriteFile(filePath)`](https://msdn.microsoft.com/library/system.web.httpresponse.writefile.aspx)方法，將要求的 PDF 檔案內容傳回給要求的用戶端。 如果您不想要啟用整合式管線，這項技術也適用于 IIS 7。

## <a name="summary"></a>總結

生產環境中的 Web 應用程式是使用 Microsoft 的 IIS web 伺服器軟體所主控。 不過，在開發環境中，應用程式可能會使用 IIS 或 ASP.NET 程式開發伺服器來裝載。 在理想的情況下，相同的 web 伺服器軟體應該用於這兩種環境中，因為使用不同的軟體會在混合中新增另一個變數。 不過，使用 ASP.NET 程式開發伺服器的便利性，讓它在開發環境中成為一項頗具吸引力的選擇。 好消息是 IIS 與 ASP.NET 程式開發伺服器之間只有幾個基本差異，如果您知道這些差異，您可以採取步驟來確保應用程式的運作和功能相同，而不論環境.

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [與 IIS 7.0 的 ASP.NET 整合](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)
- [在 IIS 7 上使用 ASP.NET 論壇驗證與所有類型的內容](https://blogs.iis.net/bills/archive/2007/05/19/using-asp-net-forms-authentication-with-all-types-of-content-with-iis7-video.aspx)（影片）
- [Visual Web Developer 中的 Web 服務器](https://msdn.microsoft.com/library/58wxa9w5.aspx)

> [!div class="step-by-step"]
> [上一頁](common-configuration-differences-between-development-and-production-cs.md)
> [下一頁](deploying-a-database-cs.md)
