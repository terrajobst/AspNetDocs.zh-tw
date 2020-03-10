---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
title: 設定用於 Web Deploy 發行的 Web 服務器（Web Deploy 處理常式） |Microsoft Docs
author: jrjlee
description: 本主題描述如何設定 Internet Information Services （IIS）網頁伺服器，以支援使用 IIS Web Deploy 漢字的 web 發行和部署 。
ms.author: riande
ms.date: 01/29/2017
ms.assetid: 90ebf911-1c46-4470-b876-1335bd0f590f
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
msc.type: authoredcontent
ms.openlocfilehash: baaebd32f08d3c6b861572c5c5a16ec0fb70aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78568562"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler"></a>設定 Web Deploy 發行的網頁伺服器 (Web Deploy 處理常式)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何使用 IIS Web Deploy 處理常式，設定 Internet Information Services （IIS）網頁伺服器，以支援 web 發行和部署。
> 
> 當您使用 Web Deploy 2.0 或更新版本時，有三種主要方法可用來將您的應用程式或網站放在 Web 服務器上。 您可以：
> 
> - 使用*Web Deploy 的遠端代理程式服務*。 這種方法需要較少的 web 伺服器設定，但您必須提供本機伺服器系統管理員的認證，才能將任何專案部署至伺服器。
> - 使用*Web Deploy 處理常式*。 這種方法比較複雜，而且需要更多的初始工作來設定 web 伺服器。 不過，當您使用這種方法時，可以設定 IIS 以允許非系統管理員使用者執行部署。 Web Deploy 處理常式僅適用于 IIS 7 版或更新版本。
> - 使用*離線部署*。 此方法需要最少的 web 伺服器設定，但伺服器管理員必須手動將 web 套件複製到伺服器，並透過 IIS 管理員將其匯入。
> 
> 如需這些方法的主要功能、優點和缺點的詳細資訊，請參閱[選擇正確的 Web 部署方法](choosing-the-right-approach-to-web-deployment.md)。

是，如果您想要允許非系統管理員的使用者將內容部署到特定的 IIS 網站。 這種方法通常適用于下列類型的案例：

- 臨時或生產環境，其中觸發遠端部署的人員或服務帳戶不太可能能夠存取伺服器管理員的認證。
- 裝載的環境，您想要讓遠端使用者能夠更新其網站，而不需讓他們完全控制您的 web 伺服器（或存取其他人的網站）。

在開發或測試案例中，或小型組織中，使用伺服器管理員認證來部署內容通常較不爭議。 在這些情況下，使用[Web Deploy 遠端代理程式服務](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)來設定您的 web 伺服器以支援部署，會提供更直接的方法。

## <a name="task-overview"></a>工作總覽

若要使用 Web Deploy 處理常式方法，將 web 伺服器設定為接受及部署遠端電腦上的網頁封裝，您必須：

- 建立或選擇要用來執行部署之認證的網域使用者帳戶（「非系統管理員使用者」）。
- 安裝 IIS 7.5，包括 Web 管理服務和基本驗證模組。
- 安裝 Web Deploy 2.1 或更新版本。
- 設定 Web 管理服務以允許遠端連線，並啟動服務。
- 建立 IIS 網站來裝載已部署的內容。
- 在 IIS 管理員中，為您的網站授與非系統管理員的使用者許可權。
- 請確定 Web 管理服務委派規則允許服務使用您的非系統管理員使用者帳戶新增和變更網站內容。
- 設定任何防火牆以允許埠8172上的連入連線。

若要特別裝載 ContactManager 範例解決方案，您也需要：

- 安裝 .NET Framework 4.0。
- 安裝 ASP.NET MVC 3。

本主題將說明如何執行上述每個程式。 本主題中的工作和逐步解說假設您是從執行 Windows Server 2016 的全新伺服器組建開始。 在繼續之前，請確定：

- Windows Server 2016
- 伺服器已加入網域。
- 伺服器具有靜態 IP 位址。

