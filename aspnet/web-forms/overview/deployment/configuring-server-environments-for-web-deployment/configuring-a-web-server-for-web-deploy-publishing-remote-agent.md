---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
title: 設定用於 Web Deploy 發佈的 Web 服務器（遠端代理程式） |Microsoft Docs
author: jrjlee
description: 本主題描述如何設定 Internet Information Services （IIS）網頁伺服器，以支援使用 IIS Web 部署的 web 發行和部署 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 239c7aa8-d09a-4d02-9c0e-6bd52be5f0d5
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
msc.type: authoredcontent
ms.openlocfilehash: ce0d246afdfb65c2ea15a287064511e7d1d58622
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78567470"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-remote-agent"></a>設定 Web Deploy 發行的網頁伺服器 (遠端代理程式)

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何使用 IIS Web Deployment Tool （Web Deploy）遠端代理程式服務，將 Internet Information Services （IIS）網頁伺服器設定為支援 web 發行和部署。
> 
> 當您使用 Web Deploy 2.0 或更新版本時，有三種主要方法可用來將您的應用程式或網站放在 Web 服務器上。 您可以：
> 
> - 使用*Web Deploy 的遠端代理程式服務*。 這種方法需要較少的 web 伺服器設定，但您必須提供本機伺服器系統管理員的認證，才能將任何專案部署至伺服器。
> - 使用*Web Deploy 處理常式*。 這種方法比較複雜，而且需要更多的初始工作來設定 web 伺服器。 不過，當您使用這種方法時，可以設定 IIS 以允許非系統管理員使用者執行部署。 Web Deploy 處理常式僅適用于 IIS 7 版或更新版本。
> - 使用*離線部署*。 此方法需要最少的 web 伺服器設定，但伺服器管理員必須手動將 web 套件複製到伺服器，並透過 IIS 管理員將其匯入。
> 
> 如需這些方法的主要功能、優點和缺點的詳細資訊，請參閱[選擇正確的 Web 部署方法](choosing-the-right-approach-to-web-deployment.md)。

## <a name="is-the-web-deploy-remote-agent-the-right-approach-for-you"></a>Web Deploy 遠端代理程式是正確的方法嗎？

是，如果要部署內容的使用者可以在目的地伺服器上提供系統管理員的認證。 這種方法通常適用于下列類型的案例：

- 開發或測試環境，開發人員可以完全掌控目的地 web 伺服器和資料庫伺服器。
- 小型組織，其中單一使用者或一小組使用者可以控制整個應用程式生命週期。

在許多大型組織中，特別是針對預備或生產環境，在網頁伺服器上提供使用者系統管理員許可權通常並不實際。 在裝載的 web 伺服器案例中，這種情況特別不太可能發生。 此外，如果您打算從組建伺服器自動進行部署，則可能不會想要使用系統管理員認證來進行部署程式。 在這些情況下，將您的網頁伺服器設定為支援使用[Web Deploy 處理常式](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)進行部署，可能會提供更令人滿意的選擇。

## <a name="task-overview"></a>工作總覽

本主題說明如何使用 Web Deploy 遠端代理程式方法，設定 Internet Information Services （IIS）7.5 網頁伺服器，以接受及部署遠端電腦上的網頁封裝。 您必須：

- 安裝 IIS 7.5 和 IIS 7 建議的設定。
- 安裝 Web Deploy 2.1 或更新版本。
- 建立 IIS 網站來裝載已部署的內容。
- 確認 Web Deployment Agent 服務正在執行。

若要明確裝載範例解決方案，您也需要：

- 安裝 .NET Framework 4.0。
- 安裝 ASP.NET MVC 3。

本主題將說明如何執行上述每個程式。 本主題中的工作和逐步解說假設您是從執行 Windows Server 2008 R2 的全新伺服器組建開始。 在繼續之前，請確定：

- Windows Server 2008 R2 Service Pack 1 和所有可用的更新都已安裝。
- 伺服器已加入網域。
- 伺服器具有靜態 IP 位址。

