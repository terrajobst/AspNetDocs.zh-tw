---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: 部署特定組建 |Microsoft Docs
author: jrjlee
description: 本主題描述如何將 web 封裝和資料庫腳本從特定的先前組建部署到新的目的地，例如預備或生產 enviro 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: 6bede6b36c24ade928ab052e14daec1e017bd0b2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639668"
---
# <a name="deploying-a-specific-build"></a>部署特定的組建

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何將 web 封裝和資料庫腳本從特定的先前組建部署到新的目的地，例如預備或生產環境。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建和部署程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="task-overview"></a>工作總覽

到目前為止，本教學課程中的主題設定著重于如何建立、封裝和部署 web 應用程式和資料庫，做為單一步驟或自動化程式的一部分。 不過，在某些常見的案例中，您會想要從 [放置] 資料夾中的組建清單來選取您部署的資源。 換句話說，最新的組建可能不是您想要部署的組建。

請考慮上一個主題中所述的持續整合（CI）案例，建立[支援部署的組建定義](creating-a-build-definition-that-supports-deployment.md)。 您已在 Team Foundation Server （TFS）2010中建立組建定義。 每當開發人員將程式碼簽入 TFS 時，Team Build 就會建立您的程式碼，將 web 封裝和資料庫腳本當做組建流程的一部分來執行、執行任何單元測試，並將您的資源部署到測試環境。 根據您在建立組建定義時所設定的保留原則，TFS 會保留特定數目的先前組建。

![](deploying-a-specific-build/_static/image1.png)

現在，假設您已針對測試環境中的其中一個組建執行驗證和驗證測試，而且您已準備好將應用程式部署至預備環境。 在此同時，開發人員可能已簽入新的程式碼。 您不想要重建解決方案並部署至預備環境，而且不想要將最新的組建部署至預備環境。 相反地，您會想要部署已在測試伺服器上驗證並驗證的特定組建。

若要完成此動作，您必須告訴 Microsoft Build Engine （MSBuild）哪裡可以找到特定組建所產生的 web 套件和資料庫腳本。

## <a name="overriding-the-outputroot-property"></a>覆寫 OutputRoot 屬性

在[範例方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)中， *Publish*檔案會宣告名為**OutputRoot**的屬性。 如其名所示，這是包含組建程式所產生之所有專案的根資料夾。 在*Publish*檔案中，您可以看到**OutputRoot**屬性指的是所有部署資源的根位置。

> [!NOTE]
> **OutputRoot**是常用的屬性名稱。 視覺C#效果和 Visual Basic 專案檔也會宣告此屬性，以儲存所有組建輸出的根位置。

[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]

如果您想要讓專案檔從不同的位置&#x2014;部署 web 封裝和資料庫腳本，例如先前 TFS 組建&#x2014;的輸出，您只需要覆寫**OutputRoot**屬性。 您應該將屬性值設定為 Team Build server 上的相關組建資料夾。 如果您是從命令列執行 MSBuild，您可以將**OutputRoot**的值指定為命令列引數：

[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]

不過，在實務上，如果您不打算使用組建輸出，&#x2014;您也會想要略過**組建目標，而不**需要建立解決方案。 您可以藉由指定要從命令列執行的目標來執行這項操作：

[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]

不過，在大部分的情況下，您會想要將部署邏輯建立至 TFS 組建定義中。 這可讓具有**佇列組建**許可權的使用者，從任何具有 TFS 伺服器連接的 Visual Studio 安裝觸發部署。

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a>建立組建定義以部署特定組建

下一個程式描述如何建立組建定義，讓使用者使用單一命令觸發對預備環境的部署。

在這種情況下，您不想讓組建定義實際建立&#x2014;您想要它在自訂專案檔中執行部署邏輯的任何作業。 如果檔案是在 Team Build 中執行，則*Publish*檔案包含會略過**組建**目標的條件式邏輯。 它會藉由評估內建的**BuildingInTeamBuild**屬性來完成這項工作，如果您在 Team Build 中執行專案檔，它會自動設定為**true** 。 因此，您可以略過建立程式，並直接執行專案檔來部署現有的組建。

