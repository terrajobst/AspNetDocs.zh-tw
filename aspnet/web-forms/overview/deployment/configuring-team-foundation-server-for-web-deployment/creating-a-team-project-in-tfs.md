---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: 在 TFS 中建立 Team 專案 |Microsoft Docs
author: jrjlee
description: 本主題描述如何在 Team Foundation Server （TFS）2010中建立新的 team 專案。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: d12e0636ce3b6239d125305db4354278f9f24960
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639654"
---
# <a name="creating-a-team-project-in-tfs"></a>在 TFS 中建立 Team 專案

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何在 Team Foundation Server （TFS）2010中建立新的 team 專案。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

## <a name="task-overview"></a>工作總覽

若要在 TFS 中布建和使用新的 team 專案，您必須完成下列高階步驟：

- 將建立新 team 專案的許可權授與給使用者。
- 建立 team 專案。
- 授與許可權給將在專案上工作的小組成員。
- 簽入某些內容。

本主題將說明如何執行這些程式，並會識別可能負責每個程式的使用者和作業角色。 請注意，根據您組織的結構，每個工作都可能是不同人員的責任。

本主題中的工作和逐步解說假設您已安裝並設定 TFS，而且您已在設定程式中建立 team 專案集合。 如需這些假設的詳細資訊，以及有關此案例的一般背景資訊，請參閱[設定 Web 部署的 TFS 組建伺服器](configuring-a-tfs-build-server-for-web-deployment.md)。

## <a name="grant-permissions-to-the-team-project-creator"></a>將許可權授與 Team 專案建立者

若要建立新的 team 專案，您需要下列許可權：

- 您必須擁有 TFS 應用層的 [**建立新專案**] 許可權。 您通常會藉由將使用者加入至 [ **Project Collection Administrators** ] TFS 群組來授與此許可權。 [ **Team Foundation Administrators** ] 全域群組也包含此許可權。
- 您必須擁有在對應至 TFS team 專案集合的 SharePoint 網站集合中，建立新小組網站的許可權。 您通常會將使用者新增至 SharePoint 群組（具有 SharePoint 網站集合的 [**完全控制**] 許可權），以授與此許可權。
- 如果您使用 SQL Server Reporting Services 功能，您必須是 Reporting Services 中 [ **Team Foundation 內容管理員**] 角色的成員。

### <a name="who-performs-these-procedures"></a>誰執行這些程式？

一般而言，負責管理 TFS 部署的人員或群組也會執行這些程式。

由於這是一組高度許可權的許可權，因此新的 team 專案通常是由一小部分的使用者所建立，負責管理 TFS 部署。 開發人員通常不會被授與建立新 team 專案所需的許可權。

### <a name="grant-permissions-in-tfs"></a>在 TFS 中授與許可權

如果您想要讓使用者建立新的 team 專案，第一個高階工作就是將使用者加入 team 專案集合的**Project Collection Administrators**群組。

**若要將使用者加入至專案集合系統管理員群組**

1. 在 TFS 伺服器的 [**開始**] 功能表上，指向 [**所有程式**]，按一下 [ **Microsoft Team Foundation Server 2010**]，然後按一下 [ **Team Foundation 管理主控台**]。
2. 在導覽樹狀檢視中，展開 [**應用層**]，然後按一下 [ **Team 專案集合**]。

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. 在 [ **Team 專案集合**] 窗格中，選取您要管理的 Team 專案集合。

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. 在 [**一般**] 索引標籤上，按一下 [**群組成員資格**]。

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. 在 [**全域群組**] 對話方塊中，選取 [ **Project Collection Administrators** ] 群組，然後按一下 [**屬性**]。
6. 在 [ **Team Foundation Server 群組屬性**] 對話方塊中，選取 [ **Windows 使用者或群組**]，然後按一下 [**新增**]。

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. 在 [**選取使用者、電腦或群組**] 對話方塊中，輸入您要能夠建立新 team 專案的使用者使用者名稱，按一下 [**檢查名稱**]，然後按一下 **[確定]** 。

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. 在 [ **Team Foundation Server 群組屬性**] 對話方塊中，按一下 **[確定]** 。
9. 在 [**全域群組**] 對話方塊中，按一下 [**關閉**]。

