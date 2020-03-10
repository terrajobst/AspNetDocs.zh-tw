---
uid: web-forms/overview/older-versions-security/membership/creating-user-accounts-cs
title: 建立使用者帳戶（C#） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將探討如何使用成員資格架構（透過 SqlMembershipProvider）來建立新的使用者帳戶。 我們將瞭解如何建立新的我們 。
ms.author: riande
ms.date: 01/18/2008
ms.assetid: f175278c-6079-4d91-b9b4-2493ed43d9ec
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-user-accounts-cs
msc.type: authoredcontent
ms.openlocfilehash: 955592320e7d36c7ae3b9c03a361bee2183f1776
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78631975"
---
# <a name="creating-user-accounts-c"></a>建立使用者帳戶 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_05_CS.zip)或[下載 PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial05_CreatingUsers_cs.pdf)

> 在本教學課程中，我們將探討如何使用成員資格架構（透過 SqlMembershipProvider）來建立新的使用者帳戶。 我們將瞭解如何透過程式設計方式和 ASP 建立新的使用者。NET 的內建 CreateUserWizard 控制項。

## <a name="introduction"></a>簡介

在<a id="_msoanchor_1"> </a>[先前的教學](creating-the-membership-schema-in-sql-server-cs.md)課程中，我們已在資料庫中安裝應用程式服務架構，這會新增 `SqlMembershipProvider` 和 `SqlRoleProvider`所需的資料表、視圖和預存程式。 這會建立此系列中其餘教學課程所需的基礎結構。 在本教學課程中，我們將探討如何使用成員資格架構（透過 `SqlMembershipProvider`）來建立新的使用者帳戶。 我們將瞭解如何透過程式設計方式和 ASP 建立新的使用者。NET 的內建 CreateUserWizard 控制項。

除了學習如何建立新的使用者帳戶之外，我們還需要更新我們最初在 *<a id="_msoanchor_2"></a>[表單驗證](../introduction/an-overview-of-forms-authentication-cs.md)* 教學課程中建立的示範網站，然後在 *<a id="https://www.asp.net/learn/security/tutorial-03-cs.aspx"></a>表單驗證設定和高級主題*教學課程中加強。 我們的示範 web 應用程式有一個登入頁面，它會驗證使用者的認證，以防止硬式編碼的使用者名稱/密碼配對。 此外，`Global.asax` 還包含可為已驗證的使用者建立自訂 `IPrincipal` 和 `IIdentity` 物件的程式碼。 我們將會更新登入頁面，以根據成員資格架構來驗證使用者的認證，並移除自訂主體和身分識別邏輯。

現在就開始吧！

## <a name="the-forms-authentication-and-membership-checklist"></a>表單驗證和成員資格檢查清單

在我們開始使用成員資格架構之前，讓我們花點時間複習一下我們所採取的重要步驟。 在以表單為基礎的驗證案例中，搭配 `SqlMembershipProvider` 使用成員資格架構時，必須先執行下列步驟，才能在 web 應用程式中實作為成員資格功能：

1. **啟用以表單為基礎的驗證。** 如我們在 *<a id="_msoanchor_4"></a>[表單驗證的總覽](../introduction/an-overview-of-forms-authentication-cs.md)* 中所討論，表單驗證是藉由編輯 `Web.config`，並將 `<authentication>` 元素的 `mode` 屬性設定為 `Forms`來啟用。 在啟用表單驗證的情況下，會檢查每個傳入要求的*表單驗證票證*（如果有的話），以識別要求者。
2. **將應用程式服務架構新增至適當的資料庫。** 使用 `SqlMembershipProvider` 我們需要將應用程式服務架構安裝到資料庫。 通常，此架構會加入至保存應用程式資料模型的相同資料庫中。 在 *<a id="_msoanchor_5"> </a>[SQL Server 中建立成員資格架構](creating-the-membership-schema-in-sql-server-cs.md)* 教學課程會探討如何使用 `aspnet_regsql.exe` 工具來完成這項操作。
3. **自訂 Web 應用程式的設定，以參考步驟2中的資料庫。** 在*SQL Server 中建立成員資格架構*教學課程示範了兩種設定 web 應用程式的方式，讓 `SqlMembershipProvider` 會使用在步驟2：中選取的資料庫來修改 `LocalSqlServer` 連接字串名稱;或者，將新註冊的提供者加入至成員資格架構提供者清單，並自訂新提供者以使用步驟2中的資料庫。

建立使用 `SqlMembershipProvider` 和表單架構驗證的 web 應用程式時，您必須先執行這三個步驟，才能使用 `Membership` 類別或 ASP.NET 登入 Web 控制項。 因為我們已在先前的教學課程中執行這些步驟，所以我們已準備好開始使用成員資格架構！

## <a name="step-1-adding-new-aspnet-pages"></a>步驟 1:加入新的 ASP.NET 網頁

在本教學課程和接下來的三個中，我們將檢查各種成員資格相關的功能和功能。 我們將需要一系列的 ASP.NET 網頁，以執行整個教學課程中所探討的主題。 讓我們建立這些頁面，然後 `(Web.sitemap)`網站地圖檔案。

首先，在名為 `Membership`的專案中建立新的資料夾。 接下來，將五個新的 ASP.NET 網頁新增至 [`Membership`] 資料夾，並使用 `Site.master` 主版頁面連結每個頁面。 將頁面命名為：

- `CreatingUserAccounts.aspx`
- `UserBasedAuthorization.aspx`
- `EnhancedCreateUserWizard.aspx`
- `AdditionalUserInfo.aspx`
- `Guestbook.aspx`

此時，專案的方案總管看起來應該像 [圖 1] 所示的螢幕擷取畫面。

[[成員資格] 資料夾中已加入 ![五個新頁面](creating-user-accounts-cs/_static/image2.png)](creating-user-accounts-cs/_static/image1.png)

**圖 1**：[`Membership`] 資料夾中已加入五個新頁面（[按一下以查看完整大小的影像](creating-user-accounts-cs/_static/image3.png)）

