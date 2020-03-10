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
# <a name="aspnet-web-deployment-using-visual-studio-setting-folder-permissions"></a><span data-ttu-id="52aa7-103">使用 Visual Studio ASP.NET Web 部署：設定資料夾許可權</span><span class="sxs-lookup"><span data-stu-id="52aa7-103">ASP.NET Web Deployment using Visual Studio: Setting Folder Permissions</span></span>

<span data-ttu-id="52aa7-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="52aa7-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="52aa7-105">下載入門專案</span><span class="sxs-lookup"><span data-stu-id="52aa7-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="52aa7-106">本教學課程系列說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商裝載提供者。</span><span class="sxs-lookup"><span data-stu-id="52aa7-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="52aa7-107">如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。</span><span class="sxs-lookup"><span data-stu-id="52aa7-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="52aa7-108">概觀</span><span class="sxs-lookup"><span data-stu-id="52aa7-108">Overview</span></span>

<span data-ttu-id="52aa7-109">在本教學課程中，您會在已部署的網站中設定*Elmah*資料夾的資料夾許可權，讓應用程式可以在該資料夾中建立記錄檔。</span><span class="sxs-lookup"><span data-stu-id="52aa7-109">In this tutorial, you set folder permissions for the *Elmah* folder in the deployed web site so that the application can create log files in that folder.</span></span>

<span data-ttu-id="52aa7-110">當您使用 Visual Studio 程式開發伺服器（Cassini）或 IIS Express 在 Visual Studio 中測試 web 應用程式時，應用程式會在您的身分識別下執行。</span><span class="sxs-lookup"><span data-stu-id="52aa7-110">When you test a web application in Visual Studio using the Visual Studio Development Server (Cassini) or IIS Express, the application runs under your identity.</span></span> <span data-ttu-id="52aa7-111">您很可能是開發電腦上的系統管理員，而且擁有完整許可權可以對任何資料夾中的任何檔案執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="52aa7-111">You are most likely an administrator on your development computer and have full authority to do anything to any file in any folder.</span></span> <span data-ttu-id="52aa7-112">但當應用程式在 IIS 底下執行時，它會在為網站指派的應用程式集區定義的身分識別下執行。</span><span class="sxs-lookup"><span data-stu-id="52aa7-112">But when an application runs under IIS, it runs under the identity defined for the application pool that the site is assigned to.</span></span> <span data-ttu-id="52aa7-113">這通常是系統定義的帳戶，其許可權有限。</span><span class="sxs-lookup"><span data-stu-id="52aa7-113">This is typically a system-defined account that has limited permissions.</span></span> <span data-ttu-id="52aa7-114">根據預設，它對您 web 應用程式的檔案和資料夾具有 [讀取] 和 [執行] 許可權，但不具有寫入存取權。</span><span class="sxs-lookup"><span data-stu-id="52aa7-114">By default it has read and execute permissions on your web application's files and folders, but it doesn't have write access.</span></span>

<span data-ttu-id="52aa7-115">如果您的應用程式會建立或更新檔案，這是 web 應用程式中常見的需求，這會變成一個問題。</span><span class="sxs-lookup"><span data-stu-id="52aa7-115">This becomes an issue if your application creates or updates files, which is a common need in web applications.</span></span> <span data-ttu-id="52aa7-116">在 Contoso 大學應用程式中，Elmah 會在*elmah*資料夾中建立 XML 檔案，以便儲存錯誤的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="52aa7-116">In the Contoso University application, Elmah creates XML files in the *Elmah* folder in order to save details about errors.</span></span> <span data-ttu-id="52aa7-117">即使您未使用類似 Elmah 的專案，您的網站可能會讓使用者上傳檔案，或執行其他工作，將資料寫入您的網站中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="52aa7-117">Even if you don't use something like Elmah, your site might let users upload files or perform other tasks that write data to a folder in your site.</span></span>

<span data-ttu-id="52aa7-118">提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="52aa7-118">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="test-error-logging-and-reporting"></a><span data-ttu-id="52aa7-119">測試錯誤記錄和報告</span><span class="sxs-lookup"><span data-stu-id="52aa7-119">Test error logging and reporting</span></span>

<span data-ttu-id="52aa7-120">若要查看應用程式在 IIS 中無法正確運作的方式（雖然在 Visual Studio 中進行測試），您可能會造成一則通常會記錄的錯誤，然後開啟 Elmah 錯誤記錄檔以查看詳細資料。</span><span class="sxs-lookup"><span data-stu-id="52aa7-120">To see how the application doesn't work correctly in IIS (although it did when you tested it in Visual Studio), you can cause an error that would normally be logged by Elmah, and then open the Elmah error log to see the details.</span></span> <span data-ttu-id="52aa7-121">如果 Elmah 無法建立 XML 檔案並儲存錯誤詳細資料，您會看到空白的錯誤報表。</span><span class="sxs-lookup"><span data-stu-id="52aa7-121">If Elmah was unable to create an XML file and store the error details, you see an empty error report.</span></span>

