---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
title: 建立支援部署的組建定義 |Microsoft Docs
author: jrjlee
description: 如果您想要在 Team Foundation Server （TFS）2010中執行任何種類的組建，您必須在 Team 專案中建立組建定義。 本主題 des 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: fe47a018-f6d0-4979-80e7-5b1fa75a5865
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
msc.type: authoredcontent
ms.openlocfilehash: e11c91a824446572aaf0b3bc6954b9b8ffb4eaff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78603996"
---
# <a name="creating-a-build-definition-that-supports-deployment"></a>建立支援部署的組建定義

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 如果您想要在 Team Foundation Server （TFS）2010中執行任何種類的組建，您必須在 Team 專案中建立組建定義。 本主題描述如何在 TFS 中建立新的組建定義，以及如何控制 web 部署，做為 Team Build 中的組建流程的一部分。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建和部署程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="task-overview"></a>工作總覽

組建定義是一種機制，可控制 TFS 中 team 專案的組建發生的方式和時機。 每個組建定義都會指定：

- 您想要建立的專案，例如 Visual Studio 方案檔或自訂 Microsoft Build Engine （MSBuild）專案檔。
- 決定何時應進行組建的準則，例如手動觸發程式、持續整合（CI）或閘道簽入。
- Team Build 應傳送組建輸出的位置，包括部署成品（例如 web 封裝和資料庫腳本）。
- 每個組建應保留的時間量。
- 組建進程的各種其他參數。

