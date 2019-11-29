---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：設定專案屬性-4/12 |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 8b013630-842c-4d44-a6fc-c6be43e7210f
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
msc.type: authoredcontent
ms.openlocfilehash: 6e63e75dca3d776fb9a1bd7e420ef48891daac69
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74569803"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-configuring-project-properties---4-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：設定專案屬性-4/12

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。 如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。 如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。
> 
> 如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署到 Azure App Service Web Apps，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概觀

某些部署選項是在專案檔（ *.csproj*或*vbproj*檔案）中儲存的專案屬性中設定。 在大部分情況下，這些設定的預設值都是您想要的，但如果您需要變更這些設定，可以使用內建于 Visual Studio 中的 [**專案屬性**] UI 來使用這些設定。 在本教學課程中，您會在 [**專案屬性**] 中查看部署設定。 您也會建立一個預留位置檔案，此檔案會導致部署空的資料夾。

## <a name="configuring-deployment-settings-in-the-project-properties-window"></a>在 [專案屬性] 視窗中進行部署設定

大部分會影響部署期間發生之動作的設定會包含在發行設定檔中，如下列教學課程所示。 您應該注意的幾項設定，都位於 [**專案屬性**] 視窗的 [**封裝/發行**] 索引標籤中。 系統會針對每個組建設定指定這些設定，也就是您的發行組建可以有不同的設定，而不是針對 Debug 組建。

在**方案總管**中，以滑鼠右鍵按一下**ContosoUniversity**專案，選取 [**屬性**]，然後選取 [**封裝/發行 Web** ] 索引標籤。

![Package_Publish_Web_tab](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image1.png)

視窗顯示時，預設會顯示方案目前使用中的設定。 如果 [設定] 方塊未**指出 [使用**中 **（發行）** ]，請選取 [**發行**]，以顯示發行組建設定的設定。 您會將發行組建部署至您的測試和生產環境。

![Package_Publish_Web_tab_selecting_Release](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image2.png)

當您選取 [作用中 **（發行）** ] 或 [**發行**] 時，您會看到使用發行組建設定進行部署時的有效值：

- 在 [**要部署的專案**] 方塊中，只會選取**執行應用程式所需的**檔案。 其他選項則是**此專案中的所有**檔案，或**此專案資料夾中的所有**檔案。 將預設選項保留為不變更，即可避免部署原始程式碼檔，例如。 這項設定是指包含 SQL Server Compact 二進位檔案的資料夾必須包含在專案中的原因。 如需此設定的詳細資訊，請參閱[ASP.NET Web 應用程式專案部署常見問題](https://msdn.microsoft.com/library/ee942158.aspx)中的**為何無法部署我的專案資料夾中的所有檔案？** 。
- 已選取 [**排除產生的 debug 符號**]。 當您使用此組建設定時，將不會進行任何調試。
- 未選取 **[從應用程式中排除檔案\_的資料] 資料夾**。 成員資格資料庫的 SQL Server Compact 檔案位於該資料夾中，而且您必須加以部署。 當您部署的更新不包含資料庫變更時，您會選取此核取方塊。
- 未選取 [**發行之前先行編譯此應用程式**]。 在大部分的情況下，不需要先行編譯 web 應用程式專案。 如需此選項的詳細資訊，請參閱[封裝/發行 Web 索引標籤、專案屬性](https://msdn.microsoft.com/library/dd410108(v=vs.110).aspx)和[Advanced 先行編譯設定對話方塊](https://msdn.microsoft.com/library/hh475319(v=vs.110).aspx)。
- **[包含在封裝/發行 sql 索引標籤中設定的所有資料庫]** 已選取，但此選項目前沒有任何作用，因為您未設定 [**封裝/發行 sql** ] 索引標籤。該索引標籤適用于舊版資料庫部署方法，這種方式是用來部署 SQL Server 資料庫的唯一選項。 您將使用 [[遷移至 SQL Server](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md) ] 教學課程中的 [**封裝/發行 SQL** ] 索引標籤。
- [ **Web 部署套件設定**] 區段不適用，因為您在這些教學課程中使用單鍵發行。

**將 [設定] 下拉式方塊**變更為 [debug]，以查看 debug build 的預設設定。 這些值是相同的，除了**排除產生的 debug 符號**會被清除，讓您可以在部署 debug 組建時進行 debug。

## <a name="making-sure-that-the-elmah-folder-gets-deployed"></a>確定已部署 Elmah 資料夾

如您在上一個教學課程中所見， [Elmah NuGet 封裝](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)提供了錯誤記錄和報告功能。 Contoso 大學應用程式中的 Elmah 已設定為將錯誤詳細資料儲存在名為*Elmah*的資料夾中：

![Elmah 資料夾](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image3.png)

從部署中排除特定檔案或資料夾是常見的需求;另一個範例是使用者可以上傳檔案的資料夾。 您不想要將在開發環境中建立的記錄檔或上傳檔案部署到生產環境。 而且，如果您要將更新部署到生產環境，您不希望部署程式刪除存在於生產環境中的檔案。 （視您設定部署選項的方式而定，如果檔案存在於目的地網站中，而不是在部署時的來源網站，Web Deploy 會將它從目的地刪除）。

如您稍早在本教學課程中所見，[**封裝/發行 Web** ] 索引標籤中的 [**要部署的專案**] 選項會設定為**只有執行此應用程式所需**的檔案。 因此，將不會部署由 Elmah 在開發期間建立的記錄檔，這就是您想要進行的動作。 （若要部署，它們必須包含在專案中，且其 [**組建動作**] 屬性必須設定為 [**內容**]。 如需詳細資訊，請參閱**為什麼我的專案資料夾中的所有檔案都不會部署？** 在[ASP.NET Web 應用程式專案部署常見問題](https://msdn.microsoft.com/library/ee942158.aspx)中）。 不過，除非至少有一個要複製的檔案，否則 Web Deploy 不會在目的地網站中建立資料夾。 因此，您會將 *.txt*檔案新增至資料夾，以作為預留位置，以便複製資料夾。

在**方案總管**中，以滑鼠右鍵按一下 [ *Elmah* ] 資料夾，選取 [**加入新專案**]，然後建立名為 [*預留位置 .txt*] 的檔案。 將下列文字放在其中：「這是一個可確保已部署資料夾的預留位置檔案。」 並儲存檔案。 這麼做是為了確保 Visual Studio 部署此檔案及其所在的資料夾，因為 *.txt*檔案的 [**組建動作**] 屬性預設會設定為 [**內容**]。

您現在已完成所有部署設定工作。 在下一個教學課程中，您會將 Contoso 大學網站部署到測試環境，並在該處進行測試。

> [!div class="step-by-step"]
> [上一頁](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
