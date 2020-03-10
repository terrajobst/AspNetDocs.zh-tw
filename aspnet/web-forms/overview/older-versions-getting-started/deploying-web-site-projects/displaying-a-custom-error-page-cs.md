---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-cs
title: 顯示自訂錯誤頁面（C#） |Microsoft Docs
author: rick-anderson
description: 當 ASP.NET web 應用程式中發生執行階段錯誤時，使用者會看到什麼內容？ 答案取決於網站的 &lt;customErrors&gt; 設定 。
ms.author: riande
ms.date: 06/09/2009
ms.assetid: cb061642-faf3-41b2-9372-69e13444d458
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-cs
msc.type: authoredcontent
ms.openlocfilehash: c1ff4c112b9a489b8fb9ef3443663cd71eda7965
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78524203"
---
# <a name="displaying-a-custom-error-page-c"></a>顯示自訂的錯誤頁面 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_11_CS.zip)或[下載 PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial11_CustomErrors_cs.pdf)

> 當 ASP.NET web 應用程式中發生執行階段錯誤時，使用者會看到什麼內容？ 答案取決於網站的 &lt;customErrors&gt; 設定的方式。 根據預設，使用者會在發生執行階段錯誤時，顯示一個不美觀的黃色螢幕讚揚。 本教學課程會示範如何自訂這些設定，以顯示符合內賞心悅目的自訂錯誤頁面，其中與您網站的外觀和風格相符。

## <a name="introduction"></a>簡介

在完美的世界中，不會發生執行階段錯誤。 程式設計人員會撰寫具有 nary 錯誤的程式碼，並提供健全的使用者輸入驗證，而外部資源（例如資料庫伺服器和電子郵件伺服器）永遠不會離線。 當然，事實上，錯誤是不可避免的。 .NET Framework 中的類別會擲回例外狀況，以通知錯誤。 例如，呼叫 SqlConnection 物件的 Open 方法會建立連接字串所指定之資料庫的連接。 不過，如果資料庫已關閉，或連接字串中的認證無效，則 Open 方法會擲回 `SqlException`。 您可以使用 `try/catch/finally` 區塊來處理例外狀況。 如果 `try` 區塊內的程式碼擲回例外狀況，控制權就會傳送至適當的 catch 區塊，讓開發人員可以嘗試從錯誤中復原。 如果沒有相符的 catch 區塊，或擲回例外狀況的程式碼不在 try 區塊中，則例外狀況會在 `try/catch/finally` 區塊的搜尋中 percolates 呼叫堆疊。

如果例外狀況在不進行處理的情況下，一直反升至 ASP.NET 執行時間，則會引發[`HttpApplication` 類別](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)的[`Error` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx)，並顯示已設定的*錯誤頁面*。 根據預設，ASP.NET 會顯示一個充滿深情稱為「死亡（YSOD）的[黃色螢幕](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)」的錯誤頁面。 YSOD 有兩個版本：一個會顯示例外狀況詳細資料、堆疊追蹤，以及其他對應用程式的開發人員很有説明的資訊（請參閱 [**圖 1**]）。另一個則是指出發生執行階段錯誤（請參閱 [**圖 2**]）。

例外狀況詳細資料 YSOD 對於偵錯工具的開發人員很有説明，但向使用者顯示 YSOD 是 tacky 和不夠專業。 相反地，應該將終端使用者導向錯誤頁面，以更方便使用的 prose 來維護網站的外觀和感覺。 好消息是，建立這類自訂的錯誤頁面相當簡單。 本教學課程一開始會探討 ASP。NET 的不同錯誤頁面。 接著，它會示範如何設定 web 應用程式，以在發生錯誤時向使用者顯示自訂錯誤頁面。

### <a name="examining-the-three-types-of-error-pages"></a>檢查三種錯誤頁面類型

當 ASP.NET 應用程式中發生未處理的例外狀況時，會顯示三種錯誤頁面類型的其中一種：

- 例外狀況詳細資料會顯示死亡錯誤頁面的黃色畫面，
- 執行階段錯誤黃色畫面的死亡錯誤頁面，或
- 自訂錯誤頁面