此時，每個頁面都應該有兩個內容控制項，每一個主版頁面的 ContentPlaceHolders： `MainContent` 和 `LoginContent`。

[!code-aspx[Main](creating-user-accounts-cs/samples/sample1.aspx)]

回想一下，`LoginContent` ContentPlaceHolder 的預設標記會根據使用者是否經過驗證，顯示登入或登出網站的連結。 不過，`Content2` 內容控制項的存在，會覆寫主版頁面的預設標記。 如同我們在 *<a id="_msoanchor_6"></a>[表單驗證](../introduction/an-overview-of-forms-authentication-cs.md)* 教學課程中所討論的，這在頁面中很有用，因為我們不想要在左欄中顯示登入相關的選項。

不過，針對這五個頁面，我們想要顯示主版頁面的 `LoginContent` ContentPlaceHolder 的預設標記。 因此，請移除 `Content2` 內容控制項的宣告式標記。 這麼做之後，這五頁的每一個標記都應該只包含一個內容控制項。

## <a name="step-2-creating-the-site-map"></a>步驟 2:建立網站地圖

除了最簡單的網站以外，您還必須執行某種形式的導覽使用者介面。 導覽使用者介面可能是網站的各種區段連結的簡單列表。 或者，這些連結可能會排列成功能表或樹狀檢視。 身為頁面開發人員，建立導覽使用者介面只是故事的一半。 我們也需要一些方法，以可維護且可更新的方式來定義網站的邏輯結構。 新增新的頁面或移除現有的頁面時，我們想要能夠更新單一來源（網站地圖），並讓這些修改反映在網站的流覽使用者介面上。