> [!NOTE]
> 如需將電腦加入網域的詳細資訊，請參閱[將電腦加入網域並登](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)入。 如需設定靜態 IP 位址的詳細資訊，請參閱[設定靜態 Ip 位址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。

## <a name="install-products-and-components"></a>安裝產品和元件

本節將引導您在 web 伺服器上安裝必要的產品和元件。 在開始之前，最好先執行 Windows Update，以確保您的伺服器完全保持在最新狀態。

在此情況下，您需要安裝下列專案：

- **IIS 7 建議**的設定。 這會啟用 web 伺服器上的**網頁伺服器（iis）** 角色，並安裝您需要的一組 IIS 模組和元件，才能裝載 ASP.NET 應用程式。
- **IIS：管理服務**。 這會在 IIS 中安裝 Web 管理服務（WMSvc）。 這項服務可讓您遠端系統管理 IIS 網站，並將 Web Deploy 處理常式端點公開給用戶端。
- **IIS：基本驗證**。 這會安裝 IIS 基本驗證模組。 這可讓 Web 管理服務（WMSvc）驗證您所提供的認證。
- **Web Deployment Tool 2.1 或更新版本**。 這會在您的伺服器上安裝 Web Deploy （及其基礎可執行檔，Msdeploy.exe）。 在此過程中，它會安裝 Web Deploy 處理常式，並將它與 Web 管理服務整合。
- **.NET Framework 4.0**。 這是執行此版本 .NET Framework 所建立之應用程式的必要項。
- **ASP.NET MVC 3**。 這會安裝執行 MVC 3 應用程式所需的元件。

> [!NOTE]
> 本逐步解說說明如何使用 Web Platform Installer 來安裝和設定各種元件。 雖然您不需要使用 Web Platform Installer，但它會自動偵測相依性，並確保您一律取得最新的產品版本，藉此簡化安裝程式。 如需詳細資訊，請參閱[Microsoft Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。

**若要安裝必要的產品和元件**

1. 下載並安裝[Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。
2. 安裝完成時，Web Platform Installer 會自動啟動。

    > [!NOTE]
    > 您現在可以隨時從 [**開始**] 功能表啟動 Web Platform Installer。 若要這樣做，請在 [**開始**] 功能表上，按一下 [**所有程式**]，然後按一下 [ **Microsoft Web Platform Installer**]。
3. 在 [Web Platform Installer] 視窗的頂端，按一下 [產品]。
4. 在視窗左側的流覽窗格中 **，按一下 [** 架構]。
5. 在 [ **Microsoft .NET Framework 4** ] 資料列中，如果尚未安裝 .NET Framework，請按一下 [**新增**]。

    > [!NOTE]
    > 您可能已經透過 Windows Update 安裝了 .NET Framework 4.0。 如果已安裝產品或元件，Web Platform Installer 會以**已安裝**的文字取代 [**新增**] 按鈕來指出這一點。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image1.png)
6. 在 [ **ASP.NET MVC 3 （Visual Studio 2010）** ] 資料列中，按一下 [**新增**]。
7. 在流覽窗格中，按一下 [**伺服器**]。
8. 在 [ **IIS 7 建議**的設定] 列中，按一下 [**新增**]。
9. 在 [ **Web Deployment Tool 2.1** ] 資料列中，按一下 [**新增**]。
10. 在 [ **IIS：基本驗證**] 資料列中，按一下 [**新增**]。
11. 在 [ **IIS：管理服務**] 資料列中，按一下 [**新增**]。
12. 按一下 [安裝]。 Web Platform Installer 將會顯示一份產品&#x2014;清單，其中包含&#x2014;要安裝的相關聯相依性，並會提示您接受授權條款。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image2.png)
13. 請參閱授權條款，如果您同意這些條款，請按一下 [**我接受**]。
14. 當安裝完成時，按一下 **[完成**]，然後關閉 [ **Web Platform Installer** ] 視窗。

如果您在安裝 IIS 之前安裝了 .NET Framework 4.0，就必須執行[ASP.NET IIS 註冊工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx)（aspnet\_regiis），以向 IIS 註冊最新版本的 ASP.NET。 如果您不這麼做，就會發現 IIS 會提供靜態內容（例如 HTML 檔案），而不會有任何問題，但會傳回**HTTP 錯誤404.0 –** 當您嘗試流覽至 ASP.NET 內容時找不到。 您可以使用下一個程式來確保 ASP.NET 4.0 已註冊。

**向 IIS 註冊 ASP.NET 4。0**

1. 按一下 [**開始**]，然後輸入**命令提示**字元。
2. 在搜尋結果中，以滑鼠右鍵按一下 [**命令提示**字元]，然後按一下 [以**系統管理員身分執行**]。
3. 在 [命令提示字元] 視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319**目錄。
4. 輸入此命令，然後按 Enter 鍵：

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample1.cmd)]
5. 如果您打算在任何時間點裝載64位的 web 應用程式，您也應該向 IIS 註冊64位版本的 ASP.NET。 若要這麼做，請在 [命令提示字元] 視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319**目錄。
6. 輸入此命令，然後按 Enter 鍵：

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample2.cmd)]

