---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
title: 企業 Web 部署：案例總覽 |Microsoft Docs
author: jrjlee
description: 這一組教學課程會使用具有實際複雜性層級的範例解決方案，以及虛構的企業部署案例，來提供 ref 。
ms.author: riande
ms.date: 05/03/2012
ms.assetid: aa862153-4cd8-4e33-beeb-abf502c6664f
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
msc.type: authoredcontent
ms.openlocfilehash: 9786879844da13c21e6a953b1ab24b29ca8121e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574127"
---
# <a name="enterprise-web-deployment-scenario-overview"></a>企業 Web 部署：案例總覽

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 這一組教學課程會使用具有實際複雜性層級的範例解決方案，以及虛構的企業部署案例，來提供參考實作為，並將工作和逐步解說授與一般內容。 本主題描述教學課程案例，並介紹範例解決方案。

## <a name="scenario-description"></a>案例描述

Fabrikam，Inc. 是一家虛構的公司，建立了一個解決方案，讓遠端銷售團隊可以從 web 介面儲存和取出連絡人資訊。

Fabrikam，Inc. 的應用程式生命週期管理（ALM）流程需要將解決方案部署到三個伺服器環境的軟體發展程式的各個階段：

- 開發人員測試或「沙箱」環境。
- 以內部網路為基礎的預備環境。
- 網際網路面向的生產環境。

這些環境中的每個都有不同的設定和安全性需求，而且每個都有獨特的部署挑戰。

### <a name="the-fabrikam-inc-server-infrastructure"></a>Fabrikam，Inc. 伺服器基礎結構

這是 Fabrikam，Inc. 的高階開發和部署基礎結構。

![](enterprise-web-deployment-scenario-overview/_static/image1.png)

開發人員工作站、原始檔控制基礎結構、開發人員測試環境和預備環境全都位於 Fabrikam.net 網域內的內部網路。 生產環境位於周邊網路（也稱為 DMZ、非軍事區域和遮蔽式子網路），其與內部網路的防火牆隔離。 這是常見的部署案例：您通常會透過使用防火牆或閘道伺服器，將網際網路對向的 web 伺服器與內部伺服器基礎結構隔離。

在這個範例中：

- 具有個別組建伺服器的 Team Foundation Server （TFS）2010伺服器提供原始檔控制和持續整合（CI）功能。
- 開發人員測試環境包含 Internet Information Services （IIS）7.5 網頁伺服器和 SQL Server 2008 R2 資料庫伺服器。
- 生產環境包含多個 IIS 7.5 網頁伺服器，由 Web 伺服陣列架構（WFF）控制器伺服器同步處理，以及 SQL Server 2008 R2 資料庫伺服器。 在實務上，資料庫伺服器可能會使用叢集或鏡像來改善擴充性和可用性。
- 預備環境的設計目的是要盡可能地複寫生產環境的設定。
- 防火牆和網路隔離原則不允許從內部網路直接進行自動部署至周邊網路。

第二個教學課程：設定[Web 部署的伺服器環境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)中會更詳細地說明每個環境的設定。

### <a name="team-roles-for-alm"></a>ALM 的小組角色

這些使用者牽涉到建立、管理、建立和發佈 Contact Manager 解決方案：

- Matt Hink 是 Fabrikam，Inc. 的 web 應用程式開發人員。他是使用 Visual Studio 2010 開發 Contact Manager 解決方案之小組的一部分。 Matt 具有開發人員測試環境中伺服器的完整系統管理員許可權，可讓他設定環境以符合其需求。 他也具有 Visual Studio 2010 TFS 實例的使用者存取權，其中儲存了 Contact Manager 解決方案的原始程式碼。
- [Walters] 是 Fabrikam，Inc. 開發小組的伺服器系統管理員。 在 TFS 伺服器上具有系統管理存取權，讓他能夠設定 TFS 和 Team Build 的所有層面。 [竊取] 也具有測試和預備 web 伺服器的系統管理存取權，並作為測試和預備環境中資料庫伺服器的資料庫管理員（DBA）。 在 TFS 伺服器上已設定 Team Build 來執行下列工作：

    - 每當使用者將檔案簽入至 TFS 時，在應用程式上建立並執行單元測試。 這稱為 CI。
    - 一旦應用程式通過單元測試，就會自動將 Contact Manager 應用程式部署至測試環境。 這包括在初始部署時，將資料庫發行到測試伺服器，以及在初始部署後對資料庫進行任何更新。
    - 將 Contact Manager 應用程式部署至預備環境，並以單一步驟的方式處理。
    - 建立 web 伺服器管理員和 DBA 可用來將應用程式發行至生產環境的網頁封裝。
- Lisa Andrews 是負責將應用程式部署到 Fabrikam，Inc. 生產伺服器的伺服器系統管理員。 她在建立 Contact Manager 應用程式之後，擁有 TFS Team Build 儲存 web 部署套件之共用的讀取權限。 她也具有生產 web 伺服器的系統管理存取權，讓她可以將應用程式部署到生產環境。 此外，她擔任 DBA，將資料庫和資料庫更新部署到生產環境中的資料庫伺服器。