> [!NOTE]
> 如需組建定義的詳細資訊，請參閱[定義您的組建進程](https://msdn.microsoft.com/library/ms181715.aspx)。

本主題將說明如何建立使用 CI 的組建定義，以便在開發人員簽入新內容時觸發組建。 如果組建成功，組建服務會執行自訂專案檔，以將方案部署到測試環境。

當您觸發組建時，必須執行下列動作：

- 首先，Team Build 應該建立解決方案。 在此程式中，Team Build 會叫用 Web 發行管線（WPP），為方案中的每個 web 應用程式專案產生 web 部署套件。 Team Build 也會執行與方案相關聯的任何單元測試。
- 如果解決方案組建失敗，則 Team Build 不應採取進一步的動作。 應該將單元測試失敗視為組建失敗。
- 如果解決方案組建成功，Team Build 應該執行自訂專案檔來控制方案的部署。 在此程式中，Team Build 會叫用 Internet Information Services （IIS） Web 部署工具（Web Deploy），在目的地 Web 服務器上安裝已封裝的 web 應用程式，而且它將會叫用 VSDBCMD 公用程式來執行資料庫建立目的地資料庫伺服器上的腳本。

這會說明此程式：

![](creating-a-build-definition-that-supports-deployment/_static/image1.png)

[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)範例解決方案包含自訂 msbuild 專案檔（ *Publish*），您可以從 msbuild 或 Team Build 執行該檔案。 如[瞭解建立](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式中所述，這個專案檔會定義將 web 封裝和資料庫部署至目標環境的邏輯。 此檔案包含的邏輯會省略建立和封裝程式（如果它是在 Team Build 中執行），只留下要執行的部署工作。 這是因為當您以這種方式自動化部署時，通常會想要確保解決方案成功建立，並在部署程式開始之前傳遞任何單元測試。

下一節將說明如何藉由建立新的組建定義來執行此程式。

> [!NOTE]
> 這&#x2014;項程式中，單一自動化進程建立、測試及部署解決方案&#x2014;可能最適合部署到測試環境。 對於預備和生產環境，您很可能會想要從先前的組建部署內容，而您已經在測試環境中驗證和驗證。 這個方法會在下一個主題中說明如何[部署特定的組建](deploying-a-specific-build.md)。

### <a name="who-performs-this-procedure"></a>誰執行此程式？

一般而言，TFS 系統管理員會執行此程式。 在某些情況下，開發人員小組領導人可能會負責 TFS 中的 team 專案集合。 若要建立新的組建定義，您必須是包含方案之 team 專案集合的 [**專案集合組建系統管理員**] 群組成員。

## <a name="create-a-build-definition-for-ci-and-deployment"></a>建立 CI 和部署的組建定義

下一個程式描述如何建立 CI 觸發程式的組建定義。 如果組建成功，則會使用自訂 MSBuild 專案檔中的邏輯來部署方案。

**建立 CI 和部署的組建定義**

1. 在 Visual Studio 2010 的 [ **Team Explorer** ] 視窗中，展開您的 Team 專案節點，以滑鼠右鍵按一下 [**組建**]，然後按一下 [**新增組建定義**]。

    ![](creating-a-build-definition-that-supports-deployment/_static/image2.png)
2. 在 [**一般**] 索引標籤上，提供組建定義的名稱（例如， **DeployToTest**）和選擇性描述。
3. 在 [**觸發**程式] 索引標籤上，選取您想要觸發新組建的準則。 例如，如果您想要建立方案，並在每次開發人員簽入新程式碼時部署至測試環境，請選取 [**持續整合**]。
4. 在 [**組建預設值**] 索引標籤的 [**將組建輸出複製到下列放置資料夾**] 方塊中，輸入放置資料夾的通用命名慣例（UNC）路徑（例如， **\\TFSBUILD\Drops**）。

    ![](creating-a-build-definition-that-supports-deployment/_static/image3.png)

    > [!NOTE]
    > 這個放置位置會儲存數個組建，視您設定的保留原則而定。 當您想要從特定組建將部署成品發佈至預備或生產環境時，您可以在這裡找到這些專案。
5. 在 [**流程**] 索引標籤的 [**建立**程式檔案] 下拉式清單中，將 [ **defaulttemplate.xaml** ] 保留為已選取。 這是新增至所有新 team 專案的其中一個預設組建流程範本。
6. 在 [**建立流程參數**] 資料表中，按一下 [**要建立的專案**] 資料列，然後按一下**省略號**按鈕。

    ![](creating-a-build-definition-that-supports-deployment/_static/image4.png)
7. 在 [**要建立的專案**] 對話方塊中，按一下 [**新增**]。
8. 流覽至方案檔的位置，然後按一下 **[確定]** 。

    ![](creating-a-build-definition-that-supports-deployment/_static/image5.png)
9. 在 [**要建立的專案**] 對話方塊中，按一下 [**新增**]。
10. 在 [**類型的專案**] 下拉式清單中，選取 [ **MSBuild 專案**檔]。
11. 流覽至您用來控制部署程式的自訂專案檔位置，選取該檔案，然後按一下 **[確定]** 。

    ![](creating-a-build-definition-that-supports-deployment/_static/image6.png)
12. [**要建立的專案**] 對話方塊現在應該會顯示兩個專案。 按一下 [確定]。

    ![](creating-a-build-definition-that-supports-deployment/_static/image7.png)
13. 在 [**流程**] 索引標籤的 [**建立流程參數**] 資料表中，展開 [ **Advanced** ] 區段。
14. 在 [ **MSBuild 引數**] 資料列中，加入任何*一個*要建立之專案所需的 MSBuild 命令列引數。 在 Contact Manager 解決方案案例中，這些引數是必要的：

    [!code-console[Main](creating-a-build-definition-that-supports-deployment/samples/sample1.cmd)]

    ![](creating-a-build-definition-that-supports-deployment/_static/image8.png)
15. 在這個範例中：

    1. 當您建立 Contact Manager 方案時，需要**DeployOnBuild = true**和**DeployTarget = package**引數。 這會指示 MSBuild 在建立每個 web 應用程式專案之後建立 web 部署封裝，如[建立和封裝 Web 應用程式專案](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)中所述。
    2. 當您建立*Publish*檔案時，需要**TargetEnvPropsFile**引數。 此屬性工作表示環境特定設定檔案的位置，如[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式中所述。
16. 在 [**保留原則**] 索引標籤上，設定您想要保留多少個類型的組建，視需要而定。
17. 按一下 [儲存]。

## <a name="queue-a-build"></a>將組建排入佇列

此時，您已建立至少一個新的組建定義。 您定義的組建進程現在會根據您在組建定義中指定的觸發程式來執行。

如果您已將組建定義設定為使用 CI，您可以透過兩種方式來測試組建定義：

- 將某些內容簽入 team 專案，以觸發自動組建。
- 手動將組建排到佇列。

**手動將組建排入佇列**

1. 在 [ **Team Explorer** ] 視窗中，以滑鼠右鍵按一下組建定義，然後按一下 [將**新組建**排入佇列]。

    ![](creating-a-build-definition-that-supports-deployment/_static/image9.png)
2. 在 [**佇列組建**] 對話方塊中，檢查組建屬性，然後按一下 [**佇列**]。

    ![](creating-a-build-definition-that-supports-deployment/_static/image10.png)

若要檢查組建&#x2014;的進度和結果，不論其是否已手動觸發，或在 [&#x2014; **Team Explorer** ] 視窗中自動按兩下組建定義。 這會開啟 [**組建瀏覽器**] 索引標籤。

![](creating-a-build-definition-that-supports-deployment/_static/image11.png)

從這裡，您可以針對失敗的組建進行疑難排解。 如果您按兩下個別的組建，您可以查看摘要資訊，並按一下以列出詳細的記錄檔。

![](creating-a-build-definition-that-supports-deployment/_static/image12.png)

您可以使用這份資訊來疑難排解失敗的組建，並解決任何問題，再嘗試另一個組建。

> [!NOTE]
> 除非您已將目的地環境中所需的任何許可權授與組建伺服器，否則執行部署邏輯的組建可能會失敗。 如需詳細資訊，請參閱設定[Team Build 部署的許可權](configuring-permissions-for-team-build-deployment.md)。

## <a name="monitor-the-build-process"></a>監視組建進程

TFS 提供各種功能，可協助您監視組建程式。 例如，TFS 可以在組建完成時，傳送電子郵件給您，或在工作列通知區域中顯示警示。 如需詳細資訊，請參閱[執行和監視組建](https://msdn.microsoft.com/library/ms181721.aspx)。

## <a name="conclusion"></a>結論

本主題說明如何在 TFS 中建立組建定義。 組建定義是針對 CI 設定的，因此每當開發人員將內容簽入 team 專案時，就會執行組建程式。 組建定義會執行自訂的 MSBuild 專案檔，將 web 封裝和資料庫腳本部署到目標伺服器環境。

為了讓自動化部署成功成為組建程式的一部分，您必須在目標 web 伺服器和目標資料庫伺服器上，將適當的許可權授與組建服務帳戶。 本教學課程中的最後一個主題是設定[Team Build 部署的許可權](configuring-permissions-for-team-build-deployment.md)，描述如何識別並設定從 Team build 伺服器進行自動化部署所需的許可權。

## <a name="further-reading"></a>進一步閱讀

如需建立組建定義的詳細資訊，請參閱[建立基本組建定義](https://msdn.microsoft.com/library/ms181716.aspx)和[定義您的組建進程](https://msdn.microsoft.com/library/ms181715.aspx)。 如需佇列組建的詳細指引，請參閱[將組建](https://msdn.microsoft.com/library/ms181722.aspx)排入佇列。

> [!div class="step-by-step"]
> [上一頁](configuring-a-tfs-build-server-for-web-deployment.md)
> [下一頁](deploying-a-specific-build.md)