### <a name="grant-permissions-in-sharepoint-services"></a>授與 SharePoint Services 中的許可權

接下來，您必須授與使用者在對應至 TFS team 專案集合的 SharePoint 網站集合中，建立新小組網站的許可權。

**授與 SharePoint 網站集合的完全控制許可權**

1. 在 Team Foundation Server 管理主控台的  **Team 專案集合** 頁面上，選取您要管理的 team 專案集合。
2. 在 [ **SharePoint 網站**] 索引標籤上，記下**目前預設網站位置**URL 的值。

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. 開啟 Internet Explorer，然後移至您在步驟2記下的 URL。

    > [!NOTE]
    > 如果您不是以建立 team 專案集合的使用者身分登入 Windows，則必須以這位使用者的身分登入 SharePoint，才能繼續。
4. 在 **[網站動作]** 功能表上，按一下 **[網站設定]** 。

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. 在 [**網站設定**] 頁面的 [**使用者和許可權**] 底下，按一下 [**人員和群組**]。
6. 在左側導覽窗格中，按一下 [**群組**]。

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. 在 [**人員和群組：所有群組**] 頁面上，按一下 [**設定此網站的群組**]。

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > 由於雙重 HTTP 編碼錯誤，您可能會收到<strong>HTTP 404 找不</strong>到的錯誤。 如果發生這種情況，請以下列內容取代 URL：   
   > 例如 `[site_collection_URL]/_layouts/permsetup.aspx`：  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. 在 [**設定此網站的群組**] 頁面上，將建立 team 專案的使用者新增至 [**擁有**者] 群組，然後按一下 **[確定]** 。

    ![](creating-a-team-project-in-tfs/_static/image10.png)

