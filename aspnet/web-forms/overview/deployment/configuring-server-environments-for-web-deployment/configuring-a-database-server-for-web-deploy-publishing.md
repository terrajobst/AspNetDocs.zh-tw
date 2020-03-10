---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
title: 設定資料庫伺服器以進行 Web Deploy 發行 |Microsoft Docs
author: jrjlee
description: 本主題說明如何設定 SQL Server 2008 R2 資料庫伺服器，以支援 web 部署和發佈。 本主題中所述的工作為「共同 ...」
ms.author: riande
ms.date: 05/04/2012
ms.assetid: e7c447f9-eddf-4bbe-9f18-3326d965d093
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
msc.type: authoredcontent
ms.openlocfilehash: ade3c1ba1c470092f512436f39b8831458408c2c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634614"
---
# <a name="configuring-a-database-server-for-web-deploy-publishing"></a>設定 Web Deploy 發行的資料庫伺服器

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題說明如何設定 SQL Server 2008 R2 資料庫伺服器，以支援 web 部署和發佈。
> 
> 本主題所述的工作在每個部署案例&#x2014;中都是常見的，無論您的 web 伺服器是否設定為使用 IIS Web 部署工具（Web Deploy）遠端代理程式服務、Web Deploy 處理常式或離線部署，或是您的應用程式是在單一 web 伺服器或伺服器陣列上執行。 根據安全性需求和其他考慮，您部署資料庫的方式可能會改變。 例如，您可以部署包含或不含範例資料的資料庫，而且您可以部署使用者角色對應，或在部署之後手動設定它們。 不過，您設定資料庫伺服器的方式維持不變。

您不需要安裝任何額外的產品或工具，就能設定資料庫伺服器以支援 web 部署。 假設您的資料庫伺服器和您的 web 伺服器在不同的電腦上執行，您只需要：

- 允許 SQL Server 使用 TCP/IP 進行通訊。
- 允許 SQL Server 流量通過任何防火牆。
- 為 web 伺服器電腦帳戶提供 SQL Server 登入。
- 將電腦帳戶登入對應到任何必要的資料庫角色。
- 將執行部署的帳戶授與 SQL Server 登入和資料庫建立者許可權。
- 若要支援重複部署，請將部署帳戶登入對應至**db\_擁有**者資料庫角色。

本主題將說明如何執行上述每個程式。 本主題中的工作和逐步解說假設您是從在 Windows Server 2008 R2 上執行的 SQL Server 2008 R2 的預設實例開始。 在繼續之前，請確定：

- Windows Server 2008 R2 Service Pack 1 和所有可用的更新都已安裝。
- 伺服器已加入網域。
- 伺服器具有靜態 IP 位址。
- SQL Server 2008 R2 Service Pack 1，並已安裝所有可用的更新。

SQL Server 實例只需要包含**資料庫引擎服務**角色，這會自動包含在任何 SQL Server 安裝中。 不過，為了簡化設定和維護，建議您包含**管理工具-基本**和**管理工具–完整**的伺服器角色。

> [!NOTE]
> 如需將電腦加入網域的詳細資訊，請參閱[將電腦加入網域並登](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)入。 如需設定靜態 IP 位址的詳細資訊，請參閱[設定靜態 Ip 位址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。 如需有關安裝 SQL Server 的詳細資訊，請參閱[安裝 SQL Server 2008 R2](https://technet.microsoft.com/library/bb500395.aspx)。

## <a name="enable-remote-access-to-sql-server"></a>啟用 SQL Server 的遠端存取

SQL Server 使用 TCP/IP 與遠端電腦通訊。 如果您的資料庫伺服器和網頁伺服器位於不同的電腦上，您需要：

- 設定 SQL Server 網路設定，以允許透過 TCP/IP 進行通訊。
- 設定任何硬體或軟體防火牆，以允許 TCP 流量（在某些情況下，使用者資料包協定（UDP）流量）在 SQL Server 實例所使用的埠上。

若要讓 SQL Server 能夠透過 TCP/IP 進行通訊，請使用 SQL Server 組態管理員來變更 SQL Server 實例的網路設定。

**啟用 SQL Server 使用 TCP/IP 進行通訊**

1. 在 [**開始**] 功能表上，依序指向 [**所有程式**]、[ **Microsoft SQL Server 2008 R2**]、[**組態工具**]，然後按一下 [ **SQL Server 組態管理員**]。
2. 在樹狀檢視窗格中，展開 [ **SQL Server 網路**設定]，然後按一下 [ **MSSQLSERVER 的通訊協定**]。

   > [!NOTE]
   > 如果您已安裝 SQL Server 的多個實例，您會看到每個實例的<em>[instance name]</em>專案的<strong>通訊協定</strong>。 您需要依實例逐一設定網路設定。
3. 在詳細資料窗格中，以滑鼠右鍵按一下 [ **tcp/ip** ] 資料列，然後按一下 [**啟用**]。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image1.png)
4. 在 [**警告**] 對話方塊中，按一下 **[確定]** 。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image2.png)
5. 您必須重新開機 MSSQLSERVER 服務，新的網路設定才會生效。 您可以在命令提示字元中、從 [服務] 主控台，或從 [SQL Server Management Studio] 執行此動作。 在此程式中，您將使用 SQL Server Management Studio。
6. 關閉 SQL Server 組態管理員。
7. 在 [**開始**] 功能表上，指向 [**所有程式**]，按一下 [ **Microsoft SQL Server 2008 R2**]，然後按一下 [ **SQL Server Management Studio**]。
8. 在 [**連接到伺服器**] 對話方塊的 [**伺服器名稱**] 方塊中，輸入資料庫伺服器的名稱，然後按一下 **[連接]** 。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image3.png)
9. 在 [**物件總管**] 窗格中，以滑鼠右鍵按一下父伺服器節點（例如， **TESTDB1**），然後按一下 [**重新開機**]。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image4.png)
10. 在 [ **Microsoft SQL Server Management Studio** ] 對話方塊中，按一下 **[是**]。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image5.png)
11. 當服務重新開機時，請關閉 SQL Server Management Studio。

