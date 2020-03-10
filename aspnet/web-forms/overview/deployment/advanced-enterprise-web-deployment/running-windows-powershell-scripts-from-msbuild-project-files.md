---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: 正在從 MSBuild 專案檔執行 Windows PowerShell 腳本 |Microsoft Docs
author: jrjlee
description: 本主題說明如何在組建和部署程式中執行 Windows PowerShell 腳本。 您可以在本機執行腳本（換句話說，在 [b ...]
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: 7b09c07b8b7c2a61ca534f7a66a929593f3d04ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548507"
---
# <a name="running-windows-powershell-scripts-from-msbuild-project-files"></a>從 MSBuild 專案檔執行 Windows PowerShell 指令碼

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題說明如何在組建和部署程式中執行 Windows PowerShell 腳本。 您可以在本機執行腳本（換句話說，在組建伺服器上）或從遠端執行（例如，在目的地 web 伺服器或資料庫伺服器上）。
> 
> 有很多原因會讓您想要執行部署後的 Windows PowerShell 腳本。 例如，您可能要：
> 
> - 將自訂事件來源新增至登錄。
> - 產生上傳的檔案系統目錄。
> - 清除組建目錄。
> - 將專案寫入自訂記錄檔。
> - 將邀請使用者的電子郵件傳送至新布建的 web 應用程式。
> - 建立具有適當許可權的使用者帳戶。
> - 設定 SQL Server 實例間的複寫。
> 
> 本主題將說明如何從 Microsoft Build Engine （MSBuild）專案檔中的自訂目標，在本機和遠端執行 Windows PowerShell 腳本。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="task-overview"></a>工作總覽

若要在自動化或單一步驟的部署程式中執行 Windows PowerShell 腳本，您必須完成下列高階工作：

- 將 Windows PowerShell 腳本新增至您的方案和原始檔控制。
- 建立命令來叫用您的 Windows PowerShell 腳本。
- 在您的命令中，將任何保留的 XML 字元轉義。
- 在您的自訂 MSBuild 專案檔中建立目標，並使用**Exec**工作來執行命令。

本主題將說明如何執行這些程式。 本主題中的工作和逐步解說假設您已熟悉 MSBuild 目標和屬性，並瞭解如何使用自訂 MSBuild 專案檔來驅動組建和部署程式。 如需詳細資訊，請參閱[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔和[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式。

## <a name="creating-and-adding-windows-powershell-scripts"></a>建立和新增 Windows PowerShell 腳本

本主題中的工作會使用名為**LogDeploy**的範例 Windows PowerShell 腳本，說明如何從 MSBuild 執行腳本。 **LogDeploy**腳本包含簡單的函式，可將單行專案寫入記錄檔：

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.ps1)]

**LogDeploy**腳本接受兩個參數。 第一個參數代表您要加入專案之記錄檔的完整路徑，而第二個參數代表您要在記錄檔中記錄的部署目的地。 當您執行腳本時，它會以下列格式在記錄檔中加入一行：

[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]

若要將**LogDeploy**腳本提供給 MSBuild 使用，您必須：

- 將腳本加入至原始檔控制。
- 將腳本新增至您在 Visual Studio 2010 的方案中。

無論您是否計畫在組建伺服器或遠端電腦上執行腳本，都不需要使用您的解決方案內容部署腳本。 其中一個選項是將腳本新增至方案資料夾。 在「連絡人管理員」範例中，因為您想要在部署程式中使用 Windows PowerShell 腳本，所以將腳本新增至「發佈解決方案」資料夾是合理的做法。

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

解決方案資料夾的內容會複製到組建伺服器做為來源材質。 不過，它們不會構成任何專案輸出的一部分。

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a>在組建伺服器上執行 Windows PowerShell 腳本

在某些情況下，您可能會想要在建立專案的電腦上執行 Windows PowerShell 腳本。 例如，您可以使用 Windows PowerShell 腳本來清除組建資料夾，或將專案寫入自訂記錄檔。

就語法而言，從 MSBuild 專案檔執行 Windows PowerShell 腳本與從一般命令提示字元執行 Windows PowerShell 腳本的方式相同。 您必須叫用 powershell .exe 可執行檔，並使用 **– command**參數來提供您想要 Windows powershell 執行的命令。 （在 Windows PowerShell v2 中，您也可以使用 **– file**參數）。 命令應採用下列格式：

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]

例如:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]

如果腳本的路徑包含空格，您必須以單引號括住檔案路徑，並在前面加上連字號。 您不能使用雙引號，因為您已經使用它們來括住命令：

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]

