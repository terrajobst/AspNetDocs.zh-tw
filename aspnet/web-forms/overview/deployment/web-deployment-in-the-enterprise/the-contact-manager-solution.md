---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: Contact Manager 解決方案 |Microsoft Docs
author: jrjlee
description: 這一系列的教學課程會使用&#x2014;Contact Manager 解決方案&#x2014;的範例解決方案，來代表具有實際層級的企業規模應用程式 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: 12ed7827f7392e559e04121386f7cd045de8462b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586265"
---
# <a name="the-contact-manager-solution"></a>連絡管理員解決方案

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 這一[系列的教學](web-deployment-in-the-enterprise.md)課程會使用&#x2014;Contact Manager 解決方案&#x2014;的範例解決方案，來代表具有實際複雜度層級的企業級應用程式。 本主題介紹 Contact Manager 解決方案，說明解決方案的主要元件，並找出在企業環境中將這類應用程式部署至各種目的地平臺的挑戰。
> 
> 當您逐步完成這些教學課程中的主題時，您可以使用 Contact Manager 解決方案做為參考，以示範如何滿足企業部署案例中的特定挑戰。 下一個主題[設定 Contact Manager 解決方案](setting-up-the-contact-manager-solution.md)，說明如何在開發人員工作站上下載並執行解決方案。

## <a name="solution-overview"></a>方案概觀

Contact Manager 解決方案包含四個個別的專案：

![](the-contact-manager-solution/_static/image1.png)

- **ContactManager。** 這是 ASP.NET MVC 3 web 應用程式專案，代表解決方案的進入點。 它提供一些基本的 web 應用程式功能，例如提供使用者建立和查看連絡人詳細資料的能力。 應用程式會依賴 Windows Communication Foundation （WCF）服務來管理連絡人和 ASP.NET 應用程式服務資料庫，以管理驗證和授權。
- **ContactManager. 資料庫**。 這是 Visual Studio 資料庫專案。 專案會定義儲存連絡人詳細資料之資料庫的架構。
- **ContactManager. 服務**。 這是 WCF web 服務專案。 WCF 服務會公開一個端點，讓呼叫者可以在**ContactManager**資料庫上執行建立、抓取、更新和刪除（CRUD）作業。 服務依賴**ContactManager**資料庫和**ContactManager 的 Common .dll**元件。
- **ContactManager。** 這是類別庫專案。 WCF 服務依賴此元件中定義的類型。

此解決方案也包含名為 Publish 的方案資料夾。 其中包含各種自訂專案檔和命令檔，可示範如何控制和操作組建和部署程式。 本教學課程稍後會詳細說明這些功能。

在概念層級中，解決方案的元件會與下列內容配合：

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> 雖然 ASP.NET MVC 3 web 應用程式使用 ASP.NET 成員資格提供者，但 web 應用程式中的所有頁面都允許匿名存取。 這顯然不是實際的設定。 不過，此解決方案是以這種方式設定，讓您可以更輕鬆地部署及測試解決方案，而不需要設定使用者帳戶和角色。

## <a name="deployment-challenges"></a>部署挑戰

Contact Manager 解決方案說明許多企業部署案例常見的幾種部署挑戰：

- 解決方案包含多個相依專案。 您需要同時部署這些專案。
- 您必須針對每個環境更新連接字串和服務端點，而且在許多情況下，這項資訊將無法供開發人員使用。
- 當您將**ContactManager**資料庫部署至預備和生產環境時，您需要在後續部署中保留現有的資料。
- 當您部署 ASP.NET 應用程式服務資料庫時，您需要部署一些設定資料，但省略任何使用者帳戶資料。
- 專案包含一些不應部署的檔案和資料夾。 您必須從部署程式中排除這些檔案和資料夾。
- 解決方案需要支援從 Team Foundation Server （TFS）組建伺服器進行自動化部署。

## <a name="conclusion"></a>結論

本主題提供了 Contact Manager 解決方案的高階總覽，並找出許多企業部署案例通用的一些固有部署挑戰。 本教學課程中的其餘主題將說明您可以用來滿足這些挑戰的一些技巧。

下一個主題[設定 Contact Manager 解決方案](setting-up-the-contact-manager-solution.md)，說明如何在開發人員工作站上下載並執行解決方案。

> [!div class="step-by-step"]
> [上一頁](web-deployment-in-the-enterprise.md)
> [下一頁](setting-up-the-contact-manager-solution.md)