若要允許 SQL Server 流量通過防火牆，您必須先知道 SQL Server 實例所使用的埠。 這將取決於建立和設定 SQL Server 實例的方式：

- SQL Server 的*預設實例*會接聽 TCP 通訊埠1433上的（並回應）要求。
- 的*已命名實例*SQL Server 會在動態指派的 TCP 通訊埠上接聽（並回應）要求。
- 如果 SQL Server Browser 服務已啟用，用戶端就可以在 UDP 埠1434上查詢服務，以找出特定 SQL Server 實例所要使用的 TCP 埠。 不過，基於安全性理由，這種服務通常是停用的。

假設您使用 SQL Server 的預設實例，您需要設定防火牆以允許流量。

| 方向 | 來源埠 | 至埠 | 連接埠類型 |
| --- | --- | --- | --- |
| 輸入 | Any | 1433 | TCP |
| 輸出 | 1433 | Any | TCP |

> [!NOTE]
> 就技術上來說，用戶端電腦會使用介於1024和5000之間的隨機指派 TCP 埠來與 SQL Server 通訊，而且您可以據以限制您的防火牆規則。 如需 SQL Server 埠和防火牆的詳細資訊，請參閱透過[防火牆與 SQL 進行通訊所需的 tcp/ip 埠號碼](https://go.microsoft.com/?linkid=9805125)和[如何：設定伺服器接聽特定 TCP 通訊埠（SQL Server 組態管理員）](https://msdn.microsoft.com/library/ms177440.aspx)。

在大部分的 Windows Server 環境中，您可能必須在資料庫伺服器上設定 Windows 防火牆。 根據預設，除非規則特別禁止，否則 Windows 防火牆會允許所有輸出流量。 若要讓您的網頁伺服器能夠連線到您的資料庫，您必須設定輸入規則，以允許 SQL Server 實例所使用之埠號碼的 TCP 流量。 如果您使用 SQL Server 的預設實例，您可以使用下一個程式來設定此規則。

**若要將 Windows 防火牆設定為允許與預設 SQL Server 實例通訊**

1. 在資料庫伺服器的 [**開始**] 功能表上，指向 [系統**管理工具**]，然後按一下 [**具有 Advanced Security 的 Windows 防火牆**]。
2. 在樹狀檢視窗格中，按一下 [**輸入規則**]。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image6.png)
3. 在 [**動作**] 窗格的 [**輸入規則**] 底下，按一下 [**新增規則**]。
4. 在 [新增輸入規則嚮導] 的 [**規則類型**] 頁面上，選取 [**埠**]，然後按 **[下一步]** 。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image7.png)
5. 在 [**通訊協定和埠**] 頁面上，確定已選取 [ **TCP** ]，然後在 [**特定本機埠**] 方塊中輸入**1433**，然後按 **[下一步]** 。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image8.png)
6. 在 [**動作**] 頁面上，保持選取 **[允許連接**]，然後按 **[下一步]** 。
7. 在 **設定檔** 頁面上，保持選取 **網域**，清除 **私**用 和 **公用** 核取方塊，然後按**下一步**

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image9.png)
8. 在 [**名稱**] 頁面上，為規則提供適當的描述性名稱（例如， **SQL Server 預設實例–網路存取**），然後按一下 **[完成]** 。

