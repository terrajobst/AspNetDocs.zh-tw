---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
title: 使用 Web 伺服陣列架構建立伺服器陣列 |Microsoft Docs
author: jrjlee
description: 本主題描述如何使用 Web 伺服陣列架構（WFF）2.0，從伺服器集合建立和設定 web 伺服器陣列。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 656dd06d-806c-467c-863d-9fc45e5ba3ab
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
msc.type: authoredcontent
ms.openlocfilehash: 204996514bed336e60ab77f184a923f04e7e2bba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637246"
---
# <a name="creating-a-server-farm-with-the-web-farm-framework"></a>使用 Web 伺服陣列架構建立伺服器陣列

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何使用 Web 伺服陣列架構（WFF）2.0，從伺服器集合建立和設定 web 伺服器陣列。

WFF 可讓您跨多個負載平衡的 web 伺服器同步處理 web 平台產品和元件、web 應用程式、網站和設定。 在您需要一部以上的 web 伺服器（例如預備和生產環境）的案例中，這可能會大幅簡化您的部署和設定程式。 您可以將 web 應用程式部署到單一伺服器&#x2014;*主伺服器*&#x2014;，而 WFF 會在伺服器陣列中的所有其他 web 伺服器上自動複寫該 web 應用程式。

## <a name="understanding-the-web-farm-framework"></a>瞭解 Web 伺服陣列架構

您可以使用 WFF 2.0 來布建、管理及部署內容到一組網頁伺服器。 WFF 部署包含三個主要伺服器角色：

- *控制器伺服器*。 您可以使用此伺服器來建立及設定 WFF 伺服器陣列。 控制器伺服器會管理伺服器陣列中網頁伺服器之間的 web 平臺元件、設定和應用程式的同步處理。 您會在控制器伺服器上安裝 WFF 2.0，而控制器伺服器會接著在伺服器陣列中的每部伺服器上安裝 WFF 代理程式。 控制器伺服器在概念上不屬於任何 WFF 伺服器陣列，而單一控制器伺服器可以管理多個伺服器陣列。 在此案例中，您會使用單一的 WFF 控制器伺服器來建立和管理預備伺服器陣列與實際執行伺服器陣列。
- *主伺服器*。 每個 WFF 伺服器陣列都包含單一的主伺服器。 當您安裝 web platform 元件或將應用程式部署到主伺服器時，WFF 會同步處理您對伺服器陣列中所有其他伺服器的變更。
- *次要伺服器*。 每個 WFF 伺服器陣列都包含一或多部次要伺服器。 您對主伺服器所做的任何變更都會複寫到伺服器陣列內的每一部次要伺服器。

這會顯示這些伺服器角色與 Fabrikam、Inc 和生產環境之間的關聯性：

![](creating-a-server-farm-with-the-web-farm-framework/_static/image1.png)

在此案例中，預備環境和生產環境都設定為 WFF 伺服器陣列。 單一 WFF 控制器伺服器會管理這兩個伺服器陣列。 在每個伺服器陣列中，對主伺服器所做的任何變更都會複寫到每個次要伺服器。

在您開始設定預備和生產環境之前，建議您先閱讀下列文章，以熟悉 WFF 2.0 的重要概念：

