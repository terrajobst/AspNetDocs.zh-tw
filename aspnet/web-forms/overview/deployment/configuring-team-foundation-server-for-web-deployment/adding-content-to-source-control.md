---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: 將內容加入至原始檔控制 |Microsoft Docs
author: jrjlee
description: 本主題說明如何將內容加入至 Team Foundation Server （TFS）2010中的原始檔控制。 其中說明如何將方案和專案加入至小組 proje 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 16073dd2fb0ea1cc4ddbc94c843181933dc174c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634460"
---
# <a name="adding-content-to-source-control"></a>將內容新增至原始檔控制

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題說明如何將內容加入至 Team Foundation Server （TFS）2010中的原始檔控制。 其中說明如何將方案和專案加入至 TFS 中的 team 專案，並說明如何將外部相依性（例如架構或元件）加入至原始檔控制。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

## <a name="task-overview"></a>工作總覽

在大部分情況下，開發人員小組的每個成員都應該能夠將內容新增至原始檔控制。 若要將方案加入至 TFS 中的原始檔控制，您必須完成下列高階步驟：

- 連接到 team 專案。
- 將伺服器上的 team 專案資料夾結構對應至本機電腦上的資料夾結構。
- 將方案和其內容新增至原始檔控制。
- 將任何外部相依性加入至原始檔控制。

本主題將說明如何執行這些程式。

本主題中的工作和逐步解說假設您已建立新的 TFS team 專案來管理您的內容。 如需建立新 team 專案的詳細資訊，請參閱[在 TFS 中建立 Team 專案](creating-a-team-project-in-tfs.md)。

### <a name="who-performs-these-procedures"></a>誰執行這些程式？

在大部分情況下，開發人員小組的每個成員都應該能夠加入和修改特定 team 專案中的內容。

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a>連接至 Team 專案並建立資料夾對應

將任何內容加入至原始檔控制之前，您必須先連接到 team 專案，並在伺服器上的資料夾結構和本機電腦上的檔案系統之間建立對應。

**若要連接至 team 專案並對應本機路徑**

1. 在開發人員工作站上，開啟 Visual Studio 2010。
2. 在 Visual Studio 的 [**小組**] 功能表上，按一下 [**連接到 Team Foundation Server]** 。

    > [!NOTE]
    > 如果您已經設定與 TFS 伺服器的連接，您可以省略步驟3-6。
3. 在 [**連接到 Team 專案**] 對話方塊中，按一下 [**伺服器**]。
4. 在 [**新增/移除 Team Foundation Server** ] 對話方塊中，按一下 [**新增**]。
5. 在 [**新增 Team Foundation Server** ] 對話方塊中，提供 TFS 實例的詳細資料，然後按一下 **[確定]** 。

    ![](adding-content-to-source-control/_static/image1.png)
6. 在 [**新增/移除 Team Foundation Server** ] 對話方塊中，按一下 [**關閉**]。
7. 在 [**連接到 Team 專案**] 對話方塊中，選取您要連接的 TFS 實例，選取 Team 專案集合，選取您要加入的 team 專案，然後按一下 **[連接]** 。

    ![](adding-content-to-source-control/_static/image2.png)
8. 在 [ **Team Explorer** ] 視窗中，展開您的 Team 專案，然後按兩下 [**原始檔控制**]。

    ![](adding-content-to-source-control/_static/image3.png)
9. 在 [**原始檔控制總管**] 索引標籤上，按一下 [**未對應**]。

    ![](adding-content-to-source-control/_static/image4.png)
10. 在 [**對應**] 對話方塊的 [**本機資料夾**] 方塊中，流覽（或建立）本機資料夾作為 team 專案的根資料夾，然後按一下 [**對應**]。

    ![](adding-content-to-source-control/_static/image5.png)
11. 當系統提示您下載原始檔時，按一下 **[是]** 。

    ![](adding-content-to-source-control/_static/image6.png)

此時，您已將 team 專案的伺服器端資料夾對應至開發人員工作站上的本機資料夾。 您也已將 team 專案中的任何現有內容下載到本機資料夾結構。 您現在可以開始將自己的內容新增至原始檔控制。

## <a name="add-projects-and-solutions-to-source-control"></a>將專案和方案加入至原始檔控制

若要將專案和方案加入至原始檔控制，您必須先將它們移至本機電腦上 team 專案的對應資料夾。 然後您可以簽入內容，將您的新增專案與伺服器同步。

**若要將專案加入至原始檔控制**