建議的作法是，在此時再次使用 Windows Update，下載並安裝您已安裝之新產品和元件的任何可用更新。

## <a name="configure-the-web-management-service"></a>設定 Web 管理服務

既然您已安裝所需的所有專案，下一步就是在 IIS 中設定 Web 管理服務。 概括而言，您必須完成下列工作：

- 啟用伺服器層級的基本驗證。
- 設定 Web 管理服務以接受遠端連線。
- 啟動 Web 管理服務。
- 檢查必要的 Web 管理服務委派規則是否已就緒。

**若要設定 Web 管理服務**

1. 在 [**開始**] 功能表上，指向 [系統**管理工具**]，然後按一下 [ **Internet Information Services （IIS）管理員**]。
2. 在 **[IIS**管理員] 的 [連線] 窗格中，按一下伺服器節點（例如， **STAGEWEB1**）。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image3.png)
3. 在中央窗格的 [ **IIS**] 底下，按兩下 [**驗證**]。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image20.png)
4. 以滑鼠右鍵按一下 [**基本驗證**]，然後按一下 [**啟用**]。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image5.png)
5. **在 [連線] 窗格**中，再次按一下伺服器節點以返回最上層設定。
6. 在中央窗格的 [**管理**] 底下，按兩下 [**管理服務**]。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image6.png)
7. 在中央窗格中，選取 [**啟用遠端連線**]。

    > [!NOTE]
    > 如果 Web 管理服務已在執行中，您必須先將它停止。
8. 在 [**動作**] 窗格中，按一下 [**啟動**] 以啟動 Web 管理服務。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image7.png)
9. 如果系統提示您儲存設定，請按一下 **[是]** 。

    > [!NOTE]
    > 您可能也會想要將服務設定為自動啟動。 若要這麼做，請開啟 [服務] 主控台，以滑鼠右鍵按一下 [ **Web 管理服務**]，然後按一下 [**屬性**]。 在 [**啟動類型**] 下拉式清單中，選取 [**自動**]，然後按一下 **[確定]** 。
10. **在 [連線] 窗格**中，再次按一下伺服器節點以返回最上層設定。
11. 在中央窗格的 [**管理**] 底下，按兩下 [**管理服務委派**]。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image8.png)
12. 確認中央窗格包含一組規則。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image9.png)

    這些規則可讓授權的 Web 管理服務使用者使用各種 Web Deploy 提供者。 例如，若要透過 Web Deploy 處理常式將 web 應用程式和內容部署至 IIS，則必須有委派規則，允許所有已驗證的 Web 管理服務使用者使用**contentPath**和**iisApp**提供者（您可以在螢幕擷取畫面中看到的最後一個規則）。

    如果您已依照本主題所述的順序安裝產品和元件，最新版本的 Web Deploy 應該會自動將所有必要的委派規則新增至 Web 管理服務。 如果 [管理服務委派] 頁面未顯示任何規則，您就必須自行建立。 如需如何執行此操作的指示，請參閱[設定 Web 部署處理常式](https://go.microsoft.com/?linkid=9805124)。
13. **在 [連線] 窗格**中，再次按一下伺服器節點以返回最上層設定。

## <a name="create-and-configure-an-iis-website"></a>建立和設定 IIS 網站

您必須先建立並設定 IIS 網站來裝載內容，才能將 web 內容部署到您的伺服器。 Web Deploy 只能將 web 套件部署到現有的 IIS 網站;它無法為您建立網站。 您也需要執行一些額外的設定，以允許您的非系統管理員帳戶從遠端部署內容。 概括而言，您必須完成下列工作：

- 在檔案系統上建立資料夾，以裝載您的內容。
- 建立 IIS 網站來提供內容，並將它與本機資料夾產生關聯。
- 授與讀取權限給本機資料夾上的應用程式集區身分識別。
- 將部署 web 應用程式所需的 IIS 許可權授與網域帳戶。

雖然沒有任何動作會阻止您將內容部署到 IIS 中的預設網站，但不建議針對測試或示範案例以外的任何專案使用此方法。 若要模擬生產環境，您應該使用特定于應用程式需求的設定來建立新的 IIS 網站。

**若要建立 IIS 網站**

1. 在本機檔案系統上，建立用來儲存內容的資料夾（例如， **C:\DemoSite**）。
2. 在 [**開始**] 功能表上，指向 [系統**管理工具**]，然後按一下 [ **Internet Information Services （IIS）管理員**]。
3. 在 **[IIS**管理員] 的 [連線] 窗格中，展開伺服器節點（例如， **STAGEWEB1**）。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image10.png)
4. 以滑鼠右鍵按一下 [**網站**] 節點，然後按一下 [**新增**網站]。
5. 在 [**網站名稱**] 方塊中，輸入 IIS 網站的名稱（例如， **DemoSite**）。
6. 在 [**實體路徑**] 方塊中，輸入（或流覽至）本機資料夾的路徑（例如， **C:\DemoSite**）。
7. 在 [**埠**] 方塊中，輸入您要用來裝載網站的埠號碼（例如， **85**）。

    > [!NOTE]
    > 適用于 HTTP 的標準埠號碼為80，HTTPS 則為443。 不過，如果您在埠80上裝載此網站，則必須先停止預設網站，才能存取您的網站。