- [IIS 7 的 Web Farm Framework 2.0 總覽](https://go.microsoft.com/?linkid=9805126)
- [使用 Web Farm Framework 2.0 為 IIS 7 設定伺服器陣列](https://go.microsoft.com/?linkid=9805127)
- [適用于 IIS 7 之 Web Farm Framework 2.0 的系統和平臺需求](https://go.microsoft.com/?linkid=9805128)

## <a name="task-overview"></a>工作總覽

若要完成本主題中的工作和逐步解說，您至少需要三部&#x2014;伺服器：一個 WFF 控制器、一個用於伺服器陣列的主要 web 伺服器，以及一個或多個伺服器陣列的次要 web 伺服器。 您可以隨時在 WFF 伺服器陣列中新增更多次要伺服器。 概括而言，若要為您的預備或生產環境建立和設定 WFF 伺服器陣列，您必須：

- 藉由安裝 Internet Information Services （IIS）7.5 和 WFF 2.0 來建立控制器伺服器。
- 藉由建立一般的系統管理員帳戶並設定防火牆例外狀況，來準備主要和次要伺服器。
- 使用控制器伺服器上的 IIS 管理員來設定伺服器陣列。
- 使用 IIS 應用程式要求路由（ARR）或替代的負載平衡技術來設定負載平衡。

本主題中的工作和逐步解說假設您是從執行 Windows Server 2008 R2 的全新伺服器組建開始。 開始之前，針對每部伺服器，請確定：

- Windows Server 2008 R2 Service Pack 1 和所有可用的更新都已安裝。
- 伺服器已加入網域。
- 伺服器具有靜態 IP 位址。

> [!NOTE]
> 如需將電腦加入網域的詳細資訊，請參閱[將電腦加入網域並登](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)入。 如需設定靜態 IP 位址的詳細資訊，請參閱[設定靜態 Ip 位址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。

## <a name="create-the-wff-controller-server"></a>建立 WFF 控制器伺服器

若要建立 WFF 控制器伺服器，您必須同時安裝 IIS 7 或更新版本，以及 WFF 2.0 或更新版本。 實際上，WFF 會使用 IIS Web Deployment Tool （Web Deploy）2.x 來同步處理您伺服器陣列中的伺服器。 如果您使用 Web Platform Installer 安裝 WFF，安裝程式會自動為您下載並安裝 Web Deploy。

**建立 WFF 控制器伺服器**

1. 下載並安裝[Web Platform Installer](https://go.microsoft.com/?linkid=9739157)。
2. 在 [ **Web Platform Installer 3.0** ] 視窗頂端，按一下 [**產品**]。
3. 在視窗左側的流覽窗格中，按一下 [**伺服器**]。
4. 在 [ **IIS 7 建議**的設定] 列中，按一下 [**新增**]。
5. 在<strong>Web Farm Framework 2 中。</strong><em>x</em>列，按一下 [<strong>新增</strong>]。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image2.png)
6. 按一下 [安裝]。 請注意，Web Platform Installer 已在安裝清單中新增 Web 部署工具以及其他各種相依性。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image3.png)
7. 請參閱授權條款，如果您同意這些條款，請按一下 [**我接受**]。
8. 當安裝完成時，按一下 **[完成]** ，然後關閉 [ **Web Platform Installer 3.0** ] 視窗。

## <a name="configure-the-primary-and-secondary-servers"></a>設定主要和次要伺服器

建立 WFF 伺服器陣列之前，您應該先在將組成伺服器陣列的 web 伺服器上完成一些準備工作：

- 新增防火牆例外，以允許**核心網路**功能、**遠端系統管理**以及檔案**和印表機共用**功能與 WFF 控制器伺服器通訊。
- 在 Active Directory 中建立網域帳戶（例如， **FABRIKAM\stagingfarm**），並將它新增至每部伺服器上的本機系統管理員群組。 當您建立伺服器陣列時，會使用此帳戶做為伺服器陣列系統管理員帳戶。

如需有關如何在 Windows 防火牆中設定這些防火牆例外的詳細資訊，請參閱[IIS 7 的 Web 伺服陣列架構2.0 的系統和平臺需求](https://go.microsoft.com/?linkid=9805128)。 如需其他防火牆系統，請參閱您的產品檔。

您可以使用下一個程式，將網域帳戶新增至 Windows Server 2008 R2 中的本機 administrators 群組。 您應該在每個想要新增至伺服器&#x2014;陣列的伺服器上執行此程式，換句話說，請將相同的網域帳戶新增至主伺服器和每部次要伺服器上的本機系統管理員群組。

**將網域帳戶新增至本機系統管理員群組**

1. 在 [**開始**] 功能表上，指向 [系統**管理工具**]，然後按一下 [**伺服器管理員**]。
2. 在 [**伺服器管理員**] 視窗的 [樹狀檢視] 窗格中，依序展開 [設定]、[**本機使用者和群組** **]，然後**按一下 [**群組**]。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image4.png)
3. 在 [**群組**] 窗格中，按兩下 [系統**管理員**]。
4. 在 [系統**管理員屬性**] 對話方塊中，按一下 [**新增**]。
5. 在 [**選取使用者、電腦、服務帳戶或群組**] 對話方塊中，輸入（或流覽）您的網域帳戶（例如， **FABRIKAM\stagingfarm**），然後按一下 **[確定]** 。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image5.png)
6. 在 [系統**管理員屬性**] 對話方塊中，按一下 **[確定]** 。

您的伺服器現在可以加入至伺服器陣列。 在主伺服器的情況下，您可以在這兩種情況下，在建立伺服器&#x2014;陣列之前或之後設定伺服器以符合您的應用程式需求，WFF 將會藉由將相同的產品、元件或設定部署到次要伺服器來同步處理伺服器。 為了簡單起見，本教學課程假設您將在完成建立伺服器陣列時設定主伺服器。

## <a name="create-the-wff-server-farm"></a>建立 WFF 伺服器陣列

此時，您的所有伺服器都已準備好新增至 WFF 伺服器陣列：

- 您已在控制器伺服器上安裝 WFF。
- 您已在主要和次要 web 伺服器上設定防火牆例外。
- 您已將網域帳戶新增至主要和次要 web 伺服器上的本機 [系統管理員] 群組。

下一步是在 WFF 中建立伺服器陣列。 您可以從 WFF 控制器伺服器上的 IIS 管理員執行此動作。

**建立 WFF 伺服器陣列**

1. 在 WFF 控制器伺服器的 [**開始**] 功能表上，指向 [系統**管理工具**]，然後按一下 [ **Internet Information Services （IIS）管理員**]。
2. 在 [**連接**] 窗格中，展開本機伺服器節點，以滑鼠右鍵按一下 [**伺服器**陣列]，然後按一下 [**建立伺服器**陣列]。
3. 在 [**建立伺服器**陣列] 對話方塊中，為伺服器陣列輸入有意義的名稱（例如，[**臨時**伺服器陣列]），然後選取 [**提供伺服器**陣列]。
4. 輸入您在每部伺服器上新增至本機 administrators 群組的網域帳戶之使用者名稱和密碼。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image6.png)
5. 按 [下一步]。
6. 在 [**新增伺服器**] 頁面上，輸入主伺服器的完整功能變數名稱（FQDN），選取 [**主伺服器**]，然後按一下 [**新增**]。
7. 此時，WFF 會嘗試使用您所提供的認證來聯繫主伺服器。 如果連線成功，主伺服器將會新增至 [**新增伺服器**] 頁面上的資料表。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image7.png)

    > [!NOTE]
    > 您可能已經注意到，預設已選取 [**伺服器已可供負載平衡**]。 WFF 會使用 IIS ARR 模組來執行負載平衡，並藉此將要求分散到伺服器陣列中的 web 伺服器上。 在大部分的情況下，如果您想要改用協力廠商負載平衡解決方案，您只會清除 [**伺服器適用于負載平衡**] 選項。