如需設定 Windows 防火牆以進行 SQL Server 的詳細資訊，特別是當您需要透過非標準或動態埠與 SQL Server 通訊時，請參閱 how [to： Configure a Windows firewall for 資料庫引擎 Access](https://technet.microsoft.com/library/ms175043.aspx)。

## <a name="configure-logins-and-database-permissions"></a>設定登入和資料庫許可權

當您將 web 應用程式部署至 Internet Information Services （IIS）時，應用程式會使用應用程式集區的身分識別來執行。 在網域環境中，應用程式集區身分識別會使用其執行所在之伺服器的電腦帳戶來存取網路資源。 電腦帳戶的格式為<em>[功能變數名稱]</em><strong>\</strong ><em>[電腦名稱稱]</em> <strong>$</strong> &#x2014;例如， <strong>FABRIKAM\TESTWEB1 $</strong>。 若要允許您的 web 應用程式透過網路存取資料庫，您需要：

- 將 web 伺服器電腦帳戶的登入新增至 SQL Server 實例。
- 將電腦帳戶登入對應到任何必要的資料庫角色（通常是**db\_datareader**和**db\_資料寫入元**）。

如果您的 web 應用程式是在伺服器陣列上執行，而不是單一伺服器，您必須針對伺服器陣列中的每一部 web 伺服器重複這些程式。

> [!NOTE]
> 如需應用程式集區身分識別和存取網路資源的詳細資訊，請參閱[應用程式集](https://go.microsoft.com/?linkid=9805123)區身分識別。

您可以透過各種方式來處理這些工作。 若要建立登入，您可以執行下列其中一項：

- 使用 Transact-sql 或 SQL Server Management Studio，以手動方式在資料庫伺服器上建立登入。
- 使用 Visual Studio 中的 SQL Server 2008 伺服器專案來建立和部署登入。

SQL Server 登入是伺服器層級物件，而不是資料庫層級物件，因此不會相依于您想要部署的資料庫。 因此，您可以在任何時間點建立登入，最簡單的方法通常是在開始部署資料庫之前，手動在資料庫伺服器上建立登入。 您可以使用下一個程式，在 SQL Server Management Studio 中建立登入。

**若要建立 web 伺服器電腦帳戶的 SQL Server 登入**

1. 在資料庫伺服器的 [**開始**] 功能表上，指向 [**所有程式**]，按一下 [ **Microsoft SQL Server 2008 R2**]，然後按一下 [ **SQL Server Management Studio**]。
2. 在 [**連接到伺服器**] 對話方塊的 [**伺服器名稱**] 方塊中，輸入資料庫伺服器的名稱，然後按一下 **[連接]** 。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image10.png)
3. 在 [**物件總管**] 窗格中，以滑鼠右鍵按一下 [**安全性**]，指向 [**新增**]，然後按一下 **[登**入]。
4. 在 [**登入-新增**] 對話方塊的 [**登入名稱**] 方塊中，輸入您的 web 伺服器電腦帳戶名稱（例如， **FABRIKAM\TESTWEB1 $** ）。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image11.png)
5. 按一下 [確定]。

此時，您的資料庫伺服器已準備好進行 Web Deploy 發佈。 不過，在您將電腦帳戶登入對應到所需的資料庫角色之前，您部署的任何解決方案都將無法正常執行。 將登入對應到資料庫角色需要更多的想法，因為您必須等到部署資料庫之後，才能對應角色。 若要將電腦帳戶登入對應到所需的資料庫角色，您可以執行下列其中一項動作：

- 在您第一次部署資料庫之後，手動將資料庫角色指派給登入。
- 使用部署後腳本，將資料庫角色指派給登入。

如需有關自動建立登入和資料庫角色對應的詳細資訊，請參閱[將資料庫角色成員資格部署到測試環境](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。 或者，您可以使用下一個程式，以手動方式將電腦帳戶登入對應到所需的資料庫角色。 請記住 *，在部署資料庫之前，* 您無法執行此程式。

**若要將資料庫角色對應至 web 伺服器電腦帳戶登入**

1. 如先前一樣開啟 SQL Server Management Studio。
2. 在 [**物件總管**] 窗格中，依序展開 [**安全性**] 節點和 [登入 **] 節點，** 然後連按兩下電腦帳戶（例如**FABRIKAM\TESTWEB1 $** ）。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image12.png)
3. 在 [**登入屬性**] 對話方塊中，按一下 [**使用者對應**]。
4. 在 [**對應至此登**入的使用者] 資料表中，選取您的資料庫名稱（例如， **ContactManager**）。
5. 在 [**資料庫角色成員資格：** *[資料庫名稱]]* 清單中，選取所需的許可權。 在 Contact Manager 範例解決方案的情況下，您必須選取**db\_datareader**和**db\_資料寫入元**角色。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image13.png)
6. 按一下 [確定]。