**若要建立組建定義以手動觸發部署**

1. 在 Visual Studio 2010 的 [ **Team Explorer** ] 視窗中，展開您的 Team 專案節點，以滑鼠右鍵按一下 [**組建**]，然後按一下 [**新增組建定義**]。

    ![](deploying-a-specific-build/_static/image2.png)
2. 在 [**一般**] 索引標籤上，提供組建定義的名稱（例如， **DeployToStaging**）和選擇性描述。
3. 在 [**觸發**程式] 索引標籤上，選取 [**手動–簽入不會觸發新的組建**]。
4. 在 [**組建預設值**] 索引標籤的 [**將組建輸出複製到下列放置資料夾**] 方塊中，輸入放置資料夾的通用命名慣例（UNC）路徑（例如， **\\TFSBUILD\Drops**）。

    ![](deploying-a-specific-build/_static/image3.png)
5. 在 [**流程**] 索引標籤的 [**建立**程式檔案] 下拉式清單中，將 [ **defaulttemplate.xaml** ] 保留為已選取。 這是新增至所有新 team 專案的其中一個預設組建流程範本。
6. 在 [**建立流程參數**] 資料表中，按一下 [**要建立的專案**] 資料列，然後按一下**省略號**按鈕。

    ![](deploying-a-specific-build/_static/image4.png)
7. 在 [**要建立的專案**] 對話方塊中，按一下 [**新增**]。
8. 在 [**類型的專案**] 下拉式清單中，選取 [ **MSBuild 專案**檔]。
9. 流覽至您用來控制部署程式的自訂專案檔位置，選取該檔案，然後按一下 **[確定]** 。

    ![](deploying-a-specific-build/_static/image5.png)
10. 在 [**要建立的專案**] 對話方塊中，按一下 **[確定]** 。
11. 在 [**建立流程參數**] 資料表中，展開 [ **Advanced** ] 區段。
12. 在 [ **MSBuild 引數**] 資料列中，指定環境特定專案檔的位置，並為您的組建資料夾位置新增預留位置：

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > 每次將組建排入佇列時，您都必須覆寫**OutputRoot**值。 這會在下一個程式中討論。
13. 按一下 [儲存]。

當您觸發組建時，您必須更新**OutputRoot**屬性以指向您想要部署的組建。

**若要從組建定義部署特定的組建**

1. 在 [ **Team Explorer** ] 視窗中，以滑鼠右鍵按一下組建定義，然後按一下 [將**新組建**排入佇列]。

    ![](deploying-a-specific-build/_static/image7.png)
2. 在 [**佇列組建**] 對話方塊的 [**參數**] 索引標籤上，展開 [ **Advanced** ] 區段。
3. 在 [ **MSBuild 引數**] 資料列中，將**OutputRoot**屬性的值取代為組建資料夾的位置。 例如:

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > 請務必在組建資料夾路徑結尾包含尾端斜線。
4. 按一下 [**佇列**]。

當您將組建排入佇列時，專案檔會從您在**OutputRoot**屬性中指定的組建放置資料夾，部署資料庫腳本和 web 封裝。

## <a name="conclusion"></a>結論

本主題描述如何使用「分割專案檔」部署模型，從特定的先前組建發行部署資源，例如 web 套件和資料庫腳本。 文中說明了如何覆寫**OutputRoot**屬性，以及如何將部署邏輯併入 TFS 組建定義中。

## <a name="further-reading"></a>進一步閱讀

如需建立組建定義的詳細資訊，請參閱[建立基本組建定義](https://msdn.microsoft.com/library/ms181716.aspx)和[定義您的組建進程](https://msdn.microsoft.com/library/ms181715.aspx)。 如需佇列組建的詳細指引，請參閱[將組建](https://msdn.microsoft.com/library/ms181722.aspx)排入佇列。

> [!div class="step-by-step"]
> [上一頁](creating-a-build-definition-that-supports-deployment.md)
> [下一頁](configuring-permissions-for-team-build-deployment.md)