8. 在 [**新增伺服器**] 頁面上，輸入第一部次要伺服器的 FQDN，然後按一下 [**新增**]。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image8.png)
9. 針對伺服器陣列中的任何其他次要伺服器重複步驟7，然後按一下 **[完成]** 。

您的 WFF 伺服器陣列現在已啟動且正在執行。 任何您安裝在主伺服器上的 web 平台產品或元件，以及您部署到主伺服器的任何 web 應用程式或內容，都會自動布建到所有次要伺服器上。

WFF 是廣泛且複雜的主題，您可以在[Microsoft Web Farm Framework 2.0 FOR IIS 7](https://go.microsoft.com/?linkid=9805129)網站深入瞭解。 不過，在這段時間內，您必須注意兩個功能區：

- *應用程式*布建是在伺服器陣列中的所有次要伺服器上複寫主伺服器內容（例如 web 應用程式和設定）的過程。 例如，如果您將 Contact Manager 範例解決方案部署到主要的預備伺服器，WFF 應用程式布建程式會將此解決方案部署到您所有的次要預備伺服器。 根據預設，每隔30秒會執行一次應用程式布建進程。
- *平臺*布建是將 web 平台產品和元件從主伺服器同步處理到伺服器陣列中所有次要伺服器的程式。 例如，如果您在主要暫存伺服器上安裝 ASP.NET MVC 3，平臺布建程式將會使用 Web Platform Installer 在所有次要暫存伺服器上安裝 ASP.NET MVC 3。 根據預設，平臺布建程式會每隔五分鐘執行一次。

您可以從 WFF 控制器伺服器上的 IIS 管理員管理基本應用程式和平臺布建設定。

**探索應用程式和平臺布建設定**

1. 在 **[IIS**管理員] 的 [連線] 窗格中，選取您的伺服器陣列。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image9.png)
2. 在 [**伺服器**陣列] 窗格中，按兩下 [**應用程式**布建]。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image10.png)
3. 如您所見，伺服器陣列目前設定為每隔30秒同步處理主伺服器和次要伺服器之間的 web 內容和設定。
4. 按一下 [**上一步**]，然後按兩下 [**平臺**布建]。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image11.png)
5. 如您所見，伺服器陣列目前設定為每隔五分鐘同步處理主伺服器和次要伺服器之間的 web 平台產品和元件。
6. 按一下 [上一步]。
7. 若要強制服務器陣列立即同步處理 web 平台產品，請在 [**動作**] 窗格中，按一下 [布建**平臺**]。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image12.png)

    > [!NOTE]
    > 平臺布建可能需要一些時間。 安裝程式進程會在伺服器陣列中的次要伺服器上以背景執行。