1. 在開發人員工作站上，將您的專案和方案移至 team 專案對應資料夾結構內的適當位置。

    > [!NOTE]
    > 許多組織都有慣用的方法，可讓您在原始檔控制中組織專案和方案的方式。 如需如何結構資料夾的指引，請參閱[如何：在 Team Foundation Server 中結構您的原始檔控制資料夾](https://msdn.microsoft.com/library/bb668992.aspx)。
2. 在 Visual Studio 2010 中開啟解決方案。
3. 在 [**方案總管**] 視窗中，以滑鼠右鍵按一下方案，然後按一下 [**將方案加入至原始檔控制**]。

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > 在某些情況下，您可能需要個別將專案新增至原始檔控制，以提供更精細的方式來控制如何組織您的原始程式碼。
4. 確認 [**原始檔控制總管**] 索引標籤會顯示您已在 team 專案的伺服器資料夾結構中新增的內容。

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > [**原始檔控制總管**] 索引標籤會顯示您的內容，而不會進一步提示，因為您已將解決方案新增至本機檔案系統上的對應資料夾。 如果您的方案位於未對應的位置，系統會提示您在 TFS 和本機檔案系統中指定資料夾位置。
5. 在 [**原始檔控制總管**] 索引標籤的 [**資料夾**] 窗格中，以滑鼠右鍵按一下 team 專案（例如， **ContactManager**），然後按一下 [**簽入暫**止的變更]。
6. 在 [**簽入-來源**檔案] 對話方塊中，輸入批註，然後按一下 [**簽入**]。

    ![](adding-content-to-source-control/_static/image9.png)

此時，您已將方案加入至 TFS 中的原始檔控制。

## <a name="add-external-dependencies-to-source-control"></a>將外部相依性加入至原始檔控制

當您將專案或方案加入至原始檔控制時，您的專案或方案中的任何檔案和資料夾也會一併加入。 不過，在許多情況下，專案和方案也依賴外部相依性（例如本機組件），才能正常運作。 您必須將任何這類資源加入至原始檔控制，讓開發人員小組的小組組建和其他成員都能順利建立您的程式碼。

例如，Contact Manager 範例解決方案的資料夾結構包含名為 [套件] 的資料夾。 其中包含 ADO.NET Entity Framework 4.1 的元件和各種支援資源。 [套件] 資料夾不是 Contact Manager 解決方案的一部分，但如果沒有，解決方案就不會成功地建立。 若要啟用 Team Build 來建立方案，您必須將 [封裝] 資料夾加入至原始檔控制。

> [!NOTE]
> 包含封裝資料夾，通常是當您使用適用于 Visual Studio 2010 的 NuGet 擴充功能將 Entity Framework 或類似的資源新增至您的解決方案時，會發生什麼情況。

**若要將非專案內容加入至原始檔控制**

1. 確定您想要新增的專案（例如封裝資料夾）位於本機檔案系統上對應資料夾內的適當位置。
2. 在 Visual Studio 2010 的 [ **Team Explorer** ] 視窗中，展開您的 Team 專案，然後按兩下 [**原始檔控制**]。

    ![](adding-content-to-source-control/_static/image10.png)
3. 在 [**原始檔控制總管**] 索引標籤的 [**資料夾**] 窗格中，選取包含您要新增之專案的資料夾。
4. 按一下 [**將專案加入資料夾**] 按鈕。

    ![](adding-content-to-source-control/_static/image11.png)
5. 在 [**加入至原始檔控制**] 對話方塊中，選取您要新增的資料夾，然後按 **[下一步]** 。

    ![](adding-content-to-source-control/_static/image12.png)
6. 在 [**排除的專案**] 索引標籤上，選取已自動排除的任何必要專案（例如 [元件]），然後按一下 [**包含專案**]。

    ![](adding-content-to-source-control/_static/image13.png)
7. 在 [**要新增的專案**] 索引標籤上，確認已列出您要包含的所有檔案，然後按一下 **[完成]** 。

    ![](adding-content-to-source-control/_static/image14.png)
8. 在 [**原始檔控制總管**] 視窗中，按一下 [**簽入**] 按鈕。

    ![](adding-content-to-source-control/_static/image15.png)
9. 在 [**簽入-來源**檔案] 對話方塊中，輸入批註，然後按一下 [**簽入**]。

此時，您已將方案的外部相依性加入至原始檔控制。

## <a name="conclusion"></a>結論

本主題說明如何連接至 team 專案、對應資料夾結構，以及將內容新增至原始檔控制。 如需如何在原始檔控制下使用專案的詳細資訊，請參閱[使用版本控制](https://msdn.microsoft.com/library/ms181368.aspx)。

下一個主題設定[Web 部署的 TFS 組建伺服器](configuring-a-tfs-build-server-for-web-deployment.md)，說明如何準備 TFS Team build server 以建立和部署您的方案。

## <a name="further-reading"></a>進一步閱讀

如需在 TFS 中使用原始檔控制的詳細資訊，請參閱[使用版本控制](https://msdn.microsoft.com/library/ms181368.aspx)。

> [!div class="step-by-step"]
> [上一頁](creating-a-team-project-in-tfs.md)
> [下一頁](configuring-a-tfs-build-server-for-web-deployment.md)
