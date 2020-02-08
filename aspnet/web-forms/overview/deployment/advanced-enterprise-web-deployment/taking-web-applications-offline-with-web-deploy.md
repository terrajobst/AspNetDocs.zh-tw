---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
title: 使用 Web Deploy 讓 Web 應用程式離線 |Microsoft Docs
author: jrjlee
description: 本主題描述如何使用 Internet Information Services （IIS） Web Depl，讓 web 應用程式在自動化部署期間離線。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 3e9f6e7d-8967-4586-94d5-d3a122f12529
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
msc.type: authoredcontent
ms.openlocfilehash: ba60664a0c3daa0650cd7e7cfc4ab9da08df3440
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075134"
---
# <a name="taking-web-applications-offline-with-web-deploy"></a>使用 Web Deploy 讓 Web 應用程式離線

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何使用 Internet Information Services （IIS） Web 部署工具（Web Deploy），讓 web 應用程式在自動化部署期間離線。 流覽至 web 應用程式的使用者會被重新導向至*應用程式\_離線 .htm*檔案，直到部署完成為止。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="task-overview"></a>工作總覽

在許多情況下，您會想要在變更相關元件（例如資料庫或 web 服務）時讓 web 應用程式離線。 一般來說，在 IIS 和 ASP.NET 中，您可以在 IIS 網站或 web 應用程式的根資料夾中，將名為 App 的檔案 *\_離線*，藉此完成這項操作。 *應用程式\_離線的 .htm*檔案是標準的 HTML 檔案，而且通常會包含一則訊息，告知使用者網站暫時無法使用，因為進行維護。 雖然*應用程式\_離線 .htm*檔案存在於網站的根資料夾中，但 IIS 會自動將所有要求重新導向至檔案。 當您完成更新時，您會移除*應用程式\_離線 .htm*檔案，而網站會如往常般繼續提供要求。

當您使用 Web Deploy 對目標環境執行自動化或單一步驟部署時，您可能會想要將*應用程式\_的離線 .htm*檔案加入至您的部署流程。 若要這樣做，您必須完成下列高階工作：

- 在您用來控制部署程式的 Microsoft Build Engine （MSBuild）專案檔中，建立 MSBuild 目標，以在任何部署工作開始之前，將*應用程式\_離線 .htm*檔案複製到目的地伺服器。
- 新增另一個 MSBuild 目標，以便在所有部署工作都完成時，從目的地伺服器移除*應用程式\_離線 .htm*檔案。
- 在 web 應用程式專案中，建立一個*wpp .targets*檔案，以確保在叫用 Web Deploy 時，會將*應用程式\_離線的 .htm*檔案加入至部署套件。

本主題將說明如何執行這些程式。 本主題中的工作和逐步解說假設您已經建立一個方案，其中包含至少一個 web 應用程式專案，而且您使用自訂專案檔來控制部署程式，如[企業中的 Web 部署中](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)所述。 或者，您可以使用[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)範例解決方案，遵循主題中的範例。

## <a name="adding-an-app_offline-file-to-a-web-application-project"></a>將應用程式\_離線檔案新增至 Web 應用程式專案

您需要完成的第一項工作是將*應用程式\_離線*檔案新增至您的 web 應用程式專案：

- 若要防止檔案干擾開發程式（您不想讓應用程式永久離線），您應該將應用程式以外的其他專案呼叫 *\_離線的 .htm*。 例如，您可以將檔案*應用程式*命名為 offline-template，\_為 .htm。
- 若要防止檔案依預設部署，您應該將 [組建] 動作設定為 [**無**]。

**將應用程式\_離線檔案加入至 web 應用程式專案**

1. 在 Visual Studio 2010 中開啟您的方案。
2. 在 [**方案總管**] 視窗中，以滑鼠右鍵按一下您的 web 應用程式專案，指向 [**加入**]，然後按一下 [**新增專案**]。
3. 在 [**加入新專案**] 對話方塊中，選取 [ **HTML 網頁**]。
4. 在 [**名稱**] 方塊中，輸入**App\_offline-template**，然後按一下 [**新增**]。

    ![](taking-web-applications-offline-with-web-deploy/_static/image1.png)
5. 新增一些簡單的 HTML 以通知使用者應用程式無法使用，然後儲存檔案。 請勿包含任何伺服器端標記（例如，任何前面加上 "asp：" 的標記）。 

    ![](taking-web-applications-offline-with-web-deploy/_static/image2.png)
6. 在 [**方案總管**] 視窗中，以滑鼠右鍵按一下新的檔案，然後按一下 [**屬性**]。
7. 在 [**屬性**] 視窗的 [**組建動作**] 資料列中，選取 [**無**]。

    ![](taking-web-applications-offline-with-web-deploy/_static/image3.png)

