---
uid: web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-vb
title: 表單驗證（VB）總覽 |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將從單純的討論變成「執行中」;特別是，我們將探討如何執行表單驗證。 Web 應用程式 。
ms.author: riande
ms.date: 01/14/2008
ms.assetid: 83267f7d-64d9-41ee-82cf-da91b1bf534d
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: d8ceb6b5290300992e52199caa9314c573de1942
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633900"
---
# <a name="an-overview-of-forms-authentication-vb"></a>表單驗證簡介（VB）

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_02_VB.zip)或[下載 PDF](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial02_FormsAuth_vb.pdf)

> 在本教學課程中，我們將從單純的討論變成「執行中」;特別是，我們將探討如何執行表單驗證。 我們在本教學課程中開始建立的 web 應用程式，將會繼續在後續的教學課程中建立，因為我們會從簡單的表單驗證移至成員資格和角色。
> 
> 如需本主題的詳細資訊，請參閱這段影片：[在 ASP.NET 中使用基本的表單驗證](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md)。

## <a name="introduction"></a>簡介

在[先前的教學](security-basics-and-asp-net-support-vb.md)課程中，我們討論了 ASP.NET 所提供的各種驗證、授權和使用者帳戶選項。 在本教學課程中，我們將從單純的討論變成「執行中」;特別是，我們將探討如何執行表單驗證。 我們在本教學課程中開始建立的 web 應用程式，將會繼續在後續的教學課程中建立，因為我們會從簡單的表單驗證移至成員資格和角色。

本教學課程一開始會深入探討表單驗證工作流程，這是我們在上一個教學課程中觸及的主題。 之後，我們將建立 ASP.NET 網站，以示範表單驗證的概念。 接下來，我們會將網站設定為使用表單驗證、建立簡單的登入頁面，以及瞭解如何在程式碼中判斷使用者是否已驗證，如果是的話，他們登入時所使用的使用者名稱。

瞭解表單驗證工作流程、在 web 應用程式中啟用，以及建立登入和登出頁面，都是建立 ASP.NET 應用程式以支援使用者帳戶並透過網頁驗證使用者時的重要步驟。 因此，由於這些教學課程是以另一種方式建立的，因此，即使您已經在過去的專案中設定表單驗證，仍建議您完整地完成本教學課程，再繼續進行下一個教學課程。

## <a name="understanding-the-forms-authentication-workflow"></a>瞭解表單驗證工作流程

