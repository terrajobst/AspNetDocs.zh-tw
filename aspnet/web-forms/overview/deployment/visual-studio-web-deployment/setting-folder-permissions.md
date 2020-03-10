---
uid: web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
title: 使用 Visual Studio ASP.NET Web 部署：設定資料夾許可權 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9715a121-fa55-4f1b-a5d2-fb3f6cd8be8f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
msc.type: authoredcontent
ms.openlocfilehash: 410525bb2e3f6e5a0be6d7d6b33fb3a40509041a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78576059"
---
# <a name="aspnet-web-deployment-using-visual-studio-setting-folder-permissions"></a>使用 Visual Studio ASP.NET Web 部署：設定資料夾許可權

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本教學課程系列說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商裝載提供者。 如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。

## <a name="overview"></a>概觀

在本教學課程中，您會在已部署的網站中設定*Elmah*資料夾的資料夾許可權，讓應用程式可以在該資料夾中建立記錄檔。

當您使用 Visual Studio 程式開發伺服器（Cassini）或 IIS Express 在 Visual Studio 中測試 web 應用程式時，應用程式會在您的身分識別下執行。 您很可能是開發電腦上的系統管理員，而且擁有完整許可權可以對任何資料夾中的任何檔案執行任何動作。 但當應用程式在 IIS 底下執行時，它會在為網站指派的應用程式集區定義的身分識別下執行。 這通常是系統定義的帳戶，其許可權有限。 根據預設，它對您 web 應用程式的檔案和資料夾具有 [讀取] 和 [執行] 許可權，但不具有寫入存取權。

如果您的應用程式會建立或更新檔案，這是 web 應用程式中常見的需求，這會變成一個問題。 在 Contoso 大學應用程式中，Elmah 會在*elmah*資料夾中建立 XML 檔案，以便儲存錯誤的詳細資料。 即使您未使用類似 Elmah 的專案，您的網站可能會讓使用者上傳檔案，或執行其他工作，將資料寫入您的網站中的資料夾。

提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](troubleshooting.md)。

## <a name="test-error-logging-and-reporting"></a>測試錯誤記錄和報告

若要查看應用程式在 IIS 中無法正確運作的方式（雖然在 Visual Studio 中進行測試），您可能會造成一則通常會記錄的錯誤，然後開啟 Elmah 錯誤記錄檔以查看詳細資料。 如果 Elmah 無法建立 XML 檔案並儲存錯誤詳細資料，您會看到空白的錯誤報表。

開啟瀏覽器並移至 `http://localhost/ContosoUniversity`，然後要求不正確 URL，例如*Studentsxxx。* 您會看到 [系統產生的錯誤] 頁面，而不是 [ *GenericErrorPage* ] 頁面，因為 web.config 檔案中的 `customErrors` 設定是 "RemoteOnly"，而且您正在本機執行 IIS：

![HTTP 404 錯誤頁面](setting-folder-permissions/_static/image1.png)

現在請執行*Elmah* ，以查看錯誤報表。 使用系統管理員帳號憑證（&quot;admin&quot; 和 &quot;devpwd&quot;）登入之後，您會看到空白的錯誤記錄檔頁面，因為 Elmah 無法在*elmah*資料夾中建立 XML 檔案：

![錯誤記錄檔空白](setting-folder-permissions/_static/image2.png)

## <a name="set-write-permission-on-the-elmah-folder"></a>設定 Elmah 資料夾的寫入權限

您可以手動設定資料夾許可權，也可以讓它成為部署程式的自動部分。 自動執行需要複雜的 MSBuild 程式碼，而且因為您在第一次部署時只需要執行這項操作，所以請以手動方式進行下列步驟。 （如需如何使此部分部署程式的相關資訊，請參閱在 Sayed Hashimi 的 blog 上[設定 Web Publish 的資料夾許可權](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx)。）

1. 在 [檔案**管理器**] 中，流覽至*C:\inetpub\wwwroot\ContosoUniversity*。 以滑鼠右鍵按一下 [ *Elmah* ] 資料夾，選取 [**屬性**]，然後選取 [**安全性**] 索引標籤。
2. 按一下 [編輯]。
3. 在 [ **Elmah 的許可權**] 對話方塊中，選取 [ **DefaultAppPool**]，然後選取 [**允許**] 資料行中的 [**寫入**] 核取方塊。

    ![ELMAH 資料夾的許可權](setting-folder-permissions/_static/image3.png)

    （如果您在 [**群組或使用者名稱**] 清單中看不到 [ **DefaultAppPool** ]，表示您可能使用的其他方法與本教學課程中指定的不同，在您的電腦上設定 IIS 和 ASP.NET 4。 在此情況下，請找出指派給 Contoso 大學應用程式的應用程式集區所使用的身分識別，並將寫入權限授與該身分識別。 請參閱本教學課程結尾處的關於應用程式集區識別的連結。）在兩個對話方塊中按一下 **[確定]** 。

## <a name="retest-error-logging-and-reporting"></a>重新測試錯誤記錄和報告

以相同方式（要求錯誤的 URL）重新產生錯誤，並執行**錯誤記錄**頁面來進行測試。 這次錯誤會出現在頁面上。

![ELMAH 錯誤記錄頁面](setting-folder-permissions/_static/image4.png)

## <a name="summary"></a>總結

您現在已完成所有必要的工作，讓 Contoso 大學能夠在本機電腦上的 IIS 中正常運作。 在下一個教學課程中，您會將網站部署至 Azure，使其可公開使用。

## <a name="more-information"></a>詳細資訊

在此範例中，為什麼 Elmah 無法儲存記錄檔的原因相當明顯。 在問題原因不明顯的情況下，您可以使用 IIS 追蹤;請參閱 IIS.net 網站上的[在 IIS 7 中使用追蹤疑難排解失敗的要求](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)。

如需如何將許可權授與應用程式集區身分識別的詳細資訊，請參閱 IIS.net 網站上的[應用程式集](https://www.iis.net/learn/manage/configuring-security/application-pool-identities)區身分識別和[IIS 中的透過檔案系統 acl 保護內容](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls)。

> [!div class="step-by-step"]
> [上一頁](deploying-to-iis.md)
> [下一頁](deploying-to-production.md)
