---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: 封裝程式的疑難排解 |Microsoft Docs
author: jrjlee
description: 本主題描述如何使用 M ... 中的 EnablePackageProcessLoggingAndAssert 屬性，來收集有關封裝程式的詳細資訊。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 8ad649dfff085a8774cc13c11d8a3e3d48277d66
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628209"
---
# <a name="troubleshooting-the-packaging-process"></a>針對封裝程序進行疑難排解

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何使用 Microsoft Build Engine （MSBuild）中的**EnablePackageProcessLoggingAndAssert**屬性，來收集有關封裝程式的詳細資訊。
> 
> 當您將**EnablePackageProcessLoggingAndAssert**屬性設定為**true**時，MSBuild 將會：
> 
> - 將有關封裝程式的其他資訊新增至組建記錄檔。
> - 在某些情況下記錄錯誤，例如，如果在封裝清單中找到重複的檔案。
> - 在*專案名稱*\_封裝資料夾中建立記錄檔目錄，並使用它來記錄您要封裝之檔案的相關資訊。
> 
> 如果封裝程式失敗，或是您的 web 部署套件未包含您預期的檔案，您可以使用這項資訊來疑難排解程式，並找出發生問題的位置。
> 
> > [!NOTE]
> > 只有當您使用**Debug**設定來建立專案時， **EnablePackageProcessLoggingAndAssert**屬性才有效。 在其他設定中會忽略屬性。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a>瞭解 EnablePackageProcessLoggingAndAssert 屬性

[建立和封裝 Web 應用程式專案](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)說明 Web 發佈管線（WPP）如何提供一組 msbuild 目標，以擴充 msbuild 的功能，並讓它與 INTERNET INFORMATION SERVICES （IIS） Web 部署工具（Web Deploy）整合。 當您封裝 web 應用程式專案時，就是叫用 WPP 目標。

其中許多的 WPP 目標包括當**EnablePackageProcessLoggingAndAssert**屬性設定為**true**時，會記錄其他資訊的條件式邏輯。 例如，如果您檢查**封裝**目標，您可以看到它會建立額外的記錄檔目錄，並在**EnablePackageProcessLoggingAndAssert**等於**true**時，將檔案清單寫入文字檔。

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]

> [!NOTE]
> WPP 目標是在% PROGRAMFILES （x86）% \ MSBuild\Microsoft\VisualStudio\v10.0\Web 資料夾中的*web.config*檔案中定義。 您可以開啟此檔案，並在 Visual Studio 2010 或任何 XML 編輯器中檢查目標。 請小心不要修改檔案的內容。

## <a name="enabling-the-additional-logging"></a>啟用其他記錄

您可以透過各種方式提供**EnablePackageProcessLoggingAndAssert**屬性的值，視您建立專案的方式而定。

如果您從命令列建立專案，您可以提供**EnablePackageProcessLoggingAndAssert**屬性的值做為命令列引數：

[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]

如果您要使用自訂專案檔來建立專案，您可以在**MSBuild**工作的**Properties**屬性中包含**EnablePackageProcessLoggingAndAssert**值：

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]

如果您要使用 Team Foundation Server （TFS）組建定義來建立專案，您可以在 [ **MSBuild 引數**] 資料列中提供**EnablePackageProcessLoggingAndAssert**屬性的值：![](troubleshooting-the-packaging-process/_static/image1.png)

> [!NOTE]
> 如需建立和設定組建定義的詳細資訊，請參閱建立[支援部署的組建定義](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。

或者，如果您想要在每個組建中包含封裝，您可以修改 web 應用程式專案的專案檔，將**EnablePackageProcessLoggingAndAssert**屬性設定為**true**。 您應該將屬性新增至 .csproj 或. vbproj 檔案中的第一個**PropertyGroup**元素。

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]

## <a name="reviewing-the-log-files"></a>查看記錄檔

當您建立並封裝已將**EnablePackageProcessLoggingAndAssert**設定為**true**的 web 應用程式專案時，MSBuild 會在*專案名稱*\_封裝資料夾中，建立名為 Log 的其他資料夾。 記錄檔資料夾包含各種檔案：

![](troubleshooting-the-packaging-process/_static/image2.png)

您所看到的檔案清單會根據您的專案和組建程式中的內容而有所不同。 不過，這些檔案通常用來記錄在程式的各個階段中，由 WPP 收集來封裝的檔案清單：

- *PreExcludePipelineCollectFilesPhaseFileList*檔案會列出 MSBuild 在指定要排除的任何檔案移除之前，所收集的檔案。
- 移除指定排除的任何檔案之後， *AfterExcludeFilesFilesList*檔案會包含修改過的檔案清單。

    > [!NOTE]
    > 如需從封裝程式排除檔案和資料夾的詳細資訊，請參閱[從部署中排除檔案和資料夾](excluding-files-and-folders-from-deployment.md)。
- 在*執行任何 web.config*轉換之後， *AfterTransformWebConfig*檔案會列出收集以封裝的檔案。 在這份清單*中，任何*設定*特定的 web.config 轉換*檔案（例如*web.config*和 web.config）都會從要封裝的檔案清單中排除。 單一轉換的*web.config*會包含在其位置。
- 在*web.config 檔案*中的連接字串已參數化之後， *PostAutoParameterizationWebConfigConnectionStrings*檔案會包含檔案的清單。 此程式可讓您在部署封裝時，將連接字串取代為目標環境的正確設定。
- *Prepackage*包含要包含在封裝中的已完成檔案預先建立清單。

> [!NOTE]
> 其他記錄檔的名稱通常會對應至 WPP 目標。 您可以檢查% PROGRAMFILES （x86）% \ MSBuild\Microsoft\VisualStudio\v10.0\Web 資料夾中的*Microsoft. web.config*檔案來檢查這些目標。

如果您的網頁封裝內容不是您所預期，則在處理常式發生錯誤時，檢查這些檔案可能是很有用的方式。

## <a name="conclusion"></a>結論

本主題說明如何使用 MSBuild 中的**EnablePackageProcessLoggingAndAssert**屬性來進行封裝程式的疑難排解。 它說明了您可以將屬性值提供給組建進程的不同方式，並說明當您將屬性設定為**true**時所記錄的其他資訊。

## <a name="further-reading"></a>進一步閱讀

如需使用自訂 MSBuild 專案檔控制部署程式的詳細資訊，請參閱[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔和[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式。 如需 WPP 以及它如何管理封裝程式的詳細資訊，請參閱[建立和封裝 Web 應用程式專案](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)。 如需有關如何從 web 部署套件中排除特定檔案和資料夾的指引，請參閱[從部署中排除檔案和資料夾](excluding-files-and-folders-from-deployment.md)。

> [!div class="step-by-step"]
> [上一篇](running-windows-powershell-scripts-from-msbuild-project-files.md)
