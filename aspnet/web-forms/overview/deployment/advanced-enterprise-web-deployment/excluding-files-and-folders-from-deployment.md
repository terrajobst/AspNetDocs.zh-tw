---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
title: 從部署中排除檔案和資料夾 |Microsoft Docs
author: jrjlee
description: 本主題說明當您建立和封裝 web 應用程式專案時，如何從 web 部署套件排除檔案和資料夾。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f4cc2d40-6a78-429b-b06f-07d000d4caad
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
msc.type: authoredcontent
ms.openlocfilehash: a262ce43d7199fb1015d54d0b7c213857c360946
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544972"
---
# <a name="excluding-files-and-folders-from-deployment"></a>從部署中排除檔案與資料夾

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題說明當您建立和封裝 web 應用程式專案時，如何從 web 部署套件排除檔案和資料夾。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="overview"></a>概觀

當您在 Visual Studio 2010 中建立 web 應用程式專案時，Web 發佈管線（WPP）可讓您將已編譯的 web 應用程式封裝成可部署的 web 套件，藉此擴充此組建進程。 接著，您可以使用 Internet Information Services （IIS） Web 部署工具（Web Deploy）將此 web 封裝部署到遠端 IIS Web 服務器，或透過 IIS 管理員以手動方式匯入 web 封裝。 [建立和封裝 Web 應用程式專案](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)中會說明此封裝程式。

那麼，您要如何控制要包含在 web 套件中的內容呢？ Visual Studio 中的專案設定，透過基礎專案檔，為許多案例提供足夠的控制。 不過，在某些情況下，您可能會想要將 web 套件的內容量身打造到特定的目的地環境。 例如，當您將應用程式部署至測試環境時，可能會想要包含記錄檔的資料夾，但當您將應用程式部署至預備或生產環境時，會將資料夾排除。 本主題將示範如何執行這種作法。

## <a name="what-gets-included-by-default"></a>預設會包含哪些專案？

當您在 Visual Studio 中設定 web 應用程式專案屬性時，[**封裝/發行**] 網頁上的 [**要部署的專案**] 清單可讓您指定要包含在 web 部署套件中的內容。 根據預設，這會設定為**只有執行此應用程式所需**的檔案。

![](excluding-files-and-folders-from-deployment/_static/image1.png)

當您**只選擇執行此應用程式所需**的檔案時，WPP 會嘗試判斷哪些檔案應該加入至 web 封裝。 包括：

- 專案的所有組建輸出。
- 任何以**內容**的組建動作標記的檔案。

> [!NOTE]
> 決定要包含哪些檔案的邏輯會包含在這個檔案中：   
> *%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ OnlyFilesToRunTheApp 的目標*

## <a name="excluding-specific-files-and-folders"></a>排除特定的檔案和資料夾

在某些情況下，您會想要更精細地控制要部署哪些檔案和資料夾。 如果您知道要事先排除哪些檔案，而且排除適用于所有目的地環境，您只要將每個檔案的**組建動作**設定為 [**無**] 即可。

**若要從部署中排除特定檔案**

1. 在 [**方案總管**] 視窗中，以滑鼠右鍵按一下該檔案，然後按一下 [**屬性**]。
2. 在 [**屬性**] 視窗的 [**組建動作**] 資料列中，選取 [**無**]。

不過，這種方法並不一定方便。 例如，您可能會想要根據您的目的地環境以及外部 Visual Studio，來改變所包含的檔案和資料夾。 例如，在 Contact Manager 範例解決方案中，查看 ContactManager 專案的內容：

![](excluding-files-and-folders-from-deployment/_static/image2.png)

- 內部資料夾包含一些 SQL 腳本，供開發人員用來建立、卸載和填入本機資料庫以供開發之用。 此資料夾中的任何內容都應該部署至預備或生產環境。
- Scripts 資料夾包含數個 JavaScript 檔案。 其中包含許多檔案，純粹是為了支援在 Visual Studio 中進行調試或提供 IntelliSense。 這些檔案中的某些檔案不應部署至預備或生產環境。 不過，您可能會想要將它們部署至開發人員測試環境，以協助進行疑難排解。

雖然您可以操作專案檔來排除特定的檔案和資料夾，但還是有更簡單的方法。 WPP 包含一個機制，藉由建立名為**ExcludeFromPackageFolders**和**ExcludeFromPackageFiles**的專案清單來排除檔案和資料夾。 您可以將自己的專案新增至這些清單，以擴充此機制。 若要這樣做，您需要完成下列高階步驟：