如需有關如何讓使用者在 team 專案集合中建立新 team 專案的詳細資訊，請參閱[設定 Team 專案集合的系統管理員許可權](https://msdn.microsoft.com/library/dd547204.aspx)。

## <a name="create-a-new-team-project-and-add-users"></a>建立新的 Team 專案並新增使用者

當您擁有必要的許可權之後，就可以使用 Visual Studio 2010 中的 [ **Team Explorer** ] 視窗來建立新的 Team 專案。 這個方法會提供一個 wizard，以收集所有必要的資訊，並在 TFS、SharePoint 和 SQL Server Reporting Services 中執行必要的工作。 您也必須將新 team 專案的許可權授與開發人員小組的成員，讓他們能夠新增和修改內容。

### <a name="who-performs-these-procedures"></a>誰執行這些程式？

通常 TFS 系統管理員或開發人員小組領導人都會執行這些程式。

### <a name="create-a-new-team-project"></a>建立新的 Team 專案

下一個程式描述如何在 TFS 2010 中建立新的 team 專案。

**若要建立新的 team 專案**

1. 在 [**開始**] 功能表上，指向 [**所有程式**]，按一下 [ **Microsoft Visual Studio 2010**]，以滑鼠右鍵按一下 [ **Microsoft Visual Studio 2010**]，然後按一下 [以**系統管理員身分執行**]。

    > [!NOTE]
    > 如果您未以系統管理員的身分執行 Visual Studio 2010，則在最後一個步驟中，[新增 Team 專案嚮導] 將會失敗。
2. 如果出現 **[使用者帳戶控制]** 對話方塊，請按一下 **[是]** 。
3. 在 Visual Studio 的 [**小組**] 功能表上，按一下 [**連接到 Team Foundation Server]** 。

    > [!NOTE]
    > 如果您已經設定與 TFS 伺服器的連接，您可以省略步驟4-7。
4. 在 [**連接到 Team 專案**] 對話方塊中，按一下 [**伺服器**]。
5. 在 [**新增/移除 Team Foundation Server** ] 對話方塊中，按一下 [**新增**]。
6. 在 [**新增 Team Foundation Server** ] 對話方塊中，提供 TFS 實例的詳細資料，然後按一下 **[確定]** 。

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. 在 [**新增/移除 Team Foundation Server** ] 對話方塊中，按一下 [**關閉**]。
8. 在 [**連接到 Team 專案**] 對話方塊中，選取您要連接的 TFS 實例，選取您要加入的 Team 專案集合，然後按一下 **[連接]** 。

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. 在 [ **Team Explorer** ] 視窗中，以滑鼠右鍵按一下 Team 專案集合，然後按一下 [**新增 team 專案**]。

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. 在 [**新增 Team 專案**] 對話方塊中，提供 Team 專案的 [名稱] 和 [描述]，然後按 **[下一步]** 。

    > [!NOTE]
    > 如果您的 team 專案包含空格，當您使用 Internet Information Services （IIS） Web 部署工具（Web Deploy）從輸出路徑部署封裝時，可能會遇到一些問題。 路徑中的空格可能會使 Web Deploy 命令的執行變得更容易。

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. 在 [**選取流程範本**] 頁面上，選取您要用來管理開發進程的流程範本，然後按 **[下一步]** 。

    > [!NOTE]
    > 如需 TFS 流程範本的詳細資訊，請參閱[流程範本和工具](https://msdn.microsoft.com/vstudio/aa718795)。
12. 在 [**小組網站設定**] 頁面上，保留預設設定不變，然後按 **[下一步]** 。
13. 此設定會建立或識別與 TFS team 專案相關聯的 SharePoint 小組網站。 您的開發小組可以使用這個網站來管理檔、參與討論執行緒、建立 wiki 頁面，以及執行與程式碼無關的其他工作。 如需詳細資訊，請參閱[SharePoint 產品與 Team Foundation Server 之間的互動](https://msdn.microsoft.com/library/ms253177.aspx)。
14. 在 [**指定原始檔控制設定**] 頁面上，保留預設設定不變，然後按 **[下一步]** 。
15. 此設定會識別或建立 TFS 資料夾階層中的位置，以作為內容的根資料夾。
16. 在 [**確認 Team 專案設定**] 頁面上，按一下 **[完成]** 。
17. 成功建立新的 team 專案時，請在 [ **Team 專案建立**] 頁面上按一下 [**關閉**]。

### <a name="add-users-to-a-team-project"></a>將使用者加入至 Team 專案

既然您已建立新的 team 專案，您可以授與許可權給使用者，讓他們能夠開始加入和共同作業內容。

**若要將使用者加入至 team 專案**

1. 在 Visual Studio 2010 的 [ **Team Explorer** ] 視窗中，以滑鼠右鍵按一下 team 專案，指向 [ **team 專案設定**]，然後按一下 [**群組成員資格**]。

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. 若要讓使用者加入、修改和移除原始檔控制下的程式碼，您必須將他或她加入至**Contributors**群組。
3. 在 [**專案群組**] 對話方塊中，選取 [ **Contributors** ] 群組，然後按一下 [**屬性**]。

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. 在 [ **Team Foundation Server 群組屬性**] 對話方塊中，選取 [ **Windows 使用者或群組**]，然後按一下 [**新增**]。

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. 在 [**選取使用者、電腦或群組**] 對話方塊中，輸入您要加入至 team 專案之使用者的使用者名稱，按一下 [**檢查名稱**]，然後按一下 **[確定]** 。

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. 在 [ **Team Foundation Server 群組屬性**] 對話方塊中，按一下 **[確定]** 。
7. 在 [**專案群組**] 對話方塊中，按一下 [**關閉**]。

## <a name="conclusion"></a>結論

此時，您的新 team 專案已準備好可供使用，而您的開發人員小組可以開始在開發程式上新增內容和共同作業。

下一個主題 [[將內容新增至原始檔控制](adding-content-to-source-control.md)] 會說明如何將內容加入至原始檔控制。

## <a name="further-reading"></a>進一步閱讀

如需在 TFS 中建立 team 專案的更廣泛指引，請參閱[建立 Team 專案](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx)。 如需有關如何讓使用者在 team 專案集合中建立新 team 專案的詳細資訊，請參閱[設定 Team 專案集合的系統管理員許可權](https://msdn.microsoft.com/library/dd547204.aspx)。 如需將使用者加入至 team 專案的詳細資訊，請參閱[將使用者加入 Team 專案](https://msdn.microsoft.com/library/bb558971.aspx)。

> [!div class="step-by-step"]
> [上一頁](configuring-team-foundation-server-for-web-deployment.md)
> [下一頁](adding-content-to-source-control.md)
