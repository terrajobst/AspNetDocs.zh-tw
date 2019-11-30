---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: 單一登入（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 7e32f444dc38132296cffd45ac658f5abf51f314
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585273"
---
# <a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a>單一登入（使用 Azure 建立真實世界的雲端應用程式）

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。 如需電子書的相關資訊，請參閱[第一章](introduction.md)。

當您開發雲端應用程式時，需要考慮許多安全性問題，但在此系列中，我們只著重于單一登入。 人們常問的一個問題是：「我主要為公司的員工建立應用程式;如何在雲端中裝載這些應用程式，並讓他們能夠使用我的員工在內部部署環境中所知道和使用的相同安全性模型，以執行裝載于防火牆內的應用程式？ 我們啟用此案例的其中一種方式，稱為 Azure Active Directory （Azure AD）。 Azure AD 可讓您透過網際網路提供企業營運（LOB）應用程式，讓您也可以將這些應用程式提供給商務合作夥伴。

## <a name="introduction-to-azure-ad"></a>Azure AD 簡介

[Azure AD](https://docs.microsoft.com/azure/active-directory/)在雲端中提供[Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) 。 主要功能包括下列各項：

- 它會與內部部署 Active Directory 整合。
- 它可讓您使用您的應用程式進行單一登入。
- 它支援開放式標準，例如[SAML](http://en.wikipedia.org/wiki/SAML_2.0)、 [WS-送](http://en.wikipedia.org/wiki/WS-Federation)出和[OAuth 2.0](http://oauth.net/2/)。
- 它支援 Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx)。

假設您有內部部署 Windows Server Active Directory 環境，可用來讓員工登入內部網路應用程式：

![](single-sign-on/_static/image1.png)

Azure AD 可讓您在雲端中建立目錄。 這是一項免費功能，而且很容易設定。

它可以完全獨立于內部部署 Active Directory;您可以將任何想要的人放在其中，並在網際網路應用程式中進行驗證。

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

或者，您也可以將它與您的內部部署 AD 整合。

![AD 與 WAAD 整合](single-sign-on/_static/image3.png)

現在，可以在內部部署驗證的所有員工也可以透過網際網路進行驗證，而不需要開啟防火牆或在您的資料中心部署任何新的伺服器。 您可以繼續利用您知道並使用的所有現有 Active Directory 環境，讓您的內部應用程式單一登入功能。

在 AD 與 Azure AD 之間進行此連線之後，您也可以讓 web 應用程式和行動裝置在雲端中驗證您的員工，而且您可以啟用協力廠商應用程式（例如 Office 365、SalesForce.com 或 Google apps）以接受您的員工的認證。 如果您使用的是 Office 365，表示您已經設定 Azure AD，因為 Office 365 會使用 Azure AD 進行驗證和授權。

![協力廠商應用程式](single-sign-on/_static/image4.png)

這種方法的優點是，每當您的組織新增或刪除使用者，或使用者變更密碼時，您就會使用您目前在內部部署環境中使用的相同程式。 您的所有內部部署 AD 變更都會自動傳播到雲端環境。

如果您的公司使用或移至 Office 365，好消息是您會自動設定 Azure AD，因為 Office 365 會使用 Azure AD 進行驗證。 因此，您可以輕鬆地在自己的應用程式中使用 Office 365 所使用的相同驗證。

## <a name="set-up-an-azure-ad-tenant"></a>設定 Azure AD 租使用者

Azure AD 目錄稱為 Azure AD[租](https://technet.microsoft.com/library/jj573650.aspx)使用者，而設定租使用者相當簡單。 我們會示範如何在 Azure 管理入口網站中完成，以說明概念，但當然也像是其他入口網站功能，您也可以使用腳本或管理 API 來執行此作業。

在管理入口網站中，按一下 [Active Directory] 索引標籤。

![入口網站中的 WAAD](single-sign-on/_static/image5.png)

您的 Azure 帳戶會自動有一個 Azure AD 租使用者，而且您可以按一下頁面底部的 [**新增**] 按鈕，以建立其他目錄。 例如，您可能會想要一個用於測試環境，另一個用於生產環境。 請仔細考慮您為新目錄命名的內容。 如果您使用目錄的名稱，然後再為其中一位使用者再次使用您的名稱，這可能會造成混淆。

![加入目錄](single-sign-on/_static/image6.png)

入口網站具有在此環境內建立、刪除及管理使用者的完整支援。 例如，若要新增使用者，請移至 [**使用者**] 索引標籤，然後按一下 [**新增使用者**] 按鈕。

![[新增使用者] 按鈕](single-sign-on/_static/image7.png)

![[新增使用者] 對話方塊](single-sign-on/_static/image8.png)

您可以建立僅存在於此目錄中的新使用者，或者您可以在此目錄中將 Microsoft 帳戶註冊為使用者，或在此目錄中註冊為使用者，或從另一個 Azure AD 目錄登錄或使用者。 （在實際目錄中，預設網域會是 ContosoTest.onmicrosoft.com。 您也可以使用自己選擇的網域，例如 contoso.com。）

![使用者類型](single-sign-on/_static/image9.png)

![[新增使用者] 對話方塊](single-sign-on/_static/image10.png)

您可以將使用者指派給角色。

![使用者設定檔](single-sign-on/_static/image11.png)

並使用暫時密碼建立帳戶。

![暫時密碼](single-sign-on/_static/image12.png)

您以這種方式建立的使用者可以立即使用此雲端目錄登入您的 web 應用程式。

不過，「企業單一登入」的絕佳功能是 [**目錄整合**] 索引標籤：

![[目錄整合] 索引標籤](single-sign-on/_static/image13.png)

如果您啟用目錄整合，並[下載工具](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)，您可以將此雲端目錄與您已在組織內使用的現有內部部署 Active Directory 同步。 然後，儲存在您目錄中的所有使用者都會顯示在此雲端目錄中。 您的雲端應用程式現在可以使用現有的 Active Directory 認證來驗證您的所有員工。 而且這一切都是免費的–同步處理工具和 Azure AD 本身。

此工具是便於使用的 wizard，您可以從這些螢幕擷取畫面查看。 這些不是完整的指示，只是示範基本程式的範例。 如需更詳細的「作法」資訊，請參閱本章結尾的 Resources （[資源](#resources)）一節中的連結。

![WAAD 同步處理工具設定向導](single-sign-on/_static/image14.png)

按 **[下一步]** ，然後輸入您的 Azure Active Directory 認證。

![WAAD 同步處理工具設定向導](single-sign-on/_static/image15.png)

按 **[下一步]** ，然後輸入您的內部部署 AD 認證。

![WAAD 同步處理工具設定向導](single-sign-on/_static/image16.png)

按 **[下一步]** ，然後指出您是否想要將 AD 密碼雜湊儲存在雲端中。

![WAAD 同步處理工具設定向導](single-sign-on/_static/image17.png)

您可以儲存在雲端中的密碼雜湊是單向雜湊;實際的密碼永遠不會儲存在 Azure AD 中。 如果您決定不將雜湊儲存在雲端中，您必須使用[Active Directory 同盟服務](https://technet.microsoft.com/library/hh831502.aspx)（ADFS）。 [選擇是否要使用 ADFS 時，還有其他因素需要考慮](https://technet.microsoft.com/library/jj573653.aspx)。 ADFS 選項需要一些額外的設定步驟。

如果您選擇將雜湊儲存在雲端中，您就完成了，而且當您按 **[下一步]** 時，工具就會開始同步處理目錄。

![WAAD 同步處理工具設定向導](single-sign-on/_static/image18.png)

幾分鐘後您就完成了。

![WAAD 同步處理工具設定向導](single-sign-on/_static/image19.png)

在 Windows 2003 或更新版本的組織中，您只需要在一個網域控制站上執行此功能。 而不需要重新開機。 當您完成時，您的所有使用者都在雲端中，而且您可以使用 SAML、OAuth 或 WS-ADDRESSING，從任何 web 或行動應用程式進行單一登入。

有時候我們會詢問您如何保護這一點– Microsoft 是否將它用於自己的機密商務資料？ 答案是肯定的。 例如，如果您移至[https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/)的內部 Microsoft SharePoint 網站，系統會提示您登入。

![Office 365 登入](single-sign-on/_static/image20.png)

Microsoft 已啟用 ADFS，因此當您輸入 Microsoft ID 時，您會被重新導向至 ADFS 登入頁面。

![ADFS 登入](single-sign-on/_static/image21.png)

當您輸入儲存在內部 Microsoft AD 帳戶中的認證之後，就可以存取此內部應用程式。

![MS SharePoint 網站](single-sign-on/_static/image22.png)

我們會使用 AD 登入伺服器，主要是因為我們已在 Azure AD 變成可用之前先設定 ADFS，但登入程式正在通過雲端中的 Azure AD 目錄。 我們將重要的檔、原始檔控制、效能管理檔案、銷售報告等等放在雲端，並使用這個完全相同的解決方案來保護它們。

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a>建立使用 Azure AD 進行單一登入的 ASP.NET 應用程式

Visual Studio 可讓您輕鬆地建立使用 Azure AD 進行單一登入的應用程式，如您在幾個螢幕擷取畫面中所見。

當您建立新的 ASP.NET 應用程式（MVC 或 Web Forms）時，預設的驗證方法會是 ASP.NET Identity。 若要將其變更為 Azure AD，請按一下 [**變更驗證**] 按鈕。

![變更驗證](single-sign-on/_static/image23.png)

選取 [組織帳戶]，輸入您的功能變數名稱，然後選取 [單一登入]。

![[設定驗證] 對話方塊](single-sign-on/_static/image24.png)

您也可以將目錄資料的讀取或讀取/寫入權限授與應用程式。 如果您這麼做，它可以使用[Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx)查閱使用者的電話號碼、找出他們是否在辦公室、上次登入的時間等等。

這就是您必須 Visual Studio 要求 Azure AD 租使用者之系統管理員的認證，然後再為新的應用程式設定您的專案和 Azure AD 租使用者。

當您執行專案時，您會看到登入頁面，而且您可以使用 Azure AD 目錄中使用者的認證來登入。

![組織帳戶登入](single-sign-on/_static/image25.png)

![已登入](single-sign-on/_static/image26.png)

當您將應用程式部署至 Azure 時，您只需要選取 [**啟用組織驗證**] 核取方塊，再一次 Visual Studio 會為您處理所有設定。

![發行網站](single-sign-on/_static/image27.png)

這些螢幕擷取畫面來自完整的逐步教學課程，說明如何建立使用 Azure AD 驗證的應用程式：[使用 Azure Active Directory 開發 ASP.NET 應用程式](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)。

## <a name="summary"></a>總結

在本章中，您會看到 Azure Active Directory、Visual Studio 和 ASP.NET，可讓您輕鬆地在網際網路應用程式中為貴組織的使用者設定單一登入。 您的使用者可以使用他們用來登入的相同認證（使用內部網路中的 Active Directory）登入網際網路應用程式。

[下一章](data-storage-options.md)探討適用于雲端應用程式的資料儲存體選項。

<a id="resources"></a>
## <a name="resources"></a>資源

如需詳細資訊，請參閱下列資源：

- [Azure Active Directory 檔](https://docs.microsoft.com/azure/active-directory/)。 Windowsazure.com 網站上 Azure AD 檔的入口網站頁面。 如需逐步教學課程，請參閱**開發**一節。
- [Azure 多重要素驗證](https://docs.microsoft.com/azure/multi-factor-authentication/)。 適用于 Azure 中多因素驗證之檔的入口網站頁面。
- [組織帳戶驗證選項](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)。 [Visual Studio 2013 新增-專案] 對話方塊中 Azure AD 驗證選項的說明。
- [Microsoft 模式和實務-同盟身分識別模式](https://msdn.microsoft.com/library/dn589790.aspx)。
- [做法：安裝 Azure Active Directory 同步處理工具](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)。
- [Active Directory 同盟服務2.0 內容對應](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)。 ADFS 2.0 相關檔的連結。
- [Windows Azure AD 應用程式中以角色為基礎和以 ACL 為基礎的授權](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)。 範例應用程式。
- [Azure Active Directory 圖形 API 的 blog](https://blogs.msdn.com/b/aadgraphteam/)。
- 在混合式身分[識別基礎結構的 BYOD 和目錄整合中存取控制](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)。 Gayana Bagdasaryan 的 Tech Ed 2014 研討會影片。

> [!div class="step-by-step"]
> [上一頁](web-development-best-practices.md)
> [下一頁](data-storage-options.md)