> [!NOTE]
> 如需將電腦加入網域的詳細資訊，請參閱[將電腦加入網域並登](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)入。 如需設定靜態 IP 位址的詳細資訊，請參閱[設定靜態 Ip 位址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。 遠端代理程式服務是由 IIS 6 和更新版本所支援，而且不需要加入網域。 不過，本教學課程中的步驟已在 IIS 7.5 上進行開發和測試，而其他版本的程式則可能有所不同。

## <a name="install-products-and-components"></a>安裝產品和元件

本節將引導您在 web 伺服器上安裝必要的產品和元件。 在開始之前，最好先執行 Windows Update，以確保您的伺服器完全保持在最新狀態。

在此情況下，您需要安裝下列專案：

- **IIS 7 建議**的設定。 這會啟用 web 伺服器上的**網頁伺服器（iis）** 角色，並安裝您需要的一組 IIS 模組和元件，才能裝載 ASP.NET 應用程式。
- **.NET Framework 4.0**。 這是執行此版本 .NET Framework 所建立之應用程式的必要項。
- **Web Deployment Tool 2.1 或更新版本**。 這會在您的伺服器上安裝 Web Deploy （及其基礎可執行檔，Msdeploy.exe）。 在此過程中，它會安裝並啟動 Web Deployment Agent 服務。 此服務可讓您從遠端電腦部署 web 封裝。
- **ASP.NET MVC 3**。 這會安裝執行 MVC 3 應用程式所需的元件。

> [!NOTE]
> 本逐步解說說明如何使用 Web Platform Installer 來安裝和設定必要的元件。 雖然您不需要使用 Web Platform Installer，但它會自動偵測相依性，並確保您一律取得最新的產品版本，藉此簡化安裝程式。 如需詳細資訊，請參閱[Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118)。

**若要安裝必要的產品和元件**

1. 下載並安裝[Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。
2. 安裝完成時，Web Platform Installer 會自動啟動。

    > [!NOTE]
    > 您現在可以隨時從 [**開始**] 功能表啟動 Web Platform Installer。 若要這樣做，請在 [**開始**] 功能表上，按一下 [**所有程式**]，然後按一下 [ **Microsoft Web Platform Installer**]。
3. 在 [ **Web Platform Installer 3.0** ] 視窗頂端，按一下 [**產品**]。
4. 在視窗左側的流覽窗格中 **，按一下 [** 架構]。
5. 在 [ **Microsoft .NET Framework 4** ] 資料列中，如果尚未安裝 .NET Framework，請按一下 [**新增**]。

    > [!NOTE]
    > 您可能已經透過 Windows Update 安裝了 .NET Framework 4.0。 如果已安裝產品或元件，Web Platform Installer 會以**已安裝**的文字取代 [**新增**] 按鈕來指出這一點。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image1.png)
6. 在 [ **ASP.NET MVC 3 （Visual Studio 2010）** ] 資料列中，按一下 [**新增**]。
7. 在流覽窗格中，按一下 [**伺服器**]。
8. 在 [ **IIS 7 建議**的設定] 列中，按一下 [**新增**]。
9. 在 [ **Web Deployment Tool 2.1** ] 資料列中，按一下 [**新增**]。
10. 按一下 [安裝]。 Web Platform Installer 將會顯示一份產品&#x2014;清單，其中包含&#x2014;要安裝的相關聯相依性，並會提示您接受授權條款。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image2.png)
11. 請參閱授權條款，如果您同意這些條款，請按一下 [**我接受**]。
12. 當安裝完成時，按一下 **[完成]** ，然後關閉 [ **Web Platform Installer 3.0** ] 視窗。

如果您在安裝 IIS 之前安裝了 .NET Framework 4.0，就必須執行[ASP.NET IIS 註冊工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx)（aspnet\_regiis），以向 IIS 註冊最新版本的 ASP.NET。 如果您不這麼做，就會發現 IIS 會提供靜態內容（例如 HTML 檔案），而不會有任何問題，但會傳回**HTTP 錯誤404.0 –** 當您嘗試流覽至 ASP.NET 內容時找不到。 您可以使用此程式來確保 ASP.NET 4.0 已註冊。

**向 IIS 註冊 ASP.NET 4。0**

1. 按一下 [**開始**]，然後輸入**命令提示**字元。
2. 在搜尋結果中，以滑鼠右鍵按一下 [**命令提示**字元]，然後按一下 [以**系統管理員身分執行**]。
3. 在 [命令提示字元] 視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319**目錄。
4. 輸入此命令，然後按 Enter 鍵：

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample1.cmd)]
5. 如果您打算在任何時間點裝載64位的 web 應用程式，您也應該向 IIS 註冊64位版本的 ASP.NET。 若要這麼做，請在 [命令提示字元] 視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319**目錄。
6. 輸入此命令，然後按 Enter 鍵：

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample2.cmd)]