## <a name="deploying-and-deleting-an-app_offline-file"></a>部署和刪除應用程式\_離線檔案

下一個步驟是修改您的部署邏輯，在部署程式開始時將檔案複製到目的地伺服器，並在結束時將它移除。

> [!NOTE]
> 下一個程式假設您是使用自訂的 MSBuild 專案檔來控制您的部署程式，如[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述。 如果您要從 Visual Studio 直接部署，則必須使用不同的方法。 Sayed Ibrahim Hashimi 說明[如何讓您的 Web 應用程式在發佈期間離線](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx)的其中一種方法。

若要將*應用程式\_離線*檔案部署到目的地 IIS 網站，您必須使用[Web Deploy **contentPath**提供者](https://technet.microsoft.com/library/dd569034(WS.10).aspx)叫用 msdeploy.exe。 **ContentPath**提供者同時支援實體目錄路徑和 iis 網站或應用程式路徑，這讓它成為在 Visual Studio 專案資料夾與 iis web 應用程式之間同步處理檔案的理想選擇。 若要部署檔案，您的 Msdeploy.exe 命令應如下所示：

[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample1.cmd)]

若要在部署程式結束時從目的地網站移除檔案，您的 Msdeploy.exe 命令應如下所示：

[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample2.cmd)]

若要將這些命令自動化為組建和部署程式的一部分，您需要將它們整合到您的自訂 MSBuild 專案檔中。 下一個程式描述如何執行此動作。

**若要部署和刪除應用程式\_離線檔案**

1. 在 Visual Studio 2010 中，開啟可控制部署程式的 MSBuild 專案檔。 在[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)範例解決方案中，這是*Publish*檔案。
2. 在根**專案**元素中，建立新的**PropertyGroup**元素，以儲存*應用程式\_離線*部署的變數：

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample3.xml)]
3. **SourceRoot**屬性是在*Publish*檔案中的其他位置定義的。 它會指出相對於目前路徑&#x2014;之來源內容的根資料夾位置（相對於*Publish*檔案的位置）。
4. **ContentPath**提供者不會接受相對檔案路徑，因此您必須先取得原始程式檔的絕對路徑，才能進行部署。 您可以使用[ConvertToAbsolutePath](https://msdn.microsoft.com/library/bb882668.aspx)工作來執行這項操作。
5. 新增名為**GetAppOfflineAbsolutePath**的新**目標**元素。 在此目標中，使用**ConvertToAbsolutePath**工作來取得應用程式的絕對路徑，\_您專案資料夾中的*離線範本*檔案。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample4.xml)]
6. 此目標會採用應用程式的相對路徑\_專案資料夾中的*離線範本*檔案，並將其儲存至新的屬性，做為絕對檔案路徑。 **BeforeTargets**屬性會指定您要在下一個步驟中建立的**DeployAppOffline**目標之前，讓此目標執行。
7. 新增名為**DeployAppOffline**的新目標。 在此目標中，叫用將您的*應用程式部署\_離線*檔案到目的地 web 伺服器的 msdeploy.exe 命令。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample5.xml)]
8. 在此範例中， **ContactManagerIisPath**屬性是在專案檔中的其他位置定義的。 這只是 IIS 應用程式路徑，格式為 *[Iis 網站名稱]/[應用程式名稱]* 。 在目標中包含條件可讓使用者藉由變更屬性值或提供命令列參數，將*應用程式\_離線*部署切換為開啟或關閉。
9. 新增名為**DeleteAppOffline**的新目標。 在此目標中，叫用從目的地 web 伺服器移除*應用程式\_離線*檔案的 msdeploy.exe 命令。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample6.xml)]
10. 最後一項工作是在執行您的專案檔期間，于適當的時間點叫用這些新目標。 您可以透過各種方式來執行這項操作。 例如，在*Publish*檔案中， **FullPublishDependsOn**屬性會指定叫用**FullPublish**預設目標時，必須按照循序執行的目標清單。
11. 修改您的 MSBuild 專案檔，以在發佈程式中的適當時間點叫用**DeployAppOffline**和**DeleteAppOffline**目標。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample7.xml)]

當您執行自訂 MSBuild 專案檔時，*應用程式\_離線*檔案會在成功組建之後立即部署至伺服器。 完成所有部署工作之後，它就會從伺服器中刪除。

## <a name="adding-an-app_offline-file-to-deployment-packages"></a>將應用程式\_離線檔案新增至部署套件

根據您設定部署的方式，當您將 web 套件部署到目的地時，&#x2014;&#x2014;可能會自動刪除目的地 IIS web 應用程式（如 App）上任何現有的內容（例如*應用程式\_離線 .htm*檔案）。 若要確保*應用\_程式*在部署期間仍會保留在相同的位置，您必須將該檔案包含在 web 部署套件本身中，除了在部署程式開始時直接部署該檔案。