<span data-ttu-id="52aa7-122">開啟瀏覽器並移至 `http://localhost/ContosoUniversity`，然後要求不正確 URL，例如*Studentsxxx。*</span><span class="sxs-lookup"><span data-stu-id="52aa7-122">Open a browser and go to `http://localhost/ContosoUniversity`, and then request an invalid URL like *Studentsxxx.aspx*.</span></span> <span data-ttu-id="52aa7-123">您會看到 [系統產生的錯誤] 頁面，而不是 [ *GenericErrorPage* ] 頁面，因為 web.config 檔案中的 `customErrors` 設定是 "RemoteOnly"，而且您正在本機執行 IIS：</span><span class="sxs-lookup"><span data-stu-id="52aa7-123">You see a system-generated error page instead of the *GenericErrorPage.aspx* page because the `customErrors` setting in the Web.config file is "RemoteOnly" and you are running IIS locally:</span></span>

![HTTP 404 錯誤頁面](setting-folder-permissions/_static/image1.png)

<span data-ttu-id="52aa7-125">現在請執行*Elmah* ，以查看錯誤報表。</span><span class="sxs-lookup"><span data-stu-id="52aa7-125">Now run *Elmah.axd* to see the error report.</span></span> <span data-ttu-id="52aa7-126">使用系統管理員帳號憑證（&quot;admin&quot; 和 &quot;devpwd&quot;）登入之後，您會看到空白的錯誤記錄檔頁面，因為 Elmah 無法在*elmah*資料夾中建立 XML 檔案：</span><span class="sxs-lookup"><span data-stu-id="52aa7-126">After you log in with the administrator account credentials (&quot;admin&quot; and &quot;devpwd&quot;), you see an empty error log page because Elmah was unable to create an XML file in the *Elmah* folder:</span></span>

![錯誤記錄檔空白](setting-folder-permissions/_static/image2.png)

## <a name="set-write-permission-on-the-elmah-folder"></a><span data-ttu-id="52aa7-128">設定 Elmah 資料夾的寫入權限</span><span class="sxs-lookup"><span data-stu-id="52aa7-128">Set write permission on the Elmah folder</span></span>