8. 除非您要設定網站的網域名稱系統（DNS）記錄，否則請將 [**主機名稱**] 方塊保留空白，然後按一下 **[確定]** 。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image11.png)

    > [!NOTE]
    > 在生產環境中，您可能會想要在埠80上裝載您的網站，並設定主機標頭和相符的 DNS 記錄。 如需在 IIS 7 中設定主機標頭的詳細資訊，請參閱[設定網站的主機標頭（iis 7）](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。 如需 Windows Server 中 DNS 伺服器角色的詳細資訊，請參閱[Dns 伺服器總覽](https://technet.microsoft.com/library/cc770392.aspx)和[dns 伺服器](https://technet.microsoft.com/windowsserver/dd448607)。
9. 在 [ **動作** ] 窗格的 [ **編輯站台**] 下方，按一下 [ **繫結**]。
10. 在 [站台繫結] 對話方塊中，按一下 [新增]。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image12.png)
11. 在 [**新增網站**系結] 對話方塊中，將 [ **IP 位址**] 和 [**埠**] 設定為符合您現有的網站設定。
12. 在 [**主機名稱**] 方塊中，輸入您的 web 伺服器名稱（例如， **STAGEWEB1**），然後按一下 **[確定]** 。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image13.png)

    > [!NOTE]
    > 第一個網站系結可讓您使用 IP 位址和埠或 `http://localhost:85`，在本機存取網站。 第二個網站系結可讓您使用電腦名稱稱（例如 http://stageweb1:85)，從網域中的其他電腦存取網站。
13. 在 [站台繫結] 對話方塊中，按一下 [關閉]。
14. **在 [連線**] 窗格中，按一下 [**應用程式**集區]。
15. 在 [**應用程式**集區] 窗格中，以滑鼠右鍵按一下應用程式集區的名稱，然後按一下 [**基本設定**]。 根據預設，您的應用程式集區名稱會與您的網站名稱相符（例如， **DemoSite**）。
16. 在 [ **.NET clr 版本**] 清單中，選取 [ **.net Clr v 4.0.30319**]，然後按一下 **[確定]** 。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image21.png)

    > [!NOTE]
    > 範例解決方案需要 .NET Framework 4.0。 這不是一般 Web Deploy 的需求。

為了讓您的網站提供內容，應用程式集區識別必須具有儲存內容之本機資料夾的讀取權限。 在 IIS 7.5 中，應用程式集區預設會以唯一的應用程式集區身分識別執行（相較于舊版的 IIS，應用程式集區通常會使用網路服務帳戶來執行）。 應用程式集區身分識別不是真正的使用者帳戶，也不會顯示在任何使用者或群組&#x2014;清單上，而是在啟動應用程式集區時動態建立的。 每個應用程式集區識別都會新增至本機**IIS\_給 iis-iusrs**安全性群組做為隱藏專案。

若要將許可權授與檔案或資料夾上的應用程式集區身分識別，您有兩個選項：

- 使用 <strong>IIS AppPool\</strong ><em>[應用程式集區名稱]</em>（例如<strong>iis AppPool\DemoSite</strong>）的格式，直接將許可權指派給應用程式集區身分識別。
- 指派許可權給**IIS\_給 iis-iusrs**群組。

最常見的方法是將許可權指派給本機**IIS\_給 iis-iusrs**群組，因為這種方法可讓您變更應用程式集區，而不需要重新設定檔案系統許可權。 下一個程式會使用這個以群組為基礎的方法。

