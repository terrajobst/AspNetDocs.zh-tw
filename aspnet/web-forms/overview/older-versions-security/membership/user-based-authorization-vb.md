---
uid: web-forms/overview/older-versions-security/membership/user-based-authorization-vb
title: 以使用者為基礎的授權（VB） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將探討如何限制頁面的存取權，並透過各種不同的技術來限制頁面層級的功能。
ms.author: riande
ms.date: 01/18/2008
ms.assetid: bc937e9d-5c14-4fc4-aec7-440da924dd18
msc.legacyurl: /web-forms/overview/older-versions-security/membership/user-based-authorization-vb
msc.type: authoredcontent
ms.openlocfilehash: dfac0c6fa955e59c6ea996533f2447e89ec8d468
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74588210"
---
# <a name="user-based-authorization-vb"></a>以使用者為基礎的授權 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_07_VB.zip)或[下載 PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial07_UserAuth_vb.pdf)

> 在本教學課程中，我們將探討如何限制頁面的存取權，並透過各種不同的技術來限制頁面層級的功能。

## <a name="introduction"></a>簡介

大部分提供使用者帳戶的 web 應用程式都有這樣的部分，以限制某些訪客存取網站內的特定頁面。 在大部分的線上 messageboard 網站中（例如，所有使用者-匿名和已驗證）都能夠查看 messageboard 的文章，但只有經過驗證的使用者可以造訪網頁來建立新的貼文。 而且可能只有特定使用者可以存取的系統管理頁面（或一組特定的使用者）。 此外，頁面層級的功能可能會因使用者而異。 當您流覽文章清單時，已驗證的使用者會看到一個介面來評等每一篇文章，而匿名訪客則無法使用此介面。

ASP.NET 可讓您輕鬆地定義以使用者為基礎的授權規則。 只有在 `Web.config`中的標記，可以鎖定特定的網頁或整個目錄，使其只能供指定的使用者子集存取。 頁面層級功能可以根據目前登入的使用者，透過程式設計和宣告式方式來開啟或關閉。

在本教學課程中，我們將探討如何限制頁面的存取權，並透過各種不同的技術來限制頁面層級的功能。 讓我們開始吧！

## <a name="a-look-at-the-url-authorization-workflow"></a>查看 URL 授權工作流程

如「[*表單驗*](../introduction/an-overview-of-forms-authentication-vb.md)證」教學課程中所述，當 ASP.NET 執行時間處理 ASP.NET 資源的要求時，要求會在其生命週期中引發數個事件。 *HTTP 模組*是受管理的類別，其程式碼會執行以回應要求生命週期中的特定事件。 ASP.NET 隨附一些可在幕後執行基本工作的 HTTP 模組。

其中一個[`FormsAuthenticationModule`](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)的 HTTP 模組。 如先前的教學課程中所討論，`FormsAuthenticationModule` 的主要功能是判斷目前要求的身分識別。 這是藉由檢查表單驗證票證（位於 cookie 中，或內嵌在 URL 內）來完成。 此識別會在[`AuthenticateRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)期間進行。

另一個重要的 HTTP 模組是[`UrlAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)，會因回應[`AuthorizeRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)而引發（發生在 `AuthenticateRequest` 事件之後）。 `UrlAuthorizationModule` 會檢查 `Web.config` 中的設定標記，以判斷目前的身分識別是否有權造訪指定的頁面。 此進程稱為*URL 授權*。

我們將在步驟1中檢查 URL 授權規則的語法，但首先讓我們看看 `UrlAuthorizationModule` 如何執行，視要求是否已授權而定。 如果 `UrlAuthorizationModule` 判斷要求已獲得授權，則它不會執行任何作業，而且要求會繼續通過其生命週期。 不過，如果要求*未*獲得授權，則 `UrlAuthorizationModule` 會中止生命週期，並指示 `Response` 物件傳回[HTTP 401 未經授權](http://www.checkupdown.com/status/E401.html)的狀態。 使用表單驗證時，此 HTTP 401 狀態永遠不會傳回用戶端，因為如果 `FormsAuthenticationModule` 偵測到 HTTP 401 狀態，則會將它修改為[HTTP 302 重新導向](http://www.checkupdown.com/status/E302.html)至登入頁面。

[圖 1] 說明 ASP.NET 管線的工作流程、`FormsAuthenticationModule`，以及未獲授權的要求抵達時的 `UrlAuthorizationModule`。 特別是，[圖 1] 顯示 `ProtectedPage.aspx`的匿名訪客提出的要求，此頁面會拒絕匿名使用者的存取。 由於訪客是匿名的，因此 `UrlAuthorizationModule` 會中止要求，並傳回 HTTP 401 未經授權的狀態。 然後，`FormsAuthenticationModule` 會將401狀態轉換成302重新導向至登入頁面。 使用者通過登入頁面驗證之後，會被重新導向至 `ProtectedPage.aspx`。 這次 `FormsAuthenticationModule` 會根據他的驗證票證來識別使用者。 現在，訪客已通過驗證，`UrlAuthorizationModule` 允許存取頁面。

[![表單驗證和 URL 授權工作流程](user-based-authorization-vb/_static/image2.png)](user-based-authorization-vb/_static/image1.png)

**圖 1**：表單驗證和 URL 授權工作流程（[按一下以查看完整大小的影像](user-based-authorization-vb/_static/image3.png)）

[圖 1] 說明當匿名訪客嘗試存取匿名使用者無法使用的資源時，所發生的互動。 在這種情況下，匿名訪客會被重新導向至登入頁面，而她嘗試造訪 querystring 中指定的頁面。 使用者成功登入後，她會自動重新導向回到她最初嘗試查看的資源。

當匿名使用者提出未經授權的要求時，此工作流程很簡單，而且訪客很容易就能瞭解發生了什麼事和原因。 但請記住，`FormsAuthenticationModule` 會將*任何*未經授權的使用者重新導向至登入頁面，即使要求是由已驗證的使用者所提出。 如果已驗證的使用者嘗試造訪她缺少授權的頁面，這可能會造成混淆的使用者體驗。

假設我們的網站已設定其 URL 授權規則，讓 ASP.NET 網頁 `OnlyTito.aspx` 只存取然後順著至 Tito。 現在，假設 Sam 造訪網站、登入，然後嘗試造訪 `OnlyTito.aspx`。 `UrlAuthorizationModule` 將會暫停要求生命週期，並傳回 HTTP 401 未授權狀態，`FormsAuthenticationModule` 將會偵測到並將 Sam 重新導向至登入頁面。 不過，由於 Sam 已經登入，因此可能會想知道她為什麼會送回登入頁面。 她可能是因為他的登入認證因某種原因而遺失，或她輸入了不正確認證。 如果 Sam 從登入頁面重新進入她的認證，她將會再次登入（再次），並將其重新導向至 `OnlyTito.aspx`。 `UrlAuthorizationModule` 會偵測到 Sam 無法造訪此頁面，她將會回到登入頁面。

[圖 2] 說明這種令人困惑的工作流程。

[![預設工作流程可能會導致令人困惑的迴圈](user-based-authorization-vb/_static/image5.png)](user-based-authorization-vb/_static/image4.png)

**圖 2**：預設工作流程可能會導致令人困惑的迴圈（[按一下以觀看完整大小的影像](user-based-authorization-vb/_static/image6.png)）

[圖 2] 中所述的工作流程，可以快速 befuddle，甚至是電腦上最聰明的訪客。 我們將在步驟2中探討避免這種混亂週期的方法。

> [!NOTE]
> ASP.NET 使用兩種機制來判斷目前的使用者是否可以存取特定的網頁： URL 授權和檔案授權。 「檔案授權」是由[`FileAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx)所執行，它會透過諮詢要求的檔案 acl 來判斷授權單位。 檔案授權最常用於 Windows 驗證，因為 Acl 是適用于 Windows 帳戶的許可權。 使用表單驗證時，不論造訪網站的使用者為何，所有作業系統和檔案系統層級的要求都會由相同的 Windows 帳戶執行。 由於本教學課程系列著重于表單驗證，因此我們不會討論檔案授權。