這兩項工作（定義網站地圖和根據網站地圖來執行導覽使用者介面）很容易完成，因為網站地圖架構和 ASP.NET 2.0 版中新增的導覽 Web 控制項。 網站地圖架構可讓開發人員定義網站地圖，然後透過程式設計 API （ [`SiteMap` 類別](https://msdn.microsoft.com/library/system.web.sitemap.aspx)）來存取網站對應。 內建的導覽 Web 控制項包括[Menu 控制項](https://msdn.microsoft.com/library/bz09dy46.aspx)、 [TreeView 控制項](https://msdn.microsoft.com/library/3eafky27.aspx)和[SiteMapPath 控制項](https://msdn.microsoft.com/library/3eafky27.aspx)。

如同成員資格和角色架構，網站地圖架構是以[提供者模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)為基礎。 網站地圖提供者類別的工作是從持續性資料存放區（例如 XML 檔案或資料庫資料表）產生 `SiteMap` 類別所使用的記憶體內部結構。 .NET Framework 隨附預設的網站地圖提供者，可從 XML 檔案（[`XmlSiteMapProvider`](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)）讀取網站地圖資料，而這是我們將在本教學課程中使用的提供者。 如需替代網站地圖提供者的執行方式，請參閱本教學課程結尾處的進一步閱讀一節。

預設的網站地圖提供者預期名為 `Web.sitemap` 的正確格式 XML 檔案，會存在於根目錄中。 因為我們使用這個預設提供者，所以我們需要新增這類檔案，並以適當的 XML 格式定義網站對應的結構。 若要加入檔案，請在方案總管中的專案名稱上按一下滑鼠右鍵，然後選擇 [加入新專案]。 從對話方塊中，選擇新增名為 `Web.sitemap`的網站地圖類型檔案。

[![將名為 Web.config 的檔案新增至專案的根目錄](creating-user-accounts-cs/_static/image5.png)](creating-user-accounts-cs/_static/image4.png)

**圖 2**：將名為 `Web.sitemap` 的檔案新增至專案的根目錄（[按一下以查看完整大小的影像](creating-user-accounts-cs/_static/image6.png)）

XML 網站地圖檔案會將網站的結構定義為階層。 這個階層式關聯性會透過 `<siteMapNode>` 專案的上階，在 XML 檔案中進行模型化。 `Web.sitemap` 必須以正好有一個 `<siteMapNode>` 子系的 `<siteMap>` 父節點為開頭。 這個最上層的 `<siteMapNode>` 專案表示階層的根，而且可能有任意數目的子代節點。 每個 `<siteMapNode>` 元素都必須包含 `title` 屬性，而且可以選擇性地包含 `url` 和 `description` 屬性，以及其他專案;每個非空白的 `url` 屬性都必須是唯一的。

在 `Web.sitemap` 檔案中輸入下列 XML：

[!code-xml[Main](creating-user-accounts-cs/samples/sample2.xml)]

上述網站地圖示記會定義如 [圖 3] 所示的階層。

[![網站地圖代表階層式導覽結構](creating-user-accounts-cs/_static/image8.png)](creating-user-accounts-cs/_static/image7.png)

**圖 3**：網站地圖代表階層式導覽結構（[按一下以觀看完整大小的影像](creating-user-accounts-cs/_static/image9.png)）

## <a name="step-3-updating-the-master-page-to-include-a-navigational-user-interface"></a>步驟 3：更新主版頁面以包含導覽使用者介面

ASP.NET 包含許多設計使用者介面的導覽相關 Web 控制項。 其中包括 Menu、TreeView 和 SiteMapPath 控制項。 [Menu] 和 [TreeView] 控制項會分別在功能表或樹狀目錄中轉譯網站地圖結構，而 SiteMapPath 則會顯示階層連結，顯示目前正在造訪的節點及其上階。 網站地圖資料可以使用 SiteMapDataSource 系結至其他資料 Web 控制項，並可透過 `SiteMap` 類別以程式設計方式存取。

由於網站地圖架構和導覽控制項的完整討論已超出本教學課程系列的範圍，而不是花時間製作自己的導覽使用者介面，而是借用在 *[ASP.NET 2.0](../../data-access/index.md)* 教學課程系列中使用的資料，改為使用「中繼器」控制項來顯示兩個深度的導覽連結清單，如 [圖 4] 所示。

### <a name="adding-a-two-level-list-of-links-in-the-left-column"></a>在左側資料行中加入兩層連結的清單

若要建立此介面，請將下列宣告式標記新增至 `Site.master` 主版頁面的左側資料行，其中的文字為「TODO：功能表將會移至這裡 ...」目前位於。

[!code-aspx[Main](creating-user-accounts-cs/samples/sample3.aspx)]

上述標記會將名為 `menu` 的中繼器控制項系結至 SiteMapDataSource，以傳回 `Web.sitemap`中定義的網站地圖階層。 由於 SiteMapDataSource 控制項的[`ShowStartingNode` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx)設定為 False，因此會從 "Home" 節點的子代開始傳回網站對應的階層。 中繼器會在 `<li>` 元素中顯示每個節點（目前只是「成員資格」）。 另一個，內部中繼器接著會在嵌套的未排序清單中顯示目前節點的子系。

[圖 4] 顯示上述標記的轉譯輸出，以及我們在步驟2中建立的網站地圖結構。 中繼器會呈現 vanilla 未排序的清單標記;`Styles.css` 中定義的級聯樣式表規則會負責內賞心悅目的版面配置。 如需上述標記運作方式的詳細描述，請參閱[主版頁面和網站導覽](https://asp.net/learn/data-access/tutorial-03-cs.aspx)教學課程。

[![使用嵌套的未排序清單呈現導覽使用者介面](creating-user-accounts-cs/_static/image11.png)](creating-user-accounts-cs/_static/image10.png)

**圖 4**：導覽使用者介面是使用嵌套的未排序清單（[按一下以查看完整大小的影像](creating-user-accounts-cs/_static/image12.png)）來呈現

### <a name="adding-breadcrumb-navigation"></a>新增軌跡導覽

除了左欄中的連結清單，讓我們也讓每個頁面都顯示一個階層[連結。](http://en.wikipedia.org/wiki/Breadcrumb_%28navigation%29) 階層連結是導覽使用者介面元素，可快速顯示使用者在網站階層中的目前位置。 SiteMapPath 控制項會使用網站地圖架構來判斷目前頁面在網站地圖中的位置，然後根據這項資訊來顯示階層連結。

具體而言，請將 `<span>` 專案新增至主版頁面的標頭 `<div>` 專案，並將新的 `<span>` 元素的 `class` 屬性設定為「階層連結」。 （`Styles.css` 類別包含「階層連結」類別的規則）。接下來，將 SiteMapPath 新增至這個新的 `<span>` 元素。

[!code-aspx[Main](creating-user-accounts-cs/samples/sample4.aspx)]

[圖 5] 顯示造訪 `~/Membership/CreatingUserAccounts.aspx`時的 SiteMapPath 輸出。

[![階層連結會顯示目前頁面及其上階的網站地圖](creating-user-accounts-cs/_static/image14.png)](creating-user-accounts-cs/_static/image13.png)

**圖 5**：階層連結會顯示目前頁面及其在網站地圖中的上階（[按一下以查看完整大小的影像](creating-user-accounts-cs/_static/image15.png)）

## <a name="step-4-removing-the-custom-principal-and-identity-logic"></a>步驟 4：移除自訂主體和身分識別邏輯

在 *<a id="_msoanchor_7"></a>[表單驗證設定和「高級主題」](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md)* 教學課程中，我們已瞭解如何將自訂主體和身分識別物件與已驗證的使用者產生關聯。 我們完成這項作業的方法是在應用程式的 `PostAuthenticateRequest` 事件 `Global.asax` 中建立事件處理常式，這會在 `FormsAuthenticationModule` 驗證使用者之後引發。 在這個事件處理常式中，我們以在該教學課程中建立的 `CustomPrincipal` 和 `CustomIdentity` 物件來取代 `FormsAuthenticationModule` 新增的 `GenericPrincipal` 和 `FormsIdentity` 物件。

雖然自訂主體和身分識別物件在特定案例中很有用，但在大多數情況下，`GenericPrincipal` 和 `FormsIdentity` 物件就已足夠。 因此，我想要回到預設行為。 藉由移除或取消批註 `PostAuthenticateRequest` 事件處理常式，或完全刪除 `Global.asax` 檔案來進行這項變更。

## <a name="step-5-programmatically-creating-a-new-user"></a>步驟 5：以程式設計方式建立新的使用者

若要透過成員資格架構來建立新的使用者帳戶，請使用 `Membership` 類別的[`CreateUser` 方法](https://msdn.microsoft.com/library/system.web.security.membership.createuser.aspx)。 這個方法具有使用者名稱、密碼和其他使用者相關欄位的輸入參數。 在叫用時，它會將新使用者帳戶的建立委派給設定的成員資格提供者，然後傳回代表剛建立之使用者帳戶的[`MembershipUser` 物件](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)。

`CreateUser` 方法有四個多載，每個都接受不同數目的輸入參數：

- [`CreateUser(username, password)`](https://msdn.microsoft.com/library/d8t4h2es.aspx)
- [`CreateUser(username, password, email)`](https://msdn.microsoft.com/library/t8yy6w3h.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, MembershipCreateStatus)`](https://msdn.microsoft.com/library/82xx2e62.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, providerUserKey, MembershipCreateStatus)`](https://msdn.microsoft.com/library/ms152012.aspx)

這四個多載會因收集的資訊量而有所不同。 例如，第一個多載只需要新使用者帳戶的使用者名稱和密碼，而第二個則需要使用者的電子郵件地址。

這些多載存在的原因是，建立新的使用者帳戶所需的資訊，取決於成員資格提供者的設定。 在 *<a id="_msoanchor_8"></a>[SQL Server 中建立成員資格架構](creating-the-membership-schema-in-sql-server-cs.md)* 教學課程中，我們已檢查在 中指定成員資格提供者的設定`Web.config`。 [表 2] 包含完整的設定清單。

其中一個成員資格提供者設定會影響可能會使用的 `CreateUser` 多載是 `requiresQuestionAndAnswer` 設定。 如果 `requiresQuestionAndAnswer` 設定為 `true` （預設值），則在建立新的使用者帳戶時，我們必須指定安全性問題和答案。 如果使用者需要重設或變更其密碼，稍後會使用此資訊。 具體來說，它們會顯示安全性問題，而且必須輸入正確的答案，才能重設或變更其密碼。 因此，如果 `requiresQuestionAndAnswer` 設定為 `true` 則呼叫前兩個 `CreateUser` 多載會導致例外狀況，因為安全性問題和答案已遺失。 因為我們的應用程式目前設定為需要安全性問題和答案，所以在以程式設計方式建立使用者時，我們必須使用後面兩個多載的其中一個。

為了說明如何使用 `CreateUser` 方法，讓我們來建立使用者介面，以提示使用者輸入其名稱、密碼、電子郵件和預先定義安全性問題的答案。 開啟 [`Membership`] 資料夾中的 [`CreatingUserAccounts.aspx`] 頁面，並將下列 Web 控制項新增至內容控制項：

- 名為 `Username` 的 TextBox
- 名為 `Password`的 TextBox，其 `TextMode` 屬性設定為 `Password`
- 名為 `Email` 的 TextBox
- 名為 `SecurityQuestion` 的標籤，其 `Text` 屬性已清除
- 名為 `SecurityAnswer` 的 TextBox
- 名為 `CreateAccountButton` 的按鈕，其 Text 屬性會設定為「建立使用者帳戶」
- 名為 `CreateAccountResults` 的標籤控制項，其 `Text` 屬性已清除

此時您的畫面看起來應該像 [圖 6] 所示的螢幕擷取畫面。

[![將各種 Web 控制項新增至 CreatingUserAccounts 頁面](creating-user-accounts-cs/_static/image17.png)](creating-user-accounts-cs/_static/image16.png)

**圖 6**：將各種 Web 控制項新增至 [`CreatingUserAccounts.aspx`] 頁面（[按一下以查看完整大小的影像](creating-user-accounts-cs/_static/image18.png)）

[`SecurityQuestion` 標籤] 和 [`SecurityAnswer`] 文字方塊的目的是要顯示預先定義的安全性問題，並收集使用者的答案。 請注意，安全性問題和答案都是以使用者為基礎來儲存，因此可能會允許每個使用者定義自己的安全性問題。 不過，在此範例中，我決定使用通用安全性問題，亦即：「您最愛的色彩為何？」

若要執行這個預先定義的安全性問題，請將常數新增至頁面的程式碼後置類別中，名為 `passwordQuestion`，並為其指派安全性問題。 然後，在 `Page_Load` 事件處理常式中，將此常數指派給 `SecurityQuestion` 標籤的 `Text` 屬性：

[!code-csharp[Main](creating-user-accounts-cs/samples/sample5.cs)]

接下來，建立 `CreateAccountButton`的 `Click` 事件的事件處理常式，並新增下列程式碼：

[!code-csharp[Main](creating-user-accounts-cs/samples/sample6.cs)]

`Click` 事件處理常式一開始會定義一個名為 `createStatus` 類型為[`MembershipCreateStatus`](https://msdn.microsoft.com/library/system.web.security.membershipcreatestatus.aspx)的變數。 `MembershipCreateStatus` 是列舉，表示 `CreateUser` 作業的狀態。 例如，如果成功建立使用者帳戶，則產生的 `MembershipCreateStatus` 實例將會設定為 `Success`的值;相反地，如果作業因為已經存在具有相同使用者名稱的使用者而失敗，則會設定為 `DuplicateUserName`的值。 在我們使用的 `CreateUser` 多載中，我們需要將 `MembershipCreateStatus` 實例以 `out` 參數的形式傳遞至方法。 這個參數會設定為 `CreateUser` 方法中的適當值，而我們可以在方法呼叫之後檢查其值，以判斷是否已成功建立使用者帳戶。

在呼叫 `CreateUser`，傳入 `createStatus`之後，`switch` 語句會根據指派給 `createStatus`的值，用來輸出適當的訊息。 [圖 7] 顯示成功建立新使用者時的輸出。 [圖 8] 和 [9] 顯示未建立使用者帳戶時的輸出。 在 [圖 8] 中，訪客輸入了五個字母的密碼，這不符合成員資格提供者的設定中所述的密碼強度需求。 在 [圖 9] 中，訪客嘗試使用現有的使用者名稱（如 [圖 7] 所建立）來建立使用者帳戶。

[已成功建立新的使用者帳戶 ![](creating-user-accounts-cs/_static/image20.png)](creating-user-accounts-cs/_static/image19.png)

**圖 7**：已成功建立新的使用者帳戶（[按一下以查看完整大小的影像](creating-user-accounts-cs/_static/image21.png)）

[![未建立使用者帳戶，因為提供的密碼太弱](creating-user-accounts-cs/_static/image23.png)](creating-user-accounts-cs/_static/image22.png)

**圖 8**：未建立使用者帳戶，因為提供的密碼太弱（[按一下以觀看完整大小的影像](creating-user-accounts-cs/_static/image24.png)）

[![使用者帳戶未建立，因為使用者名稱已在使用中](creating-user-accounts-cs/_static/image26.png)](creating-user-accounts-cs/_static/image25.png)

**圖 9**：使用者帳戶未建立，因為使用者名稱已在使用中（[按一下以觀看完整大小的影像](creating-user-accounts-cs/_static/image27.png)）

> [!NOTE]
> 您可能想知道，使用前兩個 `CreateUser` 方法多載其中之一時，如何判斷成功或失敗，兩者都不具有 `MembershipCreateStatus`類型的參數。 在發生失敗時，前兩個多載會擲回[`MembershipCreateUserException` 例外](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.aspx)狀況，其中包含 `MembershipCreateStatus`類型的[`StatusCode` 屬性](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.statuscode.aspx)。

建立幾個使用者帳戶之後，請在 `SecurityTutorials.mdf` 資料庫中列出 `aspnet_Users` 和 `aspnet_Membership` 資料表的內容，以確認帳戶是否已建立。 如 [圖 10] 所示，我透過 [`CreatingUserAccounts.aspx`] 頁面新增了兩個使用者：Tito 和 Bruce。

[![成員資格使用者存放區中有兩個使用者：Tito 和 Bruce](creating-user-accounts-cs/_static/image29.png)](creating-user-accounts-cs/_static/image28.png)

**圖 10**：成員資格使用者存放區中有兩個使用者：Tito 和 Bruce （[按一下以查看完整大小的影像](creating-user-accounts-cs/_static/image30.png)）

雖然成員資格使用者存放區現在包含 Bruce 和 Tito 的帳戶資訊，但我們尚未執行可讓 Bruce 或 Tito 登入網站的功能。 目前，`Login.aspx` 會針對一組硬式編碼的使用者名稱/密碼配對來驗證使用者的認證，*而不*會對成員資格架構驗證提供的認證。 現在，您會看到 `aspnet_Users` 中的新使用者帳戶，以及 `aspnet_Membership` 資料表的功能就足夠了。 在下一個教學課程中， *<a id="_msoanchor_9"></a>[根據成員資格使用者存放區驗證使用者認證](validating-user-credentials-against-the-membership-user-store-cs.md)* 時，我們會更新登入頁面，以對成員資格存放區進行驗證。

> [!NOTE]
> 如果您在 `SecurityTutorials.mdf` 資料庫中看不到任何使用者，可能是因為您的 web 應用程式使用預設的成員資格提供者，`AspNetSqlMembershipProvider`，其使用 `ASPNETDB.mdf` 資料庫做為其使用者存放區。 若要判斷這是否為問題，請按一下 方案總管中的 重新整理 按鈕。 如果已將名為 `ASPNETDB.mdf` 的資料庫新增至 `App_Data` 資料夾，這就是問題所在。 回到 *<a id="_msoanchor_10"></a>[SQL Server 教學課程中建立成員資格架構](creating-the-membership-schema-in-sql-server-cs.md)* 的步驟4，以取得如何正確設定成員資格提供者的指示。

在大部分的建立使用者帳戶案例中，訪客會提供一些介面，以輸入其使用者名稱、密碼、電子郵件和其他重要資訊，此時會建立新的帳戶。 在此步驟中，我們探討了如何手動建立這類介面，然後瞭解如何使用 `Membership.CreateUser` 方法，以程式設計方式根據使用者的輸入來加入新的使用者帳戶。 不過，我們的程式碼只是建立新的使用者帳戶。 它不會執行任何後續動作，像是將使用者登入到剛建立的使用者帳戶底下的網站，或傳送確認電子郵件給使用者。 這些額外的步驟會在按鈕的 `Click` 事件處理常式中需要額外的程式碼。

ASP.NET 隨附 CreateUserWizard 控制項，其設計目的是要處理使用者帳戶建立程式，從呈現使用者介面來建立新的使用者帳戶、在成員資格架構中建立帳戶，以及執行後續帳戶建立工作，例如傳送確認電子郵件，並將剛建立的使用者記錄到網站。 使用 CreateUserWizard 控制項很簡單，只要將 CreateUserWizard 控制項從 [工具箱] 拖曳到頁面上，然後再設定幾個屬性即可。 在大部分的情況下，您不需要撰寫一行程式碼。 我們將在步驟6中詳細探討這個簡潔的控制項。

如果新的使用者帳戶只會透過一般的建立帳戶網頁建立，則您不太可能需要撰寫使用 `CreateUser` 方法的程式碼，因為 CreateUserWizard 控制項可能會符合您的需求。 不過，如果您需要高度自訂的建立帳戶使用者經驗，或需要透過替代介面以程式設計方式建立新的使用者帳戶時，`CreateUser` 方法就很方便。 例如，您可能有一個頁面，可讓使用者上傳包含其他應用程式之使用者資訊的 XML 檔案。 頁面可能會剖析已上傳之 XML 檔案的內容，並藉由呼叫 `CreateUser` 方法，為 XML 中所代表的每個使用者建立新帳戶。

## <a name="step-6-creating-a-new-user-with-the-createuserwizard-control"></a>步驟 6：使用 CreateUserWizard 控制項建立新的使用者

ASP.NET 隨附許多登入 Web 控制項。 這些控制項有助於許多常見的使用者帳戶和登入相關案例。 [CreateUserWizard 控制項](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx)是一種設計來呈現使用者介面的控制項，以便將新的使用者帳戶新增至成員資格架構。

就像許多其他登入相關的 Web 控制項一樣，您可以使用 CreateUserWizard，而不需要撰寫任何一行程式碼。 它直覺提供了以成員資格提供者的設定為基礎的使用者介面，而且會在使用者輸入必要資訊並按一下 [建立使用者] 按鈕之後，于內部呼叫 `Membership` 類別的 `CreateUser` 方法。 CreateUserWizard 控制項非常可自訂。 在帳戶建立程式的各個階段，會引發事件的主機。 我們可以視需要建立事件處理常式，以將自訂邏輯插入帳戶建立工作流程中。 此外，CreateUserWizard 的外觀也非常有彈性。 有一些屬性會定義預設介面的外觀;如有必要，可以將控制項轉換成範本，或加入其他使用者註冊「步驟」。

讓我們先來看一下如何使用 CreateUserWizard 控制項的預設介面和行為。 接著，我們將探索如何透過控制項的屬性和事件來自訂外觀。

### <a name="examining-the-createuserwizards-default-interface-and-behavior"></a>檢查 CreateUserWizard 的預設介面和行為

返回 [`Membership`] 資料夾中的 [`CreatingUserAccounts.aspx`] 頁面，切換至 [設計] 或 [分割] 模式，然後將 [CreateUserWizard] 控制項加入至頁面的頂端。 CreateUserWizard 控制項會在 [工具箱] 的 [登入控制項] 區段下進行。 加入控制項之後，將其 [`ID`] 屬性設為 [`RegisterUser`]。 如 [圖 11] 中的螢幕擷取畫面所示，CreateUserWizard 會呈現介面，其中包含新使用者的使用者名稱、密碼、電子郵件地址和安全性問題和答案的文字方塊。

[![CreateUserWizard 控制項呈現一般的建立使用者介面](creating-user-accounts-cs/_static/image32.png)](creating-user-accounts-cs/_static/image31.png)

**圖 11**：CreateUserWizard 控制項會呈現一般的建立使用者介面（[按一下以查看完整大小的影像](creating-user-accounts-cs/_static/image33.png)）

讓我們花點時間比較 CreateUserWizard 控制項產生的預設使用者介面與我們在步驟5中建立的介面。 針對新手，CreateUserWizard 控制項可讓訪客同時指定安全性問題和答案，而我們手動建立的介面則使用預先定義的安全性問題。 CreateUserWizard 控制項的介面也包含驗證控制項，但我們尚未在介面的表單欄位上執行驗證。 CreateUserWizard 控制介面包含 [確認密碼] 文字方塊（連同 CompareValidator，以確保文字輸入的 [密碼] 和 [比較密碼] 文字方塊相等）。

有趣的是，當 CreateUserWizard 控制項呈現其使用者介面時，會參考成員資格提供者的設定。 例如，只有在 `requiresQuestionAndAnswer` 設定為 True 時，才會顯示 [安全性問題] 和 [解答] 文字方塊。 同樣地，CreateUserWizard 會自動新增 RegularExpressionValidator 控制項，以確保符合密碼強度需求，並根據 `minRequiredPasswordLength`、`minRequiredNonalphanumericCharacters`和 `passwordStrengthRegularExpression` 的設定來設定其 `ErrorMessage` 和 `ValidationExpression` 屬性。

如其名所示，CreateUserWizard 控制項衍生自[Wizard 控制項](https://msdn.microsoft.com/library/s2etd1ek.aspx)。 Wizard 控制項的設計目的是要提供用來完成多步驟工作的介面。 Wizard 控制項可能會有任意數目的 `WizardSteps`，其中每一個都是定義該步驟之 HTML 和 Web 控制項的範本。 Wizard 控制項一開始會顯示第一個 `WizardStep`，以及允許使用者在下一個步驟中進行的導覽控制項，或回到先前的步驟。

如 [圖 11] 中的宣告式標記所示，CreateUserWizard 控制項的預設介面包含兩個 `WizardSteps:`

- [`CreateUserWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizardstep.aspx) –呈現介面，以收集建立新使用者帳戶的資訊。 這是 [圖 11] 所示的步驟。
- [`CompleteWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.completewizardstep.aspx) –呈現一則訊息，指出已成功建立帳戶。

藉由將上述任一步驟轉換成範本，或加入您自己的 `WizardSteps`，即可修改 CreateUserWizard 的外觀和行為。 我們將在*儲存額外的使用者資訊*教學課程中，探討如何將 `WizardStep` 新增至註冊介面。

讓我們看看 CreateUserWizard 控制項的實際運作。 透過瀏覽器造訪 [`CreatingUserAccounts.aspx`] 頁面。 首先，在 CreateUserWizard 的介面中輸入一些不正確值。 請嘗試輸入不符合密碼強度需求的密碼，或將 [使用者名稱] 文字方塊保留空白。 CreateUserWizard 將會顯示適當的錯誤訊息。 [圖 12] 顯示嘗試建立具有能力不佳強式密碼的使用者時的輸出。

[![CreateUserWizard 會自動插入驗證控制項](creating-user-accounts-cs/_static/image35.png)](creating-user-accounts-cs/_static/image34.png)

**圖 12**：CreateUserWizard 會自動插入驗證控制項（[按一下以查看完整大小的影像](creating-user-accounts-cs/_static/image36.png)）

接下來，在 CreateUserWizard 中輸入適當的值，然後按一下 [建立使用者] 按鈕。 假設已輸入必要的欄位，且密碼的強度已足夠，則 CreateUserWizard 會透過成員資格架構建立新的使用者帳戶，然後顯示 `CompleteWizardStep`的介面（請參閱 [圖 13]）。 在幕後，CreateUserWizard 會呼叫 `Membership.CreateUser` 方法，就像我們在步驟5中所做的一樣。

[已成功建立新的使用者帳戶 ![](creating-user-accounts-cs/_static/image38.png)](creating-user-accounts-cs/_static/image37.png)

**圖 13**：已成功建立新的使用者帳戶（[按一下以查看完整大小的影像](creating-user-accounts-cs/_static/image39.png)）

> [!NOTE]
> 如 [圖 13] 所示，`CompleteWizardStep`的介面包含 [繼續] 按鈕。 不過，此時按一下它只會執行回傳，讓訪客在相同的頁面上。 在「透過其屬性自訂 CreateUserWizard 的外觀和行為」一節中，我們將探討如何讓此按鈕將訪客傳送至 `Default.aspx` （或其他網頁）。

建立新的使用者帳戶之後，請返回 Visual Studio 並檢查 `aspnet_Users` 和 `aspnet_Membership` 資料表，如我們在 [圖 10] 中所做的，確認已成功建立帳戶。

### <a name="customizing-the-createuserwizards-behavior-and-appearance-through-its-properties"></a>透過其屬性自訂 CreateUserWizard 的行為和外觀

透過屬性、`WizardSteps`和事件處理常式，可以各種方式自訂 CreateUserWizard。 在本節中，我們將探討如何透過其屬性自訂控制項的外觀;下一節將探討如何透過事件處理常式擴充控制項的行為。

幾乎 CreateUserWizard 控制項的預設使用者介面中顯示的所有文字，都可以透過其屬性眾多來自訂。 例如，顯示在文字方塊左邊的 [使用者名稱]、[密碼]、[確認密碼]、[電子郵件]、[安全性問題] 和 [安全性解答] 標籤，可以分別由[`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.usernamelabeltext.aspx)、 [`PasswordLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.passwordlabeltext.aspx)、 [`ConfirmPasswordLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.confirmpasswordlabeltext.aspx)、 [`EmailLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.emaillabeltext.aspx)、 [`QuestionLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.questionlabeltext.aspx)和[`AnswerLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.answerlabeltext.aspx)屬性自訂。 同樣地，還有一些屬性可在 [`CreateUserWizardStep`] 和 [`CompleteWizardStep`] 中指定 [建立使用者] 和 [繼續] 按鈕的文字，而且這些按鈕會呈現為按鈕、LinkButtons 或 ImageButtons。

色彩、框線、字型和其他視覺效果元素可透過樣式屬性的主控制項來設定。 CreateUserWizard 控制項本身具有通用的 Web 控制項樣式屬性– `BackColor`、`BorderStyle`、`CssClass`、`Font`等等–而且有一些樣式屬性可用於定義 CreateUserWizard 介面中特定區段的外觀。 例如， [`TextBoxStyle` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.textboxstyle.aspx)會定義 `CreateUserWizardStep`中文字方塊的樣式，而[`TitleTextStyle` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.titletextstyle.aspx)則會定義標題的樣式（[註冊您的新帳戶]）。

除了與外觀相關的屬性之外，還有一些屬性會影響 CreateUserWizard 控制項的行為。 如果設定為 True， [`DisplayCancelButton` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.displaycancelbutton.aspx)會在 [建立使用者] 按鈕旁邊顯示 [取消] 按鈕（預設值為 False）。 如果您顯示 [取消] 按鈕，請務必同時設定 [ [`CancelDestinationPageUrl`] 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)，它會指定使用者在按一下 [取消] 之後要傳送到的頁面。 如上一節所述，`CompleteWizardStep`介面中的 [繼續] 按鈕會導致回傳，但會將訪客留在相同的頁面上。 若要在按一下 [繼續] 按鈕之後將造訪者傳送至其他頁面，只要在 [ [`ContinueDestinationPageUrl`] 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)中指定 URL 即可。

讓我們更新 `RegisterUser` CreateUserWizard 控制項，以顯示 [取消] 按鈕，並在按下 [取消] 或 [繼續] 按鈕時，將訪客傳送至 `Default.aspx`。 若要完成這項操作，請將 `DisplayCancelButton` 屬性設為 True，並將 `CancelDestinationPageUrl` 和 `ContinueDestinationPageUrl` 屬性設定為 "~/Default.aspx"。 [圖 14] 顯示透過瀏覽器觀看時更新的 CreateUserWizard。

[![CreateUserWizardStep 包含 [取消] 按鈕](creating-user-accounts-cs/_static/image41.png)](creating-user-accounts-cs/_static/image40.png)

**圖 14**：`CreateUserWizardStep` 包含 [取消] 按鈕（[按一下以查看完整大小的影像](creating-user-accounts-cs/_static/image42.png)）

當訪客輸入使用者名稱、密碼、電子郵件地址和安全性問題和答案，並按一下 [建立使用者] 時，就會建立新的使用者帳戶，並以新建立的使用者身分登入訪客。 假設造訪頁面的人是自行建立新帳戶，這可能是想要的行為。 不過，您可能會想要允許系統管理員加入新的使用者帳戶。 如此一來，就會建立使用者帳戶，但是系統管理員會繼續以系統管理員的身分登入（而不是新建立的帳戶）。 您可以透過布林值[`LoginCreatedUser` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)來修改這個行為。

成員資格架構中的使用者帳戶包含核准的旗標;未核准的使用者無法登入網站。 根據預設，新建立的帳戶會標示為 [已核准]，讓使用者能夠立即登入網站。 不過，您可以將新的使用者帳戶標示為未核准。 也許您想讓系統管理員在登入之前手動核准新的使用者;或者，您可能想要確認在註冊時輸入的電子郵件地址是有效的，然後才允許使用者登入。 不論是哪種情況，您都可以將 CreateUserWizard 控制項的[`DisableCreatedUser` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx)設定為 True （預設值為 False），將新建立的使用者帳戶標示為未核准。

其他與行為相關的注意事項屬性包括 `AutoGeneratePassword` 和 `MailDefinition`。 如果[`AutoGeneratePassword` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.autogeneratepassword.aspx)設定為 True，則 `CreateUserWizardStep` 不會顯示 [密碼] 和 [確認密碼] 文字方塊;而是使用 `Membership` 類別的[`GeneratePassword` 方法](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)，自動產生新建立的使用者密碼。 `GeneratePassword` 方法會使用指定長度的密碼，以及具有足夠數量的非英數位元來滿足所設定的密碼強度需求。

如果您想要傳送電子郵件給帳戶建立程式期間所指定的電子郵件地址， [`MailDefinition` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx)會很有用。 `MailDefinition` 屬性包含一系列的子屬性，可定義所建立之電子郵件訊息的相關資訊。 這些子屬性包括 `Subject`、`Priority`、`IsBodyHtml`、`From`、`CC`和 `BodyFileName`之類的選項。 [`BodyFileName` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx)會指向包含電子郵件訊息本文的文字或 HTML 檔案。 主體支援兩個預先定義的預留位置： `<%UserName%>` 和 `<%Password%>`。 這些預留位置（如果存在於 `BodyFileName` 檔案中）將會取代為剛建立的使用者名稱和密碼。

> [!NOTE]
> `CreateUserWizard` 控制項的 `MailDefinition` 屬性只會指定建立新帳戶時所傳送之電子郵件訊息的詳細資料。 它不包含如何實際傳送電子郵件訊息的任何詳細資料（也就是，是否使用 SMTP 伺服器或郵件放置目錄、任何驗證資訊等等）。 這些低層級的詳細資料必須在 `Web.config`的 `<system.net>` 區段中定義。 如需有關這些設定的詳細資訊，以及從 ASP.NET 2.0 傳送電子郵件的一般資訊，請參閱 SystemNetMail.com 和我的文章在[ASP.NET 2.0 中傳送電子郵件中](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)的[常見問題](http://www.systemnetmail.com/)。

### <a name="extending-the-createuserwizards-behavior-using-event-handlers"></a>使用事件處理常式擴充 CreateUserWizard 的行為

CreateUserWizard 控制項會在其工作流程期間引發數個事件。 例如，在訪客輸入他們的使用者名稱、密碼和其他相關資訊，然後按一下 [建立使用者] 按鈕後，CreateUserWizard 控制項會引發其[`CreatingUser` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)。 如果在建立程式期間發生問題，則會引發[`CreateUserError` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx);不過，如果成功建立使用者，則會引發[`CreatedUser` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx)。 還有一些會引發的其他 CreateUserWizard 控制項事件，但這些都是最無關的三個。

在某些情況下，我們可能會想要利用 CreateUserWizard 工作流程，我們可以建立適當事件的事件處理常式。 為了說明這一點，讓我們來加強 `RegisterUser` CreateUserWizard 控制項，以在使用者名稱和密碼上加入一些自訂驗證。 特別是，讓我們來加強我們的 CreateUserWizard，使使用者名稱不能包含開頭或尾端空格，而且使用者名稱不能出現在密碼中的任何地方。 簡單地說，我們想要防止某人建立 "Scott" 之類的使用者名稱，或使用「Scott」和「Scott」之類的使用者名稱/密碼組合。

為了達成此目的，我們將建立 `CreatingUser` 事件的事件處理常式，以執行額外的驗證檢查。 如果提供的資料無效，我們必須取消建立程式。 我們也需要將標籤 Web 控制項新增至頁面，以顯示訊息，說明使用者名稱或密碼無效。 首先，在 CreateUserWizard 控制項下方新增標籤控制項，將其 `ID` 屬性設為 `InvalidUserNameOrPasswordMessage`，並將其 `ForeColor` 屬性設定為 `Red`。 清除其 `Text` 屬性，並將它的 `EnableViewState` 和 `Visible` 屬性設定為 False。

[!code-aspx[Main](creating-user-accounts-cs/samples/sample7.aspx)]

接下來，建立 CreateUserWizard 控制項 `CreatingUser` 事件的事件處理常式。 若要建立事件處理常式，請在設計工具中選取控制項，然後移至 [屬性視窗]。 從該處按一下閃電圖示，然後按兩下適當的事件以建立事件處理常式。

將下列程式碼加入至 `CreatingUser` 事件處理常式：

[!code-csharp[Main](creating-user-accounts-cs/samples/sample8.cs)]

請注意，在 CreateUserWizard 控制項中輸入的使用者名稱和密碼會分別透過其[`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx)和[`Password` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.password.aspx)來提供。 我們會在上述事件處理常式中使用這些屬性，來判斷提供的使用者名稱是否包含開頭或尾端空格，以及是否在密碼中找到使用者名稱。 如果符合上述任一條件，[`InvalidUserNameOrPasswordMessage`] 標籤中會顯示錯誤訊息，而且事件處理常式的 [`e.Cancel`] 屬性會設定為 [`true`]。 如果 `e.Cancel` 設定為 `true`，則 CreateUserWizard 會將其工作流程縮短，並有效地取消使用者帳戶建立程式。

[圖 15] 顯示當使用者輸入具有開頭空白的使用者名稱時，`CreatingUserAccounts.aspx` 的螢幕擷取畫面。

[不允許具有開頭或尾端空格的 ![使用者名稱](creating-user-accounts-cs/_static/image44.png)](creating-user-accounts-cs/_static/image43.png)

**圖 15**：不允許具有開頭或尾端空格的使用者名稱（[按一下以查看完整大小的影像](creating-user-accounts-cs/_static/image45.png)）

> [!NOTE]
> 我們會在 *<a id="_msoanchor_11"></a>[儲存額外的使用者資訊](storing-additional-user-information-cs.md)* 教學課程中，看到使用 CreateUserWizard 控制項 `CreatedUser` 事件的範例。

## <a name="summary"></a>總結

`Membership` 類別的 `CreateUser` 方法會在成員資格架構中建立新的使用者帳戶。 其方式是將呼叫委派給設定的成員資格提供者。 在 `SqlMembershipProvider`的案例中，`CreateUser` 方法會將記錄新增至 `aspnet_Users` 和 `aspnet_Membership` 資料庫資料表。

雖然可以程式設計方式建立新的使用者帳戶（如我們在步驟5中所見），但更快速且更簡單的方法是使用 CreateUserWizard 控制項。 這個控制項會轉譯一個多步驟的使用者介面，用來收集使用者資訊，並在成員資格架構中建立新的使用者。 實際上，此控制項使用步驟5中所檢查的相同 `Membership.CreateUser` 方法，但控制項會建立使用者介面、驗證控制項，並回應使用者帳戶建立錯誤，而不需要撰寫程式碼的舔。

此時，我們已準備好建立新使用者帳戶的功能。 不過，登入頁面仍然會針對我們在第二個教學課程中指定的硬式編碼認證進行驗證。 <a id="_msoanchor_12"></a>在[下一個教學](validating-user-credentials-against-the-membership-user-store-cs.md)課程中，我們將更新 `Login.aspx`，以根據成員資格架構來驗證使用者所提供的認證。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [`CreateUser` 技術檔](https://msdn.microsoft.com/library/system.web.security.membershipprovider.createuser.aspx)
- [CreateUserWizard 控制項總覽](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx)
- [建立以檔案系統為基礎的網站地圖提供者](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)
- [使用 ASP.NET 2.0 Wizard 控制項建立逐步執行的使用者介面](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [檢查 ASP.NET 2.0 的網站導覽](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [主版頁面和網站流覽](https://asp.net/learn/data-access/tutorial-03-vb.aspx)
- [您已等候的 SQL 網站地圖提供者](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx)

### <a name="about-the-author"></a>關於作者

Scott Mitchell，自1998起，有多個 ASP/ASP. NET 書籍和創辦人的4GuysFromRolla.com。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是 *[在24小時內讓自己的 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 Scott 可以在[mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或透過他在[http://ScottOnWriting.NET](http://scottonwriting.net/)的 blog。

### <a name="special-thanks-to"></a>特別感謝 。

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Teresa Murphy。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)的那一行下拉式。

> [!div class="step-by-step"]
> [上一頁](creating-the-membership-schema-in-sql-server-cs.md)
> [下一頁](validating-user-credentials-against-the-membership-user-store-cs.md)