> [!NOTE]
> 如需 IIS 7.5 中應用程式集區身分識別的詳細資訊，請參閱[應用程式集](https://go.microsoft.com/?linkid=9805123)區身分識別。

**設定 IIS 網站的資料夾許可權**

1. 在 Windows Explorer 中，流覽至本機資料夾的位置。
2. 以滑鼠右鍵按一下該資料夾，然後按一下 [**屬性**]。
3. 在 [**Security**] 索引標籤上按一下 [**Edit**]，然後按一下 [**Add**]。
4. 按一下 [位置]。 在 [**位置**] 對話方塊中，選取本機伺服器，然後按一下 **[確定]** 。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image15.png)
5. 在 [**選取使用者或群組**] 對話方塊中，輸入**IIS\_給 iis-iusrs**，按一下 [**檢查名稱**]，然後按一下 **[確定]** 。
6. 在<em>[資料夾名稱] 的 [</em> <strong>許可權</strong>] 對話方塊中，請注意，預設會將 [<strong>讀取 &amp; 執行</strong>]、[<strong>列出資料夾內容</strong>] 和 [<strong>讀取</strong>] 許可權指派給新的群組。 保持不變，然後按一下<strong>[確定]</strong>。
7. 按一下 [<strong>確定</strong>] 以關閉<em>[資料夾名稱]</em><strong>屬性</strong>對話方塊。

作為最後一項工作，您必須將適當的許可權授與您將用來部署內容之認證的非系統管理員使用者。 此使用者需要許可權，才能從遠端將內容部署至您的網站。

**為非系統管理員的網域使用者設定 IIS 網站許可權**

1. 在 [IIS 管理員] 的 [連線] 窗格中，以滑鼠右鍵按一下**您的網站**節點（例如， **DemoSite**），指向 [**部署**]，然後按一下 [**設定 Web Deploy 發佈**]。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image16.png)
2. 在 [**設定 Web Deploy 發佈**] 對話方塊中，按一下 [**選取要授與發行許可權的使用者**] 清單右邊的省略號按鈕。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image17.png)
3. 在 [**允許使用者**] 對話方塊中，輸入您要用來部署內容之帳戶的網域和使用者名稱，然後按一下 **[確定]** 。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image18.png)
4. 在 [**設定 Web Deploy 發佈**] 對話方塊中，按一下 [**設定**]。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image19.png)

    > [!NOTE]
    > 這項作業會在一個步驟中執行兩個主要功能。 首先，它會授與使用者許可權，以便根據您在上一節中檢查的委派規則，透過 Web 管理服務從遠端修改網站。 第二，它會授與使用者對網站之源資料夾的完整控制權，讓使用者能夠新增、修改及設定網站內容的許可權。
5. 在 [**設定 Web Deploy 發佈**] 對話方塊中，按一下 [**關閉**]。

## <a name="configure-firewall-exceptions"></a>設定防火牆例外狀況

根據預設，IIS Web 管理服務會接聽 TCP 通訊埠8172。 如果您的網頁伺服器上已啟用 Windows 防火牆，您將需要建立新的輸入規則，以允許埠8172上的 TCP 流量（Windows 防火牆預設允許所有輸出流量）。 如果您使用協力廠商防火牆，您必須建立規則以允許流量。

| 方向 | 來源埠 | 至埠 | 連接埠類型 |
| --- | --- | --- | --- |
| 輸入 | Any | 8172 | TCP |
| 輸出 | 8172 | Any | TCP |

如需在 Windows 防火牆中設定規則的詳細資訊，請參閱設定[防火牆規則](https://technet.microsoft.com/library/dd448559(WS.10).aspx)。 如需協力廠商防火牆，請參閱您的產品檔。

## <a name="conclusion"></a>結論

您的 web 伺服器現在應該已準備好接受透過 Web 管理服務對 Web Deploy 處理常式進行遠端部署。 嘗試將 web 應用程式部署到伺服器之前，您可能會想要檢查下列重點：

- 您是否已在 IIS 的伺服器層級上啟用基本驗證？
- 您是否已啟用 Web 管理服務的遠端連線？
- 您是否已啟動 Web 管理服務？
- 管理服務委派規則是否已就緒？
- 應用程式集區身分識別對您網站的源資料夾具有讀取權限嗎？
- 非系統管理員使用者帳戶是否具有 IIS 中的網站層級許可權？
- 您的防火牆是否允許連到 TCP 埠8172上的伺服器的連入連線？

## <a name="further-reading"></a>進一步閱讀

如需如何設定自訂 Microsoft Build Engine （MSBuild）專案檔以將 web 封裝部署至 Web Deploy 處理常式的指引，請參閱[設定目標環境的部署屬性](configuring-deployment-properties-for-a-target-environment.md)。

> [!div class="step-by-step"]
> [上一頁](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
> [下一頁](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