### <a name="the-scope-of-url-authorization"></a>URL 授權的範圍

`UrlAuthorizationModule` 是 managed 程式碼，屬於 ASP.NET 執行時間的一部分。 在第7版的 Microsoft [Internet Information Services （IIS）](https://www.iis.net/)網頁伺服器之前，IIS 的 HTTP 管線和 ASP.NET 執行時間的管線之間有不同的屏障。 簡單地說，在 IIS 6 和更早版本中，ASP。只有在將要求從 IIS 委派給 ASP.NET 執行時間時，才會執行 NET 的 `UrlAuthorizationModule`。 根據預設，IIS 會處理靜態內容本身（例如 HTML 頁面和 CSS、JavaScript 和影像檔案），而且只會在要求副檔名為 `.aspx`、`.asmx`或 `.ashx` 的頁面時，將要求交給 ASP.NET 執行時間。

不過，IIS 7 允許整合式 IIS 和 ASP.NET 管線。 透過幾個設定，您可以設定 IIS 7 來叫用*所有*要求的 `UrlAuthorizationModule`，這表示可以為任何類型的檔案定義 URL 授權規則。 此外，IIS 7 還包含自己的 URL 授權引擎。 如需有關 ASP.NET 整合和 IIS 7 原生 URL 授權功能的詳細資訊，請參閱[瞭解 IIS7 Url 授權](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)。 若要深入瞭解 ASP.NET 和 IIS 7 的整合，請挑選一份 Shahram Khosravi 的書籍、*專業的 IIS 7 和 ASP.NET 整合*式程式設計（ISBN：978-0470152539）。

簡言之，在 IIS 7 之前的版本中，URL 授權規則只會套用至 ASP.NET 執行時間所處理的資源。 但是在 IIS 7 中，您可以使用 IIS 的原生 URL 授權功能或來整合 ASP。NET 的 `UrlAuthorizationModule` 放入 IIS 的 HTTP 管線，藉此將此功能延伸至所有要求。

> [!NOTE]
> ASP 的方式有一些微妙但重要的差異。NET 的 `UrlAuthorizationModule` 和 IIS 7 的 URL 授權功能會處理授權規則。 本教學課程不會檢查 IIS 7 的 URL 授權功能，或與 `UrlAuthorizationModule`相較之下，如何剖析授權規則的差異。 如需有關這些主題的詳細資訊，請參閱 MSDN 上的 IIS 7 檔或[www.iis.net](https://www.iis.net/)。

## <a name="step-1-defining-url-authorization-rules-inwebconfig"></a>步驟1：在`Web.config` 中定義 URL 授權規則

`UrlAuthorizationModule` 根據應用程式設定中定義的 URL 授權規則，決定是否要授與或拒絕特定身分識別的要求資源存取權。 授權規則會在[`<authorization>` 元素](https://msdn.microsoft.com/library/8d82143t.aspx)中以 `<allow>` 和 `<deny>` 子專案的形式拼出。 每個 `<allow>` 和 `<deny>` 子項目都可以指定：

- 特定使用者
- 以逗號分隔的使用者清單
- 所有匿名使用者，以問號（？）表示
- 所有使用者，以星號表示（\*）

下列標記說明如何使用 URL 授權規則，讓使用者 Tito 和 Scott，並拒絕所有其他人：

[!code-xml[Main](user-based-authorization-vb/samples/sample1.xml)]

`<allow>` 元素會定義允許的使用者（Tito 和 Scott），而 `<deny>` 元素會指示*所有*使用者遭到拒絕。

> [!NOTE]
> `<allow>` 和 `<deny>` 元素也可以指定角色的授權規則。 我們將在未來的教學課程中檢查以角色為基礎的授權。

下列設定會將存取權授與 Sam 以外的任何人（包括匿名訪客）：

[!code-xml[Main](user-based-authorization-vb/samples/sample2.xml)]

若只要允許已驗證的使用者，請使用下列設定，這會拒絕所有匿名使用者的存取：

[!code-xml[Main](user-based-authorization-vb/samples/sample3.xml)]

授權規則定義于 `Web.config` 中的 `<system.web>` 元素內，並套用至 web 應用程式中的所有 ASP.NET 資源。 應用程式經常會有不同區段的不同授權規則。 例如，在電子商務網站上，所有訪客可能會詳閱產品、查看產品評論、搜尋目錄等等。 不過，只有已驗證的使用者可能會到達簽出或頁面，以管理一份出貨歷程記錄。 此外，只有選取的使用者（例如網站管理員）可以存取網站的某些部分。

ASP.NET 可讓您輕鬆地為網站中不同的檔案和資料夾定義不同的授權規則。 根資料夾的 `Web.config` 檔案中指定的授權規則適用于網站中的所有 ASP.NET 資源。 不過，藉由新增具有 `<authorization>` 區段的 `Web.config`，可以覆寫特定資料夾的這些預設授權設定。

讓我們更新我們的網站，讓只有經過驗證的使用者可以造訪 `Membership` 資料夾中的 ASP.NET 網頁。 若要完成此動作，我們必須將 `Web.config` 檔案新增至 `Membership` 資料夾，並將其授權設定設為拒絕匿名使用者。 以滑鼠右鍵按一下方案總管中的 [`Membership`] 資料夾，選擇操作功能表中的 [加入新專案] 功能表，然後新增名為 `Web.config`的新 Web 設定檔案。

[![將 Web.config 檔案新增至成員資格資料夾](user-based-authorization-vb/_static/image8.png)](user-based-authorization-vb/_static/image7.png)

**圖 3**：將 `Web.config` 檔案新增至 [`Membership`] 資料夾（[按一下以查看完整大小的影像](user-based-authorization-vb/_static/image9.png)）

此時，您的專案應該包含兩個 `Web.config` 檔案：一個在根目錄，另一個在 `Membership` 資料夾中。

[![您的應用程式現在應該包含兩個 Web.config 檔案](user-based-authorization-vb/_static/image11.png)](user-based-authorization-vb/_static/image10.png)

**圖 4**：您的應用程式現在應該包含兩個 `Web.config` 檔案（[按一下以查看完整大小的影像](user-based-authorization-vb/_static/image12.png)）

更新 `Membership` 資料夾中的設定檔，使其禁止匿名使用者的存取。

[!code-xml[Main](user-based-authorization-vb/samples/sample4.xml)]

這樣就全部完成了！

若要測試這項變更，請造訪瀏覽器中的首頁，並確認您已登出。由於 ASP.NET 應用程式的預設行為是允許所有訪客，而且因為我們並未對根目錄的 `Web.config` 檔案進行任何授權修改，所以我們能夠以匿名訪客的身分造訪根目錄中的檔案。

按一下左欄中的 [建立使用者帳戶] 連結。 這會帶您前往 `~/Membership/CreatingUserAccounts.aspx`。 由於 [`Membership`] 資料夾中的 `Web.config` 檔案定義了禁止匿名存取的授權規則，因此 `UrlAuthorizationModule` 會中止要求並傳回 HTTP 401 未經授權的狀態。 `FormsAuthenticationModule` 會將此修改為302重新導向狀態，並將我們傳送至登入頁面。 請注意，我們嘗試存取的頁面（`CreatingUserAccounts.aspx`）會透過 `ReturnUrl` querystring 參數傳遞至登入頁面。

[![因為 URL 授權規則禁止匿名存取，所以我們會被重新導向至登入頁面](user-based-authorization-vb/_static/image14.png)](user-based-authorization-vb/_static/image13.png)

**圖 5**：由於 URL 授權規則禁止匿名存取，我們會被重新導向至登入頁面（[按一下以查看完整大小的影像](user-based-authorization-vb/_static/image15.png)）

成功登入之後，系統會將我們重新導向至 [`CreatingUserAccounts.aspx`] 頁面。 這次 `UrlAuthorizationModule` 允許存取頁面，因為我們不再是匿名的。

### <a name="applying-url-authorization-rules-to-a-specific-location"></a>將 URL 授權規則套用至特定位置

在 `Web.config` 的 [`<system.web>`] 區段中定義的授權設定會套用至該目錄及其子目錄中的所有 ASP.NET 資源（直到另一個 `Web.config` 檔案覆寫為止）。 不過，在某些情況下，我們可能會想要讓指定目錄中的所有 ASP.NET 資源擁有特定的授權設定，但一或兩個特定頁面除外。 這可以藉由在 `Web.config`中新增 `<location>` 元素來達成，將其指向授權規則不同的檔案，並在其中定義其唯一的授權規則。

為了說明如何使用 `<location>` 專案來覆寫特定資源的設定，讓我們自訂授權設定，以便只有 Tito 可以流覽 `CreatingUserAccounts.aspx`。 若要完成這項操作，請將 `<location>` 元素新增至 `Membership` 資料夾的 `Web.config` 檔案，並更新其標記，使其看起來如下所示：

[!code-xml[Main](user-based-authorization-vb/samples/sample5.xml)]

`<system.web>` 中的 `<authorization>` 元素會定義在 `Membership` 資料夾及其子資料夾中 ASP.NET 資源的預設 URL 授權規則。 `<location>` 元素可讓我們覆寫特定資源的這些規則。 在上述標記中，`<location>` 元素會參考 `CreatingUserAccounts.aspx` 頁面，並指定其授權規則（例如允許 Tito），但拒絕所有其他人。

若要測試此授權變更，請先以匿名使用者的身分造訪網站。 如果您嘗試造訪 [`Membership`] 資料夾中的任何頁面，例如 `UserBasedAuthorization.aspx`，`UrlAuthorizationModule` 將會拒絕要求，而系統會將您重新導向至登入頁面。 以 Scott 的身分登入之後，您可以流覽 `Membership` 資料夾中的任何頁面，*但 `CreatingUserAccounts.aspx`除外*。 嘗試造訪 `CreatingUserAccounts.aspx` 以任何人身分登入，但 Tito 會導致未經授權的存取嘗試，將您重新導向回到登入頁面。

> [!NOTE]
> `<location>` 元素必須出現在設定的 `<system.web>` 元素之外。 您需要針對您要覆寫其授權設定的每個資源，使用個別的 `<location>` 元素。

### <a name="a-look-at-how-theurlauthorizationmoduleuses-the-authorization-rules-to-grant-or-deny-access"></a>瞭解`UrlAuthorizationModule`如何使用授權規則來授與或拒絕存取

`UrlAuthorizationModule` 會藉由一次分析一個 URL 授權規則（從第一個 URL 開始並向下工作），來決定是否要授權特定 URL 的特定識別。 一旦找到相符專案，就會根據是否在 `<allow>` 或 `<deny>` 元素中找到相符專案，授與或拒絕使用者存取。 <strong>如果找不到相符的，則會授與使用者存取權。</strong> 因此，如果您想要限制存取權，請務必使用 `<deny>` 元素做為 URL 授權設定中的最後一個元素。 <strong>如果您省略</strong><strong>`<deny>`</strong><strong>元素，則所有使用者都會被授與存取權。</strong>

若要進一步瞭解 `UrlAuthorizationModule` 用來判斷授權單位的程式，請考慮我們稍早在此步驟中探討的範例 URL 授權規則。 第一個規則是允許存取 Tito 和 Scott 的 `<allow>` 元素。 第二個規則是拒絕所有人存取的 `<deny>` 元素。 如果匿名使用者造訪，`UrlAuthorizationModule` 一開始會詢問，匿名是 Scott 或 Tito？ 答案顯然是「否」，因此它會繼續進行第二個規則。 匿名是否在每個人的集合中？ 因為這裡的答案是肯定的，所以 `<deny>` 規則會生效，而訪客會重新導向至登入頁面。 同樣地，如果 Jisun 正在造訪，`UrlAuthorizationModule` 一開始會詢問，Jisun 是 Scott 或 Tito？ 因為她不是，`UrlAuthorizationModule` 會繼續進行第二個問題，Jisun 在每個人的集合中嗎？ 她也會拒絕存取。 最後，如果 Tito 造訪，`UrlAuthorizationModule` 所提出的第一個問題就是肯定的答案，因此 Tito 會被授與存取權。

由於 `UrlAuthorizationModule` 會處理由上而下的授權規則，在任何相符的處停止，因此在較不明確的規則之前，一定要有更明確的規則。 也就是說，若要定義禁止 Jisun 和匿名使用者的授權規則，但允許其他所有已驗證的使用者，您可以從最特定的規則開始，這會影響 Jisun，然後繼續進行較不特定的規則-允許其他已驗證的使用者，但拒絕所有匿名使用者。 下列 URL 授權規則會先拒絕 Jisun，然後拒絕任何匿名使用者，藉此執行此原則。 除了 Jisun 以外的任何已驗證使用者都將被授與存取權，因為這兩個 `<deny>` 語句都不會相符。

[!code-xml[Main](user-based-authorization-vb/samples/sample6.xml)]

## <a name="step-2-fixing-the-workflow-for-unauthorized-authenticated-users"></a>步驟2：為未經授權的已驗證使用者修正工作流程

如我們稍早在本教學課程的「查看 URL 授權工作流程」一節中所述，每當未經授權的要求過大幅簡化時，`UrlAuthorizationModule` 都會中止要求，並傳回 HTTP 401 未經授權的狀態。 此401狀態已由 `FormsAuthenticationModule` 修改為302重新導向狀態，會將使用者傳送至登入頁面。 即使使用者已通過驗證，此工作流程還是會發生在任何未經授權的要求上。

將已驗證的使用者傳回至登入頁面可能會使其混淆，因為他們已經登入系統。 有了一點工作，我們就可以藉由將未經授權的使用者重新導向至頁面，來改善這個工作流程，以說明他們嘗試存取受限制的頁面。

首先，在 web 應用程式的根資料夾中建立名為 `UnauthorizedAccess.aspx`的新 ASP.NET 網頁;別忘了將此頁面與 `Site.master` 主版頁面建立關聯。 建立此頁面之後，請移除參照 `LoginContent` ContentPlaceHolder 的內容控制項，如此就會顯示主版頁面的預設內容。 接下來，新增說明這種情況的訊息，亦即使用者嘗試存取受保護的資源。 加入這類訊息之後，`UnauthorizedAccess.aspx` 頁面的宣告式標記看起來應該如下所示：

[!code-aspx[Main](user-based-authorization-vb/samples/sample7.aspx)]

我們現在需要變更工作流程，以便在經過驗證的使用者執行未經授權的要求時，會將其傳送至 [`UnauthorizedAccess.aspx`] 頁面，而不是登入頁面。 將未經授權的要求重新導向至登入頁面的邏輯會隱藏在 `FormsAuthenticationModule` 類別的私用方法中，因此我們無法自訂此行為。 不過，我們可以將自己的邏輯新增至登入頁面，視需要將使用者重新導向至 `UnauthorizedAccess.aspx`。

當 `FormsAuthenticationModule` 將未經授權的訪客重新導向至登入頁面時，它會將要求的、未經授權的 URL 附加至名稱為 `ReturnUrl`的 querystring。 例如，如果未經授權的使用者嘗試造訪 `OnlyTito.aspx`，`FormsAuthenticationModule` 會將他們重新導向至 `Login.aspx?ReturnUrl=OnlyTito.aspx`。 因此，如果通過驗證的使用者以包含 `ReturnUrl` 參數的 querystring 來到達登入頁面，我們就知道這個未驗證的使用者剛嘗試造訪的頁面未獲授權觀看。 在這種情況下，我們想要將她重新導向至 `UnauthorizedAccess.aspx`。

若要完成這項操作，請將下列程式碼新增至登入頁面的 `Page_Load` 事件處理常式：

[!code-vb[Main](user-based-authorization-vb/samples/sample8.vb)]

上述程式碼會將已驗證、未經授權的使用者重新導向至 [`UnauthorizedAccess.aspx`] 頁面。 若要查看此邏輯的實際運作情形，請以匿名訪客的身分造訪網站，然後按一下左欄中的 [建立使用者帳戶] 連結。 這會帶您前往 [`~/Membership/CreatingUserAccounts.aspx`] 頁面，在步驟1中，我們已設定為只允許存取 Tito。 由於不允許匿名使用者，`FormsAuthenticationModule` 會將我們重新導向回到登入頁面。

此時我們是匿名的，因此 `Request.IsAuthenticated` 會傳回 `False` 而不會重新導向至 `UnauthorizedAccess.aspx`。 相反地，會顯示登入頁面。 以 Tito 以外的使用者身分登入，例如 Bruce。 輸入適當的認證之後，登入頁面會將我們重新導向回到 `~/Membership/CreatingUserAccounts.aspx`。 不過，由於只有 Tito 可存取此頁面，因此我們未經授權可加以查看，並會立即返回登入頁面。 不過，這次 `Request.IsAuthenticated` 會傳回 `True` （而 `ReturnUrl` querystring 參數存在），所以我們會被重新導向至 `UnauthorizedAccess.aspx` 頁面。

[![驗證，未經授權的使用者會重新導向至 UnauthorizedAccess .aspx](user-based-authorization-vb/_static/image17.png)](user-based-authorization-vb/_static/image16.png)

**圖 6**：已驗證的未經授權使用者會重新導向至 `UnauthorizedAccess.aspx` （[按一下以觀看完整大小的影像](user-based-authorization-vb/_static/image18.png)）

這個自訂的工作流程藉由簡短地計算 [圖 2] 中所描述的迴圈，以提供更合理且直接的使用者體驗。

## <a name="step-3-limiting-functionality-based-on-the-currently-logged-in-user"></a>步驟3：根據目前登入的使用者限制功能

[URL 授權] 可讓您輕鬆地指定粗略的授權規則。 如我們在步驟1中所見，使用 URL 授權，我們可以簡潔地陳述允許哪些身分識別，以及哪些身分識別會被拒絕，以查看資料夾中的特定頁面或所有頁面。 不過，在某些情況下，我們可能會想要允許所有使用者流覽頁面，但根據造訪網頁的使用者限制頁面的功能。

請考慮使用電子商務網站的案例，讓已驗證的訪客可以審查他們的產品。 當匿名使用者造訪產品的頁面時，他們只會看到產品資訊，而且不會有機會離開評論。 不過，造訪相同頁面的已驗證使用者會看到審核介面。 如果已驗證的使用者尚未審核此產品，則介面可以讓他們提交評論;否則，它會顯示他們先前提交的評論。 若要進一步執行此案例，[產品] 頁面可能會顯示其他資訊，並提供適用于電子商務公司的使用者擴充功能。 例如，[產品] 頁面可能會列出庫存存貨，並包含可在員工造訪時編輯產品價格和描述的選項。

這類精細的授權規則可以透過宣告方式或程式設計方式（或兩者的組合）來執行。 在下一節中，我們將瞭解如何透過 LoginView 控制項來執行精細的授權。 之後，我們將探索程式設計技巧。 不過，在查看如何套用精細的授權規則之前，我們必須先建立一個頁面，其功能取決於造訪它的使用者。

讓我們建立一個頁面，其中列出 GridView 內特定目錄中的檔案。 除了列出每個檔案的名稱、大小和其他資訊，GridView 會包含兩個 LinkButtons 的資料行：一個標題為 View，另一個標題為 Delete。 如果按一下 [View LinkButton]，則會顯示所選取檔案的內容;如果按一下 [刪除] LinkButton，則會刪除檔案。 我們一開始會建立此頁面，讓所有使用者都可以使用其視圖和刪除功能。 在使用 LoginView 控制項和以程式設計方式限制功能章節中，我們將瞭解如何根據造訪頁面的使用者來啟用或停用這些功能。

> [!NOTE]
> 我們即將建立的 ASP.NET 網頁會使用 GridView 控制項來顯示檔案清單。 由於本教學課程系列的重點在於表單驗證、授權、使用者帳戶和角色，因此我不想花太多時間來討論 GridView 控制項的內部運作。 雖然本教學課程提供設定此頁面的特定逐步指示，但並不會深入探討某些選擇的原因，或特定屬性對轉譯輸出的影響。 如需 GridView 控制項的完整檢查，請參閱我 *[在 ASP.NET 2.0 教學課程系列中使用資料](../../data-access/index.md)* 。

一開始先開啟 [`Membership`] 資料夾中的 `UserBasedAuthorization.aspx` 檔案，然後將 GridView 控制項新增至名為 `FilesGrid`的頁面。 從 GridView 的智慧標籤中，按一下 [編輯資料行] 連結以啟動 [欄位] 對話方塊。 從這裡，取消核取左下角的 [自動產生欄位] 核取方塊。 接下來，從左上角新增 [選取] 按鈕、[刪除] 按鈕和兩個 BoundFields （[選取] 和 [刪除] 按鈕可在 CommandField 類型底下找到）。 將 [選取] 按鈕的 [`SelectText`] 屬性設定為 [View]，並將第一個 BoundField 的 `HeaderText` 和 `DataField` 屬性命名為 Name。 將第二個 BoundField 的 `HeaderText` 屬性設定為 [大小（位元組）]、其 [`DataField`] 屬性設為 [長度]、其 `DataFormatString` 屬性設為 [{0:N0}]，其 [`HtmlEncode`] 屬性

設定 GridView 的資料行之後，請按一下 [確定] 以關閉 [欄位] 對話方塊。 從屬性視窗，將 GridView 的 `DataKeyNames` 屬性設定為 [`FullName`]。 此時，GridView 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](user-based-authorization-vb/samples/sample9.aspx)]

建立 GridView 的標記之後，我們就可以撰寫程式碼來抓取特定目錄中的檔案，並將它們系結至 GridView。 將下列程式碼新增至頁面的 `Page_Load` 事件處理常式：

[!code-vb[Main](user-based-authorization-vb/samples/sample10.vb)]

上述程式碼會使用[`DirectoryInfo` 類別](https://msdn.microsoft.com/library/system.io.directoryinfo.aspx)來取得應用程式根資料夾中的檔案清單。 [`GetFiles()` 方法](https://msdn.microsoft.com/library/system.io.directoryinfo.getfiles.aspx)會將目錄中的所有檔案當做[`FileInfo` 物件](https://msdn.microsoft.com/library/system.io.fileinfo.aspx)的陣列傳回，然後系結至 GridView。 `FileInfo` 物件具有各種屬性，例如 `Name`、`Length`和 `IsReadOnly`等等。 如同您在宣告式標記中所見，GridView 只會顯示 `Name` 和 `Length` 屬性。

> [!NOTE]
> `DirectoryInfo` 和 `FileInfo` 類別可在[`System.IO` 命名空間](https://msdn.microsoft.com/library/system.io.aspx)中找到。 因此，您需要在這些類別名稱前面加上其命名空間名稱，或將命名空間匯入類別檔案（透過 `Imports System.IO`）。

請花點時間透過瀏覽器造訪此頁面。 它會顯示位於應用程式根目錄中的檔案清單。 按一下任何一個 View 或 Delete LinkButtons 會導致回傳，但因為我們尚未建立必要的事件處理常式，所以不會發生任何動作。

[![GridView 會列出 Web 應用程式根目錄中的檔案](user-based-authorization-vb/_static/image20.png)](user-based-authorization-vb/_static/image19.png)

**圖 7**： GridView 會列出 Web 應用程式根目錄中的檔案（[按一下以查看完整大小的影像](user-based-authorization-vb/_static/image21.png)）

我們需要一種方法來顯示所選檔案的內容。 返回 Visual Studio，並在 GridView 上方加入名為 `FileContents` 的 TextBox。 將其 `TextMode` 屬性設為 `MultiLine`，並將其 `Columns` 和 `Rows` 屬性分別設定為95% 和10。

[!code-aspx[Main](user-based-authorization-vb/samples/sample11.aspx)]

接下來，建立 GridView [`SelectedIndexChanged` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindexchanged.aspx)的事件處理常式，並新增下列程式碼：

[!code-vb[Main](user-based-authorization-vb/samples/sample12.vb)]

這段程式碼會使用 GridView 的 `SelectedValue` 屬性來判斷所選檔案的完整檔案名。 就內部而言，會參考 `DataKeys` 集合以取得 `SelectedValue`，因此，您必須將 GridView 的 `DataKeyNames` 屬性設定為 [名稱]，如此步驟稍早所述。 [`File` 類別](https://msdn.microsoft.com/library/system.io.file.aspx)是用來將選取的檔案內容讀取到字串中，然後將其指派給 `FileContents` TextBox 的 `Text` 屬性，藉此顯示頁面上所選檔案的內容。

[![選取的檔案內容會顯示在文字方塊中](user-based-authorization-vb/_static/image23.png)](user-based-authorization-vb/_static/image22.png)

**圖 8**：選取的檔案內容會顯示在文字方塊中（[按一下以查看完整大小的影像](user-based-authorization-vb/_static/image24.png)）

> [!NOTE]
> 如果您要查看包含 HTML 標籤的檔案內容，然後嘗試查看或刪除檔案，將會收到 `HttpRequestValidationException` 錯誤。 之所以會發生這種情況，是因為在回傳時，文字方塊的內容會傳送回 web 伺服器。 根據預設，當偵測到潛在危險的回傳內容（例如 HTML 標籤）時，ASP.NET 會引發 `HttpRequestValidationException` 錯誤。 若要停用此錯誤，請將 `ValidateRequest="false"` 新增至 `@Page` 指示詞，關閉頁面的要求驗證。 如需有關要求驗證的優點，以及停用它時應採取哪些預防措施的詳細資訊，請參閱[要求驗證-防止腳本攻擊](https://asp.net/learn/whitepapers/request-validation/)。

最後，針對 GridView 的[`RowDeleting` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx)，使用下列程式碼來新增事件處理常式：

[!code-vb[Main](user-based-authorization-vb/samples/sample13.vb)]

程式碼只會顯示要在 [`FileContents`] 文字方塊中刪除之檔案的完整名稱，*而不需要*實際刪除檔案。

[![按一下 [刪除] 按鈕並不會實際刪除檔案](user-based-authorization-vb/_static/image26.png)](user-based-authorization-vb/_static/image25.png)

**圖 9**：按一下 [刪除] 按鈕並不會實際刪除檔案（[按一下以觀看完整大小的影像](user-based-authorization-vb/_static/image27.png)）

在步驟1中，我們設定了 URL 授權規則，禁止匿名使用者查看 `Membership` 資料夾中的頁面。 為了更清楚展現更精細的驗證，讓匿名使用者可以流覽 `UserBasedAuthorization.aspx` 頁面，但功能有限。 若要開啟此頁面，以供所有使用者存取，請將下列 `<location>` 元素新增至 `Membership` 資料夾中的 `Web.config` 檔案：

[!code-xml[Main](user-based-authorization-vb/samples/sample14.xml)]

新增此 `<location>` 專案之後，請登出網站以測試新的 URL 授權規則。 身為匿名使用者，您應允許造訪 `UserBasedAuthorization.aspx` 頁面。

目前，任何已驗證或匿名的使用者都可以造訪 `UserBasedAuthorization.aspx` 頁面，並查看或刪除檔案。 讓我們將它設為只有經過驗證的使用者可以查看檔案的內容，而且只有 Tito 可以刪除檔案。 這類精細的授權規則可以透過程式設計方式或兩種方法的組合來套用。 讓我們使用宣告式方法來限制可以查看檔案內容的人員;我們會使用程式設計方式來限制可以刪除檔案的人員。

### <a name="using-the-loginview-control"></a>使用 LoginView 控制項

如我們在過去的教學課程中所見，LoginView 控制項適用于針對已驗證和匿名的使用者顯示不同的介面，並提供簡單的方式來隱藏匿名使用者無法存取的功能。 因為匿名使用者無法查看或刪除檔案，所以只有經過驗證的使用者造訪網頁時，才需要顯示 [`FileContents`] 文字方塊。 若要達到此目的，請將 LoginView 控制項新增至頁面，並將其命名為 `LoginViewForFileContentsTextBox`，然後將 `FileContents` TextBox 的宣告式標記移至 LoginView 控制項的 `LoggedInTemplate`中。

[!code-aspx[Main](user-based-authorization-vb/samples/sample15.aspx)]

LoginView 範本中的 Web 控制項無法再從程式碼後置類別中直接存取。 例如，`FilesGrid` GridView 的 `SelectedIndexChanged` 和 `RowDeleting` 事件處理常式目前使用類似的程式碼來參考 `FileContents` TextBox 控制項：

[!code-aspx[Main](user-based-authorization-vb/samples/sample16.aspx)]

不過，此程式碼已不再有效。 將 [`FileContents`] 文字方塊移至 [`LoggedInTemplate`] 文字方塊就無法直接存取。 相反地，我們必須使用 `FindControl("controlId")` 方法，以程式設計方式參考控制項。 更新 `FilesGrid` 事件處理常式來參考 TextBox，如下所示：

[!code-vb[Main](user-based-authorization-vb/samples/sample17.vb)]

將 TextBox 移至 LoginView 的 `LoggedInTemplate` 並使用 `FindControl("controlId")` 模式更新頁面的程式碼以參考文字方塊之後，請以匿名使用者的身分造訪頁面。 如 [圖 10] 所示，[`FileContents`] 文字方塊不會顯示。 不過，仍會顯示 View LinkButton。

[![LoginView 控制項只會呈現已驗證使用者的 FileContents 文字方塊](user-based-authorization-vb/_static/image29.png)](user-based-authorization-vb/_static/image28.png)

**圖 10**： LoginView 控制項只呈現已驗證使用者的 `FileContents` 文字方塊（[按一下以觀看完整大小的影像](user-based-authorization-vb/_static/image30.png)）

為匿名使用者隱藏 [View] 按鈕的其中一種方式，就是將 GridView 欄位轉換成 TemplateField。 這會產生一個範本，其中包含 View LinkButton 的宣告式標記。 然後，我們可以將 LoginView 控制項新增至 TemplateField，並將 LinkButton 放在 LoginView 的 `LoggedInTemplate`中，藉此隱藏匿名訪客的 [View] \ （編輯 \）按鈕。 若要完成此動作，請按一下 GridView 智慧標籤中的 [編輯資料行] 連結，以啟動 [欄位] 對話方塊。 接下來，從左下角的清單中選取 [選取] 按鈕，然後按一下 [將此欄位轉換成 TemplateField] 連結。 這麼做會從下列來源修改欄位的宣告式標記：

[!code-aspx[Main](user-based-authorization-vb/samples/sample18.aspx)]

 收件者： 

[!code-aspx[Main](user-based-authorization-vb/samples/sample19.aspx)]

 此時，我們可以將 LoginView 新增至 TemplateField。 下列標記只會顯示已驗證使用者的 View LinkButton。 

[!code-aspx[Main](user-based-authorization-vb/samples/sample20.aspx)]

如 [圖 11] 所示，最後的結果並不是因為即使資料行內的 View LinkButtons 隱藏，還是會顯示 View 資料行。 在下一節中，我們將探討如何隱藏整個 GridView 資料行（而不只是 LinkButton）。

[![LoginView 控制項隱藏匿名訪客的 View LinkButtons](user-based-authorization-vb/_static/image32.png)](user-based-authorization-vb/_static/image31.png)

**圖 11**： LoginView 控制項會隱藏匿名訪客的 View LinkButtons （[按一下以觀看完整大小的影像](user-based-authorization-vb/_static/image33.png)）

### <a name="programmatically-limiting-functionality"></a>以程式設計方式限制功能

在某些情況下，宣告式技術不足以限制頁面的功能。 例如，某些頁面功能的可用性可能會相依于使用者流覽網頁是否為匿名或已驗證的條件。 在這種情況下，可以透過程式設計方式來顯示或隱藏各種不同的使用者介面元素。

為了以程式設計方式限制功能，我們需要執行兩個工作：

1. 判斷造訪頁面的使用者是否可以存取此功能，以及
2. 以程式設計方式根據使用者是否可以存取有問題的功能來修改使用者介面。

為了示範這兩項工作的應用程式，讓我們只允許 Tito 刪除 GridView 中的檔案。 接著，我們的第一項工作是要判斷它是否 Tito 造訪頁面。 一旦決定之後，我們需要隱藏（或顯示） GridView 的刪除資料行。 GridView 的資料行可以透過其 `Columns` 屬性來存取;只有當資料行的 `Visible` 屬性設定為 `True` （預設值）時，才會轉譯該資料行。

將下列程式碼加入至 `Page_Load` 事件處理常式，然後再將資料系結至 GridView：

[!code-vb[Main](user-based-authorization-vb/samples/sample21.vb)]

如我們在表單驗證教學課程[*的總覽*](../introduction/an-overview-of-forms-authentication-vb.md)中所討論，`User.Identity.Name` 會傳回身分識別的名稱。 這會對應至登入控制項中輸入的使用者名稱。 如果 Tito 造訪頁面，GridView 的第二個數據行的 `Visible` 屬性會設定為 `True`;否則，它會設定為 `False`。 最後結果是，當 Tito 以外的人造訪網頁時，另一個已驗證的使用者或匿名使用者，則不會轉譯 Delete 資料行（請參閱 [圖 12]）。不過，當 Tito 造訪頁面時，會出現 [刪除] 資料行（請參閱 [圖 13]）。

[![不是由 Tito （例如 Bruce）流覽時，就不會轉譯 [刪除] 資料行。](user-based-authorization-vb/_static/image35.png)](user-based-authorization-vb/_static/image34.png)

**圖 12**： Tito 以外的其他人（例如 Bruce）流覽時，不會轉譯 [刪除] 資料行（[按一下以查看完整大小的影像](user-based-authorization-vb/_static/image36.png)）

[![Tito 的 [刪除] 資料行呈現](user-based-authorization-vb/_static/image38.png)](user-based-authorization-vb/_static/image37.png)

**圖 13**： Tito 的刪除資料行（[按一下以觀看完整大小的影像](user-based-authorization-vb/_static/image39.png)）

## <a name="step-4-applying-authorization-rules-to-classes-and-methods"></a>步驟4：將授權規則套用至類別和方法

在步驟3中，我們不允許匿名使用者看到檔案的內容，並禁止所有使用者，但 Tito 刪除檔案。 這是藉由透過宣告式和程式設計技術，針對未經授權的訪客隱藏相關聯的使用者介面元素來完成。 在我們的簡單範例中，適當地隱藏使用者介面專案很簡單，但如果有許多不同的方法可以執行相同的功能，該怎麼做呢？ 在將該功能限制為未經授權的使用者時，如果我們忘記隱藏或停用所有適用的使用者介面元素，會發生什麼事？

有一個簡單的方法可確保未經授權的使用者無法存取特定功能，就是使用[`PrincipalPermission` 屬性](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)來裝飾該類別或方法。 當 .NET 執行時間使用類別或執行其其中一個方法時，它會檢查以確定目前的安全性內容具有使用類別的許可權，或執行方法。 `PrincipalPermission` 屬性提供一種機制，可讓我們定義這些規則。

讓我們來示範如何在 GridView 的 `SelectedIndexChanged` 上使用 `PrincipalPermission` 屬性，並 `RowDeleting` 事件處理常式，分別禁止匿名使用者和 Tito 以外的使用者執行。 我們只需要在每個函式定義的上方新增適當的屬性即可：

[!code-vb[Main](user-based-authorization-vb/samples/sample22.vb)]

`SelectedIndexChanged` 事件處理常式的屬性規定，只有經過驗證的使用者可以執行事件處理常式，因為 `RowDeleting` 事件處理常式上的屬性會將執行限制為 Tito。

> [!NOTE]
> 屬性可以套用至類別、方法、屬性或事件。 加入屬性時，它必須是類別、方法、屬性或事件宣告語句的一部分。 由於 Visual Basic 會使用分行符號做為語句分隔符號，因此屬性必須出現在與宣告相同的行上，或在其正上方加上行接續字元（底線）。 在上述的程式碼片段中，行接續字元是用來將屬性放在一行上，並將方法宣告放置在另一個行上。

如果是，Tito 以外的使用者嘗試執行 `RowDeleting` 事件處理常式或未驗證的使用者嘗試執行 `SelectedIndexChanged` 事件處理常式，則 .NET 執行時間會引發 `SecurityException`。

[![如果未授權安全性內容執行方法，則會擲回 SecurityException](user-based-authorization-vb/_static/image41.png)](user-based-authorization-vb/_static/image40.png)

**圖 14**：如果安全性內容未獲授權，無法執行方法，就會擲回 `SecurityException` （[按一下以查看完整大小的影像](user-based-authorization-vb/_static/image42.png)）

> [!NOTE]
> 若要允許多個安全性內容存取類別或方法，請使用每個安全性內容的 `PrincipalPermission` 屬性來裝飾類別或方法。 也就是說，若要允許 Tito 和 Bruce 執行 `RowDeleting` 事件處理常式，請新增*兩個*`PrincipalPermission` 屬性：

[!code-vb[Main](user-based-authorization-vb/samples/sample23.vb)]

除了 ASP.NET 網頁之外，許多應用程式也具有包含各種層級的架構，例如商務邏輯和資料存取層。 這些層通常會實作為類別庫，並提供類別和方法來執行商務邏輯和資料相關的功能。 `PrincipalPermission` 屬性適用于將授權規則套用至這些層級。

如需使用 `PrincipalPermission` 屬性來定義類別和方法授權規則的詳細資訊，請參閱[Scott Guthrie](https://weblogs.asp.net/scottgu/)的 Blog 專案[使用 `PrincipalPermissionAttributes`將授權規則新增至商務和資料層](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)。

## <a name="summary"></a>總結

在本教學課程中，我們探討了如何套用以使用者為基礎的授權規則。 一開始我們先看一下 ASP。NET 的 URL 授權架構。 在每個要求中，ASP.NET 引擎的 `UrlAuthorizationModule` 會檢查應用程式設定中定義的 URL 授權規則，以判斷身分識別是否獲得授權可存取要求的資源。 簡言之，URL 授權可讓您輕鬆地為特定的頁面或特定目錄中的所有頁面指定授權規則。

URL 授權架構會依頁面逐一套用授權規則。 使用 URL 授權時，要求的身分識別會獲得授權來存取特定資源。 不過，許多情況下，呼叫更精細的授權規則。 我們可能需要讓每個人都能存取頁面，而不是定義誰可以存取頁面，而是根據造訪頁面的使用者，顯示不同的資料或提供不同的功能。 頁面層級授權通常包含隱藏特定的使用者介面元素，以防止未經授權的使用者存取禁止的功能。 此外，也可以使用屬性來限制對特定使用者的類別和執行其方法。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [使用 `PrincipalPermissionAttributes` 將授權規則新增至商務和資料層](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [ASP.NET 授權](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [IIS6 與 IIS7 安全性之間的變更](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [設定特定檔案和子目錄](https://msdn.microsoft.com/library/6hbkh9s7.aspx)
- [根據使用者限制資料修改功能](../../data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb.md)
- [LoginView 控制項快速入門](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/loginview.aspx)
- [瞭解 IIS7 URL 授權](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)
- [`UrlAuthorizationModule` 技術檔](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)
- [使用 ASP.NET 2.0 中的資料](../../data-access/index.md)

### <a name="about-the-author"></a>關於作者

Scott Mitchell，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是 *[在24小時內讓自己的 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 Scott 可以在[mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)的那一行下拉式。

> [!div class="step-by-step"]
> [上一頁](validating-user-credentials-against-the-membership-user-store-vb.md)
> [下一頁](storing-additional-user-information-vb.md)