當 ASP.NET 執行時間處理 ASP.NET 資源（例如 ASP.NET 網頁或 ASP.NET Web 服務）的要求時，要求會在其生命週期中引發數個事件。 在要求的開頭和結尾都會引發事件，在要求通過驗證和授權時引發，事件發生在未處理的例外狀況時引發，依此類推。 若要查看完整的事件清單，請參閱[HttpApplication 物件的事件](https://msdn.microsoft.com/library/system.web.httpapplication_events.aspx)。

*HTTP 模組*是受管理的類別，其程式碼會執行以回應要求生命週期中的特定事件。 ASP.NET 隨附一些可在幕後執行基本工作的 HTTP 模組。 與我們的討論特別相關的兩個內建 HTTP 模組如下：

- **[又稱為 formsauthenticationmodule](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)** -藉由檢查表單驗證票證（通常包含在使用者的 cookie 集合中）來驗證使用者。 如果沒有表單驗證票證存在，則使用者為匿名。
- **[UrlAuthorizationModule](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)** -判斷目前的使用者是否有權存取要求的 URL。 此模組會藉由查閱應用程式佈建檔中指定的授權規則來判斷授權單位。 ASP.NET 也包含[FileAuthorizationModule](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx) ，可透過諮詢要求的檔案 acl 來判斷授權單位。

在執行 UrlAuthorizationModule （和 FileAuthorizationModule）之前，又稱為 formsauthenticationmodule 會嘗試驗證使用者。 如果提出要求的使用者未獲授權，無法存取要求的資源，則授權模組會終止要求，並傳回[HTTP 401 未經授權](http://www.checkupdown.com/status/E401.html)的狀態。 在 Windows 驗證案例中，會將 HTTP 401 狀態傳回給瀏覽器。 此狀態碼會使瀏覽器透過強制回應對話方塊提示使用者輸入其認證。 不過，使用表單驗證時，HTTP 401 未經授權的狀態永遠不會傳送至瀏覽器，因為又稱為 formsauthenticationmodule 會偵測到此狀態並加以修改，改為將使用者重新導向至登入頁面（透過[HTTP 302 重新導向](http://www.checkupdown.com/status/E302.html)狀態）。

登入頁面的責任是判斷使用者的認證是否有效，如果是，則會建立表單驗證票證，並將使用者重新導向回到他們嘗試造訪的網頁。 驗證票證會包含在網站上頁面的後續要求中，而又稱為 formsauthenticationmodule 會使用此資訊來識別使用者。

[![表單驗證工作流程](an-overview-of-forms-authentication-vb/_static/image2.png)](an-overview-of-forms-authentication-vb/_static/image1.png)

**圖 01**：表單驗證工作流程（[按一下以觀看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image3.png)）

### <a name="remembering-the-authentication-ticket-across-page-visits"></a>跨頁面流覽記住驗證票證

登入之後，表單驗證票證必須在每個要求上傳送回 web 伺服器，讓使用者在流覽網站時保持登入。 這通常是藉由將驗證票證放在使用者的 cookie 集合中完成。 [Cookie](http://en.wikipedia.org/wiki/HTTP_cookie)是位在使用者電腦上的小型文字檔，會在每個要求的 HTTP 標頭中傳輸到建立 cookie 的網站。 因此，一旦表單驗證票證已建立並儲存在瀏覽器的 cookie 中，後續每次造訪該網站時，會連同要求一起傳送驗證票證，藉此識別使用者。

> [!NOTE]
> 每個教學課程中使用的示範 web 應用程式都可供下載。 這個可下載的應用程式是使用以 .NET Framework 版本3.5 為目標的 Visual Web Developer 2008 所建立。 由於應用程式是以 .NET 3.5 為目標，因此其 Web.config 檔案包含額外的3.5 特定設定元素。 簡短故事說，如果您還沒有在電腦上安裝 .NET 3.5，下載的 web 應用程式將無法使用，而不需要先從 Web.config 移除3.5 特定的標記。

Cookie 的其中一個層面就是其到期日，也就是瀏覽器捨棄 cookie 的日期和時間。 當表單驗證 cookie 過期時，使用者將無法再進行驗證，因此會變成匿名。 當使用者從公用終端機造訪時，他們可能會希望其驗證票證在關閉瀏覽器時過期。 不過，從家裡造訪時，同一位使用者可能會想要在瀏覽器重新開機時記住驗證票證，如此一來，他們就不必在每次造訪網站時重新登入。 這項決定通常是由使用者在登入頁面上以 [記住我] 核取方塊的形式進行。 在步驟3中，我們將探討如何在登入頁面中執行 [記住我] 核取方塊。 下列教學課程會詳細說明驗證票證超時設定。

> [!NOTE]
> 用來登入網站的使用者代理程式可能不支援 cookie。 在這種情況下，ASP.NET 可以使用無 cookie 的表單驗證票證。 在此模式中，驗證票證會編碼為 URL。 在下一個教學課程中，我們將探討使用無 cookie 驗證票證的時機，以及如何建立和管理它們。

### <a name="the-scope-of-forms-authentication"></a>表單驗證的範圍

又稱為 formsauthenticationmodule 是 managed 程式碼，屬於 ASP.NET 執行時間的一部分。 在第7版的 Microsoft [Internet Information Services （IIS）](https://www.iis.net/)網頁伺服器之前，IIS 的 HTTP 管線和 ASP.NET 執行時間的管線之間有不同的屏障。 簡單地說，在 IIS 6 和更早版本中，又稱為 formsauthenticationmodule 只會在將要求從 IIS 委派給 ASP.NET 執行時間時執行。 根據預設，IIS 會處理靜態內容本身（例如 HTML 頁面和 CSS 和影像檔案），而且只會在要求副檔名為 .aspx、.asmx 或. ashx 的頁面時，將要求交給 ASP.NET 執行時間。

不過，IIS 7 允許整合式 IIS 和 ASP.NET 管線。 有幾個設定，您可以設定 IIS 7 來叫用*所有*要求的又稱為 formsauthenticationmodule。 此外，透過 IIS 7，您可以為任何類型的檔案定義 URL 授權規則。 如需詳細資訊，請參閱[IIS6 與 IIS7 安全性之間的變更](https://www.iis.net/learn/get-started/whats-new-in-iis-7/changes-in-security-between-iis-60-and-iis-7-and-above)、[您的 Web 平臺安全性](https://www.iis.net/learn/get-started/whats-new-in-iis-7/iis7-and-above-security-improvements)，以及[瞭解 IIS7 URL 授權](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)。

長時間簡短，在 IIS 7 之前的版本中，您只能使用表單驗證來保護 ASP.NET 執行時間所處理的資源。 同樣地，URL 授權規則只會套用至 ASP.NET 執行時間所處理的資源。 但是有了 IIS 7，就可以將又稱為 formsauthenticationmodule 和 UrlAuthorizationModule 整合到 IIS 的 HTTP 管線中，藉此將此功能延伸至所有要求。

## <a name="step-1-creating-an-aspnet-website-for-this-tutorial-series"></a>步驟1：建立本教學課程系列的 ASP.NET 網站

為了達到最廣泛的可能物件，我們將在此系列中建立的 ASP.NET 網站，會使用 Microsoft 的免費版 Visual Studio 2008、 [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)來建立。 我們將在[Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx)資料庫中執行 SqlMembershipProvider 使用者存放區。 如果您使用 Visual Studio 2005 或不同版本的 Visual Studio 2008 或 SQL Server，別擔心，這些步驟將會幾乎相同，而且會指出任何非一般的差異。

我們先需要 ASP.NET 網站，才可以設定表單驗證。 一開始請先建立新的以檔案系統為基礎的 ASP.NET 網站。 若要完成此動作，請啟動 Visual Web Developer，然後移至 [檔案] 功能表，並選擇 [新網站]，顯示 [新網站] 對話方塊。 選擇 [ASP.NET 網站] 範本，將 [位置] 下拉式清單設定為 [檔案系統]，選擇要放置網站的資料夾，然後將語言設定為 VB。 這會建立新的網站，其中包含 default.aspx ASP.NET 網頁、應用程式\_資料夾和 web.config 檔案。

> [!NOTE]
> Visual Studio 支援兩種專案管理模式：網站專案和 Web 應用程式專案。 網站專案缺少專案檔，而 Web 應用程式專案在 Visual Studio .NET 2002/2003 中模擬專案架構-它們包括專案檔，並將專案的原始程式碼編譯成單一元件，並放在/bin 資料夾中。 Visual Studio 2005 一開始只有支援的網站專案，雖然 Web 應用程式專案模型已與 Service Pack 1 一併重新引入，Visual Studio 2008 提供這兩個專案模型。 不過，Visual Web Developer 2005 和2008版本只支援網站專案。 我將使用網站專案模型。 如果您使用非 Express edition，而且想要改為使用[Web 應用程式專案模型](https://msdn.microsoft.com/library/aa730880(vs.80).aspx)，請隨意執行此動作，但請注意，您在畫面上看到的內容和您必須採取的步驟，以及這些教學課程中提供的指示，都可能不一致。

[![建立以檔案系統為基礎的新網站](an-overview-of-forms-authentication-vb/_static/image5.png)](an-overview-of-forms-authentication-vb/_static/image4.png)

**圖 02**：建立以檔案系統為基礎的新網站（[按一下以觀看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image6.png)）

### <a name="adding-a-master-page"></a>加入主版頁面

接下來，在名為 [網站] 的根目錄中，將新的主版頁面新增至網站。 [主版頁面](https://msdn.microsoft.com/library/wtxbf3hh.aspx)可讓網頁開發人員定義可以套用至 ASP.NET 網頁的全網站範本。 主版頁面的主要優點是可以在單一位置定義網站的整體外觀，以便輕鬆地更新或調整網站的版面配置。

[![將名為網站的主版頁面新增至網站](an-overview-of-forms-authentication-vb/_static/image8.png)](an-overview-of-forms-authentication-vb/_static/image7.png)

**圖 03**：將名為網站的主版頁面新增至網站（[按一下以觀看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image9.png)）

在主版頁面中定義整個網站的頁面配置。 您可以使用設計檢視並新增您需要的任何版面配置或 Web 控制項，也可以手動在來源視圖中新增標記。 我將主頁面的版面配置結構化，以模擬在 *[ASP.NET 2.0](../../data-access/index.md)* 教學課程系列中使用資料時所用的版面配置（請參閱 [圖 4]）。 主版頁面會使用[級聯樣式表](http://www.w3schools.com/css/default.asp)來定位和樣式，以及在檔案樣式 .css 中定義的 css 設定（包含在本教學課程的相關下載中）。 雖然您無法從下面所示的標記中得知，但 CSS 規則的定義是讓導覽 &lt;div&gt;的內容絕對是定位，使其顯示在左邊，且固定寬度為200圖元。

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample1.aspx)]

主版頁面會定義靜態頁面配置，以及可由使用主版頁面的 ASP.NET 網頁編輯的區域。 這些可編輯的區域是由 ContentPlaceHolder 控制項所表示，您可以在內容 &lt;div&gt;中看到這些內容。 我們的主版頁面只有一個 ContentPlaceHolder （MainContent），但主版頁面可能會有多個 ContentPlaceHolders。

在上方輸入標記之後，切換到設計檢視會顯示主版頁面的版面配置。 任何使用此主版頁面的 ASP.NET 網頁都將具有此統一版面配置，而且能夠指定 MainContent 區域的標記。

[![主版頁面（透過設計檢視查看時）](an-overview-of-forms-authentication-vb/_static/image11.png)](an-overview-of-forms-authentication-vb/_static/image10.png)

**圖 04**：透過設計檢視查看主版頁面時（[按一下以觀看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image12.png)）

### <a name="creating-content-pages"></a>建立內容頁

此時我們的網站中有預設的 .aspx 頁面，但它不會使用剛剛建立的主版頁面。 雖然您可以操控網頁的宣告式標記來使用主版頁面，但如果網頁未包含任何內容，則只需刪除頁面，然後將它重新加入至專案，並指定要使用的主版頁面，會比較容易。 因此，請從刪除專案中的 default.aspx 開始。

接下來，以滑鼠右鍵按一下 方案總管中的專案名稱，然後選擇新增名為 default.aspx 的新 Web 表單。 這次，請核取 [選取主版頁面] 核取方塊，然後從清單中選擇 [網站] 主版頁面。

[![新增預設的 default.aspx 頁面，選擇選取主版頁面](an-overview-of-forms-authentication-vb/_static/image14.png)](an-overview-of-forms-authentication-vb/_static/image13.png)

**圖 05**：新增新的 default.aspx 頁面選擇以選取主版頁面（[按一下以查看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image15.png)）

[![使用網站。主要主版頁面](an-overview-of-forms-authentication-vb/_static/image17.png)](an-overview-of-forms-authentication-vb/_static/image16.png)

**圖 06**：使用 [網站] 主版頁面（[按一下以觀看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image18.png)）

> [!NOTE]
> 如果您使用 Web 應用程式專案模型，[加入新專案] 對話方塊不會包含 [選取主版頁面] 核取方塊。 相反地，您需要加入 Web 內容表單類型的專案。 選擇 [Web 內容表單] 選項並按一下 [新增] 之後，Visual Studio 將會顯示 [圖 6] 所示的相同 [選取主要] 對話方塊。

新的 default.aspx 頁面的宣告式標記僅包含一個 @Page 指示詞，其中指定主版頁面檔案的路徑和主版頁面的 MainContent ContentPlaceHolder 的內容控制項。

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample2.aspx)]

現在，將 default.aspx 保留為空白。 我們稍後會在本教學課程中返回它來新增內容。

> [!NOTE]
> 我們的主版頁面包含功能表或其他導覽介面的區段。 我們將在未來的教學課程中建立這類介面。

## <a name="step-2-enabling-forms-authentication"></a>步驟2：啟用表單驗證

建立 ASP.NET 網站之後，我們的下一項工作就是啟用表單驗證。 應用程式的驗證設定是透過 Web.config 中的[&lt;authentication&gt; 元素](https://msdn.microsoft.com/library/532aee0e.aspx)所指定。&lt;authentication&gt; 元素包含名為 mode 的單一屬性，它會指定應用程式所使用的驗證模型。 這個屬性可以有下列四個值的其中一個：

- **Windows** -如先前的教學課程所述，當應用程式使用 Windows 驗證時，web 伺服器會負責驗證訪客，而這通常是透過基本、摘要式或整合式 Windows 驗證來完成。
- **表單**-使用者是透過網頁上的表單進行驗證。
- **Passport**-使用者會使用 Microsoft 的 Passport 網路進行驗證。
- **無**-不使用驗證模型;所有的訪客都是匿名的。

根據預設，ASP.NET 應用程式會使用 Windows 驗證。 若要將驗證類型變更為表單驗證，則需要將 &lt;authentication&gt; 元素的模式屬性修改為表單。

如果您的專案尚未包含 web.config 檔案，請在 方案總管中的專案名稱上按一下滑鼠右鍵，選擇 加入新專案，然後新增 Web 設定檔，以立即加入一個檔案。

[![如果您的專案尚未包含 web.config，請立即新增](an-overview-of-forms-authentication-vb/_static/image20.png)](an-overview-of-forms-authentication-vb/_static/image19.png)

**圖 07**：如果您的專案尚未包含 web.config，請立即新增（[按一下以觀看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image21.png)）

接下來，找出 &lt;authentication&gt; 元素，並將它更新為使用表單驗證。 在這項變更之後，您的 web.config 檔案的標記看起來應該如下所示：

[!code-xml[Main](an-overview-of-forms-authentication-vb/samples/sample3.xml)]

> [!NOTE]
> 因為 web.config 是 XML 檔案，所以大小寫很重要。 請確定您已將模式屬性設定為表單，並使用大寫 F。如果您使用不同的大小寫，例如表單，當您透過瀏覽器造訪網站時，將會收到設定錯誤。

&lt;authentication&gt; 元素可以選擇性地包含 &lt;forms&gt; 子項目，其中包含表單驗證特有的設定。 現在，讓我們使用預設的表單驗證設定。 在下一個教學課程中，我們將更詳細地探討 &lt;表單&gt; 子項目。

## <a name="step-3-building-the-login-page"></a>步驟3：建立登入頁面

為了支援表單驗證，我們的網站需要登入頁面。 如瞭解表單驗證工作流程一節中所述，如果使用者嘗試存取未獲授權觀看的頁面，又稱為 formsauthenticationmodule 會自動將其重新導向至登入頁面。 另外還有 ASP.NET 的 Web 控制項，會向匿名使用者顯示登入頁面的連結。 這接踵而來問題，登入頁面的 URL 為何？

根據預設，表單驗證系統會預期登入頁面命名為 Login .aspx，並放在 web 應用程式的根目錄中。 如果您想要使用不同的登入頁面 URL，您可以在 Web.config 中指定它。我們會在後續的教學課程中瞭解如何執行這項操作。

登入頁面有三個責任：

1. 提供可讓訪客輸入其認證的介面。
2. 判斷提交的認證是否有效。
3. 藉由建立表單驗證票證來登入使用者。

### <a name="creating-the-login-pages-user-interface"></a>建立登入頁面的使用者介面

讓我們開始著手進行第一個工作。 將新的 ASP.NET 網頁新增至名為 Login 的網站根目錄，並將其與網站. 主版頁面建立關聯。

[![新增名為 Login .aspx 的 ASP.NET 網頁](an-overview-of-forms-authentication-vb/_static/image23.png)](an-overview-of-forms-authentication-vb/_static/image22.png)

**圖 08**：加入名為 Login 的新 ASP.NET 網頁（[按一下以查看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image24.png)）

一般登入頁面介面包含兩個文字方塊：一個用於使用者的名稱，一個用於密碼，另一個則是用來提交表單的按鈕。 網站通常會包含 [記住我] 核取方塊，如果已核取，則會在瀏覽器重新開機時保存產生的驗證票證。

將兩個文字方塊新增至 [登入 .aspx]，並將其 ID 屬性分別設定為 [使用者名稱和密碼]。 同時將 Password 的 TextMode 屬性設定為 Password。 接下來，新增 CheckBox 控制項，將其 ID 屬性設定為 RememberMe，並將其 Text 屬性設為 [記住我]。 接著，新增名為 LoginButton 的按鈕，其 Text 屬性會設定為 Login。 最後，新增標籤 Web 控制項，並將其 ID 屬性設為 InvalidCredentialsMessage，其 Text 屬性設為您的使用者名稱或密碼無效。 請再試一次。，其前景屬性設為紅色，而其 Visible 屬性設為 False。

此時您的畫面看起來應該類似 [圖 9] 中的螢幕擷取畫面，而頁面的宣告式語法應如下所示：

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample4.aspx)]

[![登入頁面包含兩個文字方塊、一個核取方塊、一個按鈕和一個標籤](an-overview-of-forms-authentication-vb/_static/image26.png)](an-overview-of-forms-authentication-vb/_static/image25.png)

**圖 09**：登入頁面包含兩個文字方塊、一個核取方塊、一個按鈕和一個標籤（[按一下以查看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image27.png)）

最後，建立 LoginButton Click 事件的事件處理常式。 從設計工具中，只要按兩下 [Button] 控制項，即可建立此事件處理常式。

### <a name="determining-if-the-supplied-credentials-are-valid"></a>判斷提供的認證是否有效

我們現在需要在按鈕的 Click 事件處理常式中執行工作 2-判斷提供的認證是否有效。 若要這麼做，必須要有一個使用者存放區來保存所有使用者的認證，才能判斷提供的認證是否與任何已知的認證相符。

在 ASP.NET 2.0 之前，開發人員會負責同時執行自己的使用者存放區，以及撰寫程式碼來驗證針對存放區所提供的認證。 大部分的開發人員會在資料庫中執行使用者存放區，並建立名為 Users 的資料表，其中的資料行如 UserName、Password、Email、LastLoginDate 等等。 然後，此資料表會有每個使用者帳戶的一筆記錄。 驗證使用者提供的認證會牽涉到查詢資料庫中是否有相符的使用者名稱，然後確保資料庫中的密碼雖然該值至所提供的密碼。

使用 ASP.NET 2.0 時，開發人員應該使用其中一個成員資格提供者來管理使用者存放區。 在本教學課程系列中，我們將使用 SqlMembershipProvider，它會針對使用者存放區使用 SQL Server 資料庫。 使用 SqlMembershipProvider 時，我們需要執行特定的資料庫架構，其中包含提供者所預期的資料表、視圖和預存程式。 我們將在 SQL Server 教學課程中的 *[建立成員資格架構](../membership/creating-the-membership-schema-in-sql-server-vb.md)* 中，檢查如何執行此架構。 當成員資格提供者備妥時，驗證使用者的認證就像呼叫[成員資格類別](https://msdn.microsoft.com/library/system.web.security.membership.aspx)的[ValidateUser （使用者*名稱*，*密碼*）方法](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)一樣簡單，它會傳回布林值，指出使用者*名稱*和*密碼*組合的有效性。 因為我們尚未實行 SqlMembershipProvider 的使用者存放區，所以我們目前無法使用成員資格類別的 ValidateUser 方法。

而不是花時間建立自己的自訂使用者資料庫資料表（在我們實 SqlMembershipProvider 之後就會過時），讓我們改為在登入頁面本身中硬式編碼有效的認證。 在 LoginButton 的 Click 事件處理常式中，新增下列程式碼：

[!code-vb[Main](an-overview-of-forms-authentication-vb/samples/sample5.vb)]

如您所見，有三個有效的使用者帳戶-Scott、Jisun 和 Sam，而這三個都有相同的密碼（密碼）。 程式碼會在使用者和密碼陣列中迴圈，以尋找有效的使用者名稱和密碼。 如果使用者名稱和密碼都是有效的，我們必須登入使用者，然後將其重新導向至適當的頁面。 如果認證無效，則會顯示 [InvalidCredentialsMessage] 標籤。

當使用者輸入有效的認證時，我曾說過，他們會被重新導向到適當的頁面。 不過，什麼是適當的頁面？ 回想一下，當使用者造訪未獲授權觀看的頁面時，又稱為 formsauthenticationmodule 會自動將它們重新導向至登入頁面。 在這種情況下，它會透過 ReturnUrl 參數在查詢字串中包含要求的 URL。 也就是說，如果使用者嘗試造訪 ProtectedPage，但未獲授權這麼做，又稱為 formsauthenticationmodule 會將他們重新導向至：

登入 .aspx？ReturnUrl = ProtectedPage .aspx

成功登入之後，應該將使用者重新導向回 ProtectedPage。 或者，使用者可以流覽自己的 volition 登入頁面。 在此情況下，使用者必須在登入後，將他們傳送至根資料夾的 default.aspx 頁面。

### <a name="logging-in-the-user"></a>登入使用者

假設提供的認證有效，我們必須建立表單驗證票證，以便將使用者登入網站。 [System.web 命名空間](https://msdn.microsoft.com/library/system.web.security.aspx)中的[FormsAuthentication 類別](https://msdn.microsoft.com/library/system.web.security.formsauthentication.aspx)提供各種方法，可讓您透過表單驗證系統來登入和登出使用者。 雖然 FormsAuthentication 類別中有數種方法，但我們在這方面有興趣的三種：

- [GetAuthCookie （*username*， *persistCookie*）](https://msdn.microsoft.com/library/system.web.security.formsauthentication.getauthcookie.aspx) -為提供的名稱*username*建立表單驗證票證。 接下來，這個方法會建立並傳回保存驗證票證內容的 HttpCookie 物件。 如果*persistCookie*為 True，則會建立持續性 cookie。
- [SetAuthCookie （*username*， *persistCookie*）](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) -呼叫 GetAuthCookie （*username*， *persistCookie*）方法來產生表單驗證 cookie。 此方法接著會將 GetAuthCookie 傳回的 cookie 新增至 Cookie 集合（假設使用以 cookie 為基礎的表單驗證; 否則，這個方法會呼叫處理無 cookie 票證邏輯的內部類別）。
- [RedirectFromLoginPage （*username*， *persistCookie*）](https://msdn.microsoft.com/library/system.web.security.formsauthentication.redirectfromloginpage.aspx) -此方法會呼叫 SetAuthCookie （*username*， *persistCookie*），然後將使用者重新導向至適當的頁面。

當您需要在將 cookie 寫入 Cookie 集合之前修改驗證票證時，GetAuthCookie 就很方便。 如果您想要建立表單驗證票證，並將它新增至 Cookie 集合，但不想要將使用者重新導向至適當的頁面，SetAuthCookie 就很有用。 也許您想要將它們保留在登入頁面上，或將它們傳送到一些替代頁面。

因為我們想要登入使用者，並將其重新導向至適當的頁面，所以讓我們使用 RedirectFromLoginPage。 更新 LoginButton 的 Click 事件處理常式，以下列程式程式碼取代兩個批註的 TODO 行：

FormsAuthentication. RedirectFromLoginPage （UserName. Text，RememberMe）

建立表單驗證票證時，我們會使用表單驗證票證使用者*名稱*參數的 [使用者名稱] 文字方塊的 [Text] 屬性，以及*persistCookie*參數的 [RememberMe] 核取方塊的核取狀態。

若要測試登入頁面，請在瀏覽器中造訪。 開始輸入不正確認證，例如使用者名稱不對和密碼錯誤。 按一下 [登入] 按鈕時，將會發生回傳，並顯示 InvalidCredentialsMessage 標籤。

[![輸入不正確認證時，會顯示 [InvalidCredentialsMessage] 標籤](an-overview-of-forms-authentication-vb/_static/image29.png)](an-overview-of-forms-authentication-vb/_static/image28.png)

**圖 10**：輸入不正確認證時，會顯示 InvalidCredentialsMessage 標籤（[按一下以查看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image30.png)）

接下來，輸入有效的認證，然後按一下 [登入] 按鈕。 這次回傳時，會建立表單驗證票證，而且您會自動重新導向回 default.aspx。 此時您已登入網站，但沒有任何視覺提示指出您目前已登入。 在步驟4中，我們會瞭解如何以程式設計方式判斷使用者是否已登入，以及如何識別造訪頁面的使用者。

步驟5會檢查將使用者登出網站的技術。

### <a name="securing-the-login-page"></a>保護登入頁面

當使用者輸入自己的認證並提交登入頁面表單時，包含密碼的認證會透過網際網路以*純文字*格式傳送至 web 伺服器。 這表示任何駭客探查網路流量都可以看到使用者名稱和密碼。 若要避免這種情況，請務必使用[安全通訊端層（SSL）](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)來加密網路流量。 這可確保在網頁伺服器收到認證（以及整個網頁的 HTML 標籤）後，就會將它們從離開瀏覽器的時間加密。

除非您的網站包含敏感性資訊，否則您只需要在登入頁面上使用 SSL，而在其他網頁上，則會以純文字方式透過網路傳送使用者的密碼。 您不需要擔心保護表單驗證票證的安全，因為根據預設，它會經過加密和數位簽署（以防止進行篡改）。 在下列教學課程中會提供表單驗證票證安全性的更全面討論。

> [!NOTE]
> 許多財務和醫療網站都設定為在已驗證的使用者可存取的*所有*頁面上使用 SSL。 如果您要建立這類網站，您可以設定表單驗證系統，讓表單驗證票證只能透過安全連線傳輸。 我們將在下一個教學課程 [ *[表單驗證](../membership/creating-the-membership-schema-in-sql-server-vb.md)* 設定] 和 [高級] 主題中查看各種表單驗證設定選項。

## <a name="step-4-detecting-authenticated-visitors-and-determining-their-identity"></a>步驟4：偵測已驗證的訪客並判斷其身分識別

此時，我們已啟用表單驗證，並建立了基本的登入頁面，但我們尚未檢查如何判斷使用者是否已驗證或為匿名。 在某些情況下，我們可能會想要顯示不同的資料或資訊，視已驗證或匿名使用者是否造訪網頁而定。 此外，我們經常需要知道已驗證使用者的身分識別。

讓我們擴充現有的 default.aspx 頁面，以說明這些技巧。 在 default.aspx 中，新增兩個面板控制項，一個名為 AuthenticatedMessagePanel，另一個名為 AnonymousMessagePanel。 在第一個面板中，新增名為 WelcomeBackMessage 的標籤控制項。 在第二個面板中新增超連結控制項，將其 Text 屬性設為 [登入]，並將其 NavigateUrl 屬性設定為 ~/Login.aspx。 此時，default.aspx 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample6.aspx)]

您可能已經猜到，這裡的想法是只向已驗證的訪客顯示 AuthenticatedMessagePanel，而只是對匿名訪客的 AnonymousMessagePanel。 為了達成此目的，我們必須根據使用者是否登入，設定這些面板的可見屬性。

[IsAuthenticated 屬性](https://msdn.microsoft.com/library/system.web.httprequest.isauthenticated.aspx)會傳回布林值，指出是否已驗證要求。 在頁面中輸入下列程式碼\_載入事件處理常式程式碼：

[!code-vb[Main](an-overview-of-forms-authentication-vb/samples/sample7.vb)]

將此程式碼備妥之後，請透過瀏覽器造訪 default.aspx。 假設您尚未登入，您會看到登入頁面的連結（請參閱 [圖 11]）。 按一下此連結並登入網站。 如我們在步驟3中所見，在輸入您的認證之後，您會回到 default.aspx，但這次頁面會顯示 [歡迎回來]！ 訊息（請參閱 [圖 12]）。

[![以匿名方式造訪時，會顯示 [登入] 連結](an-overview-of-forms-authentication-vb/_static/image32.png)](an-overview-of-forms-authentication-vb/_static/image31.png)

**圖 11**：匿名造訪時，會顯示 [登入] 連結（[按一下以查看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image33.png)）

[![已驗證的使用者會顯示為歡迎回來！消息](an-overview-of-forms-authentication-vb/_static/image35.png)](an-overview-of-forms-authentication-vb/_static/image34.png)

**圖 12**：已驗證的使用者會顯示在歡迎畫面上！ 訊息（[按一下以查看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image36.png)）

我們可以透過[HttpCoNtext 物件](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)的[使用者屬性](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx)來判斷目前登入的使用者身分識別。 HttpCoNtext 物件代表目前要求的相關資訊，而這是這類常見 ASP.NET 物件的首頁，做為回應、要求和會話等。 User 屬性代表目前 HTTP 要求的安全性內容，並會執行[IPrincipal 介面](https://msdn.microsoft.com/library/system.security.principal.iprincipal.aspx)。

User 屬性是由又稱為 formsauthenticationmodule 所設定。 具體而言，當又稱為 formsauthenticationmodule 在連入要求中找到表單驗證票證時，它會建立新的 GenericPrincipal 物件，並將它指派給使用者屬性。

Principal 物件（例如 GenericPrincipal）會提供使用者身分識別及其所屬角色的相關資訊。 IPrincipal 介面會定義兩個成員：

- [IsInRole （](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole.aspx)角色角色）-傳回布林值的方法，指出主體是否屬於指定的角色。
- [Identity](https://msdn.microsoft.com/library/system.security.principal.iprincipal.identity.aspx) -傳回執行[IIdentity 介面](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx)之物件的屬性。 IIdentity 介面會定義三個屬性： [AuthenticationType](https://msdn.microsoft.com/library/system.security.principal.iidentity.authenticationtype.aspx)、 [IsAuthenticated](https://msdn.microsoft.com/library/system.security.principal.iidentity.isauthenticated.aspx)和[Name](https://msdn.microsoft.com/library/system.security.principal.iidentity.name.aspx)。

我們可以使用下列程式碼來判斷目前訪客的名稱：

Dim currentUsersName As String = User.Identity.Name

使用表單驗證時，會針對 GenericPrincipal 的 Identity 屬性建立[FormsIdentity 物件](https://msdn.microsoft.com/library/system.web.security.formsidentity.aspx)。 FormsIdentity 類別一律會傳回其 AuthenticationType 屬性的字串表單，並針對其 IsAuthenticated 屬性傳回 True。 Name 屬性會傳回建立表單驗證票證時所指定的使用者名稱。 除了這三個屬性之外，FormsIdentity 還包含透過其[票證屬性](https://msdn.microsoft.com/library/system.web.security.formsidentity.ticket.aspx)存取基礎驗證票證的功能。 Ticket 屬性會傳回[FormsAuthenticationTicket](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx)類型的物件，其屬性如逾期、IsPersistent、IssueDate、Name 等等。

這裡要注意的重點是，FormsAuthentication. GetAuthCookie （*username*， *PersistCookie*）、FormsAuthentication. SetAuthCookie （*Username，* *persistCookie*）和 FormsAuthentication. RedirectFromLoginPage （*username*， *persistCookie*）方法中指定的*username*參數，與 User.Identity.Name 所傳回的值相同。 此外，藉由將 User. Identity 轉換成 FormsIdentity 物件，然後存取 Ticket 屬性，即可使用這些方法所建立的驗證票證：

Dim ident As FormsIdentity = CType （User. Identity，FormsIdentity）

Dim authTicket As FormsAuthenticationTicket = ident。票

讓我們在 default.aspx 中提供更個人化的訊息。 更新頁面\_載入事件處理常式，以便將 WelcomeBackMessage 標籤的 Text 屬性指派給 [歡迎使用的字串]、[使用者*名稱*]！

WelcomeBackMessage。 Text = "歡迎回來" &amp; User.Identity.Name &amp; "！"

[圖 13] 顯示這項修改的效果（以使用者 Scott 的身分登入）。

[![歡迎訊息包含目前登入的使用者名稱](an-overview-of-forms-authentication-vb/_static/image38.png)](an-overview-of-forms-authentication-vb/_static/image37.png)

**圖 13**：歡迎訊息包含目前登入的使用者名稱（[按一下以查看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image39.png)）

### <a name="using-the-loginview-and-loginname-controls"></a>使用 LoginView 和 LoginName 控制項

將不同的內容顯示給已驗證和匿名的使用者是常見的需求;因此，會顯示目前登入之使用者的名稱。 基於這個理由，ASP.NET 包含兩個 Web 控制項，提供如 [圖 13] 所示的相同功能，但不需要撰寫一行程式碼。

[LoginView 控制項](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx)是以範本為基礎的 Web 控制項，可讓您輕鬆地向已驗證和匿名的使用者顯示不同的資料。 LoginView 包含兩個預先定義的範本：

- AnonymousTemplate-加入此範本的任何標記只會向匿名訪客顯示。
- LoggedInTemplate-此範本的標記只會顯示給已驗證的使用者。

讓我們將 LoginView 控制項新增至網站的主版頁面：網站。 除了只新增 LoginView 控制項，讓我們新增新的 ContentPlaceHolder 控制項，然後將 LoginView 控制項放在該新 ContentPlaceHolder 中。 這種決策的基本原理很快就會變得顯而易見。

> [!NOTE]
> 除了 AnonymousTemplate 和 LoggedInTemplate，LoginView 控制項也可以包含角色特定的範本。 角色特定範本只會對屬於指定角色的使用者顯示標記。 我們將在未來的教學課程中，檢查 LoginView 控制項的角色式功能。

首先，將名為 LoginContent 的 ContentPlaceHolder 加入至導覽 &lt;div&gt; 元素中的主版頁面。 您可以直接將 ContentPlaceHolder 控制項從 [工具箱] 拖曳至 [來源] 視圖，將產生的標記放在 [TODO：] 功能表的上方。

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample8.aspx)]

接下來，在 LoginContent ContentPlaceHolder 中新增 LoginView 控制項。 放在主版頁面 ContentPlaceHolder 控制項中的內容會被視為 ContentPlaceHolder 的*預設內容*。 也就是說，使用此主版頁面的 ASP.NET 網頁可以為每個 ContentPlaceHolder 指定自己的內容，或使用主版頁面的預設內容。

LoginView 和其他登入相關的控制項位於 [工具箱] 的 [登入] 索引標籤中。

[![[工具箱] 中的 LoginView 控制項](an-overview-of-forms-authentication-vb/_static/image41.png)](an-overview-of-forms-authentication-vb/_static/image40.png)

**圖 14**： [工具箱] 中的 LoginView 控制項（[按一下以查看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image42.png)）

接下來，在 LoginView 控制項之後立即加入兩個 &lt;br/&gt; 元素，但仍在 ContentPlaceHolder 內。 此時，導覽 &lt;div&gt; 元素的標記應該如下所示：

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample9.aspx)]

您可以從設計工具或宣告式標記定義 LoginView 的範本。 從 Visual Studio 的設計工具中，展開 LoginView 的智慧標籤，它會在下拉式清單中列出已設定的範本。 輸入文字 Hello，stranger 到 AnonymousTemplate;接下來，新增超連結控制項，並將其 Text 和 NavigateUrl 屬性分別設定為登入和 ~/Login.aspx。

設定 AnonymousTemplate 之後，請切換至 LoggedInTemplate 並輸入「歡迎回來」文字。 然後將 LoginName 控制項從 [工具箱] 拖曳至 LoggedInTemplate，並將它放在「歡迎回來」文字後面。 [LoginName 控制項](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginname.aspx)如其名所示，會顯示目前登入之使用者的名稱。 就內部而言，LoginName 控制項只會輸出 User.Identity.Name 屬性

將這些專案新增至 LoginView 的範本之後，標記看起來應該如下所示：

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample10.aspx)]

透過此網站的新增功能，網站中的每個頁面都會根據使用者是否經過驗證，顯示不同的訊息。 [圖 15] 顯示使用者 Jisun 透過瀏覽器造訪時的 default.aspx 頁面。 [歡迎使用] Jisun 訊息重複出現兩次：一次在主版頁面的導覽區段中（透過我們剛才新增的 LoginView 控制項），以及一次在 default.aspx 的內容區域中（透過 [面板控制項] 和 [程式設計邏輯]）。

[![LoginView 控制項會顯示 [歡迎回來]、[Jisun]。](an-overview-of-forms-authentication-vb/_static/image44.png)](an-overview-of-forms-authentication-vb/_static/image43.png)

**圖 15**： LoginView 控制項顯示歡迎回來，Jisun。 （[按一下以查看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image45.png)）

因為我們已將 LoginView 新增至主版頁面，所以它可能會出現在網站上的每個頁面中。 不過，您可能會有不想顯示此訊息的網頁。 其中一個頁面是登入頁面，因為登入頁面的連結似乎不在該處。 由於我們將 LoginView 控制項放在主版頁面的 ContentPlaceHolder 中，因此我們可以在內容頁面中覆寫此預設標記。 開啟 Login .aspx 並移至設計工具。 由於我們尚未在主版頁面中明確定義 LoginContent ContentPlaceHolder 的內容控制項，登入頁面將會顯示此 ContentPlaceHolder 的主版頁面預設標記。 您可以透過設計工具查看這一點-[LoginContent] ContentPlaceHolder 會顯示預設標記（LoginView 控制項）。

[![登入頁面會顯示主版頁面的 LoginContent ContentPlaceHolder 的預設內容](an-overview-of-forms-authentication-vb/_static/image47.png)](an-overview-of-forms-authentication-vb/_static/image46.png)

**圖 16**：登入頁面會顯示主版頁面的 LoginContent ContentPlaceHolder 的預設內容（[按一下以觀看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image48.png)）

若要覆寫 LoginContent ContentPlaceHolder 的預設標記，只要以滑鼠右鍵按一下設計工具中的區域，然後從內容功能表選擇 [建立自訂內容] 選項即可。 （使用 Visual Studio 2008 時，ContentPlaceHolder 會包含智慧標籤，在選取時，會提供相同的選項）。這會將新的內容控制項加入頁面的標記中，因此可讓我們定義此頁面的自訂內容。 您可以在這裡新增自訂訊息，例如，請登入，但讓我們將此內容保留空白。

> [!NOTE]
> 在 Visual Studio 2005 中，建立自訂內容會在 [ASP.NET] 頁面中建立空白的內容控制項。 不過，在 Visual Studio 2008 中，建立自訂內容會將主版頁面的預設內容複寫到新建立的內容控制項。 如果您使用 Visual Studio 2008，則在建立新的內容控制項之後，請務必清除從主版頁面複製的內容。

[圖 17] 顯示在進行這種變更之後，從瀏覽器造訪的登入 .aspx 頁面。 請注意，左側導覽中沒有 [Hello]、[stranger] 或 [歡迎使用]、[使用者*名稱*] 訊息，&lt;div&gt;，如同造訪 default.aspx 時的情況。

[![登入頁面會隱藏預設 LoginContent ContentPlaceHolder 的標記](an-overview-of-forms-authentication-vb/_static/image50.png)](an-overview-of-forms-authentication-vb/_static/image49.png)

**圖 17**：登入頁面會隱藏預設 LoginContent ContentPlaceHolder 的標記（[按一下以查看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image51.png)）

## <a name="step-5-logging-out"></a>步驟5：登出

在步驟3中，我們探討了如何建立登入頁面，將使用者登入網站，但我們還沒看到如何將使用者登出。除了在中記錄使用者的方法之外，FormsAuthentication 類別也會提供[SignOut 方法](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)。 SignOut 方法只會終結表單驗證票證，因而將使用者登出網站。

提供登出連結是常見的功能，ASP.NET 包含特別設計來登出使用者的控制項。[LoginStatus 控制項會](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginstatus.aspx)根據使用者的驗證狀態，顯示登入 LinkButton 或登出 LinkButton。 匿名使用者會呈現登入 LinkButton，而已驗證的使用者會看到登出 LinkButton。 您可以透過 LoginStatus 的 LoginText 和 LogoutText 屬性來設定登入和登出 LinkButtons 的文字。

按一下登入 LinkButton 會導致回傳，其中會將重新導向發出至登入頁面。 按一下 [登出] LinkButton 會導致 LoginStatus 控制項叫用 FormsAuthentication 方法，然後將使用者重新導向至頁面。 已登出使用者的重新導向目標頁面取決於 LogoutAction 屬性，其可指派給下列三個值的其中一個：

- Refresh-預設值;將使用者重新導向至他們剛造訪的網頁。 如果他們剛造訪的頁面不允許匿名使用者，則又稱為 formsauthenticationmodule 會自動將使用者重新導向至登入頁面。

您可能想知道在這裡執行重新導向的原因。 如果使用者想要保留在相同的頁面上，為什麼需要明確的重新導向？ 原因是當按下 [登出] LinkButton 時，使用者在其 cookie 集合中仍會有表單驗證票證。 因此，回傳要求是已驗證的要求。 LoginStatus 控制項會呼叫 SignOut 方法，但在又稱為 formsauthenticationmodule 已經驗證使用者之後就會發生這種情況。 因此，明確的重新導向會導致瀏覽器重新要求頁面。 當瀏覽器重新要求頁面時，表單驗證票證已移除，因此連入要求是匿名的。

- 重新導向-使用者會重新導向至 LoginStatus 的 LogoutPageUrl 屬性所指定的 URL。
- RedirectToLoginPage-使用者會重新導向至登入頁面。

讓我們將 LoginStatus 控制項新增至主版頁面，並將它設定為使用 [重新導向] 選項，將使用者傳送至顯示訊息的頁面，確認已登出。首先，在名為 [登出 .aspx] 的根目錄中建立頁面。 別忘了將此頁面與網站的主版頁面產生關聯。 接下來，在頁面的標記中輸入一則訊息，向使用者說明他們已登出。

接下來，返回 [網站] 主版頁面，並在 LoginContent ContentPlaceHolder 中的 LoginView 底下新增 LoginStatus 控制項。 將 LoginStatus 控制項的 LogoutAction 屬性設為 [重新導向]，並將其 LogoutPageUrl 屬性設定為 ~/Logout.aspx。

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample11.aspx)]

由於 LoginStatus 是在 LoginView 控制項外，因此匿名和已驗證的使用者都會出現這種情況，但這是正常的，因為 LoginStatus 會正確顯示登入或登出 LinkButton。 透過新增 LoginStatus 控制項，AnonymousTemplate 中的 [登入] 超連結是多餘的，因此請將它移除。

[圖 18] 顯示 Jisun 造訪時的 default.aspx。 請注意，左欄會顯示訊息、歡迎返回、Jisun 以及登出的連結。按一下 [登出] LinkButton 會導致回傳、將 Jisun 登出系統，然後將她重新導向至 [登出]。 如 [圖 19] 所示，Jisun 到達登出時，她已經登出，因此是匿名的。 因此，左欄會顯示 [歡迎使用]、[stranger] 和登入頁面的連結。

[![default.aspx 會顯示 [歡迎回來]、[Jisun] 和 [登出 LinkButton]](an-overview-of-forms-authentication-vb/_static/image53.png)](an-overview-of-forms-authentication-vb/_static/image52.png)

**圖 18**： Default.aspx 顯示歡迎回來、Jisun 以及登出 LinkButton （[按一下以觀看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image54.png)）

[![登出 會顯示 [歡迎使用]、[stranger] 和登入 LinkButton](an-overview-of-forms-authentication-vb/_static/image56.png)](an-overview-of-forms-authentication-vb/_static/image55.png)

**圖 19**：登出 .Aspx 會顯示 [歡迎]、[stranger] 和登入 LinkButton （[按一下以查看完整大小的影像](an-overview-of-forms-authentication-vb/_static/image57.png)）

> [!NOTE]
> 我建議您自訂 [登出 .aspx] 頁面，以隱藏主版頁面的 LoginContent ContentPlaceHolder （就像我們在步驟4中的 Login .aspx 所做的一樣）。 原因是因為 LoginStatus 控制項所轉譯的登入 LinkButton （Hello、stranger 底下的）會將使用者傳送至登入頁面，並在 ReturnUrl querystring 參數中傳遞目前的 URL。 簡單地說，如果已登出的使用者按一下這個 LoginStatus 的登入 LinkButton，然後登入，則會將他們重新導向回 [登出]，這可能會讓使用者輕鬆混淆。

## <a name="summary"></a>總結

在本教學課程中，我們會先檢查表單驗證工作流程，然後在 ASP.NET 應用程式中開始執行表單驗證。 表單驗證由又稱為 formsauthenticationmodule 提供技術支援，其具有兩種責任：根據表單驗證票證來識別使用者，並將未經授權的使用者重新導向至登入頁面。

.NET Framework 的 FormsAuthentication 類別包含用來建立、檢查和移除表單驗證票證的方法。 IsAuthenticated 屬性和 User 物件會提供額外的程式設計支援，以判斷要求是否已驗證，以及使用者身分識別的相關資訊。 此外，還有 LoginView、LoginStatus 和 LoginName Web 控制項，可提供開發人員快速、無程式碼的方式，來執行許多常見的登入相關工作。 在未來的教學課程中，我們將更詳細地探討這些和其他登入相關的 Web 控制項。

本教學課程為表單驗證提供粗略的總覽。 我們不會檢查各種設定選項、查看無 cookie 表單驗證票證的使用方式，或探索 ASP.NET 如何保護表單驗證票證的內容。 在[下一個教學](forms-authentication-configuration-and-advanced-topics-vb.md)課程中，我們將討論這些主題和更多內容。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [IIS6 與 IIS7 安全性之間的變更](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [登入 ASP.NET 控制項](https://msdn.microsoft.com/library/d51ttbhx.aspx)
- [Professional ASP.NET 2.0 安全性、成員資格和角色管理](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html)（ISBN：978-0-7645-9698-8）
- [&lt;authentication&gt; 元素](https://msdn.microsoft.com/library/532aee0e.aspx)
- [&lt;驗證的 &lt;表單&gt; 元素&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>本教學課程中所含主題的影片訓練

- [在 ASP.NET 中使用基本的表單驗證](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md)

### <a name="about-the-author"></a>關於作者

Scott Mitchell，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是 *[在24小時內讓自己的 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 Scott 可以在[mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者包括 Alicja Maziarz、John Suru 和 Teresa Murphy。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)的那一行下拉式。

> [!div class="step-by-step"]
> [上一頁](security-basics-and-asp-net-support-vb.md)
> [下一頁](forms-authentication-configuration-and-advanced-topics-vb.md)
