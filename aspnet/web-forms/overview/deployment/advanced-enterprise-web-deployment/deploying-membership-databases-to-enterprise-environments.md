---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
title: 將成員資格資料庫部署到企業環境 |Microsoft Docs
author: jrjlee
description: 本主題說明您在布建 ASP.NET 應用程式服務資料庫時需要克服的重要考慮和挑戰（較常見的 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 3cf765df-d311-4f68-a295-c9685ceea830
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
msc.type: authoredcontent
ms.openlocfilehash: 50f49af502b75aa5ad52756a76a5e7340aca53f7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526002"
---
# <a name="deploying-membership-databases-to-enterprise-environments"></a>將成員資格資料庫部署到企業環境

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題說明當您在測試、預備或生產環境中布建 ASP.NET 應用程式服務資料庫（通常稱為成員資格資料庫）時，必須克服的重要考慮和挑戰。 它也會描述您可以用來滿足這些挑戰的方法。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="what-are-the-issues-when-you-deploy-a-membership-database"></a>當您部署成員資格資料庫時，會發生什麼問題？

在大多數情況下，當您設計資料庫的部署策略時，您必須考慮的第一件事是您想要部署的資料。 在開發或測試環境中，您可能會想要部署使用者帳戶資料，以方便快速且輕鬆地進行測試。 在預備或生產環境中，您不太可能想要部署使用者帳戶資料。

可惜的是，ASP.NET 成員資格資料庫會引進一些特定的挑戰，讓這種決策更為複雜：

- 僅限架構的部署會讓成員資格資料庫處於無法運作的狀態。 這是因為成員資格資料庫包含了資料庫所需的一些設定資料（在**aspnet\_SchemaVersions**資料表中），以便能夠運作。 因此，如果您執行成員資格資料庫的僅限架構部署以排除使用者帳戶資料，您將需要執行部署後腳本，以新增基本的設定資料。
- 根據您的成員資格資料庫的設定方式而定，成員資格提供者可能會使用電腦金鑰來加密密碼，並將其儲存在資料庫中。 在此情況下，您使用資料庫部署的任何使用者帳戶資料將會在目的地伺服器上變成無法使用。 基於這個理由，部署使用者帳戶資料並不是支援的案例。

## <a name="choosing-a-membership-database-strategy"></a>選擇成員資格資料庫策略

當您選擇如何在企業伺服器環境中布建成員資格資料庫時，請使用下列指導方針：

- 請盡可能不要部署成員資格資料庫。 相反地，請在目標資料庫伺服器上手動建立成員資格資料庫。 如果您尚未自訂您的成員資格資料庫架構，只要使用[ASP.NET SQL Server 註冊工具（aspnet\_regsql）](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)，就可以在目的地的原位中建立一個新的。
- 如果您沒有選項可以部署成員資格資料庫&#x2014;，例如，如果您對資料庫架構&#x2014;進行了廣泛的修改，就應該執行成員資格資料庫的僅限架構部署，以排除使用者帳戶資料，然後執行部署後腳本來新增任何必要的設定資料。 您可以在[如何：部署 ASP.NET 成員資格資料庫而不包含使用者帳戶](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)中找到這些方法的廣泛指引。

請務必記住，您的*成員資格資料庫的架構可能相當靜態*。 即使您已自訂成員資格資料庫，也不太可能需要定期&#x2014;更新架構，而不會變更與 web 應用程式或資料庫專案中的程式碼相同的頻率。 因此，您應該不需要在任何自動化或單一步驟的部署程式中包含成員資格資料庫。

## <a name="using-vsdbcmd-to-update-a-membership-database-schema"></a>使用 VSDBCMD 來更新成員資格資料庫架構

如果您在第一次部署之後修改成員資格資料庫的結構，您可能不會想要使用 Internet Information Services （IIS） Web 部署工具（Web Deploy）重新部署資料庫。 Web Deploy 中的資料庫部署功能並不包含對目的地資料庫&#x2014;進行差異更新的功能，Web Deploy 必須卸載並重新建立資料庫。 這表示您會遺失任何現有的使用者帳戶資料，這通常不會在預備或生產環境中出現。

替代方式是使用 VSDBCMD 公用程式來更新目的地資料庫的架構。 VSDBCMD 包含兩個重要功能。 首先，它可以將現有資料庫的架構匯入到 .dbschema 檔案中。 其次，它可以將 .dbschema 檔案部署到現有的資料庫做為差異更新，這表示它只會進行必要的變更，讓目標資料庫保持在最新狀態，而且您不會遺失任何資料。

您可以使用下列高階步驟來更新成員資格資料庫架構：

1. 使用 [VSDBCMD 匯**入**] 動作，為您的來源成員資格資料庫產生 .dbschema 檔案。 [如何：從命令提示字元匯入架構](https://msdn.microsoft.com/library/dd172135.aspx)中會描述此程式。
2. 使用 [VSDBCMD**部署**] 動作，將 .dbschema 檔案部署到目的地成員資格資料庫。 [VSDBCMD 的命令列參考中會描述此程式。EXE （部署和架構匯入）](https://msdn.microsoft.com/library/dd193283.aspx)。

## <a name="conclusion"></a>結論

本主題說明當您需要在各種目標環境中布建 ASP.NET 成員資格資料庫時，可能會面臨的一些挑戰。 特別是，它會說明為何僅限架構部署將成員資格資料庫保留在非運作狀態，以及為什麼不支援部署使用者帳戶資料。 本主題也提供如何在不同案例中布建、部署和更新成員資格資料庫的指引。

## <a name="further-reading"></a>進一步閱讀

如需如何使用 VSDBCMD 的詳細指引和範例，請參閱[VSDBCMD 的命令列參考。EXE （部署和架構匯入）](https://msdn.microsoft.com/library/dd193283.aspx)和[如何：從命令提示字元匯入架構](https://msdn.microsoft.com/library/dd172135.aspx)。 如需使用 aspnet\_regsql 建立成員資格資料庫的詳細資訊，請參閱[ASP.NET SQL Server 註冊工具（aspnet\_regsql .exe）](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)。 如需有關部署成員資格資料庫的一般指引，請參閱[如何：部署 ASP.NET 成員資格資料庫，而不包含使用者帳戶](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)。

> [!div class="step-by-step"]
> [上一頁](deploying-database-role-memberships-to-test-environments.md)
> [下一頁](excluding-files-and-folders-from-deployment.md)
