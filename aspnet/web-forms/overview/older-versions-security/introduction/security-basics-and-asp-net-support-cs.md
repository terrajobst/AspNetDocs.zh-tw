---
uid: web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-cs
title: 安全性基本概念和 ASP.NET 支援C#（） |Microsoft Docs
author: rick-anderson
description: 這是一系列教學課程中的第一個教學課程，將探索透過 web 表單驗證訪客的技術，並授權存取參與 。
ms.author: riande
ms.date: 01/13/2008
ms.assetid: 07e15538-2f29-40c6-b2e7-e6115075ac83
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-cs
msc.type: authoredcontent
ms.openlocfilehash: 1ccaac101a83d0e28b07b220b8b7b61a9039227e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74642426"
---
# <a name="security-basics-and-aspnet-support-c"></a>安全性基本概念與 ASP.NET 支援 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載 PDF](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial01_Basics_cs.pdf)

> 這是一系列教學課程中的第一個教學課程，將探索透過 web 表單驗證訪客、授權存取特定頁面和功能，以及在 ASP.NET 應用程式中管理使用者帳戶的技術。

## <a name="introduction"></a>簡介

什麼是論壇、電子商務網站、線上電子郵件網站、入口網站和社交網站全都有共同的功能？ 它們全都提供*使用者帳戶*。 提供使用者帳戶的網站必須提供許多服務。 最少的新訪客必須能夠建立帳戶並傳回訪客，才能登入。 這類 web 應用程式可以根據登入的使用者做出決策：某些頁面或動作可能會限制為僅限登入的使用者，或是特定的使用者子集;其他頁面可能會顯示已登入使用者的特定資訊，或者可能會顯示更多或更少的資訊，視使用者在頁面上的流覽方式而定。

這是一系列教學課程中的第一個教學課程，將探索透過 web 表單驗證訪客、授權存取特定頁面和功能，以及在 ASP.NET 應用程式中管理使用者帳戶的技術。 在這些教學課程中，我們將探討如何：

- 識別使用者並將其登入網站
- 使用 ASP。用來管理使用者帳戶的網路成員資格架構
- 建立、更新和刪除使用者帳戶
- 根據登入的使用者限制存取網頁、目錄或特定功能
- 使用 ASP。將使用者帳戶與角色建立關聯的網路角色架構
- 管理使用者角色
- 根據已登入使用者的角色，限制存取網頁、目錄或特定功能
- 自訂和擴充 ASP。NET 的安全性 Web 控制項

這些教學課程的目的是要精簡，並提供逐步指示，讓您能以視覺化方式逐步完成整個流程。 每個教學課程都C#可在和 Visual Basic 版本中取得，並包含下載所使用的完整程式碼。 （第一個教學課程著重于高階觀點的安全性概念，因此不包含任何相關的程式碼）。

在本教學課程中，我們將討論重要的安全性概念，以及 ASP.NET 中可用來協助執行表單驗證、授權、使用者帳戶和角色的功能。 讓我們開始吧！

> [!NOTE]
> 安全性是任何應用程式的重要層面，其中涵蓋實體、技術和原則決策，而且需要高程度的規劃和領域知識。 本教學課程系列並非用於開發安全 web 應用程式的指南。 相反地，它特別著重于表單驗證、授權、使用者帳戶和角色。 雖然此系列中會討論一些關於這些問題的安全性概念，但有些是未探索。

## <a name="authentication-authorization-user-accounts-and-roles"></a>驗證、授權、使用者帳戶和角色

「驗證」、「授權」、「使用者帳戶」和「角色」是在此教學課程系列中經常使用的四個詞彙，所以我想要在 web 安全性內容中快速地定義這些詞彙。 在用戶端伺服器模型（例如網際網路）中，有許多情況下，伺服器需要識別提出要求的用戶端。 *驗證*是查明用戶端身分識別的程式。 已成功識別的用戶端稱為「已*驗證*」。 無法識別的用戶端稱為未*驗證*或*匿名*。

