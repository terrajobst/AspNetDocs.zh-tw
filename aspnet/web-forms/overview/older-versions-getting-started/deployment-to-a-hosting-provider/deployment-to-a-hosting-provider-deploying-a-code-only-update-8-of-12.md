---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署僅限程式碼的更新-8/12 |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: e4d094ef84a747c36ce05ddb0e3d1ce0391d5605
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74572739"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署僅限程式碼的更新-8/12

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。 如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。 如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。
> 
> 如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署到 Azure App Service Web Apps，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概觀

在初始部署之後，您維護和開發網站的工作會繼續進行，而且在很久之前，您會想要部署更新。 本教學課程會引導您完成將更新部署至應用程式程式碼的流程。 此更新不需要變更資料庫;在下一個教學課程中，您會看到部署資料庫變更的不同之處。

提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="making-a-code-change"></a>進行程式碼變更

做為應用程式更新的簡單範例，您會將所選講師所教授的課程清單新增到**講師**頁面。

如果您執行 [**講師**] 頁面，您會發現方格中有 [**選取**] 連結，但它們不會執行任何動作，而是讓資料列背景變成灰色。

[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)

現在您將新增在按一下 [**選取**] 連結時執行的程式碼，並顯示所選講師所教授的課程清單。

在 [ **ErrorMessageLabel** ] `Label` 控制項之後，于 [ *.aspx*] 中立即新增下列標記：

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

執行頁面，然後選取講師。 您會看到該講師所教授的課程清單。

[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)

## <a name="deploying-the-code-update-to-the-test-environment"></a>將程式碼更新部署到測試環境

部署到測試環境是一種簡單的事，就是再次執行單鍵發行。 若要讓此程式更快速，您可以使用 Web 單鍵 [**發行**] 工具列。

在 [ **View** ] 功能表中，選擇 [**工具列**]，然後選取 [ **Web One**] [發佈]。

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

在 **方案總管**中，選取 ContosoUniversity 專案。

Web 單鍵 [**發行**] 工具列，選擇 [**測試**發行設定檔]，然後按一下 [**發佈 Web** ] （箭號向左和向右的圖示）。

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

Visual Studio 會部署已更新的應用程式，且瀏覽器會自動開啟至首頁。 執行 [講師] 頁面，然後選取講師以確認更新已成功部署。

[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)

您通常也會進行迴歸測試（也就是測試網站的其餘部分，以確保新的變更不會中斷任何現有的功能）。 但是在本教學課程中，您會略過該步驟，並繼續將更新部署至生產環境。

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a>防止將初始資料庫狀態重新部署到生產環境

在實際的應用程式中，使用者會在初始部署之後與您的生產網站互動，並以即時資料填入資料庫。 因此，您不想要在初始狀態中重新部署成員資格資料庫，這會清除所有的即時資料。 因為 SQL Server Compact 的資料庫是*應用程式\_* 資料夾中的檔案，所以您必須藉由變更部署設定來避免此情況，讓 *\_應用程式*中的檔案不會部署。

開啟 ContosoUniversity 專案的 [**專案屬性**] 視窗，然後選取 [**封裝/發行 Web** ] 索引標籤。請確定 [設定 **] 下拉式方塊已選取 [作用**中 **（發行）** ] 或 [**發行**]，然後選取 **[從應用程式\_資料夾中排除**檔案]。

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

如果您決定要在未來部署「偵錯工具」組建，建議您對「偵錯工具」組建設定進行相同的變更 **：將設定變更為**「 **debug** 」，然後選取 **[從 App\_資料夾中排除**檔案]。

儲存並關閉 [**封裝/發行 Web** ] 索引標籤。

> [!NOTE] 
> 
> [!IMPORTANT]
> 請確定您未在發行設定檔中選取 [**在目的地移除其他**檔案]。 如果您選取該選項，部署程式將會刪除部署的網站中您在 App\_資料中的資料庫，而它將會刪除應用程式\_資料檔案夾本身。

## <a name="preventing-user-access-to-the-production-site-during-update"></a>在更新期間防止使用者存取生產網站

您要部署的變更現在是單一頁面的簡單變更。 但有時候您會部署較大的變更，在這種情況下，如果使用者在部署完成之前要求頁面，則網站的行為可能會奇怪。 若要避免這種情況，您可以使用*應用程式\_離線 .htm*檔案。 當您在應用程式的根資料夾中，將名為 app 的檔案 *\_離線*時，IIS 會自動顯示該檔案，而不是執行您的應用程式。 因此，若要在部署期間防止存取，請將*應用程式\_離線 .htm* ，執行部署程式，然後移除 *\_離線的應用程式*。

在**方案總管**中，以滑鼠右鍵按一下方案（不是其中一個專案），然後選取 [**新增方案資料夾**]。

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

將資料夾命名為*SolutionFiles*。

在新資料夾中，建立名為*app\_離線*的 HTML 網頁。 以下列標記取代現有的內容：

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

您可以在主控提供者的控制台中，使用 FTP 連接或**檔案管理員**公用程式，將*應用程式\_離線 .htm*檔案複製到網站。 在本教學課程中，您將使用 [**檔案管理員**]。

開啟 [控制台]，然後選取 [**檔案管理員**]，如同您在[部署至生產環境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教學課程中所做的一樣。 選取 [ **contosouniversity.com** ]，然後選取 [ **wwwroot** ] 以前往應用程式的根資料夾，然後按一下 **[上傳**]。

[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)

在 [**上傳**檔案] 對話方塊中，選取 *\_離線 .htm 檔案的應用程式*，然後按一下 **[上傳**]。

[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)

流覽至您網站的 URL。 您會看到*應用程式\_離線 .htm*  頁面，而不是您的首頁。

[![App_offline。 htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)

您現在已準備好部署到生產環境。

## <a name="deploying-the-code-update-to-the-production-environment"></a>將程式碼更新部署至生產環境

在 Web 單鍵的 [**發行**] 工具列中，選擇 [**生產**] 發行設定檔，然後按一下 [**發佈 Web**]。

Visual Studio 會部署已更新的應用程式，並將瀏覽器開啟至網站的首頁。 隨即顯示*應用程式\_離線的 .htm*檔案。 您必須先移除*應用程式\_離線 .htm*檔案，才能進行測試以確認部署是否成功。

回到 [控制台] 中的 [**檔案管理員**] 應用程式。 選取 [ **contosouniversity.com** ] 和 [ **wwwroot**]，選取 [**應用程式\_離線**]，然後按一下 [**刪除**]。

[![Deleting_app_offline .htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)

在瀏覽器中，開啟公用網站中的 [講師] 頁面，然後選取講師以確認更新已成功部署。

[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)

您現在已部署未牽涉到資料庫變更的應用程式更新。 下一個教學課程會說明如何部署資料庫變更。

> [!div class="step-by-step"]
> [上一頁](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
