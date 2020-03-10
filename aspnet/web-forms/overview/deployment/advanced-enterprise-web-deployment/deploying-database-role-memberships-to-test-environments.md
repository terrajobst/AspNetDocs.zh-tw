---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
title: 將資料庫角色成員資格部署到測試環境 |Microsoft Docs
author: jrjlee
description: 本主題描述如何將使用者帳戶新增至資料庫角色，做為方案部署到測試環境的一部分。 當您部署包含 ... 的方案時
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 9b2af539-7ad9-47aa-b66e-873bd9906e79
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
msc.type: authoredcontent
ms.openlocfilehash: a15f5bf5f659d151e91ef9e53c5ad55bcd8e2b01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587588"
---
# <a name="deploying-database-role-memberships-to-test-environments"></a>將資料庫角色成員資格部署到測試環境

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何將使用者帳戶新增至資料庫角色，做為方案部署到測試環境的一部分。
> 
> 當您將包含資料庫專案的方案部署至預備或生產環境時，您通常不會想要讓開發人員自動將使用者帳戶新增至資料庫角色。 在大部分情況下，開發人員不會知道需要將哪些使用者帳戶新增至哪些資料庫角色，而這些需求可能會隨時變更。 不過，當您將包含資料庫專案的方案部署到開發或測試環境時，通常會有不同的情況：
> 
> - 開發人員通常會定期重新部署解決方案，通常是一天多次。
> - 資料庫通常會在每個部署上重新建立，這表示必須在每次部署之後建立資料庫使用者，並將其新增至角色。
> - 開發人員通常可以完全掌控目標開發或測試環境。
> 
> 在此案例中，在部署程式中自動建立資料庫使用者並指派資料庫角色成員資格，通常會有説明。
> 
> 主要因素是，此作業必須根據目標環境進行條件式設定。 如果您要部署至預備或生產環境，您會想要略過此作業。 如果您要部署至開發人員或測試環境，您會想要部署角色成員資格，而不需要進一步介入。 本主題說明您可以用來解決這項挑戰的一種方法。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="task-overview"></a>工作總覽

本主題假設：

