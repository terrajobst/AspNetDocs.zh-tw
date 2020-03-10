---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: 手動安裝 Web 套件 |Microsoft Docs
author: jrjlee
description: 本主題描述如何以手動方式將 web 部署套件匯入 Internet Information Services （IIS）中。 建立和封裝 Web Applicati 主題 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: f778549d3e26989a2e71ef21171adec521842729
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634201"
---
# <a name="manually-installing-web-packages"></a>手動安裝 Web 套件

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何以手動方式將 web 部署套件匯入 Internet Information Services （IIS）中。
> 
> [建立和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)主題說明了 IIS Web Deployment Tool （Web Deploy）與 Microsoft Build Engine （MSBuild）和 Web 發行管線（WPP）如何搭配使用，讓您將 web 應用程式專案封裝成單一的 zip 檔案。 此檔案通常稱為 web 部署套件（或只是部署套件），其中包含 IIS 在 web 伺服器上重新建立 web 應用程式所需的所有內容和設定資訊。
> 
> 建立 web 部署套件之後，您可以透過各種方式將它發佈至 IIS 伺服器。 在許多情況下，您會想要利用 MSBuild、WPP 和 Web Deploy 之間的整合點，在自動或單一步驟的組建和部署程式中，從遠端建立和安裝 Web 套件。 [部署 Web 套件](deploying-web-packages.md)中會說明此程式。 不過，這不一定可行。 假設您想要將 web 應用程式部署到網際網路面向的生產環境。 基於安全性理由，這類生產環境最不可能位於與組建伺服器不同的子網上的防火牆後方，位於周邊網路（也稱為 DMZ、非軍事區域和遮蔽式子網路）。 在許多情況下，生產環境會位於不同的網域或實體隔離的網路上。
> 
> 在這些情況下，您的唯一選項可能是將 web 套件移植到目的地伺服器，並手動將它匯入到 IIS 中。 雖然這種方法會排除自動化部署，但它仍然是發佈 web 應用程式&#x2014;的高效率技巧，只要將單一 zip 檔案複製到您的 web 伺服器，然後使用 wizard 引導您完成匯入程式。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

## <a name="task-overview"></a>工作總覽

您必須完成這些高階工作，才能將 web 部署套件匯入 IIS：

- 使用 MSBuild 命令列、Team Build 或 Visual Studio 2010 建立 web 部署套件。
- 將網頁套件複製到目的地 web 伺服器。
- 使用 IIS 管理員中的 [匯入應用程式封裝]，即可安裝 web 套件並提供變數的值，例如連接字串和服務端點。

本主題將說明如何執行這些程式。 本主題中的工作和逐步解說假設您已經熟悉 web 套件、Web Deploy 和 WPP 背後的概念。 如需詳細資訊，請參閱[建立和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)。

> [!NOTE]
> 本主題最適合用於[[設定用於 Web Deploy 發佈的 Web 服務器（離線部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)]，其中說明如何安裝必要的元件，並準備 IIS 網站以進行套件匯入。

## <a name="create-a-web-deployment-package"></a>建立 Web 部署套件

第一個工作是為您想要部署的 web 應用程式專案建立 web 部署套件。 您可以用各種方式建立網頁封裝。

**方法1：使用 Visual Studio 在組建程式中建立封裝**

您可以設定 web 應用程式專案，透過專案屬性頁上的 [**封裝/發行 web** ] 索引標籤，在每個組建之後建立 web 部署封裝。 [建立和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)中會說明這個程式。

**方法2：使用 MSBuild 建立封裝作為組建程式的一部分**

如果您直接使用 MSBuild 建立 web 應用程式專案（不論是透過自訂 MSBuild 專案檔或從命令列），您可以在命令中包含**DeployOnBuild = true**和**DeployTarget = package**屬性，以建立 web 部署封裝做為建立程式的一部分。 瞭解此程式的說明請參閱[瞭解組建流程](understanding-the-build-process.md)。

**方法3：依需求在 Visual Studio 中建立套件**

您可以在 Visual Studio 2010 中隨時建立 web 應用程式專案的 web 部署套件。 若要這麼做，請在 [**方案總管**] 視窗中，以滑鼠右鍵按一下您的 web 應用程式專案，然後按一下 [**建立部署封裝**]。

![](manually-installing-web-packages/_static/image1.png)

**方法4：依需求從命令列建立套件**

您可以使用 MSBuild 在 web 應用程式專案上叫用**封裝**目標，以從命令列建立 web 部署封裝。 命令應如下所示：

[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]