1. 在與專案檔相同的資料夾中，建立名為 *[project name]* 的自訂專案檔。

    > [!NOTE]
    > &#x2014;.Csproj &#x2014;.targets 檔案必須與您的 web 應用程式專案檔案位於相同的資料夾中，例如*ContactManager*，而不是與您用來控制組建和部署程式的任何自訂專案檔位於相同的資料夾中。
2. 在 *.targets*檔案中，新增**ItemGroup**元素。
3. 在**ItemGroup**元素中，新增**ExcludeFromPackageFolders**和**ExcludeFromPackageFiles**專案，以視需要排除特定的檔案和資料夾。

這是這個*wpp .targets*檔案的基本結構：

[!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample1.xml)]

請注意，每個專案都包含名為**FromTarget**的專案中繼資料元素。 這是不會影響組建進程的選擇性值。它只是用來指出當有人審查組建記錄檔時，會省略特定檔案或資料夾的原因。

## <a name="excluding-files-and-folders-from-a-web-package"></a>從 Web 套件排除檔案和資料夾

下一個程式會示範如何將 *.targets*檔案加入至 web 應用程式專案，以及如何在建立專案時，使用檔案從 web 封裝中排除特定的檔案和資料夾。

**從 web 部署套件排除檔案和資料夾**

1. 在 Visual Studio 2010 中開啟您的方案。
2. 在 [**方案總管**] 視窗中，以滑鼠右鍵按一下您的 web 應用程式專案節點（例如**ContactManager**），指向 [**加入**]，然後按一下 [**新增專案**]。
3. 在 [**加入新專案**] 對話方塊中，選取 [ **XML**檔案] 範本。
4. 在 [**名稱**] 方塊中，輸入 *[project Name] * * *. wpp. .targets** （例如， **ContactManager**），然後按一下 [**新增**]。

    ![](excluding-files-and-folders-from-deployment/_static/image3.png)

    > [!NOTE]
    > 如果您將新的專案加入至專案的根節點，該檔案會建立在與專案檔相同的資料夾中。 您可以在 Windows Explorer 中開啟資料夾來確認這一點。
5. 在檔案中，新增**專案**元素和**ItemGroup**元素：

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample2.xml)]
6. 如果您想要從 web 封裝排除資料夾，請將**ExcludeFromPackageFolders**元素新增至**ItemGroup**元素：

   1. 在 [**包含**] 屬性中，提供您要排除的檔案夾清單（以分號分隔）。
   2. 在**FromTarget**中繼資料專案中，提供有意義的值來指出排除資料夾的原因，*例如檔案名。*

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample3.xml)]
7. 如果您想要從 web 封裝排除檔案，請將**ExcludeFromPackageFiles**元素新增至**ItemGroup**元素：

   1. 在 [**包含**] 屬性中，提供您想要排除的檔案清單（以分號分隔）。
   2. 在**FromTarget**中繼資料元素中，提供有意義的值來指出排除檔案的原因，*例如檔案名。*

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample4.xml)]
8. *[Project name]. wpp .targets*檔案現在看起來應該像這樣：

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample5.xml)]
9. 儲存並關閉 *[project name]. wpp .targets*檔案。

下一次建立和封裝 web 應用程式專案時，WPP 會自動偵測 *.targets*檔案。 您指定的任何檔案和資料夾都不會包含在 web 封裝中。

## <a name="conclusion"></a>結論

本主題說明如何在建立 web 套件時，排除特定的檔案和資料夾，方法是在與 web 應用程式專案檔相同的資料夾中建立自訂的 *. wpp .targets*檔案。

## <a name="further-reading"></a>進一步閱讀

如需使用自訂 Microsoft Build Engine （MSBuild）專案檔控制部署程式的詳細資訊，請參閱[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔和[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式。 如需封裝和部署程式的詳細資訊，請參閱[建立和封裝 Web 應用程式專案](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)、設定[web 封裝部署的參數](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)和[部署 web 封裝](../web-deployment-in-the-enterprise/deploying-web-packages.md)。

> [!div class="step-by-step"]
> [上一頁](deploying-membership-databases-to-enterprise-environments.md)
> [下一頁](taking-web-applications-offline-with-web-deploy.md)
