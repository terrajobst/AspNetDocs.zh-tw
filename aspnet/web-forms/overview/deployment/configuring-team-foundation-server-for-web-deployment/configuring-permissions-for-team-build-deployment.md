---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: 正在設定 Team Build 部署的許可權 |Microsoft Docs
author: jrjlee
description: 本主題描述如何設定許可權，讓您的組建伺服器將內容部署到 web 伺服器和資料庫伺服器，做為自動化 b 的一部分 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: 5699f72af6b8d7f18d1a2c631dfdedd63c66e1e6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638422"
---
# <a name="configuring-permissions-for-team-build-deployment"></a>設定小組組建部署的權限

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何設定許可權，讓您的組建伺服器將內容部署到 web 伺服器和資料庫伺服器，做為自動化組建程式的一部分。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="task-overview"></a>工作總覽

當您安裝 Team Foundation Server （TFS）2010組建服務時，請指定您要用來執行服務的身分識別。 根據預設，這是網路服務帳戶。 或者，您可以將組建服務設定為使用網域帳戶來執行。

任何需要 Windows 驗證，而且您打算使用 Team Build 自動化的部署工作，都將使用組建服務身分識別來執行。 因此，您必須將 web 伺服器和資料庫伺服器上的任何必要許可權授與組建服務識別。

> [!NOTE]
> Network Service 帳戶會使用電腦帳戶向其他電腦進行驗證。 電腦帳戶的格式為 * [功能變數名稱]\[電腦名稱稱] * **$** &#x2014;例如**FABRIKAM\TFSBUILD $** 。 因此，如果您的組建服務使用網路服務識別執行，您應該將任何必要的許可權授與給組建伺服器的電腦帳戶識別。

## <a name="configuring-web-server-permissions"></a>設定 Web 服務器許可權

如[選擇正確的 Web 部署方法](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)中所述，如果您想要將 Web 套件部署到遠端 web 伺服器，您可以使用兩種主要方法：

- 將目標設為目的地伺服器上的*Web Deployment Agent 服務*（也稱為遠端代理程式），以從遠端位置部署應用程式。
- 以目的地伺服器上的*Internet Information Services* （*IIS） Web Deploy 處理*程式為目標，從遠端位置部署應用程式。

在此情況下，遠端代理程式有兩個主要限制：

- 遠端代理程式僅支援 NTLM 驗證。 換句話說，部署必須使用組建服務身分識別&#x2014;您無法模擬另一個帳戶。
- 若要使用遠端代理程式，執行部署的帳戶必須是目標伺服器上的系統管理員。

總之，這兩項限制讓遠端代理程式不需要自動化 Team Build 部署的方法。 若要使用此方法，您必須將組建服務帳戶設為任何目標 web 伺服器上的系統管理員。

相反地，Web Deploy 處理常式方法會提供各種優點：

- Web Deploy 處理常式支援透過 HTTPS 進行基本驗證，可讓您將替代帳戶的認證傳遞給 IIS Web 部署工具（Web Deploy）。
- 您可以設定目標 web 伺服器，讓非系統管理員使用者使用 Web Deploy 處理常式將內容部署到特定的 IIS 網站。

如此一來，當您從 Team Build 將 Web 套件部署自動化時，最好將目標設為 Web Deploy 處理常式。 這是建議的程式：

1. 建立要用於部署的低許可權網域帳戶。
2. 設定 Web Deploy 處理常式，並授與帳戶將內容部署到特定 IIS 網站的必要許可權，如設定[Web Deploy 發佈的 Web 服務器（Web Deploy 處理常式）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)中所述。
3. 使用基本驗證並提供您建立的網域帳號憑證來執行部署，以叫用 Web Deploy 並以 Web Deploy 處理常式為目標。

在[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)範例解決方案中，您可以在環境特定的專案檔中指定驗證類型（[基本] 或 [NTLM]）、[Web Deploy 認證] 和 [端點位址] （[遠端代理程式] 或 [Web Deploy 處理常式]）。 當執行專案檔時，會使用這些值來制訂和執行 Web Deploy 命令。 如需詳細資訊，請參閱[部署 Web 封裝](../web-deployment-in-the-enterprise/deploying-web-packages.md)。

如需設定 Web Deploy 處理常式的詳細資訊，包括如何設定許可權，請參閱設定[用於 Web Deploy 發佈的 Web 服務器（Web Deploy 處理常式）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。 如需有關設定遠端代理程式的詳細資訊，請參閱設定[用於 Web Deploy 發佈的 Web 服務器（遠端代理程式）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。

## <a name="configuring-database-server-permissions"></a>正在設定資料庫伺服器許可權

若要將資料庫部署到 SQL Server，您必須：

- 在 SQL Server 實例上建立部署帳戶的登入。
- 授與 SQL Server 實例的登入**DBCreator**許可權。
- 在初始部署之後，將登入新增至目標資料庫上的**db\_擁有**者角色。 這是必要的，因為在後續的部署中，您要修改現有的資料庫，而不是建立新的資料庫。

您可以使用 NTLM 驗證或 SQL Server authentication，向 SQL Server 實例進行驗證：

- 如果您使用 NTLM 驗證，則需要將上述許可權授與組建服務帳戶。
- 如果您使用 SQL Server 驗證，則需要將上述許可權授與 SQL Server 帳戶。 您也必須在用來部署資料庫的連接字串中包含 SQL Server 的使用者名稱和密碼。

如需如何設定資料庫部署之許可權的逐步詳細資料，請參閱設定用於[Web Deploy 發行的資料庫伺服器](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)。

## <a name="conclusion"></a>結論

此時，當您從 Team Build 將 web 應用程式和資料庫部署自動化時，您應該瞭解所需的許可權，以及為您開啟的驗證選項。 您也應該能夠在 IIS 網頁伺服器和 SQL Server 資料庫伺服器上執行必要的許可權。

## <a name="further-reading"></a>進一步閱讀

如需有關設定 Windows server 環境以支援遠端部署的詳細資訊，請參閱設定[Web 部署的伺服器環境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。

> [!div class="step-by-step"]
> [上一篇](deploying-a-specific-build.md)