建議的作法是，在此時再次使用 Windows Update，下載並安裝您已安裝之新產品和元件的任何可用更新。

## <a name="configure-the-iis-website"></a>設定 IIS 網站

您必須先建立並設定 IIS 網站來裝載內容，才能將 web 內容部署到您的伺服器。 Web Deploy 只能將 web 套件部署到現有的 IIS 網站;它無法為您建立網站。 概括而言，您必須完成下列工作：

- 在檔案系統上建立資料夾，以裝載您的內容。
- 建立 IIS 網站來提供內容，並將它與本機資料夾產生關聯。
- 授與讀取權限給本機資料夾上的應用程式集區身分識別。

雖然沒有任何動作會阻止您將內容部署到 IIS 中的預設網站，但不建議針對測試或示範案例以外的任何專案使用此方法。 若要模擬生產環境，您應該使用特定于應用程式需求的設定來建立新的 IIS 網站。

**建立和設定 IIS 網站**

1. 在本機檔案系統上，建立用來儲存內容的資料夾（例如， **C:\DemoSite**）。
2. 在 [**開始**] 功能表上，指向 [系統**管理工具**]，然後按一下 [ **Internet Information Services （IIS）管理員**]。
3. 在 **[IIS**管理員] 的 [連線] 窗格中，展開伺服器節點（例如， **TESTWEB1**）。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image3.png)
4. 以滑鼠右鍵按一下 [**網站**] 節點，然後按一下 [**新增**網站]。
5. 在 [**網站名稱**] 方塊中，輸入 IIS 網站的名稱（例如， **DemoSite**）。
6. 在 [**實體路徑**] 方塊中，輸入（或流覽至）本機資料夾的路徑（例如， **C:\DemoSite**）。
7. 在 [**埠**] 方塊中，輸入您要用來裝載網站的埠號碼（例如， **85**）。

    > [!NOTE]
    > 適用于 HTTP 的標準埠號碼為80，HTTPS 則為443。 不過，如果您在埠80上裝載此網站，則必須先停止預設網站，才能存取您的網站。
8. 除非您要設定網站的網域名稱系統（DNS）記錄，否則請將 [**主機名稱**] 方塊保留空白，然後按一下 **[確定]** 。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image4.png)

    > [!NOTE]
    > 在生產環境中，您可能會想要在埠80上裝載您的網站，並設定主機標頭和相符的 DNS 記錄。 如需在 IIS 7 中設定主機標頭的詳細資訊，請參閱[設定網站的主機標頭（iis 7）](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。 如需有關 Windows Server 2008 R2 中 DNS 伺服器角色的詳細資訊，請參閱[Dns 伺服器總覽](https://technet.microsoft.com/library/cc770392.aspx)和[dns 伺服器](https://technet.microsoft.com/windowsserver/dd448607)。
9. 在 [ **動作** ] 窗格的 [ **編輯站台**] 下方，按一下 [ **繫結**]。
10. 在 [站台繫結] 對話方塊中，按一下 [新增]。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image5.png)
11. 在 [**新增網站**系結] 對話方塊中，將 [ **IP 位址**] 和 [**埠**] 設定為符合您現有的網站設定。
12. 在 [**主機名稱**] 方塊中，輸入您的 web 伺服器名稱（例如， **TESTWEB1**），然後按一下 **[確定]** 。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image6.png)

    > [!NOTE]
    > 第一個網站系結可讓您使用 IP 位址和埠或 `http://localhost:85`，在本機存取網站。 第二個網站系結可讓您使用電腦名稱稱（例如 http://testweb1:85)，從網域中的其他電腦存取網站。
