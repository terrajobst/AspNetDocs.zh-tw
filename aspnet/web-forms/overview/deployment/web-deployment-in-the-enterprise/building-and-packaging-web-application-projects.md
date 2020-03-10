---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
title: 建立和封裝 Web 應用程式專案 |Microsoft Docs
author: jrjlee
description: 當您想要將 web 應用程式專案部署到遠端伺服器環境時，您的第一項工作就是建立專案並產生 web 部署套件 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 94e92f80-a7e3-4d18-9375-ff8be5d666ac
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
msc.type: authoredcontent
ms.openlocfilehash: 1d0ee0264ce6461d7b0159f1a44de4de31e2d079
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78573917"
---
# <a name="building-and-packaging-web-application-projects"></a>建置及封裝 Web 應用程式專案

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 當您想要將 web 應用程式專案部署到遠端伺服器環境時，您的第一項工作就是建立專案並產生 web 部署封裝。 本主題描述 web 應用程式專案的組建進程如何運作。 特別是，它會說明：
> 
> - Web 發佈管線（WPP）如何擴充組建進程以包含部署功能。
> - Internet Information Services （IIS） Web 部署工具（Web Deploy）如何將您的 web 應用程式轉換成部署套件。
> - 組建和封裝程式的運作方式，以及所建立的檔案。

在 Visual Studio 2010 中，WPP 支援 web 應用程式專案的組建和部署流程。 WPP 會提供一組 Microsoft Build Engine （MSBuild）目標，以擴充 MSBuild 的功能，並讓它與 Web Deploy 整合。 在 Visual Studio 中，您可以在 web 應用程式專案的屬性頁上看到此延伸功能。 [**封裝/發行**] 網頁連同 [**封裝/發行 SQL** ] 頁面，可讓您設定 Web 應用程式專案如何封裝，以在組建程式完成時進行部署。

![](building-and-packaging-web-application-projects/_static/image1.png)

## <a name="how-does-the-wpp-work"></a>WPP 如何運作？

如果您查看以為C#基礎之 web 應用程式專案的專案檔，您可以看到它匯入兩個 .targets 檔案。

[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample1.xml)]

第一個匯**入**語句通用於所有視覺C#專案。 這個*檔案，包括*視覺效果C#特有的目標和工作。 例如，這裡會C#叫用編譯器（**Csc**）工作。 然後， *microsoft 的 CSharp .targets*檔案會匯入*microsoft Common .targets*檔案。 這會定義所有專案通用的目標，例如**組建**、**重建**、**執行**、**編譯**和**清除**。 第二個**Import**語句是 web 應用程式專案特有的。 然後， *WebApplication*檔案會匯入*microsoft. web.config*檔案。 *Microsoft. web.config*檔案基本上*是*WPP。 它會定義會叫用 Web Deploy 來完成各種部署工作的目標，例如**封裝**和**MSDeployPublish**。

若要瞭解如何使用這些額外的目標，請在 Contact Manager 範例解決方案中開啟*Publish*檔案，並查看**BuildProjects**目標。

[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample2.xml)]

此目標會使用**MSBuild**工作來建立各種專案。 請注意**DeployOnBuild**和**DeployTarget**屬性：

- **DeployOnBuild = true**屬性基本上表示「我想要在組建成功完成時執行其他目標」。
- 當**DeployOnBuild**屬性等於**True**時， **DeployTarget**屬性會識別您想要執行的目標名稱。 在此情況下，您要指定在建立專案之後，MSBuild 才會執行**封裝**目標。

**封裝**目標會定義在*Microsoft* web.config 檔案中。 基本上，此目標會接受 web 應用程式專案的組建輸出，並將它轉換成可發行至 IIS web 伺服器的 web 部署封裝。

