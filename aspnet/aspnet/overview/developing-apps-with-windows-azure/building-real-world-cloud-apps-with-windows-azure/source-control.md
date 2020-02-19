---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
title: 原始檔控制（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 06/23/2015
ms.assetid: 2a0370d3-c2fb-4bf3-88b8-aad5a736c793
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
msc.type: authoredcontent
ms.openlocfilehash: 5a1e0d7cd3c396d4be79c8958422602055eb3db1
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457098"
---
# <a name="source-control-building-real-world-cloud-apps-with-azure"></a>原始檔控制（使用 Azure 建立真實世界的雲端應用程式）

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。 如需電子書的相關資訊，請參閱[第一章](introduction.md)。

原始檔控制對於所有雲端開發專案都是不可或缺的，而不只是小組環境。 您不想要在沒有復原功能和自動備份的情況下編輯原始程式碼或甚至是 Word 檔，而原始檔控制會在專案層級提供這些函式，以便在發生錯誤時更多時間儲存。 使用雲端原始檔控制服務時，您不再需要擔心複雜的設定，而且您可以免費使用 Azure Repos 的原始檔控制，最多5位使用者。

本章的第一個部分將說明要牢記在心的三個重要最佳作法：

- 將[自動化腳本視為原始程式碼](#scripts)，並將它們與您的應用程式程式碼搭配使用。
- [請勿將秘密（機密](#secrets)資料，例如認證）簽入原始程式碼存放庫。
- [設定來源分支](#devops)以啟用 DevOps 工作流程。

本章的其餘部分會在 Visual Studio、Azure 和 Azure Repos 中提供這些模式的一些範例執行：

- [在 Visual Studio 中將腳本加入至原始檔控制](#vsscripts)
- [將敏感性資料儲存在 Azure 中](#appsettings)
- [在 Visual Studio 和 Azure Repos 中使用 Git](#gittfs)

<a id="scripts"></a>
## <a name="treat-automation-scripts-as-source-code"></a>將自動化腳本視為原始程式碼

當您正在處理雲端專案時，您會經常變更，而且您想要能夠快速地回應客戶所回報的問題。 快速回應包括使用自動化腳本，如[自動化所有事項](automate-everything.md)一章所述。 您用來建立環境、加以部署、調整規模等等的所有腳本，都必須與您的應用程式原始程式碼同步。

若要讓腳本與程式碼保持同步，請將其儲存在您的原始檔控制系統中。 然後，如果您需要復原變更，或快速修正與開發程式碼不同的實際執行程式碼，則不必浪費時間嘗試追蹤哪些設定已變更，或是哪些小組成員有您需要的版本複本。 您可以確定所需的腳本與您所需的程式碼基底同步，而且您可以確保所有小組成員都使用相同的腳本。 然後，不論您是否需要將熱修正的測試和部署作業自動化至生產環境或新功能開發，您都可以使用正確的腳本來處理需要更新的程式碼。

<a id="secrets"></a>
## <a name="dont-check-in-secrets"></a>不簽入秘密

原始碼存放庫通常可供太多人存取，以確保機密資料（例如密碼）有適當的安全位置。 如果腳本依賴秘密（例如密碼），請將這些設定參數化，讓它們不會儲存在原始程式碼中，並將您的密碼儲存在其他地方。

例如，Azure 可讓您下載包含發行設定的檔案，以便自動建立發行設定檔。 這些檔案包括已獲授權可管理 Azure 服務的使用者名稱和密碼。 如果您使用此方法來建立發行設定檔，而且將這些檔案簽入原始檔控制，任何可存取您存放庫的人都可以看到那些使用者名稱和密碼。 您可以安全地將密碼儲存在發行設定檔本身，因為它已加密，而且它是在預設不包含在原始檔控制中的 *.pubxml*檔案中。

<a id="devops"></a>
## <a name="structure-source-branches-to-facilitate-devops-workflow"></a>結構來源分支以加速 DevOps 工作流程

您在存放庫中執行分支的方式，會影響您在生產環境中開發新功能和修正問題的能力。 以下是許多中型小組使用的模式：

![來源分支結構](source-control/_static/image1.png)

主要分支一律會符合生產環境中的程式碼。 Master 底下的分支對應到開發生命週期中的不同階段。 開發分支是您可在其中執行新功能的位置。 對於小型小組，您可能只是主要和開發，但我們通常建議使用者在開發與主伺服器之間擁有預備分支。 您可以使用預備來進行最終的整合測試，再將更新移至生產環境。

對於大型團隊而言，每項新功能可能會有個別的分支;對於較小的小組，您可能會有每個人簽入開發分支。

如果您有每個功能的分支，當功能 A 準備好時，您可以將其原始程式碼變更合併到開發分支，再將其移至其他功能分支。 此原始程式碼合併程式可能非常耗時，若要避免該工作，同時仍保持功能的不同，某些小組會執行稱為 *[功能切換](http://en.wikipedia.org/wiki/Feature_toggle)* 的替代方法（也稱為*功能旗標*）。 這表示所有功能的所有程式碼都位於相同的分支中，但是您可以使用程式碼中的參數來啟用或停用每項功能。 例如，假設「功能 A」是用來修正 It 應用程式工作的新欄位，而「功能 B」則新增快取功能。 這兩個功能的程式碼可以在開發分支中，但只有當變數設定為 true 時，應用程式才會顯示新的欄位，而且當不同的變數設定為 true 時，它只會使用快取。 如果功能 A 尚未準備好升級，但功能 B 已準備就緒，您可以將所有的程式碼升級至生產環境，並將功能切換為關閉，並開啟功能 B 開關。 接著，您可以完成功能 A 並于稍後升級，而不需要合併原始程式碼。

不論您是使用分支還是切換功能，這類分支結構都可讓您以敏捷且可重複的方式，將您的程式碼從開發流到生產環境。

此結構也可讓您快速回應客戶的意見反應。 如果您需要快速修正生產環境，您也可以透過敏捷的方式有效率地進行。 您可以從主要或預備環境建立分支，並在它準備好將它合併到主伺服器和功能分支中。

![修補程式分支](source-control/_static/image2.png)

如果沒有像這樣的分支結構，並將其與生產和開發分支分開，則生產環境問題可能會讓您進入必須升級新功能程式碼的位置，以及您的生產環境修正。 新的功能程式碼可能尚未經過完整測試，且可供生產環境使用，您可能需要執行許多工作，以備份尚未準備好的變更。 或者，您可能必須延遲修正程式，才能測試變更並準備好進行部署。

接下來，您會看到如何在 Visual Studio、Azure 和 Azure Repos 中執行這三種模式的範例。 這些是範例，而不是詳細的逐步操作方法指示;如需提供所有必要內容的詳細指示，請參閱本章結尾的[Resources （資源](#resources)）一節。

<a id="vsscripts"></a>
## <a name="add-scripts-to-source-control-in-visual-studio"></a>在 Visual Studio 中將腳本加入至原始檔控制

在 Visual Studio 中，您可以將腳本加入至原始檔控制中，方法是將它們包含在 Visual Studio 方案資料夾中（假設您的專案是在原始檔控制中）。 以下是其中一種方法。

為方案資料夾中的腳本建立資料夾（具有 *.sln*檔案的相同資料夾）。

![自動化資料夾](source-control/_static/image3.png)

將腳本檔案複製到資料夾中。

![自動化資料夾內容](source-control/_static/image4.png)

在 Visual Studio 中，將 [方案] 資料夾新增至專案。

![新增方案資料夾功能表選取專案](source-control/_static/image5.png)

並將腳本檔案加入至 [方案] 資料夾。

![[加入現有專案] 功能表選取範圍](source-control/_static/image6.png)

![加入現有項目對話方塊](source-control/_static/image7.png)

腳本檔案現在已包含在您的專案中，而原始檔控制會追蹤其版本變更以及對應的原始程式碼變更。

<a id="appsettings"></a>
## <a name="store-sensitive-data-in-azure"></a>將敏感性資料儲存在 Azure 中

如果您在 Azure 網站中執行應用程式，其中一個避免將認證儲存在原始檔控制中的方法，就是將其儲存在 Azure 中。

例如，Fix It 應用程式會在其 Web.config 檔案中儲存兩個將在生產環境中具有密碼的連接字串，以及一個可存取您 Azure 儲存體帳戶的金鑰。

[!code-xml[Main](source-control/samples/sample1.xml?highlight=2-3,11)]

如果您將這些設定的實際生產值放在*web.config 檔案*中，或將它們放在*web.config*檔案中以設定 web.config 轉換，以便在部署期間將其插入，它們將會儲存在來源存放庫中。 如果您在生產發行設定檔中輸入資料庫連接字串，密碼將會在您的 *.pubxml*檔案中。 （您可以將 *.pubxml*檔案從原始檔控制中排除，但這樣會失去共用所有其他部署設定的優點）。

Azure 為您*提供 web.config 檔案*中**appSettings**和連接字串區段的替代方案。 以下是 Azure 入口網站中網站的 [**設定] 索引標籤的相關**部分：

![入口網站中的 appSettings 和 connectionStrings](source-control/_static/image8.png)

當您將專案部署到這個網站並執行應用程式時，任何您儲存在 Azure 中的值都會覆寫 Web.config 檔案中的任何值。

您可以使用管理入口網站或腳本，在 Azure 中設定這些值。 您在[自動化所有事項](automate-everything.md)一章中看到的環境建立自動化腳本會建立一個 Azure SQL Database、取得儲存體並 SQL Database 連接字串，並將這些秘密儲存在您的網站設定中。

[!code-powershell[Main](source-control/samples/sample2.ps1)]

[!code-powershell[Main](source-control/samples/sample3.ps1)]

請注意，腳本已參數化，因此實際值不會保存至來源存放庫。

當您在開發環境中于本機執行時，應用程式會讀取您的本機 Web.config 檔案，而您的連接字串會指向 Web 專案之*應用程式\_Data*資料夾中的 LocalDB SQL Server 資料庫。 當您在 Azure 中執行應用程式，且應用程式嘗試從 Web.config 檔案讀取這些值時，它所傳回的內容是儲存在網站上的值，而不是在 web.config 檔案中實際的值。

<a id="gittfs"></a>
## <a name="use-git-in-visual-studio-and-azure-devops"></a>在 Visual Studio 和 Azure DevOps 中使用 Git

您可以使用任何原始檔控制環境來執行稍早所提供的 DevOps 分支結構。 對於分散式小組而言，[分散式版本控制系統](http://en.wikipedia.org/wiki/Distributed_revision_control)（DVCS）可能會有最佳效果;對於其他小組而言，[集中式系統](http://en.wikipedia.org/wiki/Revision_control)可能更有效果。

[Git](http://git-scm.com/)是受歡迎的分散式版本控制系統。 當您使用 Git 進行原始檔控制時，您可以在本機電腦上擁有完整的存放庫複本及其所有歷程記錄。 許多人偏好這麼做，因為當您未連線到網路時，可以更輕鬆地繼續工作--您可以繼續執行認可和復原、建立和切換分支等等。 即使您已連線到網路，當所有專案都在本機時，建立分支和切換分支會變得更容易且更快速。 您也可以執行本機認可和回復，而不會影響其他開發人員。 而且您可以先批次處理認可，再將它們傳送至伺服器。

[Azure Repos](/azure/devops/repos/index?view=vsts)提供[Git](/azure/devops/repos/git/?view=vsts)和[Team Foundation 版本控制](/azure/devops/repos/tfvc/index?view=vsts)（TFVC; 集中式原始檔控制）。 從[這裡](https://app.vsaex.visualstudio.com/signup)開始使用 Azure DevOps。

Visual Studio 2017 包含內建的第一級[Git 支援](https://msdn.microsoft.com/library/hh850437.aspx)。 以下是其運作方式的快速示範。

在 Visual Studio 中開啟專案時，以滑鼠右鍵按一下**方案總管**中的方案，然後選擇 [**將方案加入至原始檔控制**]。

![將方案加入至原始檔控制](source-control/_static/image9.png)

Visual Studio 詢問您是否要使用 TFVC （集中式版本控制）或 Git。

![選擇原始檔控制](source-control/_static/image10.png)

當您選取 [Git]，然後按一下 **[確定]** 時，Visual Studio 會在方案資料夾中建立新的本機 Git 存放庫。 新的存放庫尚未提供任何檔案;您必須執行 Git 認可，將它們新增至存放庫。 以滑鼠右鍵按一下**方案總管**中的方案，然後按一下 [**認可**]。

![Commit](source-control/_static/image11.png)

Visual Studio 會自動為認可的所有專案檔案設置階段，並在 [**包含的變更**] 窗格的**Team Explorer**中列出它們。 （如果有一些您不想要包含在認可中，您可以選取它們、按一下滑鼠右鍵，然後按一下 [**排除**]）。

![Team Explorer](source-control/_static/image12.png)

輸入認可批註，然後按一下 [**認可**]，Visual Studio 執行認可並顯示認可識別碼。

![Team Explorer 變更](source-control/_static/image13.png)

現在，如果您變更一些程式碼，使其與存放庫中的不同，您可以輕鬆地查看差異。 以滑鼠右鍵按一下您已變更的檔案，選取 [**與未修改的比較**]，然後取得顯示未認可變更的比較顯示。

![與未修改的比較](source-control/_static/image14.png)

![差異顯示變更](source-control/_static/image15.png)

您可以輕鬆地查看您所做的變更，並將其簽入。

假設您需要建立分支–您也可以在 Visual Studio 中這麼做。 在**Team Explorer**中，按一下 [**新增分支**]。

![Team Explorer 新增分支](source-control/_static/image16.png)

輸入分支名稱、按一下 [**建立分支**]，如果您選取 [**簽出分支**]，Visual Studio 會自動簽出新的分支。

![Team Explorer 新增分支](source-control/_static/image17.png)

您現在可以對檔案進行變更，並將其簽入此分支。 而且您可以輕鬆地在分支之間切換，Visual Studio 會自動將檔案同步處理至您已簽出的任何分支。在此範例中， *\_Layout*中的網頁標題已變更為 HotFix1 分支中的「熱修復1」。

![Hotfix1 分支](source-control/_static/image18.png)

如果您切換回主要分支， *\_Layout*檔案的內容會自動還原成主要分支中的檔案。

![主要分支](source-control/_static/image19.png)

這是一個簡單的範例，說明如何快速建立分支並在分支之間來回切換。 這項功能可讓您使用 [[自動化所有專案](automate-everything.md)] 一章中所提供的分支結構和自動化腳本，來進行高度 agile 工作流程。 例如，您可以在開發分支中工作、從 master 建立熱修復分支、切換到新分支、在該處進行變更並加以認可，然後切換回開發分支並繼續進行。

您在這裡看到的是如何在 Visual Studio 中使用本機 Git 存放庫。 在小組環境中，您通常也會將變更推送到通用存放庫。 Visual Studio 工具也可讓您指向遠端 Git 存放庫。 您可以針對該目的使用 GitHub.com，也可以使用[Git 和 Azure Repos](/azure/devops/repos/git/overview?view=vsts)與所有其他 Azure DevOps 功能整合，例如工作專案和 bug 追蹤。

當然，這並不是您可以實現 agile 分支策略的唯一方法。 您可以使用集中式原始檔控制存放庫來啟用相同的 agile 工作流程。

## <a name="summary"></a>摘要

根據您可進行變更的速度，並以安全且可預測的方式，測量您的原始檔控制系統是否成功。 如果您發現自己的害怕進行變更，因為您必須對其進行一天或兩次的手動測試，您可能會問自己，您必須採取何種方式進行處理或測試，讓您可以在幾分鐘內進行變更，或在最差時間不到一小時。 執行這項作業的其中一個策略是執行持續整合和持續傳遞，我們將在[下一章](continuous-integration-and-continuous-delivery.md)中討論。

<a id="resources"></a>
## <a name="resources"></a>資源

如需分支策略的詳細資訊，請參閱下列資源：

- [使用 Team Foundation Server 2012 建立發行管線](https://msdn.microsoft.com/library/dn449957.aspx)。 Microsoft 模式和實務檔。 如需分支策略的討論，請參閱第6章。 提倡者功能會切換功能分支，如果使用功能分支，則會讓它們保持短期（最多數小時或數天）。
- [版本控制指南](https://aka.ms/vsarsolutions)。 ALM Ranger 的分支策略指南。 請參閱 [下載] 索引標籤上的分支策略 .pdf。
- [使用功能切換進行軟體發展](https://msdn.microsoft.com/magazine/dn683796.aspx)。 MSDN 雜誌文章。
- [功能切換](http://martinfowler.com/bliki/FeatureToggle.html)。 在聖馬丁 Fowler 的 blog 上的功能切換/功能旗標簡介。
- [功能會切換 Vs 功能分支](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx)。 另一個關於功能切換的 blog 文章 Dylan Smith。

如需如何處理不應保留在原始檔控制存放庫中之機密資訊的詳細資訊，請參閱下列資源：

- [將密碼和其他機密資料部署至 ASP.NET 和 Azure App Service 的最佳作法](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。
- [Azure 網站：應用程式字串與連接字串的運作方式](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)。 說明會覆寫*web.config*檔案中 `appSettings` 和 `connectionStrings` 資料的 Azure 功能。
- [Azure 網站中的自訂設定和應用程式設定-使用 Stefan Schackow](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/)。

如需其他將機密資訊保留在原始檔控制之外之方法的詳細資訊，請參閱[ASP.NET MVC：將私用設定保留在原始](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)檔控制中。

> [!div class="step-by-step"]
> [上一頁](automate-everything.md)
> [下一頁](continuous-integration-and-continuous-delivery.md)
