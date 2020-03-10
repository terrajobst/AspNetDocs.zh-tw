---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：設定資料夾許可權-6/12 |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: cd03a188-e947-4f55-9bda-b8bce201d8c6
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
msc.type: authoredcontent
ms.openlocfilehash: 85a77a196cf3458bbb2e6308838a846936cd070b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78630505"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-setting-folder-permissions---6-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：設定資料夾許可權-6/12

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。 如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。 如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。
> 
> 如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署到 Azure App Service Web Apps，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概觀

在本教學課程中，您會在已部署的網站中設定*Elmah*資料夾的資料夾許可權，讓應用程式可以在該資料夾中建立記錄檔。

當您使用 Visual Studio 程式開發伺服器（Cassini）在 Visual Studio 中測試 web 應用程式時，應用程式會在您的身分識別下執行。 您很可能是開發電腦上的系統管理員，而且擁有完整許可權可以對任何資料夾中的任何檔案執行任何動作。 但當應用程式在 IIS 底下執行時，它會在為網站指派的應用程式集區定義的身分識別下執行。 這通常是系統定義的帳戶，其許可權有限。 根據預設，它對您 web 應用程式的檔案和資料夾具有 [讀取] 和 [執行] 許可權，但不具有寫入存取權。

如果您的應用程式會建立或更新檔案，這是 web 應用程式中常見的需求，這會變成一個問題。 在 Contoso 大學應用程式中，Elmah 會在*elmah*資料夾中建立 XML 檔案，以便儲存錯誤的詳細資料。 即使您未使用類似 Elmah 的專案，您的網站可能會讓使用者上傳檔案，或執行其他工作，將資料寫入您的網站中的資料夾。

提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="testing-error-logging-and-reporting"></a>測試錯誤記錄和報告

若要查看應用程式在 IIS 中無法正確運作的方式（雖然在 Visual Studio 中進行測試），您可能會造成一則通常會記錄的錯誤，然後開啟 Elmah 錯誤記錄檔以查看詳細資料。 如果 Elmah 無法建立 XML 檔案並儲存錯誤詳細資料，您會看到空白的錯誤報表。

開啟瀏覽器並移至 `http://localhost/ContosoUniversity`，然後要求不正確 URL，例如*Studentsxxx。* 您會看到 [系統產生的錯誤] 頁面，而不是 [ *GenericErrorPage* ] 頁面，因為 web.config 檔案中的 `customErrors` 設定是 "RemoteOnly"，而且您正在本機執行 IIS：

[![Error_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image2.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image1.png)

現在請執行*Elmah* ，以查看錯誤報表。 您會看到空白的錯誤記錄檔頁面，因為 Elmah 無法在*elmah*資料夾中建立 XML 檔案：

[![Error_log_page_empty](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image4.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image3.png)

## <a name="setting-write-permission-on-the-elmah-folder"></a>設定 Elmah 資料夾的寫入權限

您可以手動設定資料夾許可權，也可以讓它成為部署程式的自動部分。 讓它自動需要複雜的 MSBuild 程式碼，而且因為您在第一次部署時只需要執行此動作，所以本教學課程只會顯示如何手動執行此動作。 （如需如何使此部分部署程式的相關資訊，請參閱在 Sayed Hashimi 的 blog 上[設定 Web Publish 的資料夾許可權](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx)。）

在**Windows Explorer**中，流覽至*C:\inetpub\wwwroot\ContosoUniversity*。 以滑鼠右鍵按一下 [ *Elmah* ] 資料夾，選取 [**屬性**]，然後選取 [**安全性**] 索引標籤。

[![Elmah_folder_Properties_Security_tab](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image6.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image5.png)

（如果您在 [**群組或使用者名稱**] 清單中看不到 [ **DefaultAppPool** ]，表示您可能使用的其他方法與本教學課程中指定的不同，在您的電腦上設定 IIS 和 ASP.NET 4。 在此情況下，請找出指派給 Contoso 大學應用程式的應用程式集區所使用的身分識別，並將寫入權限授與該身分識別。 請參閱本教學課程結尾處的關於應用程式集區識別的連結。）

按一下 [編輯]。 在 [ **Elmah 的許可權**] 對話方塊中，選取 [ **DefaultAppPool**]，然後選取 [**允許**] 資料行中的 [**寫入**] 核取方塊。

[![Permissions_for_Elmah_dialog_box](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image8.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image7.png)

在兩個對話方塊中按一下 **[確定]** 。

## <a name="retesting-error-logging-and-reporting"></a>重新測試錯誤記錄和報告

以相同方式（要求錯誤的 URL）重新產生錯誤，並執行**錯誤記錄**頁面來進行測試。 這次錯誤會出現在頁面上。

[![Elmah_Error_Log_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image10.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image9.png)

您也需要*應用程式\_Data*資料夾的寫入權限，因為您在該資料夾中有 SQL Server Compact 的資料庫檔案，而且您想要能夠更新這些資料庫中的資料。 不過，在這種情況下，您不需要執行任何額外的動作，因為部署程式會自動設定*App\_Data*資料夾的寫入權限。

您現在已完成所有必要的工作，讓 Contoso 大學能夠在本機電腦上的 IIS 中正常運作。 在下一個教學課程中，您會將網站部署至主機服務提供者，使其可公開使用。

## <a name="more-information"></a>詳細資訊

在此範例中，為什麼 Elmah 無法儲存記錄檔的原因相當明顯。 在問題原因不明顯的情況下，您可以使用 IIS 追蹤;請參閱 IIS.net 網站上的[在 IIS 7 中使用追蹤疑難排解失敗的要求](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)。

如需如何將許可權授與應用程式集區身分識別的詳細資訊，請參閱 IIS.net 網站上的[應用程式集](https://www.iis.net/learn/manage/configuring-security/application-pool-identities)區身分識別和[IIS 中的透過檔案系統 acl 保護內容](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls)。

> [!div class="step-by-step"]
> [上一頁](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