8. 當您有足夠的時間讓布建程式完成時，您可以確認您新增到主伺服器的產品和元件現在已複寫到次要伺服器上。 例如，您可以登入次要伺服器，並使用 [**伺服器管理員**] 視窗，確認已安裝 web 伺服器角色。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image13.png)
9. 您也可以檢查 [已安裝的程式] 清單，以確認已新增各種 web 平臺元件。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image14.png)

## <a name="configure-load-balancing"></a>設定負載平衡

當您建立 web 伺服陣列時，您必須設定某種形式的負載平衡，以便在您的 web 伺服器之間散發 HTTP 要求。 這可能是 Windows Server 2008 網路負載平衡、IIS ARR，或協力廠商軟體型或硬體型負載平衡解決方案。

WFF 的設計目的是要與 IIS ARR 緊密整合。 若要利用這項整合，您必須在 WFF 控制器伺服器上安裝 ARR 模組。 接著，您可以將所有網路流量導向控制器伺服器，通常是藉由設定網域名稱系統（DNS）記錄。 然後，控制器伺服器會根據伺服器可用性和其他各種準則，將傳入要求分散到您伺服器陣列中的伺服器。

> [!NOTE]
> 您不需要使用 ARR 搭配 WFF;您可以將 WFF 設定為與協力廠商負載平衡解決方案搭配使用。 如需詳細資訊，請參閱[IIS 7 的 Web Farm Framework 2.0 總覽](https://go.microsoft.com/?linkid=9805126)。

使用 ARR 進行負載平衡是一個複雜的主題，其中大部分都超出本教學課程的範圍。 不過，您可以使用下一個程式來安裝 ARR 模組，並開始使用負載平衡。

**在 WFF 控制器伺服器上設定負載平衡**

1. 在 WFF 控制器伺服器上，啟動 Web Platform Installer。
2. 在 [ **Web Platform Installer 3.0** ] 視窗頂端，按一下 [**產品**]。
3. 在視窗左側的流覽窗格中，按一下 [**伺服器**]。
4. 在 [**應用程式要求路由 2.5** ] 資料列中，按一下 [**新增**]。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image15.png)
5. 按一下 [**安裝**]，然後依照 [ **Web Platform 安裝**] 視窗中的指示進行。
6. 當安裝完成時，啟動 [IIS 管理員]，**然後在 [連線] 窗格**中，按一下您的伺服器陣列節點。 請注意，[**伺服器**陣列] 窗格中已加入數個新的圖示。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image16.png)
7. 在 [伺服器陣列] 窗格中，按兩下 [負載平衡]。
8. 在 [**負載平衡**] 窗格中，選取負載平衡演算法（例如，**最少目前的要求**）。

    > [!NOTE]
    > 如需負載平衡演算法和其他設定的詳細資訊，請參閱[應用程式要求路由模組](https://go.microsoft.com/?linkid=9805130)。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image17.png)
9. 在 [**動作**] 窗格中 **，按一下 [** 套用]。

您現在已為伺服器陣列中的伺服器設定基本負載平衡。 如果您將所有的 web 伺服陣列流量導向至控制器伺服器，則會根據您選取的可用性和負載平衡演算法，將要求分散到您伺服器陣列中的伺服器。

如需有關如何使用 ARR 來設定負載平衡的詳細資訊，請參閱[應用程式要求路由模組](https://go.microsoft.com/?linkid=9805130)。

## <a name="monitor-the-server-farm"></a>監視伺服器陣列

您可以隨時透過控制器伺服器上的 IIS 管理員監視伺服器陣列的健全狀況。 在 [**連接**] 窗格中，展開您的伺服器陣列，然後按一下 [**伺服器**]。 中間窗格會顯示伺服器陣列中每一部伺服器的摘要，以及最近活動的追蹤記錄。

![](creating-a-server-farm-with-the-web-farm-framework/_static/image18.png)

## <a name="conclusion"></a>結論

您的 WFF 伺服器陣列現在應該已啟動並執行。 您可以設定主伺服器，以支援您偏好&#x2014;的任何部署方法，請參閱進一步閱讀章節&#x2014;以取得詳細資料，而且您的設定將會在伺服器陣列中的每部次要伺服器上複寫。

## <a name="further-reading"></a>進一步閱讀

如需有關設定和使用 WFF 的所有層面的詳細指引，請參閱[Microsoft Web Farm Framework 2.0 FOR IIS 7](https://go.microsoft.com/?linkid=9805129)網站。

> [!div class="step-by-step"]
> [上一頁](configuring-a-database-server-for-web-deploy-publishing.md)
> [下一頁](configuring-deployment-properties-for-a-target-environment.md)
