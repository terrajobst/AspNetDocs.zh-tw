---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
title: 選擇正確的 Web 部署方法 |Microsoft Docs
author: jrjlee
description: 當您使用 Internet Information Services （IIS） Web 部署工具（Web Deploy）2.0 或更新版本時，您可以使用三種主要方法來取得 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 787a53fd-9901-4a11-9d58-61e0509cda45
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13f784dd8e6404806104d56b026b3c41ca178892
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548479"
---
# <a name="choosing-the-right-approach-to-web-deployment"></a>選擇 Web 部署的正確方法

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 當您使用 Internet Information Services （IIS） Web 部署工具（Web Deploy）2.0 或更新版本時，您可以使用三種主要方法，將封裝的 web 應用程式放在 web 伺服器上。 您可以：
> 
> - 以目的地伺服器上的*Web Deployment Agent 服務*（也稱為「遠端代理程式」）為目標，從遠端位置部署應用程式。
> - 使用 Web Deploy 點播（也稱為「temp 代理程式」）從遠端位置部署應用程式。
> - 以目的地伺服器上的*IIS Web Deploy 處理常式*為目標，從遠端位置部署應用程式。
> - 手動將 web 套件複製到目的地伺服器，並透過 IIS 管理員將其匯入，以部署應用程式。
> 
> 您設定目的地 web 伺服器的方式取決於您想要使用的部署方法。 本主題將協助您決定哪種部署方法最適合您。

下表顯示每種部署方法的主要優點和缺點，以及通常會符合每種方法的案例。

| 方法 | 優點 | 缺點 | 典型案例 |
| --- | --- | --- | --- |
| 遠端代理程式 | 這很容易設定。 適用于 web 應用程式和內容的定期更新。 | 使用者必須是目標伺服器上的系統管理員。 使用者無法提供替代的認證。 | 開發環境。 測試環境。 |
| 暫存代理程式 | 不需要在目的電腦上安裝 Web Deploy。 系統會自動使用最新版本的 Web Deploy。 | 使用者必須是目標伺服器上的系統管理員。 使用者無法提供替代的認證。 | 開發環境。 測試環境。 |
| Web Deploy 處理常式 | 非系統管理員使用者可以部署內容。 適用于 web 應用程式和內容的定期更新。 | 設定變得更複雜。 | 預備環境。 內部網路生產環境。 主控環境。 |
| 離線部署 | 設定非常容易。 它適用于隔離的環境。 | 伺服器系統管理員必須每次手動複製並匯入 web 封裝。 | 網際網路面向的生產環境。 隔離的網路環境。 |

## <a name="using-the-remote-agent"></a>使用遠端代理程式

當您使用目的地伺服器上的預設設定來安裝 Web Deploy 時，會自動安裝及啟動 Web Deployment Agent 服務（「遠端代理程式」）。 根據預設，遠端代理程式會在此位址公開 HTTP 端點：

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample1.cmd)]

> [!NOTE]
> 您可以使用 web 伺服器的電腦名稱稱、web 伺服器的 IP 位址，或解析為 web 伺服器的主機名稱來取代 [*server*]。

伺服器系統管理員可以藉由指定此端點位址，從遠端位置（例如開發人員電腦或組建伺服器）部署 web 封裝。 例如，假設 Fabrikam，Inc. 的 Matt Hink 已在他的開發人員電腦上建立 ContactManager Mvc web 應用程式專案。 組建程式會產生 web 封裝，以及包含安裝封裝所需之 Web Deploy 命令的 *.deploy .cmd 檔案。* 如果 Matt 是 TESTWEB1 伺服器上的伺服器管理員，他可以在他的開發電腦上執行這個命令，將 web 應用程式部署到測試 web 伺服器：

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample2.cmd)]

實際上，如果您提供電腦名稱稱，Web Deploy 可執行檔可以推斷遠端代理程式的端點位址，因此 Matt 只需要輸入下列內容：

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample3.cmd)]

> [!NOTE]
> 如需有關 Web Deploy 命令列語法和*部署 .cmd*檔案的詳細資訊，請參閱[如何：使用 Deploy 檔案安裝部署套件](https://msdn.microsoft.com/library/ff356104.aspx)。

遠端代理程式可讓您直接從遠端位置部署內容，此方法適用于單鍵或自動化部署。 不過，執行部署命令的使用者也必須是網域系統管理員，或是目的地伺服器上本機系統管理員群組的成員。 此外，遠端代理程式不支援基本驗證，因此您無法在命令列上傳遞替代認證。

遠端代理程式在開發或測試案例中提供了一種實用的方法，讓開發人員在測試伺服器環境上擁有完整的系統管理員控制權，而且通常會重建和重新部署應用程式非常罕見眾. 不過，對於臨時或生產環境而言，這種方法通常較不容易接受。

如需使用遠端代理程式方法之案例的端對端範例，請參閱[案例：設定 Web 部署的測試環境](scenario-configuring-a-test-environment-for-web-deployment.md)。

## <a name="using-the-temp-agent"></a>使用 Temp 代理程式

部署的 temp 代理程式方法類似于遠端代理程式方法。 不過，與遠端代理程式方法不同的是，您不需要在目的地 Web 服務器上安裝 Web Deploy。 相反地，當您執行部署時，Web Deploy 會在目的地伺服器上安裝 Web 部署代理程式服務的暫存版本，並使用這個來將您的內容部署到 IIS。 當部署完成時，就會移除所有的暫存檔案。

如果您想要使用 temp 代理程式提供者設定，請將 **/g**旗標新增至您的部署命令：

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample4.cmd)]