安全驗證系統至少需要下列三個 facet 之一：[您知道的專案、您有的東西，或是您](http://www.cs.cornell.edu/Courses/cs513/2005fa/NNLauthPeople.html)的事物。 大部分的 web 應用程式都依賴用戶端知道的某個專案，例如密碼或 PIN。 例如，用來識別使用者的使用者名稱和密碼的資訊稱為*認證*。 本教學課程系列著重于*表單驗*證，這是一種驗證模型，使用者可以在網頁表單中提供認證，以登入網站。 在之前，我們都已經歷過這種類型的驗證。 前往任何電子商務網站。 當您準備好要簽出時，系統會要求您登入，方法是在網頁的文字方塊中輸入您的使用者名稱和密碼。

除了識別用戶端，伺服器可能需要根據提出要求的用戶端，限制可存取的資源或功能。 「授權」（ *Authorization* ）是判斷特定使用者是否有權存取特定資源或功能的程式。

*使用者帳戶*是保存特定使用者相關資訊的存放區。 使用者帳戶必須至少包含可唯一識別使用者的資訊，例如使用者的登入名稱和密碼。 除了這項基本資訊之外，使用者帳戶可能還包括：使用者的電子郵件地址、建立帳戶的日期和時間;上次登入的日期和時間;名字和姓氏;電話號碼;和郵寄地址。 使用表單驗證時，使用者帳戶資訊通常會儲存在關係資料庫中，例如 Microsoft SQL Server。

支援使用者帳戶的 Web 應用程式可以選擇性地將使用者分組為*角色*。 角色只是套用至使用者的標籤，並提供定義授權規則和頁面層級功能的抽象概念。 例如，網站可能會包含系統管理員角色，其授權規則會禁止任何人（但系統管理員）存取一組特定的網頁。 此外，所有使用者（包括非系統管理員）都可以存取的各種頁面，可能會顯示額外的資料，或在系統管理員角色的使用者造訪時提供額外的功能。 藉由使用角色，我們可以依角色逐一定義這些授權規則，而不是以使用者為依據。

## <a name="authenticating-users-in-an-aspnet-application"></a>在 ASP.NET 應用程式中驗證使用者

當使用者在瀏覽器的位址視窗中輸入 URL 或按一下連結時，瀏覽器會針對指定的內容，對 web 伺服器進行[超文字傳輸通訊協定（HTTP）](http://en.wikipedia.org/wiki/HTTP)要求，其為 ASP.NET 網頁、影像、JavaScript 檔案或任何其他類型的內容。 Web 服務器負責傳回要求的內容。 在這種情況下，它必須判斷有關要求的一些事項，包括提出要求的人員，以及身分識別是否獲得授權可取得要求的內容。

根據預設，瀏覽器會傳送缺少任何類型識別資訊的 HTTP 要求。 但是，如果瀏覽器確實包含驗證資訊，則 web 伺服器會啟動驗證工作流程，這會嘗試識別提出要求的用戶端。 驗證工作流程的步驟取決於 web 應用程式所使用的驗證類型。 ASP.NET 支援三種類型的驗證： Windows、Passport 和 forms。 本教學課程系列著重于表單驗證，但讓我們花一點時間比較和對比 Windows 驗證使用者存放區和工作流程。

### <a name="authentication-via-windows-authentication"></a>透過 Windows 驗證進行驗證

Windows 驗證工作流程會使用下列其中一種驗證技術：

- 基本驗證
- 摘要式驗證
- Windows 整合式驗證

這三種技術的工作大致相同：當未經授權的匿名要求抵達時，web 伺服器會傳回 HTTP 回應，表示需要授權才能繼續。 然後，瀏覽器會顯示一個強制回應對話方塊，提示使用者輸入其使用者名稱和密碼（請參閱 [圖 1]）。 此資訊接著會透過 HTTP 標頭傳送回 web 伺服器。

![強制回應對話方塊會提示使用者輸入其認證](security-basics-and-asp-net-support-cs/_static/image1.png)

**圖 1**：強制回應對話方塊會提示使用者輸入其認證

提供的認證會針對網頁伺服器的 Windows 使用者存放區進行驗證。 這表示您的 web 應用程式中每個已驗證的使用者，在您的組織中都必須有 Windows 帳戶。 這在內部網路案例中很常見。 事實上，在內部網路設定中使用「Windows 整合式驗證」時，瀏覽器會自動為網頁伺服器提供用來登入網路的認證，藉此隱藏 [圖 1] 所示的對話方塊。 雖然 Windows 驗證適用于內部網路應用程式，但通常會不可行網際網路應用程式，因為您不想要為每個在您網站上註冊的使用者建立 Windows 帳戶。

### <a name="authentication-via-forms-authentication"></a>透過表單驗證驗證

另一方面，表單驗證是網際網路 web 應用程式的理想選擇。 回想一下，表單驗證會藉由提示使用者透過 web 表單輸入其認證來識別使用者。 因此，當使用者嘗試存取未經授權的資源時，系統會自動將他們重新導向至登入頁面，讓他們可以在其中輸入其認證。 提交的認證接著會針對自訂使用者存放區（通常是資料庫）進行驗證。

確認提交的認證之後，就會為使用者建立*表單驗證票證*。 此票證表示使用者已通過驗證，並包含識別資訊，例如使用者名稱。 表單驗證票證（通常）會在用戶端電腦上儲存為 cookie。 因此，後續造訪網站時，會在 HTTP 要求中包含表單驗證票證，藉此讓 web 應用程式在使用者登入後識別該使用者。

[圖 2] 說明來自高層級有利點的表單驗證工作流程。 請注意 ASP.NET 中的驗證和授權片段如何作為兩個不同的實體。 表單驗證系統會識別使用者（或其為匿名的報告）。 授權系統可判斷使用者是否有權存取要求的資源。 如果使用者未經授權（如 [圖 2] 嘗試匿名流覽 ProtectedPage），授權系統會報告使用者遭到拒絕，導致表單驗證系統自動將使用者重新導向至登入頁面。

使用者成功登入之後，後續的 HTTP 要求會包含表單驗證票證。 表單驗證系統只會識別使用者-它是用來判斷使用者是否可以存取所要求資源的授權系統。

![表單驗證工作流程](security-basics-and-asp-net-support-cs/_static/image2.png)

**圖 2**：表單驗證工作流程

在接下來的兩個教學課程中，我們將深入探討「表單驗證」的詳細資訊，[概述表單驗](an-overview-of-forms-authentication-cs.md)證和[表單驗證設定和 Advanced 主題](forms-authentication-configuration-and-advanced-topics-cs.md)。 深入瞭解 ASP。NET 的驗證選項，請參閱[ASP.NET authentication](https://msdn.microsoft.com/library/eeyk640h.aspx)。

## <a name="limiting-access-to-web-pages-directories-and-page-functionality"></a>限制網頁、目錄和頁面功能的存取

ASP.NET 包含兩種判斷特定使用者是否有權存取特定檔案或目錄的方式：

- 檔案**授權**-由於 ASP.NET 網頁和 web 服務會實作為位於 web 伺服器檔案系統上的檔案，因此可以透過存取控制清單（acl）來指定這些檔案的存取權。 檔案授權最常用於 Windows 驗證，因為 Acl 是適用于 Windows 帳戶的許可權。 使用表單驗證時，不論造訪網站的使用者為何，所有作業系統和檔案系統層級的要求都會由相同的 Windows 帳戶執行。
- **Url 授權**-使用 url 授權，網頁開發人員會在 web.config 中指定授權規則。這些授權規則會指定允許哪些使用者或角色存取，或拒絕其存取應用程式中的特定頁面或目錄。

檔案授權和 URL 授權會定義用來存取特定 ASP.NET 網頁或特定目錄中所有 ASP.NET 網頁的授權規則。 我們可以使用這些技巧來指示 ASP.NET 拒絕特定使用者對特定頁面的要求，或允許存取一組使用者，並拒絕其他人存取。 那麼，所有使用者都可以存取該頁面的情況，但是網頁的功能取決於使用者的情況呢？ 例如，許多支援使用者帳戶的網站，都有頁面顯示已驗證使用者的不同內容或資料，而不是匿名使用者。 匿名使用者可能會看到用來登入網站的連結，而已驗證的使用者會看到像是「歡迎回來 *」的訊息，以及登出*的連結。另一個範例：當您在拍賣網站上觀看專案時，您會看到不同的資訊，取決於您是 bidder 或拍賣專案的人。

這類頁面層級的調整可以透過宣告方式或以程式設計方式完成。 若要顯示與已驗證使用者不同的匿名內容，只要將[LoginView 控制項](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx)拖曳到頁面上，並在其 AnonymousTemplate 和 LoggedInTemplate 範本中輸入適當的內容即可。 或者，您可以透過程式設計方式判斷目前的要求是否已驗證、使用者是誰，以及它們屬於哪些角色（如果有的話）。 您可以使用這項資訊，在頁面上的方格或面板中顯示或隱藏資料行。

此系列包含三個著重于授權的教學課程。 以***使用者為基礎的授權***會檢查如何限制特定使用者帳戶對目錄中頁面或頁面的存取權;以***角色為基礎的授權***會查看在角色層級提供授權規則;最後，***根據目前登入的使用者***教學課程來顯示內容，會根據造訪頁面的使用者，探索修改特定頁面的內容和功能。 深入瞭解 ASP。NET 的授權選項，請參閱[ASP.NET 授權](https://msdn.microsoft.com/library/wce3kxhd.aspx)。

## <a name="user-accounts-and-roles"></a>使用者帳戶和角色

ASP.NET 的表單驗證提供了一種基礎結構，可讓使用者登入網站，並在頁面流覽時記住其已驗證的狀態。 和 URL 授權提供了一種架構，可限制對 ASP.NET 應用程式中特定檔案或資料夾的存取。 不過，這兩種功能都不提供儲存使用者帳戶資訊或管理角色的方法。

在 ASP.NET 2.0 之前，開發人員會負責建立自己的使用者和角色存放區。 它們也是在設計使用者介面的攔截程式，並撰寫程式碼來進行重要的使用者帳戶相關頁面，例如登入頁面和建立新帳戶的頁面，還有其他專案。 如果 ASP.NET 中沒有任何內建的使用者帳戶架構，則每位開發人員都必須負責自己的問題，例如，如何? 儲存密碼或其他機密資訊？那麼，我應該對密碼長度和強度施加哪些指導方針？

現在，在 ASP.NET 應用程式中執行使用者帳戶，會因為*成員資格架構*和內建的登入 Web 控制項而變得更簡單。 成員資格架構是[system.web. Security 命名空間](https://msdn.microsoft.com/library/system.web.security.aspx)中的少數類別，可提供執行重要使用者帳戶相關工作的功能。 成員資格架構中的主要類別是[成員資格類別](https://msdn.microsoft.com/library/system.web.security.membership.aspx)，其具有如下的方法：

- CreateUser
- DeleteUser
- GetAllUsers
- GetUser
- UpdateUser
- ValidateUser

成員資格架構使用[提供者模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)，其可將成員資格架構的 API 與其執行方式完全分開。 這可讓開發人員使用通用的 API，但可讓他們使用符合其應用程式自訂需求的執行方式。 簡單地說，成員資格類別會定義架構的基本功能（方法、屬性和事件），但不會實際提供任何的執行詳細資料。 相反地，成員資格類別的方法會叫用已設定的提供者，這就是執行實際工作的方式。 例如，當叫用成員資格類別的 CreateUser 方法時，成員資格類別並不知道使用者存放區的詳細資料。 它不知道使用者是在資料庫中，或是在 XML 檔案或其他存放區中進行維護。 成員資格類別會檢查 web 應用程式的設定，以判斷要將呼叫委派給哪個提供者，而該提供者類別負責在適當的使用者存放區中實際建立新的使用者帳戶。 這項互動如 [圖 3] 所示。

Microsoft 在 .NET Framework 中送出兩個成員資格提供者類別：

- [System.web.security.activedirectorymembershipprovider](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) -在 Active Directory 和 Active Directory 應用程式模式（ADAM）伺服器中執行成員資格 API。
- [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) -在 SQL Server 資料庫中執行成員資格 API。

本教學課程系列僅著重于 SqlMembershipProvider。

[![提供者模型可讓不同的執行順暢地插入架構中，&lt;/strong&gt;](security-basics-and-asp-net-support-cs/_static/image4.png)](security-basics-and-asp-net-support-cs/_static/image3.png)

**圖 03**：提供者模型可讓不同的執行順暢地插入架構中（[按一下以觀看完整大小的影像](security-basics-and-asp-net-support-cs/_static/image5.png)）

提供者模型的優點是可以由 Microsoft、協力廠商或個別開發人員開發，並順暢地插入成員資格架構。 例如，Microsoft 已發行[Microsoft Access 資料庫的成員資格提供者](https://download.microsoft.com/download/5/5/b/55bc291f-4316-4fd7-9269-dbf9edbaada8/sampleaccessproviders.vsi)。 如需成員資格提供者的詳細資訊，請參閱[提供者工具](https://msdn.microsoft.com/asp.net/aa336558.aspx)組，其中包括成員資格提供者的逐步解說、範例自訂提供者、提供者模型上超過100頁的檔，以及內建成員資格提供者（亦即 System.web.security.activedirectorymembershipprovider 和 SqlMembershipProvider）的完整原始程式碼。

ASP.NET 2.0 也引進了 Roles 架構。 如同成員資格架構，角色架構是建立在提供者模型的上方。 其 API 是透過[Roles 類別](https://msdn.microsoft.com/library/system.web.security.roles.aspx)公開，而 .NET Framework 隨附三個提供者類別：

- [AuthorizationStoreRoleProvider](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx) -管理授權管理員原則存放區中的角色資訊，例如 ACTIVE DIRECTORY 或 ADAM。
- [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) -在 SQL Server 資料庫中執行角色。
- [WindowsTokenRoleProvider](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx) -根據訪客的 Windows 群組建立角色資訊的關聯。 這個方法通常與 Windows 驗證搭配使用。

本教學課程系列僅著重于 SqlRoleProvider。

由於提供者模型包含一個順向對應的 API （成員資格和角色類別），因此可以在該 API 周圍建立功能，而不必擔心執行細節，這些是由頁面所選取的提供者所處理。員. 這個整合的 API 可讓 Microsoft 和協力廠商廠商建立 Web 控制項，以與成員資格和角色架構進行介面。 ASP.NET 隨附許多[登入 Web 控制項](https://msdn.microsoft.com/library/ms178329.aspx)，可用於執行一般使用者帳戶的使用者介面。 例如，登入[控制項會](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)提示使用者提供其認證、進行驗證，然後透過表單驗證將其記錄在中。 [LoginView 控制項](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx)提供的範本可向匿名使用者和已驗證的使用者顯示不同的標記，或是根據使用者的角色而不同的標記。 而[CreateUserWizard 控制項](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.aspx)提供逐步執行的使用者介面，用來建立新的使用者帳戶。

底下的各種登入控制項會與成員資格和角色架構互動。 大部分的登入控制項都可以執行，而不需要撰寫任何一行程式碼。 在未來的教學課程中，我們將更詳細地探討這些控制項，包括擴充和自訂其功能的技巧。

## <a name="summary"></a>總結

所有支援使用者帳戶的 web 應用程式都需要類似的功能，例如：使用者能夠登入，並在頁面流覽時記住其登入狀態;用來建立帳戶的新訪客的網頁;網頁開發人員能夠指定哪些資源、資料和功能可供使用者或角色使用。 驗證和授權使用者，以及管理使用者帳戶和角色的工作，在 ASP.NET 應用程式中很容易完成，因為表單驗證、URL 授權和成員資格和角色架構。

在接下來的幾個教學課程中，我們將逐步建立一個可運作的 web 應用程式，從頭開始探討這些層面。 在接下來的兩個教學課程中，我們將詳細探討表單驗證。 我們會看到表單驗證工作流程的運作方式、仔細分析表單驗證票證、討論安全性考慮，以及瞭解如何設定表單驗證系統，同時建立 web 應用程式，讓訪客能夠登入和登出。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ASP.NET 2.0 成員資格、角色、表單驗證和安全性資源](https://weblogs.asp.net/scottgu/ASP.NET-2.0-Membership_2C00_-Roles_2C00_-Forms-Authentication_2C00_-and-Security-Resources-)
- [ASP.NET 2.0 安全性指導方針](https://msdn.microsoft.com/library/ms998258.aspx)
- [ASP.NET 驗證](https://msdn.microsoft.com/library/eeyk640h.aspx)
- [ASP.NET 授權](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [ASP.NET 登入控制項總覽](https://msdn.microsoft.com/library/ms178329.aspx)
- [檢查 ASP.NET 2.0 的成員資格、角色和設定檔](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [如何：使用成員資格和角色保護我的網站？](https://asp.net/learn/videos/video-45.aspx) 影片
- [成員資格簡介](https://msdn.microsoft.com/library/yh26yfzy.aspx)
- [MSDN 安全性開發人員中心](https://msdn.microsoft.com/security/default.aspx)
- [Professional ASP.NET 2.0 安全性、成員資格和角色管理](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html)（ISBN：978-0-7645-9698-8）
- [提供者工具組](https://msdn.microsoft.com/asp.net/aa336558.aspx)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者是由許多有用的審核者所審查的教學課程系列。 本教學課程的領導審查者包括 Alicja Maziarz、John Suru 和 Teresa Murphy。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一步](an-overview-of-forms-authentication-cs.md)