開發人員最熟悉的錯誤頁面是例外狀況詳細資料 YSOD。 根據預設，會對流覽本機的使用者顯示此頁面，因此是在開發環境中測試網站時發生錯誤時所看到的頁面。 正如其名，例外狀況詳細資料 YSOD 提供例外狀況的詳細資料，也就是類型、訊息和堆疊追蹤。 此外，如果例外狀況是由您 ASP.NET 網頁的程式碼後置類別中的程式碼所引發，而且如果應用程式已設定為進行偵測，則 [例外狀況詳細資料] YSOD 也會顯示這行程式碼（和其底下的幾行程式碼）。

[**圖 1** ] 顯示 [例外狀況詳細資料 YSOD] 頁面。 請注意瀏覽器的 位址 視窗中的 URL： `http://localhost:62275/Genre.aspx?ID=foo`。 回想一下，[`Genre.aspx`] 頁面會列出特定內容類型中的書籍評論。 它需要透過 querystring 傳遞 `GenreId` 值（`uniqueidentifier`）;例如，您可以 `Genre.aspx?ID=7683ab5d-4589-4f03-a139-1c26044d0146`查看小說評論的適當 URL。 如果透過 querystring （例如 "foo"）傳入非`uniqueidentifier` 值，則會擲回例外狀況（exception）。

> [!NOTE]
> 若要在可供下載的示範 web 應用程式中重現此錯誤，您可以直接造訪 `Genre.aspx?ID=foo`，或按一下 `Default.aspx`中的 [產生執行階段錯誤] 連結。

請注意 [**圖 1**] 中顯示的例外狀況資訊。 出現在頁面頂端的「從字元字串轉換為 uniqueidentifier 時轉換失敗」例外狀況訊息。 也會列出例外狀況的類型，`System.Data.SqlClient.SqlException`。 還有堆疊追蹤。

[![](displaying-a-custom-error-page-cs/_static/image2.png)](displaying-a-custom-error-page-cs/_static/image1.png)

**圖 1**：例外狀況詳細資料 YSOD 包含例外狀況的相關資訊  
 （[按一下以查看完整大小的影像](displaying-a-custom-error-page-cs/_static/image3.png)）

另一種類型的 YSOD 是執行時間錯誤 YSOD，如 [**圖 2**] 所示。 [執行時間錯誤 YSOD] 會通知訪客發生執行階段錯誤，但不包含所擲回之例外狀況的任何相關資訊。 （不過，它會提供有關如何藉由修改 `Web.config` 檔案來查看錯誤詳細資料的指示，這是這類 YSOD 外觀不夠專業的一部分）。

根據預設，在 [**圖 2**： `http://httpruntime.web703.discountasp.net/Genre.aspx?ID=foo`] 的瀏覽器網址列中，從遠端存取的使用者（透過 http://www.yoursite.com)，會顯示 [執行時間錯誤] YSOD。 有兩個不同的 YSOD 畫面存在，是因為開發人員想要知道錯誤詳細資料，但這類資訊不應該顯示在即時網站上，因為它可能會顯示潛在的安全性弱點或其他機密資訊給造訪您的點.

> [!NOTE]
> 如果您遵循並使用 DiscountASP.NET 做為您的 web 主機，您可能會注意到 [執行時間錯誤] YSOD 不會在造訪即時網站時顯示。 這是因為 DiscountASP.NET 預設會將其伺服器設定為顯示例外狀況詳細資料 YSOD。 好消息是，您可以藉由將 `<customErrors>` 區段新增至 `Web.config` 檔案，來覆寫此預設行為。 [設定顯示的錯誤頁面] 區段會詳細檢查 `<customErrors>` 區段。

[![](displaying-a-custom-error-page-cs/_static/image5.png)](displaying-a-custom-error-page-cs/_static/image4.png)

**圖 2**：執行階段錯誤 YSOD 不包含任何錯誤詳細資料  
 （[按一下以查看完整大小的影像](displaying-a-custom-error-page-cs/_static/image6.png)）

第三種錯誤頁面是 [自訂錯誤網頁]，這是您建立的網頁。 自訂錯誤頁面的優點是您可以完全掌控向使用者顯示的資訊，以及網頁的外觀和風格;[自訂錯誤] 頁面可以使用與其他頁面相同的主版頁面和樣式。 「使用自訂錯誤頁面」一節會逐步解說如何建立自訂錯誤頁面，並將它設定為在發生未處理的例外狀況時顯示。 [**圖 3** ] 提供此自訂錯誤頁面的搶先尖峰。 如您所見，[錯誤] 頁面的外觀與風格比 [圖 1] 和 [2] 所示的黃色螢幕中的任何一種，都比較專業。

