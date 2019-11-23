---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
title: 瞭解專案檔 |Microsoft Docs
author: jrjlee
description: Microsoft Build Engine （MSBuild）專案檔案位於組建和部署程式的核心。 本主題一開始會說明 MSBuild 的概念總覽 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 07978d9d-341c-4524-bcba-62976f390f77
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
msc.type: authoredcontent
ms.openlocfilehash: 419fe51aaf65bddcc2c50380f099f842a8d9439c
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445696"
---
# <a name="understanding-the-project-file"></a>瞭解專案檔

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Microsoft Build Engine （MSBuild）專案檔案位於組建和部署程式的核心。 本主題一開始會概述 MSBuild 和專案檔的概念。 其中描述當您使用專案檔時，您會遇到的主要元件，而且它會透過如何使用專案檔來部署實際應用程式的範例來運作。
> 
> 您將瞭解的內容：
> 
> - MSBuild 如何使用 MSBuild 專案檔來建立專案。
> - MSBuild 如何與部署技術整合，例如 Internet Information Services （IIS） Web 部署工具（Web Deploy）。
> - 如何瞭解專案檔的主要元件。
> - 如何使用專案檔來建立及部署複雜的應用程式。

## <a name="msbuild-and-the-project-file"></a>MSBuild 和專案檔

當您在 Visual Studio 中建立並建立解決方案時，Visual Studio 會使用 MSBuild 來建立方案中的每個專案。 每個 Visual Studio 專案都包含一個 MSBuild 專案檔，其副檔名會反映專案&#x2014;的類型，例如， C#專案（.csproj）、Visual Basic.NET 專案（. vbproj）或資料庫專案（.dbproj）。 為了建立專案，MSBuild 必須處理與專案相關聯的專案檔。 專案檔是一個 XML 檔，其中包含 MSBuild 所需的所有資訊和指示，以建立您的專案，例如要包含的內容、平臺需求、版本資訊、網頁伺服器或資料庫伺服器設定，以及必須執行的工作。

MSBuild 專案檔是以[MSBUILD XML 架構](/visualstudio/msbuild/msbuild-project-file-schema-reference)為基礎，因此組建程式完全開放且透明。 此外，您不需要安裝 Visual Studio，就能使用 MSBuild 引擎&#x2014;，msbuild.exe 可執行檔是 .NET Framework 的一部分，而且您可以從命令提示字元中執行它。 身為開發人員，您可以使用 MSBuild XML 架構製作自己的 MSBuild 專案檔，以對您的專案建立和部署方式進行精密且精細的控制。 這些自訂專案檔的工作方式與 Visual Studio 自動產生的專案檔完全相同。