> [!NOTE]
> 若要在 Visual Studio 2010 中查看專案檔（例如<em>ContactManager</em>），您必須先從方案中卸載專案。 在 [<strong>方案總管</strong>] 視窗中，以滑鼠右鍵按一下專案節點，然後按一下<strong>[卸載專案</strong>]。 再次以滑鼠右鍵按一下專案節點，然後按一下 [<strong>編輯</strong><em>[專案檔]]</em>）。 專案檔會以其原始 XML 格式開啟。 當您完成時，請記得重載專案。  
> 如需有關 MSBuild 目標、工作和匯<strong>入</strong>語句的詳細資訊，請參閱[瞭解專案檔案](understanding-the-project-file.md)。 如需更深入的專案檔和 WPP 簡介，請參閱[Microsoft Build Engine 內：使用 MSBuild 和 Team Foundation Build](http://amzn.com/0735645248) By Sayed Ibrahim Hashimi 和 William BARTHOLOMEW，ISBN：978-0-7356-4524-0。

## <a name="what-is-a-web-deployment-package"></a>什麼是 Web 部署套件？

當您使用 Visual Studio 2010 或直接使用 MSBuild 來建立和部署 web 應用程式專案時，最後的結果通常是*web 部署套件*。 Web 部署套件是一個 .zip 檔案。 其中包含 IIS 和 Web Deploy 為了重新建立 Web 應用程式所需的所有專案，包括：

- Web 應用程式的已編譯輸出，包括內容、資源檔、設定檔、JavaScript 和級聯樣式表（CSS）資源等等。
- 您的 web 應用程式專案的元件，以及方案中任何參考的專案。
- SQL 腳本，用來產生您要使用 web 應用程式部署的任何資料庫。

一旦產生 web 部署套件之後，您就可以透過各種方式將它發佈至 IIS web 伺服器。 例如，您可以將目標設為遠端代理程式服務或目的地 web 伺服器上的 Web Deploy 處理常式，從 Web Deploy 遠端部署它，或者您可以使用 IIS 管理員，在目的地 web 伺服器上手動匯入封裝。 如需這些部署方法的詳細資訊，請參閱[選擇正確的 Web 部署方法](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)。

## <a name="how-does-the-build-process-work"></a>組建流程如何運作？

這會顯示當您建立並封裝 web 應用程式專案時，會發生什麼情況：

![](building-and-packaging-web-application-projects/_static/image2.png)

當您建立 web 應用程式專案時，組建進程會產生名為 *[專案名稱] 的檔案。SourceManifest*。 連同專案檔和組建輸出，這也是 *。SourceManifest*會告訴 Web Deploy 它必須包含在 Web 部署套件中的內容。 Web Deploy 會使用這些輸入，產生名為 *[專案名稱] .zip*的 Web 部署套件。

在 web 部署套件中，組建程式會產生兩個可協助您使用套件的檔案：

- *.Deploy*檔案包含一組參數化 Web Deploy （msdeploy.exe）命令，可將您的 Web 部署套件發佈至遠端 IIS Web 服務器。 以適當的參數執行 *.deploy*檔案，通常可提供更快速且更輕鬆的替代方法，以手動方式自行建立 msdeploy.exe 命令。
- *SetParameters*會提供一組參數值給 msdeploy.exe 命令。 這些值包括您要部署封裝之 IIS web 應用程式的名稱、 *web.config*檔案中所定義之任何服務端點和連接字串的值，以及專案屬性頁面上定義的任何部署屬性值等屬性。

*SetParameters*是管理部署程式的關鍵。 這個檔案是根據 web 應用程式專案的內容動態產生的。 例如，如果您將連接字串加入*至 web.config 檔案*，則組建程式會自動偵測連接字串、據以參數化部署，並在*SetParameters*中建立專案，以讓您修改連接字串，做為部署程式的一部分。 下一個主題設定[Web 封裝部署的參數](configuring-parameters-for-web-package-deployment.md)、詳細說明此檔案的角色，並說明在組建和部署期間修改該檔案的各種方式。

> [!NOTE]
> 在 Visual Studio 2010 中，WPP 不支援在封裝之前先行編譯 web 應用程式中的頁面。 下一個版本的 Visual Studio 和 WPP 會包含將 web 應用程式先行編譯為封裝選項的功能。

## <a name="conclusion"></a>結論

本主題提供 Visual Studio 2010 中 web 應用程式專案的組建和封裝程式的總覽。 其中描述了 WPP 如何讓您從 MSBuild 叫用 Web Deploy 命令，並說明組建和封裝程式的運作方式。

建立 web 部署套件之後，下一步就是部署它。 如需這種情況的詳細資訊，請參閱設定[Web 套件部署的參數](configuring-parameters-for-web-package-deployment.md)和[部署 web](deploying-web-packages.md)封裝。

## <a name="further-reading"></a>進一步閱讀

本教學課程中的下一個主題，設定[Web 封裝部署](configuring-parameters-for-web-package-deployment.md)和[部署 Web](deploying-web-packages.md)封裝的參數，提供如何使用您所建立之 web 套件的指引。 本系列的最後一個教學課程[Advanced Enterprise Web Deployment](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)，提供如何自訂和疑難排解封裝程式的指引。

如需更深入的專案檔和 WPP 簡介，請參閱[Microsoft Build Engine 內：使用 MSBuild 和 Team Foundation Build](http://amzn.com/0735645248) By Sayed Ibrahim Hashimi 和 William BARTHOLOMEW，ISBN：978-0-7356-4524-0。

> [!div class="step-by-step"]
> [上一頁](understanding-the-build-process.md)
> [下一頁](configuring-parameters-for-web-package-deployment.md)