- 如[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述，您可以使用分割專案檔案方法來部署解決方案。
- 您可以從專案檔呼叫 VSDBCMD 來部署資料庫專案，如[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式中所述。

當您將資料庫專案部署至測試環境時，若要建立資料庫使用者並指派角色成員資格，您必須：

- 建立交易結構化查詢語言 (SQL) （Transact-sql）腳本，以進行必要的資料庫變更。
- 建立使用 sqlcmd 公用程式執行 SQL 腳本的 Microsoft Build Engine （MSBuild）目標。
- 將您的方案部署到測試環境時，設定您的專案檔以叫用目標。

本主題將說明如何執行上述每個程式。

## <a name="scripting-the-database-role-memberships"></a>編寫資料庫角色成員資格的腳本

您可以用許多不同的方式，以及您選擇的任何位置來建立 Transact-sql 腳本。 最簡單的方法是在您的解決方案中建立 Visual Studio 2010 的腳本。

**若要建立 SQL 腳本**

1. 在 [**方案總管**] 視窗中，展開您的資料庫專案節點。
2. 在 [**腳本**] 資料夾上按一下滑鼠右鍵，指向 [**加入**]，然後按一下 [**新增資料夾**]。
3. 輸入**Test**作為資料夾名稱，然後按 enter。
4. 以滑鼠右鍵按一下 [ **Test** ] 資料夾，指向 [**新增**]，然後按一下 [**腳本**]。
5. 在 [**加入新專案**] 對話方塊中，為您的腳本提供有意義的名稱（例如**AddRoleMemberships**），然後按一下 [**新增**]。

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. 在*AddRoleMemberships*檔案中，加入下列的 transact-sql 語句：

    1. 為將存取資料庫的 SQL Server 登入建立資料庫使用者。
    2. 將資料庫使用者新增至任何必要的資料庫角色。
7. 檔案看起來應該像這樣：

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. 儲存檔案。

## <a name="executing-the-script-on-the-target-database"></a>在目標資料庫上執行腳本

在理想的情況下，您會在部署資料庫專案時，執行任何必要的 Transact-sql 腳本作為部署後腳本的一部分。 不過，部署後腳本並不允許您根據解決方案設定或組建屬性，有條件地執行邏輯。 替代方式是建立執行 sqlcmd 命令的**目標**專案，直接從 MSBuild 專案檔執行 SQL 腳本。 您可以使用此命令在目標資料庫上執行腳本：

[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]

> [!NOTE]
> 如需 sqlcmd 命令列選項的詳細資訊，請參閱[Sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx)。

在 MSBuild 目標中內嵌此命令之前，您必須考慮要執行腳本的條件：

- 目標資料庫必須先存在，您才能變更其角色成員資格。 因此，您必須在資料庫部署*之後*執行此腳本。
- 您需要包含條件，才會針對測試環境執行腳本。
- 如果您執行的是「假設」部署&#x2014;，但如果您要產生部署腳本，但未實際執行，&#x2014;則不應該執行 SQL 腳本。

如果您使用[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法（如 Contact Manager 範例解決方案所示），您可以分割 SQL 腳本的組建指示，如下所示：

- 任何必要的環境特定屬性，以及決定是否要部署許可權的屬性，都應該在環境特定的專案檔（例如*Env-Dev*）中進行。
- MSBuild 目標本身和任何在目的地環境之間不會變更的屬性，都應該放在通用專案檔（例如， *Publish*）中。

在環境特定的專案檔中，您必須定義資料庫伺服器名稱、目標資料庫名稱，以及可讓使用者指定是否要部署角色成員資格的布林值屬性。

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]

在通用專案檔中，您必須提供 sqlcmd 可執行檔的位置，以及您想要執行之 SQL 腳本的位置。 不論目的地環境為何，這些屬性都會維持不變。 您也需要建立 MSBuild 目標來執行 sqlcmd 命令。

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]

請注意，您會將 sqlcmd 可執行檔的位置新增為靜態屬性，因為這對其他目標很有用。 相反地，您會將 SQL 腳本的位置和 sqlcmd 命令的語法定義為目標內的動態屬性，因為在執行目標之前，不需要它們。 在此情況下，只有在符合下列條件時，才會執行**DeployTestDBPermissions**目標：

- **DeployTestDBRoleMemberships**屬性設定為**true**。
- 使用者未指定**WhatIf = true**旗標。

最後，別忘了叫用目標。 在*Publish*檔案中，您可以藉由將目標新增至預設**FullPublish**目標的相依性清單來執行這項操作。 您必須確保在執行**PublishDbPackages**目標之前，不會執行**DeployTestDBPermissions**目標。

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]

## <a name="conclusion"></a>結論

本主題描述了一種方式，可讓您在部署資料庫專案時，將資料庫使用者和角色成員資格加入為部署後動作。 當您在測試環境中定期重新建立資料庫時，這通常很有用，但當您將資料庫部署至預備或生產環境時，通常應該避免這種情況。 因此，您應該確定使用必要的條件式邏輯，以便只在適當的情況下才建立資料庫使用者和角色成員資格。

## <a name="further-reading"></a>進一步閱讀

如需使用 VSDBCMD 來部署資料庫專案的詳細資訊，請參閱[部署資料庫專案](../web-deployment-in-the-enterprise/deploying-database-projects.md)。 如需針對不同目標環境自訂資料庫部署的指引，請參閱[自訂多個環境的資料庫部署](customizing-database-deployments-for-multiple-environments.md)。 如需使用自訂 MSBuild 專案檔控制部署程式的詳細資訊，請參閱[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔和[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式。 如需 sqlcmd 命令列選項的詳細資訊，請參閱[Sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx)。

> [!div class="step-by-step"]
> [上一頁](customizing-database-deployments-for-multiple-environments.md)
> [下一頁](deploying-membership-databases-to-enterprise-environments.md)