- 如果您已遵循本主題中先前的工作，則會將應用程式 *\_離線 .htm*檔案新增至您的 web 應用程式專案（我們使用了*應用程式\_offline-template*），而您會將組建動作設定為 [**無**]。 這些變更是防止檔案干擾開發和調試的必要變更。 因此，您必須自訂封裝程式，以確保 web 部署套件中會包含*應用程式\_離線的 .htm*檔案。

Web 發行管線（WPP）使用名為**FilesForPackagingFromProject**的專案清單，建立應該包含在 Web 部署套件中的檔案清單。 您可以將自己的專案新增到此清單中，以自訂 web 套件的內容。 若要這樣做，您需要完成下列高階步驟：

1. 在與專案檔相同的資料夾中，建立名為 *[project name]* 的自訂專案檔。

    > [!NOTE]
    > &#x2014;.Csproj &#x2014;.targets 檔案必須與您的 web 應用程式專案檔案位於相同的資料夾中，例如*ContactManager*，而不是與您用來控制組建和部署程式的任何自訂專案檔位於相同的資料夾中。
2. 在 *.targets*檔案中，建立在**CopyAllFilesToSingleFolderForPackage**目標*之前*執行的新 MSBuild 目標。 這是可建立要包含在封裝中之專案清單的 WPP 目標。
3. 在新的目標中，建立**ItemGroup**元素。
4. 在**ItemGroup**元素中，新增**FilesForPackagingFromProject**專案，並指定*應用程式\_離線 .htm*檔案。

*. Wpp .targets*檔案應如下所示：

[!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample8.xml)]

以下是此範例中的重點事項：

- **BeforeTargets**屬性會藉由指定應該緊接在**CopyAllFilesToSingleFolderForPackage**目標之前執行，將此目標插入至 WPP。
- **FilesForPackagingFromProject**專案會使用**DestinationRelativePath**中繼資料值，將*應用程式\_offline-template*中的檔案重新命名為*應用程式\_離線*，因為它已新增至清單。

下一個程式會示範如何將此*wpp .targets*檔案加入至 web 應用程式專案。

**將 .targets 檔案新增至 web 部署套件**

1. 在 Visual Studio 2010 中開啟您的方案。
2. 在 [**方案總管**] 視窗中，以滑鼠右鍵按一下您的 web 應用程式專案節點（例如**ContactManager**），指向 [**加入**]，然後按一下 [**新增專案**]。
3. 在 [**加入新專案**] 對話方塊中，選取 [ **XML**檔案] 範本。
4. 在 [**名稱**] 方塊中，輸入 *[project Name] * * *. wpp. .targets** （例如， **ContactManager**），然後按一下 [**新增**]。

    ![](taking-web-applications-offline-with-web-deploy/_static/image4.png)

    > [!NOTE]
    > 如果您將新的專案加入至專案的根節點，該檔案會建立在與專案檔相同的資料夾中。 您可以在 Windows Explorer 中開啟資料夾來確認這一點。
5. 在檔案中，新增先前所述的 MSBuild 標記。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample9.xml)]
6. 儲存並關閉 *[project name]. wpp .targets*檔案。

下一次建立和封裝 web 應用程式專案時，WPP 會自動偵測 *.targets*檔案。 *應用程式\_offline-template*會包含在產生的 web 部署套件中，作為*應用程式\_離線 .htm*。

> [!NOTE]
> 如果您的部署失敗，*應用程式\_離線 .htm*檔案會保留在原處，且您的應用程式會保持離線狀態。 這通常是所需的行為。 若要讓您的應用程式重新上線，您可以從 web 伺服器刪除*應用程式\_離線 .htm*檔案。 或者，如果您更正任何錯誤並執行部署成功，將會移除*應用程式\_離線的 .htm*檔案。

## <a name="conclusion"></a>結論

本主題說明如何在部署期間將 web 應用程式離線，方法是將*應用程式\_離線的 .htm*檔案發佈到目的地伺服器，並在結束時將它移除。 同時也涵蓋了如何在 web 部署套件中包含*應用程式\_離線 .htm*檔案。

## <a name="further-reading"></a>進階閱讀

如需封裝和部署程式的詳細資訊，請參閱[建立和封裝 Web 應用程式專案](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)、設定[web 封裝部署的參數](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)和[部署 web 封裝](../web-deployment-in-the-enterprise/deploying-web-packages.md)。

如果您直接從 Visual Studio 發行 web 應用程式，而不是使用這些教學課程中所述的自訂 MSBuild 專案檔方法，則在發行期間，您將需要使用稍微不同的方法讓應用程式離線流程.

> [!div class="step-by-step"]
> [上一頁](excluding-files-and-folders-from-deployment.md)
> [下一頁](running-windows-powershell-scripts-from-msbuild-project-files.md)