<a id="_The_Contact_Manager"></a>

### <a name="the-contact-manager-solution"></a>連絡管理員解決方案

Contact Manager 解決方案的設計目的是讓已註冊的登入使用者透過 web 介面新增和編輯連絡人資訊。 Contact Manager 解決方案包含四個個別的專案：

![](enterprise-web-deployment-scenario-overview/_static/image2.png)

- **ContactManager。** 這是 ASP.NET MVC3 web 應用程式專案，代表解決方案的進入點。 它提供一些基本的 web 應用程式功能，例如提供使用者建立和查看連絡人詳細資料的能力。 應用程式會依賴 Windows Communication Foundation （WCF）服務來管理連絡人和 ASP.NET 應用程式服務資料庫，以管理驗證和授權。
- **ContactManager. 資料庫**。 這是 Visual Studio 2010 資料庫專案。 專案會定義儲存連絡人詳細資料之資料庫的架構。
- **ContactManager. 服務**。 這是 WCF web 服務專案。 WCF 會公開一個端點，讓呼叫者能夠在 Contact Manager 資料庫上執行建立、取得、更新和刪除（CRUD）作業。 此服務依賴 Contact Manager 資料庫和 ContactManager. Common .dll 元件。
- **ContactManager。** 這是類別庫專案。 WCF 服務依賴此元件中定義的類型。

本系列的第一個教學課程（[企業中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)）提供了解決方案及其部署需求的完整審查。

<a id="_Deployment_Tasks"></a>

## <a name="deployment-tasks"></a>部署工作

將應用程式部署到大型組織中的不同環境時，涉及數個不同的工作。 這些是教學課程涵蓋的重要工作：

![](enterprise-web-deployment-scenario-overview/_static/image3.png)

以下是此檔中稍早所述使用者觀點的部署程式中的每個步驟清單：

1. 小組的所有成員都會複習 Visual Studio 2010 中的 Contact Manager 解決方案，以判斷重要的部署需求和問題。
2. Matt Hink 可將 Contact Manager 解決方案直接從開發人員工作站部署到開發人員測試環境，以進行部署邏輯的初始測試。
3. Matt Hink 會將應用程式加入至 TFS 中的原始檔控制。
4. [Walters] 會在 Team Build 中為 Contact Manager 方案建立各種組建定義。 一個組建定義會使用 CI，在使用者每次簽入新的程式碼時，將解決方案部署至開發人員測試環境。 另一個組建定義可讓使用者視需要觸發對預備環境的部署。
5. 每次使用者簽入新的程式碼時，Team Build 會自動建立方案元件、執行單元測試，並在組建成功且單元測試通過時，將方案部署至開發人員測試環境。
6. 當使用者觸發對預備環境的部署時，解決方案會在單一步驟的程式中進行封裝和部署。 此程式也會產生用於手動部署到生產環境的封裝。
7. Lisa Andrews 會將應用程式部署到生產環境，方法是手動匯入在步驟6中建立的 web 封裝。

### <a name="key-deployment-issues"></a>金鑰部署問題

Contact Manager 解決方案和 Fabrikam，Inc. 案例強調了當您部署複雜的企業規模解決方案時，可能會遇到的各種常見問題和挑戰。 例如:

- 您必須能夠將專案部署到多個環境，例如開發人員或測試環境、預備平臺，以及實際執行伺服器。 您必須使用每個環境的不同設定來部署解決方案。
- 您需要同時部署多個相依專案，以做為單一步驟或自動化組建和部署程式的一部分。
- 您必須能夠從自動化程式中推動部署。 例如，您想要在簽入新的程式碼時，使用 CI 進程將 web 應用程式部署至預備環境。
- 您必須能夠控制部署程式，並從外部 Visual Studio 設定部署變數，因為開發人員不太可能具有每個目標環境的正確設定或必要認證。
- 您需要部署以架構為基礎的資料庫專案，並在後續的部署中保留現有的資料。
- 您需要在不部署使用者帳戶資料的情況下，以特定方式部署成員資格資料庫。 您可能也需要更新已部署的成員資格資料庫的架構，而不會遺失現有的使用者帳戶資料。
- 當您將內容部署至各種目標環境時，您需要排除特定的檔案或資料夾。

此外，在經常更新和累加時管理部署，會擲回一些額外的挑戰。 例如:

- 每次開發人員簽入新程式碼時，就會執行單元測試。 如果程式碼通過單元測試，您只想要部署方案。
- 當您將 web 應用程式部署至預備或生產環境時，您會想要在部署程式期間，將使用者重新導向到 *\_離線的 .htm*檔案。
- 您想要記錄部署活動。 部署程式應該將成功或失敗部署的電子郵件通知傳送給指定的收件者。
- 如果自動化部署失敗，部署程式應重試目前的部署，或改為部署先前的 web 封裝。

> [!div class="step-by-step"]
> [上一頁](deploying-web-applications-in-enterprise-scenarios.md)
> [下一頁](application-lifecycle-management-from-development-to-production.md)