13. 在 [站台繫結] 對話方塊中，按一下 [關閉]。
14. **在 [連線**] 窗格中，按一下 [**應用程式**集區]。
15. 在 [**應用程式**集區] 窗格中，以滑鼠右鍵按一下應用程式集區的名稱，然後按一下 [**基本設定**]。 根據預設，您的應用程式集區名稱會與您的網站名稱相符（例如， **DemoSite**）。
16. 在 [ **.NET Framework 版本**] 清單中，選取 [ **.NET Framework v 4.0.30319**]，然後按一下 **[確定]** 。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image7.png)

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

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image8.png)
5. 在 [**選取使用者或群組**] 對話方塊中，輸入**IIS\_給 iis-iusrs**，按一下 [**檢查名稱**]，然後按一下 **[確定]** 。
6. 在<em>[資料夾名稱] 的 [</em><strong>許可權</strong>] 對話方塊中，請注意，預設會將 [<strong>讀取 &amp; 執行</strong>]、[<strong>列出資料夾內容</strong>] 和 [<strong>讀取</strong>] 許可權指派給新的群組。 保持不變，然後按一下<strong>[確定]</strong>。
7. 按一下 [<strong>確定</strong>] 以關閉<em>[資料夾名稱]</em><strong>屬性</strong>對話方塊。

在您嘗試將任何 web 封裝部署到伺服器之前，您應該先確定 Web Deployment Agent 服務正在執行，這是最後一項工作。 當您從遠端電腦部署封裝時，Web Deployment Agent 服務會負責解壓縮和安裝封裝的內容。 當您安裝 Web 部署工具並以網路服務識別執行時，預設會啟動此服務。

您可以使用各種命令列公用程式或 Windows PowerShell Cmdlet，以多種不同的方式來檢查服務是否正在執行。 此程式描述以 UI 為基礎的簡單方法。

**若要檢查 Web Deployment Agent 服務是否正在執行**

1. 在 [開始] 功能表上，指向 [系統管理工具]，然後按一下 [服務]。
2. 找出 [ **Web Deployment Agent 服務**] 資料列，然後確認 [**狀態**] 設定為 [**已啟動**]。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image9.png)
3. 如果服務尚未啟動，請按一下 [**啟動**]。

## <a name="configure-firewall-exceptions"></a>設定防火牆例外狀況

根據預設，遠端代理程式服務會接聽 TCP 通訊埠80，網址為：

<http://servername.com/MSDEPLOYAGENTSERVICE>

在大部分情況下，您不需要為遠端代理程式服務設定任何額外的防火牆規則，因為 web 伺服器通常會接聽埠80上的 HTTP 要求。 如果您將安裝自訂為在非標準埠上接聽，您必須視需要設定防火牆例外。

## <a name="conclusion"></a>結論

此時，您的網頁伺服器已準備好接受遠端電腦上的 web 套件並加以安裝。 嘗試將 web 應用程式部署到伺服器之前，您可能會想要檢查下列重點：

- 您是否已向 IIS 註冊 ASP.NET 4.0？
- 應用程式集區身分識別對您網站的源資料夾具有讀取權限嗎？
- Web Deployment Agent 服務是否正在執行？

## <a name="further-reading"></a>進一步閱讀

如需如何設定自訂 Microsoft Build Engine （MSBuild）專案檔以將 web 封裝部署到遠端代理程式服務的指引，請參閱[設定目標環境的部署屬性](configuring-deployment-properties-for-a-target-environment.md)。

> [!div class="step-by-step"]
> [上一頁](scenario-configuring-a-production-environment-for-web-deployment.md)
> [下一頁](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