雖然手動對應資料庫角色通常會比測試環境所需的還多，但對臨時或生產環境的自動化或單鍵部署較不理想。 您可以使用[部署資料庫角色成員資格](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)中的部署後腳本，在測試環境中找到自動化這種工作的詳細資訊。

> [!NOTE]
> 如需伺服器專案和資料庫專案的詳細資訊，請參閱[Visual Studio 2010 SQL Server 資料庫專案](https://msdn.microsoft.com/library/ff678491.aspx)。

## <a name="configure-permissions-for-the-deployment-account"></a>設定部署帳戶的許可權

如果您用來執行部署的帳戶不是 SQL Server 系統管理員，您也必須為此帳戶建立登入。 若要建立資料庫，帳戶必須是**dbcreator**伺服器角色的成員，或具有對等的許可權。

> [!NOTE]
> 當您使用 Web Deploy 或 VSDBCMD 部署資料庫時，可以使用 Windows 認證或 SQL Server 認證（如果您的 SQL Server 實例設定為支援混合模式驗證）。 下一個程式假設您想要使用 Windows 認證，但當您設定部署時，並不會阻止您在連接字串中指定 SQL Server 的使用者名稱和密碼。

**設定部署帳戶的許可權**

1. 如先前一樣開啟 SQL Server Management Studio。
2. 在 [**物件總管**] 窗格中，以滑鼠右鍵按一下 [**安全性**]，指向 [**新增**]，然後按一下 **[登**入]。
3. 在 [**登入-新增**] 對話方塊的 [**登入名稱**] 方塊中，輸入部署帳戶的名稱（例如， **FABRIKAM\matt**）。
4. 在 [**選取頁面**] 窗格中，按一下 [**伺服器角色**]。
5. 選取 [ **Dbcreator**]，然後按一下 **[確定]** 。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image14.png)

若要支援後續部署，您也必須在第一次部署之後，將部署帳戶新增至資料庫上的**db\_擁有**者角色。 這是因為在後續的部署中，您要修改現有資料庫的架構，而不是建立新的資料庫。 如上一節所述，在您建立資料庫之前，您無法將使用者加入至資料庫角色，原因很明顯。

**將部署帳戶登入對應至 db\_擁有者資料庫角色**

1. 如先前一樣開啟 SQL Server Management Studio。
2. 在 [**物件總管**] 視窗中，依序展開 [**安全性**] 節點和 [登入 **] 節點，** 然後連按兩下電腦帳戶（例如， **FABRIKAM\matt**）。
3. 在 [**登入屬性**] 對話方塊中，按一下 [**使用者對應**]。
4. 在 [**對應至此登**入的使用者] 資料表中，選取您的資料庫名稱（例如， **ContactManager**）。
5. 在 [**資料庫角色成員資格：** *[資料庫名稱]]* 清單中，選取 [ **db\_擁有**者] 角色。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image15.png)
6. 按一下 [確定]。

## <a name="conclusion"></a>結論

您的資料庫伺服器現在應該已準備好接受遠端資料庫部署，並允許遠端 IIS 網頁伺服器存取您的資料庫。 在您嘗試部署和使用資料庫之前，您可能會想要檢查下列重點：

- 您是否已設定 SQL Server 接受遠端 TCP/IP 連接？
- 您是否已設定任何防火牆以允許 SQL Server 流量？
- 您是否已針對將存取 SQL Server 的每一部 web 伺服器建立電腦帳戶登入？
- 您的資料庫部署是否包含用來建立使用者角色對應的腳本，或者您是否需要在第一次部署資料庫之後手動建立這些專案？
- 您是否已建立部署帳戶的登入，並將它新增至**dbcreator**伺服器角色？

## <a name="further-reading"></a>進一步閱讀

如需部署資料庫專案的指引，請參閱[部署資料庫專案](../web-deployment-in-the-enterprise/deploying-database-projects.md)。 如需執行部署後腳本來建立資料庫角色成員資格的指引，請參閱[將資料庫角色成員資格部署到測試環境](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。 如需如何滿足成員資格資料庫所造成之獨特部署挑戰的指引，請參閱將[成員資格資料庫部署到企業環境](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)。

> [!div class="step-by-step"]
> [上一頁](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
> [下一頁](creating-a-server-farm-with-the-web-farm-framework.md)