> [!NOTE]
> 您也可以在 Team Foundation Server （TFS）中搭配使用 MSBuild 專案檔與 Team Build service。 例如，您可以使用連續整合（CI）案例中的專案檔，在簽入新的程式碼時自動部署至測試環境。 如需詳細資訊，請參閱設定[自動化 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。

### <a name="project-file-naming-conventions"></a>專案檔案命名慣例

當您建立自己的專案檔時，可以使用任何您喜歡的副檔名。 不過，若要讓其他人更容易瞭解您的解決方案，您應該使用下列常見的慣例：

- 當您建立建立專案的專案檔時，請使用 proj 副檔名。
- 當您建立可重複使用的專案檔以匯入其他專案檔時，請使用 .targets 副檔名。 具有 .targets 副檔名的檔案通常不會建立任何專案，而是只包含您可以匯入到您的 .targets 檔案的指示。

### <a name="integration-with-deployment-technologies"></a>與部署技術整合

如果您已在 Visual Studio 2010 中使用 web 應用程式專案（例如 ASP.NET web 應用程式和 ASP.NET MVC web 應用程式），您會知道這些專案包含內建支援，可將 web 應用程式封裝及部署至目標環境。 這些專案的 [**屬性**] 頁面包括 [**封裝/發行 Web** ] 和 [**封裝/發行 SQL** ] 索引標籤，可讓您用來設定應用程式元件的封裝和部署方式。 這會顯示 [**封裝/發行 Web** ] 索引標籤：

![](understanding-the-project-file/_static/image1.png)

這些功能背後的基礎技術稱為「Web 發佈管線」（WPP）。 WPP 基本上會將 MSBuild 和[Web Deploy](https://go.microsoft.com/?linkid=9805122)整合在一起，為您的 Web 應用程式提供完整的組建、封裝和部署流程。

好消息是，您可以在建立 Web 專案的自訂專案檔時，利用 WPP 提供的整合點。 您可以在專案檔中包含部署指示，讓您建立專案、建立 web 部署套件，以及透過單一專案檔和對 MSBuild 的單一呼叫，在遠端伺服器上安裝這些套件。 您也可以在組建程式中呼叫任何其他可執行檔。 例如，您可以執行 VSDBCMD 命令列工具，從架構檔案部署資料庫。 在本主題的課程中，您將瞭解如何利用這些功能來滿足企業部署案例的需求。

> [!NOTE]
> 如需 web 應用程式部署流程運作方式的詳細資訊，請參閱[ASP.NET Web 應用程式專案部署總覽](https://msdn.microsoft.com/library/dd394698.aspx)。

## <a name="the-anatomy-of-a-project-file"></a>專案檔的剖析

在您仔細查看組建程式之前，值得花一些時間讓自己熟悉 MSBuild 專案檔的基本結構。 本節概述當您查看、編輯或建立專案檔時，將會遇到的更常見元素。 特別是，您將瞭解：

- 如何使用*屬性*來管理組建進程的變數。
- 如何使用*專案*來識別組建進程的輸入，例如程式碼檔案。
- 如何使用*目標* *和工作，將*執行指示提供給 MSBuild，方法是使用專案檔中其他位置所定義的*屬性*和*專案*。

這會顯示 MSBuild 專案檔中的主要元素之間的關聯性：

![](understanding-the-project-file/_static/image2.png)

### <a name="the-project-element"></a>專案元素

[Project](https://msdn.microsoft.com/library/bcxfsh87.aspx)元素是每個專案檔的根項目。 除了識別專案檔的 XML 架構之外， **Project 專案**還可以包含屬性，以指定組建進程的進入點。 例如，在[Contact Manager 範例方案](the-contact-manager-solution.md)中， *Publish*檔案會指定組建應從呼叫名為**FullPublish**的目標開始。

[!code-xml[Main](understanding-the-project-file/samples/sample1.xml)]

### <a name="properties-and-conditions"></a>屬性和條件

專案檔通常需要提供許多不同的資訊片段，才能成功建立及部署您的專案。 這些資訊片段可能包括伺服器名稱、連接字串、認證、組建設定、來源與目的地檔案路徑，以及您想要包含以支援自訂的任何其他資訊。 在專案檔中，屬性必須在[PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx)元素內定義。 MSBuild 屬性是由索引鍵/值組所組成。 在**PropertyGroup**元素中，元素名稱會定義屬性索引鍵，而元素的內容則會定義屬性值。 例如，您可以定義名為**ServerName**和**ConnectionString**的屬性，以儲存靜態伺服器名稱和連接字串。

[!code-xml[Main](understanding-the-project-file/samples/sample2.xml)]

若要取出屬性值，請使用 *$ （PropertyName）* 格式。 例如，若要取出**ServerName**屬性的值，您必須輸入：

[!code-powershell[Main](understanding-the-project-file/samples/sample3.ps1)]

> [!NOTE]
> 您會在本主題稍後看到如何及何時使用屬性值的範例。

在專案檔中將資訊內嵌為靜態屬性，並不一定是管理組建程式的理想方法。 在許多情況下，您會想要從其他來源取得資訊，或讓使用者從命令提示字元提供資訊。 MSBuild 可讓您將任何屬性值指定為命令列參數。 例如，使用者可以在從命令列執行 Msbuild.exe 時，提供**ServerName**的值。

[!code-console[Main](understanding-the-project-file/samples/sample4.cmd)]

> [!NOTE]
> 如需可搭配 Msbuild.exe 使用之引數和參數的詳細資訊，請參閱[Msbuild 命令列參考](https://msdn.microsoft.com/library/ms164311.aspx)。

您可以使用相同的屬性語法來取得環境變數和內建專案屬性的值。 許多常用的屬性都是為您定義的，而且您可以藉由加入相關的參數名稱，在專案檔中使用它們。 例如，若要取出目前的專案平臺&#x2014;（例如， **x86**或**AnyCpu**&#x2014;），您可以在專案檔中包含 **$ （platform）** 屬性參考。 如需詳細資訊，請參閱[組建命令和屬性的宏](https://msdn.microsoft.com/library/c02as0cs.aspx)、[一般 MSBuild 專案屬性](https://msdn.microsoft.com/library/bb629394.aspx)和[保留的屬性](https://msdn.microsoft.com/library/ms164309.aspx)。

屬性通常會與*條件*搭配使用。 大部分的 MSBuild 專案都支援**Condition**屬性，可讓您指定 MSBuild 應該評估專案的準則。 例如，請考慮這個屬性定義：

[!code-xml[Main](understanding-the-project-file/samples/sample5.xml)]

當 MSBuild 處理這個屬性定義時，它會先檢查 **$ （OutputRoot）** 屬性值是否可用。 如果屬性值為空白&#x2014;，則表示使用者未提供此屬性&#x2014;的值，條件評估為**true** ，且屬性值設定為 **。\Publish\Out**。如果使用者已提供此屬性的值，則條件會評估為**false** ，而且不會使用靜態屬性值。

如需您可以指定條件之不同方式的詳細資訊，請參閱[MSBuild 條件](https://msdn.microsoft.com/library/7szfhaft.aspx)。

### <a name="items-and-item-groups"></a>專案和專案群組

專案檔的其中一個重要角色是定義組建進程的輸入。 一般而言，這些輸入是檔案&#x2014;程式碼檔案、設定檔案、命令檔，以及您需要在組建流程中處理或複製的任何其他檔案。 在 MSBuild 專案架構中，這些輸入是以[專案](https://msdn.microsoft.com/library/ms164283.aspx)元素表示。 在專案檔中，專案必須在[ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx)元素內定義。 就像**屬性**專案一樣，您可以用您喜歡的方式來命名**Item**元素。 不過，您必須指定**包含**屬性，以識別專案所代表的檔案或萬用字元。

[!code-xml[Main](understanding-the-project-file/samples/sample6.xml)]

藉由指定多個具有相同名稱的**專案**元素，您就可以有效地建立命名資源的清單。 若要查看其實際運作方式，最好先查看 Visual Studio 建立的其中一個專案檔。 例如，範例方案中的*ContactManager*檔案包含許多專案群組，每個都有數個名稱相同的**專案**元素。

[!code-xml[Main](understanding-the-project-file/samples/sample7.xml)]

如此一來，專案檔會指示 MSBuild 建立檔案清單，這些檔案必須以**參考**清單所含的相同方式&#x2014;來處理，而此清單中包含必須針對成功組建準備就緒的元件、**編譯**清單包含必須編譯的程式碼檔案，且**內容**清單包含必須原封不動地複製的資源。 我們將在本主題稍後探討組建程式如何參考和使用這些專案。

專案元素也可以包含[ItemMetadata](https://msdn.microsoft.com/library/ms164284.aspx)的子項目。 這些是使用者定義的索引鍵/值組，基本上代表該專案特有的屬性。 例如，專案檔中的許多**編譯**專案元素都包含**DependentUpon**的子項目。

[!code-xml[Main](understanding-the-project-file/samples/sample8.xml)]

> [!NOTE]
> 除了使用者建立的專案中繼資料以外，所有專案都會在建立時指派各種共同的中繼資料。 如需詳細資訊，請參閱[已知的項目中繼資料](https://msdn.microsoft.com/library/ms164313.aspx)。

您可以在根層級的**專案**元素內或特定**目標**元素內建立**ItemGroup**元素。 **ItemGroup**元素也支援**條件**屬性，可讓您根據專案設定或平臺之類的條件，量身打造組建程式的輸入。

### <a name="targets-and-tasks"></a>目標和工作

在 MSBuild 架構中， [Task](https://msdn.microsoft.com/library/77f2hx1s.aspx)元素代表個別的組建指令（或工作）。 MSBuild 包含許多預先定義的工作。 例如：

- **複製**工作會將檔案複製到新的位置。
- **Csc**工作會叫用 Visual C#編譯器。
- **Vbc**工作會叫用 Visual Basic 編譯器。
- **Exec**工作會執行指定的程式。
- **Message**工作會將訊息寫入記錄器。

> [!NOTE]
> 如需現成可用工作的完整詳細資料，請參閱[MSBuild 工作參考](https://msdn.microsoft.com/library/7z253716.aspx)。 如需工作的詳細資訊，包括如何建立您自己的自訂作業，請參閱[MSBuild tasks](https://msdn.microsoft.com/library/ms171466.aspx)。

工作必須一律包含在[目標](https://msdn.microsoft.com/library/t50z2hka.aspx)元素內。 **Target**專案是一組依序執行的一或多個工作，而專案檔可以包含多個目標。 當您想要執行工作或一組工作時，您會叫用包含它們的目標。 例如，假設您有一個簡單的專案檔，會記錄一則訊息。

[!code-xml[Main](understanding-the-project-file/samples/sample9.xml)]

您可以從命令列叫用目標，方法是使用 **/t**參數指定目標。

[!code-console[Main](understanding-the-project-file/samples/sample10.cmd)]

或者，您也可以將**DefaultTargets**屬性加入至**Project**元素，以指定您要叫用的目標。

[!code-xml[Main](understanding-the-project-file/samples/sample11.xml)]

在此情況下，您不需要從命令列指定目標。 您可以直接指定專案檔，MSBuild 將會為您叫用**FullPublish**目標。

[!code-console[Main](understanding-the-project-file/samples/sample12.cmd)]

目標和工作都可以包含**條件**屬性。 因此，您可以選擇在符合特定條件時，省略整個目標或個別工作。

一般而言，當您建立有用的工作和目標時，您必須參考您在專案檔中的其他位置定義的屬性和專案：

- 若要使用屬性值，請輸入 **$ （***propertyname***）** ，其中*PropertyName*是**property**元素的名稱或參數的名稱。
- 若要使用專案，請輸入 **@（** 專案名稱） *，其中*專案名稱是**item**元素的名稱。

> [!NOTE]
> 請記住，如果您使用相同的名稱建立多個專案，則會建立一個清單。 相反地，如果您建立多個具有相同名稱的屬性，您提供的最後一個屬性值將會覆寫具有相同名稱&#x2014;的任何先前屬性，而屬性只能包含單一值。

例如，在範例方案的*Publish*檔案中，請查看**BuildProjects**目標。

[!code-xml[Main](understanding-the-project-file/samples/sample13.xml)]

在此範例中，您可以觀察下列重點：

- 如果指定**BuildingInTeamBuild**參數，且其值為**true**，則不會執行此目標中的任何工作。
- 目標包含[MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx)工作的單一實例。 這項工作可讓您建立其他 MSBuild 專案。
- **ProjectsToBuild**專案會傳遞至工作。 這個專案可以代表專案或方案檔的清單，這些檔案都是由專案群組中的**ProjectsToBuild**專案元素所定義。 在此情況下， **ProjectsToBuild**專案會參考單一方案檔。

    [!code-xml[Main](understanding-the-project-file/samples/sample14.xml)]
- 傳遞至**MSBuild**工作的屬性值包含名為**OutputRoot**和**Configuration**的參數。 如果有提供參數值，則會將它們設定為，如果不是，則設為靜態屬性值。

    [!code-xml[Main](understanding-the-project-file/samples/sample15.xml)]

您也可以看到**MSBuild**工作會叫用名為**Build**的目標。 這是幾個廣泛用於 Visual Studio 專案檔中的內建目標之一，可供您在自訂專案檔中使用，例如**組建**、**清除**、**重建**和**發行**。 您將會進一步瞭解如何使用目標和工作來控制組建程式，以及在本主題稍後的關於**MSBuild**工作。

> [!NOTE]
> 如需目標的詳細資訊，請參閱[MSBuild 目標](https://msdn.microsoft.com/library/ms171462.aspx)。

## <a name="splitting-project-files-to-support-multiple-environments"></a>分割專案檔案以支援多個環境

假設您想要能夠將解決方案部署到多個環境，例如測試伺服器、預備平臺及生產環境。 在這些環境&#x2014;中，設定可能會有極大的差異，而不只是伺服器名稱、連接字串等，而且也可能在認證、安全性設定和許多其他因素方面。 如果您需要定期執行此動作，您可以在每次切換目標環境時，編輯專案檔中的多個屬性並不容易。 也不是理想的解決方案，需要提供無止盡的屬性值清單給組建進程。

幸好有替代方案。 MSBuild 可讓您將組建設定分割成多個專案檔案。 若要查看其運作方式，請注意，在範例解決方案中，有兩個自訂專案檔案：

- *Publish*，其中包含所有環境通用的屬性、專案和目標。
- *Env-Dev. proj*，其中包含開發人員環境特有的屬性。

現在請注意， *Publish*檔案包含匯[入](https://msdn.microsoft.com/library/92x05xfs.aspx)元素，緊接在開啟**專案**標記的正下方。

[!code-xml[Main](understanding-the-project-file/samples/sample16.xml)]

**Import**元素可用來將另一個 msbuild 專案檔的內容匯入到目前的 msbuild 專案檔中。 在此情況下， **TargetEnvPropsFile**參數會提供您想要匯入之專案檔的檔案名。 當您執行 MSBuild 時，可以提供此參數的值。

[!code-console[Main](understanding-the-project-file/samples/sample17.cmd)]

這會將這兩個檔案的內容有效率地合併成一個專案檔。 使用這種方法，您可以建立一個包含萬用群組建設定的專案檔，以及包含環境特定屬性的多個補充專案檔案。 因此，只要以不同的參數值執行命令，就可以將您的方案部署到不同的環境。

![](understanding-the-project-file/_static/image3.png)

以這種方式分割專案檔是很好的作法。 它可讓開發人員藉由執行單一命令來部署至多個環境，同時避免跨多個專案檔重複萬用群組建屬性。

> [!NOTE]
> 如需如何為您自己的伺服器環境自訂環境特定專案檔案的指引，請參閱[設定目標環境的部署屬性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。

## <a name="conclusion"></a>結論

本主題提供 MSBuild 專案檔案的一般簡介，並說明如何建立您自己的自訂專案檔來控制組建程式。 同時也引進了將專案檔分割成萬用群組建指示和環境特定組建屬性的概念，讓您輕鬆建立專案並將其部署至多個目的地。

下一個主題：[瞭解組建](understanding-the-build-process.md)程式，可讓您更深入瞭解如何使用專案檔來控制組建和部署，方法是逐步執行解決方案的部署，並提供實際的複雜性層級。

## <a name="further-reading"></a>進一步閱讀

如需更深入的專案檔和 WPP 簡介，請參閱[Microsoft Build Engine 內：使用 MSBuild 和 Team Foundation Build](http://amzn.com/0735645248) By Sayed Ibrahim Hashimi 和 William BARTHOLOMEW，ISBN：978-0-7356-4524-0。

> [!div class="step-by-step"]
> [上一頁](setting-up-the-contact-manager-solution.md)
> [下一頁](understanding-the-build-process.md)