<span data-ttu-id="52aa7-129">您可以手動設定資料夾許可權，也可以讓它成為部署程式的自動部分。</span><span class="sxs-lookup"><span data-stu-id="52aa7-129">You can set folder permissions manually or you can make it an automatic part of the deployment process.</span></span> <span data-ttu-id="52aa7-130">自動執行需要複雜的 MSBuild 程式碼，而且因為您在第一次部署時只需要執行這項操作，所以請以手動方式進行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="52aa7-130">Making it automatic requires complex MSBuild code, and since you only have to do this the first time you deploy, the following steps how to do it manually.</span></span> <span data-ttu-id="52aa7-131">（如需如何使此部分部署程式的相關資訊，請參閱在 Sayed Hashimi 的 blog 上[設定 Web Publish 的資料夾許可權](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx)。）</span><span class="sxs-lookup"><span data-stu-id="52aa7-131">(For information about how to make this part of the deployment process, see [Setting Folder Permissions on Web Publish](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) on Sayed Hashimi's blog.)</span></span>

1. <span data-ttu-id="52aa7-132">在 [檔案**管理器**] 中，流覽至*C:\inetpub\wwwroot\ContosoUniversity*。</span><span class="sxs-lookup"><span data-stu-id="52aa7-132">In **File Explorer**, navigate to *C:\inetpub\wwwroot\ContosoUniversity*.</span></span> <span data-ttu-id="52aa7-133">以滑鼠右鍵按一下 [ *Elmah* ] 資料夾，選取 [**屬性**]，然後選取 [**安全性**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="52aa7-133">Right-click the *Elmah* folder, select **Properties**, and then select the **Security** tab.</span></span>
2. <span data-ttu-id="52aa7-134">按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="52aa7-134">Click **Edit**.</span></span>
3. <span data-ttu-id="52aa7-135">在 [ **Elmah 的許可權**] 對話方塊中，選取 [ **DefaultAppPool**]，然後選取 [**允許**] 資料行中的 [**寫入**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="52aa7-135">In the **Permissions for Elmah** dialog box, select **DefaultAppPool**, and then select the **Write** check box in the **Allow** column.</span></span>

    ![ELMAH 資料夾的許可權](setting-folder-permissions/_static/image3.png)

    <span data-ttu-id="52aa7-137">（如果您在 [**群組或使用者名稱**] 清單中看不到 [ **DefaultAppPool** ]，表示您可能使用的其他方法與本教學課程中指定的不同，在您的電腦上設定 IIS 和 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="52aa7-137">(If you don't see **DefaultAppPool** in the **Group or user names** list, you probably used some other method than the one specified in this tutorial to set up IIS and ASP.NET 4 on your computer.</span></span> <span data-ttu-id="52aa7-138">在此情況下，請找出指派給 Contoso 大學應用程式的應用程式集區所使用的身分識別，並將寫入權限授與該身分識別。</span><span class="sxs-lookup"><span data-stu-id="52aa7-138">In that case, find out what identity is used by the application pool assigned to the Contoso University application, and grant write permission to that identity.</span></span> <span data-ttu-id="52aa7-139">請參閱本教學課程結尾處的關於應用程式集區識別的連結。）在兩個對話方塊中按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="52aa7-139">See the links about application pool identities at the end of this tutorial.) Click **OK** in both dialog boxes.</span></span>

## <a name="retest-error-logging-and-reporting"></a><span data-ttu-id="52aa7-140">重新測試錯誤記錄和報告</span><span class="sxs-lookup"><span data-stu-id="52aa7-140">Retest error logging and reporting</span></span>

<span data-ttu-id="52aa7-141">以相同方式（要求錯誤的 URL）重新產生錯誤，並執行**錯誤記錄**頁面來進行測試。</span><span class="sxs-lookup"><span data-stu-id="52aa7-141">Test by causing an error again in the same way (request a bad URL) and run the **Error Log** page.</span></span> <span data-ttu-id="52aa7-142">這次錯誤會出現在頁面上。</span><span class="sxs-lookup"><span data-stu-id="52aa7-142">This time the error appears on the page.</span></span>

![ELMAH 錯誤記錄頁面](setting-folder-permissions/_static/image4.png)

## <a name="summary"></a><span data-ttu-id="52aa7-144">總結</span><span class="sxs-lookup"><span data-stu-id="52aa7-144">Summary</span></span>

<span data-ttu-id="52aa7-145">您現在已完成所有必要的工作，讓 Contoso 大學能夠在本機電腦上的 IIS 中正常運作。</span><span class="sxs-lookup"><span data-stu-id="52aa7-145">You have now completed all of the tasks necessary to get Contoso University working correctly in IIS on your local computer.</span></span> <span data-ttu-id="52aa7-146">在下一個教學課程中，您會將網站部署至 Azure，使其可公開使用。</span><span class="sxs-lookup"><span data-stu-id="52aa7-146">In the next tutorial, you will make the site publicly available by deploying it to Azure.</span></span>

## <a name="more-information"></a><span data-ttu-id="52aa7-147">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="52aa7-147">More information</span></span>

<span data-ttu-id="52aa7-148">在此範例中，為什麼 Elmah 無法儲存記錄檔的原因相當明顯。</span><span class="sxs-lookup"><span data-stu-id="52aa7-148">In this example, the reason why Elmah was unable to save log files was fairly obvious.</span></span> <span data-ttu-id="52aa7-149">在問題原因不明顯的情況下，您可以使用 IIS 追蹤;請參閱 IIS.net 網站上的[在 IIS 7 中使用追蹤疑難排解失敗的要求](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)。</span><span class="sxs-lookup"><span data-stu-id="52aa7-149">You can use IIS tracing in cases where the cause of the problem is not so obvious; see [Troubleshooting Failed Requests Using Tracing in IIS 7](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) on the IIS.net site.</span></span>

<span data-ttu-id="52aa7-150">如需如何將許可權授與應用程式集區身分識別的詳細資訊，請參閱 IIS.net 網站上的[應用程式集](https://www.iis.net/learn/manage/configuring-security/application-pool-identities)區身分識別和[IIS 中的透過檔案系統 acl 保護內容](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls)。</span><span class="sxs-lookup"><span data-stu-id="52aa7-150">For more information about how to grant permissions to application pool identities, see [Application Pool Identities](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) and [Secure Content in IIS Through File System ACLs](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) on the IIS.net site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="52aa7-151">[上一頁](deploying-to-iis.md)
> [下一頁](deploying-to-production.md)</span><span class="sxs-lookup"><span data-stu-id="52aa7-151">[Previous](deploying-to-iis.md)
[Next](deploying-to-production.md)</span></span>