[![](displaying-a-custom-error-page-cs/_static/image8.png)](displaying-a-custom-error-page-cs/_static/image7.png)

**圖 3**：自訂錯誤網頁提供更量身打造的外觀和操作  
 （[按一下以查看完整大小的影像](displaying-a-custom-error-page-cs/_static/image9.png)）

請花點時間檢查 [**圖 3**] 中的瀏覽器網址列。 請注意，網址列會顯示自訂錯誤網頁的 URL （`/ErrorPages/Oops.aspx`）。 在 [圖 1] 和 [2] 中，燈的黃色螢幕會顯示在錯誤來源的相同頁面中（`Genre.aspx`）。 自訂錯誤頁面會透過 `aspxerrorpath` querystring 參數，傳遞錯誤發生所在之頁面的 URL。

## <a name="configuring-which-error-page-is-displayed"></a>設定顯示的錯誤頁面

顯示三個可能錯誤頁面的哪一個是以兩個變數為基礎：

- [`<customErrors>`] 區段中的設定資訊，以及
- 使用者是否在本機或遠端存取網站。

`Web.config` 中的[`<customErrors>` 區段](https://msdn.microsoft.com/library/h0hfz6fc.aspx)有兩個屬性會影響顯示的錯誤頁面： `defaultRedirect` 和 `mode`。 `defaultRedirect` 屬性是選擇性的。 如果有提供，它會指定自訂錯誤網頁的 URL，並指出應該顯示自訂錯誤頁面，而不是執行階段錯誤 YSOD。 需要 `mode` 屬性，並接受下列三個值的其中一個： `On`、`Off`或 `RemoteOnly`。 這些值具有下列行為：

- `On`-指出自訂錯誤網頁或執行時間錯誤 YSOD 會顯示給所有訪客，不論它們是在本機或遠端。
- `Off`-指定 [例外狀況詳細資料] YSOD 會顯示給所有訪客，不論它們是在本機或遠端。
- `RemoteOnly`-指出 [自訂錯誤] 頁面或 [執行階段錯誤] YSOD 會向遠端訪客顯示，而 [例外狀況詳細資料] YSOD 會向本機訪客顯示。

除非您另外指定，否則 ASP.NET 的作用就如同您已將 mode 屬性設為 `RemoteOnly`，而且尚未指定 `defaultRedirect` 值。 換句話說，預設行為是，在 [執行時間錯誤] YSOD 向遠端訪客顯示時，[例外狀況詳細資料] YSOD 會顯示給本機訪客。 您可以藉由將 `<customErrors>` 區段新增至 web 應用程式的 `Web.config file.` 來覆寫此預設行為

## <a name="using-a-custom-error-page"></a>使用自訂錯誤頁面

每個 web 應用程式都應該有自訂錯誤頁面。 它提供了「執行時間錯誤 YSOD 的更專業型式替代方案，它很容易建立，而且設定應用程式以使用自訂錯誤頁面只需要幾分鐘。 第一個步驟是建立自訂錯誤網頁。 我已將新資料夾新增至名為 `ErrorPages` 的書籍審核應用程式，並新增至名為 `Oops.aspx`的新 ASP.NET 網頁。 讓頁面使用與網站上其餘頁面相同的主版頁面，讓它自動繼承相同的外觀與風格。

[![](displaying-a-custom-error-page-cs/_static/image11.png)](displaying-a-custom-error-page-cs/_static/image10.png)

**圖 4**：建立自訂錯誤頁面

接下來，請花幾分鐘的時間建立錯誤頁面的內容。 我建立了一個簡單的自訂錯誤頁面，其中包含一則訊息，指出發生未預期的錯誤和連結回到網站的首頁。

[![](displaying-a-custom-error-page-cs/_static/image13.png)](displaying-a-custom-error-page-cs/_static/image12.png)

**圖 5**：設計您的自訂錯誤頁面  
 （[按一下以查看完整大小的影像](displaying-a-custom-error-page-cs/_static/image14.png)）

當錯誤頁面完成時，請將 web 應用程式設定為使用自訂錯誤頁面，代替執行時間錯誤 YSOD。 這是藉由在 `<customErrors>` 區段的 `defaultRedirect` 屬性中指定錯誤頁面的 URL 來完成。 將下列標記新增至您應用程式的 `Web.config` 檔案：

[!code-xml[Main](displaying-a-custom-error-page-cs/samples/sample1.xml)]

上述標記會將應用程式設定為向本機流覽的使用者顯示例外狀況詳細資料 YSOD，同時針對遠端流覽的使用者使用自訂錯誤頁面糟糕。 若要查看其實際運作情形，請將您的網站部署到生產環境，然後流覽具有無效 querystring 值的即時網站上的內容類型 .aspx 頁面。 您應該會看到 [自訂錯誤] 頁面（請參閱 [**圖 3**]）。

若要確認自訂錯誤頁面只會向遠端使用者顯示，請從開發環境流覽具有無效 querystring 的 [`Genre.aspx`] 頁面。 您仍然應該會看到 [例外狀況詳細資料] YSOD （請參閱 [**圖 1**]）。 [`RemoteOnly`] 設定可確保在生產環境上造訪網站的使用者，請參閱自訂錯誤頁面，而開發人員在本機工作時，會繼續查看例外狀況的詳細資料。

## <a name="notifying-developers-and-logging-error-details"></a>通知開發人員和記錄錯誤詳細資料

開發環境中發生的錯誤是由開發人員在電腦上所造成。 她在 [例外狀況詳細資料] YSOD 中顯示例外狀況的資訊，而她知道發生錯誤時所執行的步驟。 但在生產環境中發生錯誤時，開發人員並不知道發生錯誤，除非流覽網站的使用者需要時間報告錯誤。 而且，即使使用者不知道例外狀況類型、訊息和堆疊追蹤，也會提醒開發小組發生錯誤，就難以診斷錯誤的原因，讓我們單獨加以修正。

基於這些理由，將生產環境中的任何錯誤記錄到某個持續性存放區（例如資料庫），以及開發人員會收到此錯誤的警示，是很重要的。 自訂錯誤頁面看起來就像是執行此記錄和通知的好位置。 可惜的是，自訂錯誤網頁沒有錯誤詳細資料的存取權，因此無法用來記錄此資訊。 好消息是，有許多方法可以攔截錯誤詳細資料並加以記錄，接下來的三個教學課程會更詳細地探索這個主題。

## <a name="using-different-custom-error-pages-for-different-http-error-statuses"></a>針對不同的 HTTP 錯誤狀態使用不同的自訂錯誤頁面

當 ASP.NET 網頁擲回例外狀況，但未處理時，例外狀況會 percolates 到 ASP.NET 執行時間，這會顯示已設定的錯誤頁面。 如果要求進入 ASP.NET 引擎，但因為某些原因而無法處理，可能是因為找不到要求的檔案，或檔案已停用讀取權限，則 ASP.NET 引擎會引發 `HttpException`。 這個例外狀況（例如從 ASP.NET 網頁引發的例外狀況）會反升至執行時間，導致顯示適當的錯誤頁面。

對於生產環境中的 web 應用程式，這表示如果使用者要求找不到的頁面，他們會看到自訂錯誤頁面。 [**圖 6** ] 顯示這類範例。 由於要求是針對不存在的頁面（`NoSuchPage.aspx`），因此會擲回 `HttpException` 並顯示自訂錯誤頁面（請注意 `aspxerrorpath` querystring 參數中 `NoSuchPage.aspx` 的參考）。

[![](displaying-a-custom-error-page-cs/_static/image16.png)](displaying-a-custom-error-page-cs/_static/image15.png)

**圖 6**： ASP.NET 執行時間顯示已設定的錯誤網頁，以回應不正確要求（[按一下以查看完整大小的影像](displaying-a-custom-error-page-cs/_static/image17.png)）

根據預設，所有類型的錯誤都會顯示相同的自訂錯誤頁面。 不過，您可以使用 `<customErrors>` 區段內 `<error>` 個子項目，為特定的 HTTP 狀態碼指定不同的自訂錯誤頁面。 例如，若要在 [找不到頁面] 錯誤的事件中顯示不同的錯誤頁面，其 HTTP 狀態碼為404，請更新 `<customErrors>` 區段以包含下列標記：

[!code-xml[Main](displaying-a-custom-error-page-cs/samples/sample2.xml)]

進行這項變更之後，每當使用者造訪遠端要求不存在的 ASP.NET 資源時，就會將他們重新導向至 `404.aspx` 的自訂錯誤頁面，而不是 `Oops.aspx`。 如 [**圖 7** ] 所示，[`404.aspx`] 頁面可以包含比一般自訂錯誤頁面更具體的訊息。

> [!NOTE]
> 如需建立有效404錯誤網頁的指引[，另請參閱404錯誤網頁](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/)。

[![](displaying-a-custom-error-page-cs/_static/image19.png)](displaying-a-custom-error-page-cs/_static/image18.png)

**圖 7**： [自訂404錯誤] 頁面會顯示比 `Oops.aspx` 更具目標的訊息  
（[按一下以查看完整大小的影像](displaying-a-custom-error-page-cs/_static/image20.png)） 

由於您知道，只有在使用者對找不到的頁面提出要求時，才會到達 [`404.aspx`] 頁面，因此您可以增強此自訂錯誤頁面，以包含可協助使用者解決這種特定類型錯誤的功能。 例如，您可以建立一個資料庫資料表，將已知的錯誤 Url 對應至正確的 Url，然後讓 `404.aspx` 的自訂錯誤頁面對該資料表執行查詢，並建議使用者可能嘗試連接的頁面。

> [!NOTE]
> 只有在對 ASP.NET 引擎所處理的資源提出要求時，才會顯示 [自訂錯誤] 頁面。 如我們在[IIS 與 ASP.NET 程式開發伺服器教學課程之間的核心差異](core-differences-between-iis-and-the-asp-net-development-server-cs.md)中所討論，web 伺服器可能會自行處理特定要求。 根據預設，IIS 網頁伺服器會處理靜態內容（例如影像和 HTML 檔案）的要求，而不會叫用 ASP.NET 引擎。 因此，如果使用者要求不存在的影像檔案，就會收到 IIS 的預設404錯誤訊息，而不是 ASP。NET 已設定的錯誤頁面。

## <a name="summary"></a>總結

當 ASP.NET 應用程式中發生未處理的例外狀況時，使用者會顯示在下列三個錯誤頁面中：例外狀況詳細資料的黃色畫面為死亡;執行階段錯誤的黃色畫面為死亡;或自訂的錯誤頁面。 顯示的錯誤頁面取決於應用程式的 `<customErrors>` 設定，以及使用者是在本機或遠端存取。 預設行為是顯示 YSOD 至本機訪客的例外狀況詳細資料，並將執行階段錯誤 YSOD 至遠端訪客。

雖然執行時間錯誤 YSOD 會從流覽網站的使用者中隱藏潛在的機密錯誤資訊，但它會從您的網站外觀和風格中斷，讓您的應用程式看起來不正確。 較好的方法是使用自訂錯誤網頁，這需要建立和設計自訂錯誤網頁，並在 `<customErrors>` 區段的 `defaultRedirect` 屬性中指定其 URL。 您甚至可以在不同的 HTTP 錯誤狀態中有多個自訂錯誤頁面。

[自訂錯誤] 頁面是針對生產環境中的網站提供完整錯誤處理策略的第一個步驟。 發出錯誤的開發人員警示並記錄其詳細資料，也是很重要的步驟。 接下來的三個教學課程會探索錯誤通知和記錄的技術。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [錯誤頁面，一次](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/)
- [例外狀況的設計方針](https://msdn.microsoft.com/library/ms229014.aspx)
- [使用者易記的錯誤頁面](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [處理和擲回例外狀況](https://msdn.microsoft.com/library/5b2yeyab.aspx)
- [在 ASP.NET 中正確使用自訂錯誤頁面](http://professionalaspnet.com/archive/2007/09/30/Properly-Using-Custom-Error-Pages-in-ASP.NET.aspx)

> [!div class="step-by-step"]
> [上一頁](strategies-for-database-development-and-deployment-cs.md)
> [下一頁](processing-unhandled-exceptions-cs.md)