> [!NOTE]
> 如果 web 部署代理程式服務已安裝在目的地電腦上，即使服務並未執行，您也無法使用 temp 代理程式。

這種方法的優點是您不需要在目的地伺服器上維護 Web Deploy 的安裝。 此外，您不需要確保來源和目的電腦執行相同版本的 Web Deploy。 不過，此方法與遠端代理程式方法有相同的主體限制，也就是您必須是目的地伺服器上的本機系統管理員，才能部署內容，而且只支援 NTLM 驗證。 暫時代理程式方法也需要更多的目的地環境初始設定。

如需使用 temp 代理程式的詳細資訊，請參閱[如何：使用 deploy 檔案安裝部署套件](https://msdn.microsoft.com/library/ff356104.aspx)和[隨選 Web Deploy](https://technet.microsoft.com/library/ee517345(WS.10).aspx)。

## <a name="using-the-web-deploy-handler"></a>使用 Web Deploy 處理常式

針對 IIS 7 和更新版本，Web Deploy 透過 IIS Web Deploy 處理常式提供替代的部署方法。 Web Deploy 處理常式與 IIS Web 管理服務（WMSvc）緊密整合，其設計目的是讓使用者從遠端位置管理 IIS 網站。

根據預設，遠端代理程式會在此位址公開 HTTP 端點：

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample5.cmd)]

> [!NOTE]
> 您可以使用 web 伺服器的電腦名稱稱、web 伺服器的 IP 位址，或解析為 web 伺服器的主機名稱來取代 [*server*]。

透過遠端代理程式和 temp 代理程式的 Web Deploy 處理常式，最大的優點是您可以將 IIS 設定為允許非系統管理員使用者將應用程式和內容部署到特定的 IIS 網站。 Web Deploy 處理常式也支援基本驗證，因此您可以在 Web Deploy 命令中提供替代的認證做為參數。 最主要的缺點是，Web Deploy 處理常式一開始會變得很複雜，而無法設定。

在非系統管理員使用者的情況下，Web 管理服務（WMSvc）只允許使用者使用網站層級連線（而不是伺服器層級連線）連接到 IIS。 若要存取特定網站，您可以在端點位址中包含網站特定的查詢字串：

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample6.cmd)]

例如，假設組建程式設定為在每次成功組建之後，自動將 web 應用程式部署至預備環境。 如果您使用遠端代理程式方法，您必須將組建進程識別為目的地伺服器上的系統管理員。 相反地，使用 Web Deploy 處理常式方法時，您可以授與非系統&#x2014;管理員的使用者**FABRIKAM\stagingdeployer**在此情況下&#x2014;僅限特定 IIS 網站的許可權，而組建程式則可以提供這些認證來部署 Web 封裝。

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample7.cmd)]

> [!NOTE]
> 如需有關 Web Deploy 命令列作業和語法的詳細資訊，請參閱[Web Deploy 命令列參考](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)。 如需使用*deploy .cmd*檔案的詳細資訊，請參閱[如何：使用 Deploy 檔案安裝部署套件](https://msdn.microsoft.com/library/ff356104.aspx)。

Web Deploy 處理常式在預備環境、託管環境和以內部網路為基礎的生產環境中提供了一種實用的方法，可從遠端存取服務器，但系統管理員認證則不會。

如需使用 Web Deploy 處理常式方法之案例的端對端範例，請參閱[案例：設定 Web 部署的預備環境](scenario-configuring-a-staging-environment-for-web-deployment.md)。

## <a name="using-offline-deployment"></a>使用離線部署

在某些情況下，從遠端位置將應用程式和內容部署到 IIS 網站並不可行。 例如，來源和目的地電腦可能位於隔離的網路或網路區段，或防火牆原則可能不允許遠端存取。

在這類案例中，您仍然可以使用 Web Deploy 的封裝和發行功能;您只能從遠端位置使用它們。 相反地，目的地伺服器上的系統管理員必須將 web 套件複製到伺服器，並透過 IIS 管理員將它匯入。

![](choosing-the-right-approach-to-web-deployment/_static/image1.png)

離線部署方法通常適用于網際網路對向的生產環境，其中周邊網路中的伺服器可能會限制與內部網路中的電腦之間的連線能力。

如需使用離線部署方法之案例的端對端範例，請參閱[案例：設定 Web 部署的生產環境](scenario-configuring-a-production-environment-for-web-deployment.md)。

## <a name="further-reading"></a>進一步閱讀

如需有關 Web Deploy 命令列作業和語法的詳細資訊，請參閱[Web Deploy 命令列參考](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)。 如需使用*deploy .cmd*檔案的詳細資訊，請參閱[如何：使用 Deploy 檔案安裝部署套件](https://msdn.microsoft.com/library/ff356104.aspx)。

如需有關可從遠端電腦部署網頁封裝之不同方式的一般指引，請參閱從[遠端使用 Web Deploy](https://technet.microsoft.com/library/ee461175(WS.10).aspx)。 如需使用 Web Deploy 隨選安裝的詳細資訊，請參閱[隨選 Web Deploy](https://technet.microsoft.com/library/ee517345(WS.10).aspx)。

> [!div class="step-by-step"]
> [上一頁](configuring-server-environments-for-web-deployment.md)
> [下一頁](scenario-configuring-a-test-environment-for-web-deployment.md)