當您從 MSBuild 叫用此命令時，還有一些額外的考慮。 首先，您應該包含 **–非互動式**旗標，以確保腳本會以安靜的模式執行。 接下來，您應該包含 **– ExecutionPolicy**旗標與適當的引數值。 這會指定 Windows PowerShell 套用至腳本的執行原則，並可讓您覆寫預設的執行原則，這可能會導致腳本無法執行。 您可以從下列引數值中選擇：

- 不**受限制**的值可讓 Windows PowerShell 執行您的腳本，不論腳本是否已簽署。
- **RemoteSigned**的值可讓 Windows PowerShell 執行在本機電腦上建立的未簽署腳本。 不過，在其他地方建立的腳本必須經過簽署。 （實際上，在組建伺服器上，您不太可能在本機建立 Windows PowerShell 腳本）。
- **AllSigned**的值可讓 Windows PowerShell 只執行已簽署的腳本。

預設執行原則是**受限制**的，這可防止 Windows PowerShell 執行任何腳本檔案。

最後，您必須將任何在 Windows PowerShell 命令中發生的保留 XML 字元加以轉義：

- 將單引號取代**為&amp;** 的
- 將雙引號取代為 **&amp;**
- 將符號取代為 **&amp;amp;**

- 當您進行這些變更時，您的命令會如下所示：

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]

在您的自訂 MSBuild 專案檔中，您可以建立新的目標，並使用**Exec**工作來執行此命令：

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]

在此範例中，請注意：

- 任何變數（例如參數值和 Windows PowerShell 可執行檔的位置）都會宣告為 MSBuild 屬性。
- 包含的條件可讓使用者從命令列覆寫這些值。
- **MSDeployComputerName**屬性會在專案檔中的其他位置宣告。

當您執行此目標做為組建程式的一部分時，Windows PowerShell 將會執行您的命令，並將記錄專案寫入您指定的檔案。

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a>在遠端電腦上執行 Windows PowerShell 腳本

Windows PowerShell 能夠透過[Windows 遠端管理](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx)（WinRM）在遠端電腦上執行腳本。 若要這樣做，您需要使用[Invoke 命令](https://technet.microsoft.com/library/dd347578.aspx)Cmdlet。 這可讓您針對一或多部遠端電腦執行腳本，而不需要將腳本複製到遠端電腦。 任何結果都會傳回您執行腳本的本機電腦。

> [!NOTE]
> 使用**Invoke 命令**Cmdlet 在遠端電腦上執行 Windows PowerShell 腳本之前，您必須先設定 WinRM 接聽程式以接受遠端訊息。 若要這麼做，您可以在遠端電腦上執行**winrm quickconfig**命令。 如需詳細資訊，請參閱[Windows 遠端管理的安裝和](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx)設定。

在 Windows PowerShell 視窗中，您可以使用此語法在遠端電腦上執行**LogDeploy**腳本：

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]

> [!NOTE]
> 有各種其他方法可以使用**Invoke 命令**來執行腳本檔案，但當您需要提供參數值和管理具有空格的路徑時，這個方法是最直接的方式。

當您從命令提示字元執行此動作時，您必須叫用 Windows PowerShell 可執行檔，並使用 **– command**參數來提供您的指示：

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]

如先前所述，當您從 MSBuild 執行命令時，您必須提供一些額外的參數，並將任何保留的 XML 字元換行：

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]

最後，您可以像之前一樣，在自訂 MSBuild 目標內使用**Exec**工作來執行命令：

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]

當您執行此目標做為組建程式的一部分時，Windows PowerShell 會在您于 **– computername**引數中指定的電腦上執行您的腳本。

## <a name="conclusion"></a>結論

本主題說明如何從 MSBuild 專案檔執行 Windows PowerShell 腳本。 您可以使用此方法，在自動或單一步驟的組建和部署程式中，于本機或遠端電腦上執行 Windows PowerShell 腳本。

## <a name="further-reading"></a>進一步閱讀

如需簽署 Windows PowerShell 腳本和管理執行原則的指引，請參閱執行[Windows Powershell 腳本](https://technet.microsoft.com/library/ee176949.aspx)。 如需有關從遠端電腦執行 Windows PowerShell 命令的指引，請參閱執行[遠端命令](https://technet.microsoft.com/library/dd819505.aspx)。

如需使用自訂 MSBuild 專案檔控制部署程式的詳細資訊，請參閱[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔和[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式。

> [!div class="step-by-step"]
> [上一頁](taking-web-applications-offline-with-web-deploy.md)
> [下一頁](troubleshooting-the-packaging-process.md)