無論您使用哪種方法，最後的結果都一樣。 WPP 會在您 web 應用程式專案的輸出檔案夾中，建立一個 zip 檔案和各種支援資源的 web 部署套件。

![](manually-installing-web-packages/_static/image2.png)

當您打算手動匯入 web 套件時，您只需要 zip 檔案。 將此檔案複製到您的目標 web 伺服器，然後您就可以開始匯入程式。

## <a name="import-a-web-package-into-iis"></a>將 Web 封裝匯入 IIS

您可以使用下一個程式，將 web 部署套件從本機檔案系統匯入到 IIS 網站。 執行此程式之前，請確定您有：

- 已將 web 部署套件複製到 web 伺服器。
- 設定 IIS web 伺服器來裝載您的應用程式。

如需設定 IIS web 伺服器以支援 web 部署套件的詳細資訊，請參閱[Configure a Web server for Web Deploy 發佈（離線部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。

**使用 IIS 管理員匯入 web 部署套件**

1. 在 **[Iis**管理員] 的 [連線] 窗格中，以滑鼠右鍵按一下您的 IIS 網站，指向 [**部署**]，然後按一下 [匯**入應用程式**]。

    ![](manually-installing-web-packages/_static/image3.png)
2. 在 [匯入應用程式套件] 中，于 [**選取封裝**] 頁面上，流覽至 web 部署套件的位置，然後按 **[下一步]** 。
3. 在 [**選取封裝的內容**] 頁面上，清除您不需要的任何內容，然後按 **[下一步]** 。

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > 在許多情況下，您可能不想要匯入 web 部署套件隨附的所有內容。 例如，您可能不想讓 Web Deploy 取代相關聯的資料庫。  
    > **授與許可權**專案會在目的地檔案系統上設定許可權，以確保應用程式集區身分識別可以存取儲存網站內容的實體資料夾。 此外，會將資料夾的讀取權限授與匿名驗證使用者，讓應用程式提供多用途網際網路郵件延伸（MIME）類型檔案。 如果您想要的話，也可以移除這些專案，並手動設定許可權。
4. 在 [**輸入應用程式封裝資訊**] 頁面上，提供所要求的資訊。

    ![](manually-installing-web-packages/_static/image5.png)
5. 當您建立 web 套件時，WPP 會分析應用程式的設定檔案，並偵測任何變數，例如連接字串和服務端點。 在此情況下：

    1. [**應用程式路徑**] 是您要安裝應用程式的 IIS 路徑。 此設定通用於 WPP 所建立的所有部署套件。
    2. **ContactService 服務端點位址**是應用程式應該用來與已部署的 WCF 服務進行通訊的位址。 此設定會對應*至 web.config 檔案*中的專案。
    3. 第一個**連接字串**設定是 Web Deploy 應該用來部署與應用程式相關聯之資料庫的連接字串（在此案例中為 ASP.NET 成員資格資料庫）。 此設定會對應至 Visual Studio 中 [**封裝/發行 SQL** ] 索引標籤上的設定。
    4. 第二個**連接字串**設定是連接字串，當應用程式啟動並執行時，它會實際用來與資料庫進行通訊。 這會對應*至 web.config 檔案*中的連接字串專案。

        > [!NOTE]
        > 如需這些參數來自何處的詳細資訊，請參閱設定[Web 封裝部署的參數](configuring-parameters-for-web-package-deployment.md)。
6. 按 [下一步]。
7. 如果這不是您第一次將應用程式部署到此網站，系統會提示您指定是否要在安裝前刪除所有現有的內容。 選擇適合您需求的選項，然後按 **[下一步]** 。

    ![](manually-installing-web-packages/_static/image6.png)
8. 當 IIS 完成安裝套件時，請按一下 **[完成]** 。

    ![](manually-installing-web-packages/_static/image7.png)

此時，您已成功將 web 應用程式發佈至 IIS。

## <a name="conclusion"></a>結論

本主題說明如何使用 IIS 管理員將 web 部署套件匯入 IIS 網站。 當安全性或基礎結構的條件約束不可能或不想要進行遠端部署時，此 web 應用程式發佈的方法會很適合

## <a name="further-reading"></a>進一步閱讀

如需如何設定 IIS web 伺服器以支援手動匯入 web 封裝的指引，請參閱[設定用於 Web Deploy 發佈的 Web 服務器（離線部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。 如需部署 web 套件的一般指引，請參閱[逐步解說：使用 Web 部署封裝部署 Web 應用程式專案（第1部，共4部）](https://msdn.microsoft.com/library/dd483479.aspx)。

> [!div class="step-by-step"]
> [上一篇](creating-and-running-a-deployment-command-file.md)
