---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
title: 使用 Visual Studio 或 Visual Web Developer 的 SQL Server Compact 部署 ASP.NET Web 應用程式：疑難排解（12/12） |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 3fc23eed-921d-4d46-a610-a2d156e4bd03
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
msc.type: authoredcontent
ms.openlocfilehash: db8f58e3679e6dea865dadb6f64916032dd9f38c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74639867"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-troubleshooting-12-of-12"></a><span data-ttu-id="86e21-103">使用 Visual Studio 或 Visual Web Developer 的 SQL Server Compact 部署 ASP.NET Web 應用程式：疑難排解（12/12）</span><span class="sxs-lookup"><span data-stu-id="86e21-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Troubleshooting (12 of 12)</span></span>

<span data-ttu-id="86e21-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="86e21-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="86e21-105">下載入門專案</span><span class="sxs-lookup"><span data-stu-id="86e21-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="86e21-106">這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="86e21-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="86e21-107">如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="86e21-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="86e21-108">如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。</span><span class="sxs-lookup"><span data-stu-id="86e21-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="86e21-109">如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署至 Windows Azure 網站，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="86e21-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

<span data-ttu-id="86e21-110">此頁面說明當您使用 Visual Studio 部署 ASP.NET web 應用程式時，可能會發生的一些常見問題。</span><span class="sxs-lookup"><span data-stu-id="86e21-110">This page describes some common problems that may arise when you deploy an ASP.NET web application by using Visual Studio.</span></span> <span data-ttu-id="86e21-111">針對每一個，會提供一或多個可能的原因和對應的解決方案。</span><span class="sxs-lookup"><span data-stu-id="86e21-111">For each one, one or more possible causes and corresponding solutions are provided.</span></span>

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a><span data-ttu-id="86e21-112">'/' 應用程式中的伺服器錯誤-目前的自訂錯誤設定導致無法從遠端查看錯誤的詳細資料</span><span class="sxs-lookup"><span data-stu-id="86e21-112">Server Error in '/' Application - Current Custom Error Settings Prevent Details of the Error from Being Viewed Remotely</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-113">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-113">Scenario</span></span>

<span data-ttu-id="86e21-114">將網站部署至遠端主機之後，您會收到錯誤訊息，指出 Web.config 檔案中的 customErrors 設定，但不會指出錯誤的實際原因：</span><span class="sxs-lookup"><span data-stu-id="86e21-114">After deploying a site to a remote host, you get an error message that mentions the customErrors setting in the Web.config file but doesn't indicate what the actual cause of the error was:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample1.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-115">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-115">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-116">根據預設，只有當您的 web 應用程式在本機電腦上執行時，ASP.NET 才會顯示詳細的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="86e21-116">By default, ASP.NET shows detailed error information only when your web application is running on the local computer.</span></span> <span data-ttu-id="86e21-117">當您的 web 應用程式可透過網際網路公開取得時，通常不會想要顯示詳細錯誤資訊，因為駭客可能可以使用這項資訊來找出應用程式中的弱點。</span><span class="sxs-lookup"><span data-stu-id="86e21-117">Generally you don't want to display detailed error information when your web application is publicly available over the Internet, because hackers may be able to use this information to find vulnerabilities in the application.</span></span> <span data-ttu-id="86e21-118">不過，當您將網站或更新部署至網站時，有時會發生錯誤，而且您需要取得實際的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="86e21-118">However, when you are deploying a site or updates to a site, sometimes something will go wrong and you need to get the actual error message.</span></span>

<span data-ttu-id="86e21-119">若要讓應用程式在遠端主機上執行時顯示詳細的錯誤訊息，請編輯 Web.config 檔案以將 `customErrors` 模式設定為關閉、重新部署應用程式，然後再次執行應用程式：</span><span class="sxs-lookup"><span data-stu-id="86e21-119">To enable the application to display detailed error messages when it runs on the remote host, edit the Web.config file to set `customErrors` mode off, redeploy the application, and run the application again:</span></span>

1. <span data-ttu-id="86e21-120">如果應用程式的 web.config 檔案在 `system.web` 元素中具有 `customErrors` 元素，請將 `mode` 屬性變更為 "off"。</span><span class="sxs-lookup"><span data-stu-id="86e21-120">If the application Web.config file has a `customErrors` element in the `system.web` element, change the `mode` attribute to "off".</span></span> <span data-ttu-id="86e21-121">否則，請將 `mode` 屬性設為 "off" 的 `system.web` 元素中的 `customErrors` 元素，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="86e21-121">Otherwise add a `customErrors` element in the `system.web` element with the `mode` attribute set to "off", as shown in the following example:</span></span>

    [!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample2.xml?highlight=3)]
2. <span data-ttu-id="86e21-122">部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="86e21-122">Deploy the application.</span></span>
3. <span data-ttu-id="86e21-123">執行應用程式，並重複先前造成錯誤發生的任何動作。</span><span class="sxs-lookup"><span data-stu-id="86e21-123">Run the application and repeat whatever you did earlier that caused the error to occur.</span></span> <span data-ttu-id="86e21-124">現在您可以看到實際的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="86e21-124">Now you can see what the actual error message is.</span></span>
4. <span data-ttu-id="86e21-125">當您解決錯誤時，請還原原始的 `customErrors` 設定，然後重新部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="86e21-125">When you have resolved the error, restore the original `customErrors` setting and redeploy the application.</span></span>

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a><span data-ttu-id="86e21-126">在使用 SQL Server Compact 的網頁中拒絕存取</span><span class="sxs-lookup"><span data-stu-id="86e21-126">Access is Denied in a Web Page that Uses SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-127">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-127">Scenario</span></span>

<span data-ttu-id="86e21-128">當您部署使用 SQL Server Compact 的網站，並在已部署的網站中執行可存取資料庫的頁面時，您會看到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="86e21-128">When you deploy a site that uses SQL Server Compact and you run a page in the deployed site that accesses the database, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-129">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-129">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-130">伺服器上的網路服務帳戶必須能夠讀取*bin\amd64*或*bin\x86*資料夾中的 SQL 服務 Compact 原生二進位檔，但它並沒有這些資料夾的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="86e21-130">The NETWORK SERVICE account on the server needs to be able to read SQL Service Compact native binaries that are in the *bin\amd64* or *bin\x86* folder, but it does not have read permissions for those folders.</span></span> <span data-ttu-id="86e21-131">在*bin*資料夾上設定 NETWORK SERVICE 的 [讀取] 許可權，並務必將許可權延伸至子資料夾。</span><span class="sxs-lookup"><span data-stu-id="86e21-131">Set read permission for NETWORK SERVICE on the *bin* folder, making sure to extend the permissions to subfolders.</span></span>

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a><span data-ttu-id="86e21-132">無法讀取設定檔案，因為許可權不足</span><span class="sxs-lookup"><span data-stu-id="86e21-132">Cannot Read Configuration File Due to Insufficient Permissions</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-133">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-133">Scenario</span></span>

<span data-ttu-id="86e21-134">當您按一下 [Visual Studio 發佈] 按鈕，將應用程式部署到本機電腦上的 IIS 時，發佈會失敗，而且 [**輸出**] 視窗會顯示類似下面的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="86e21-134">When you click the Visual Studio publish button to deploy an application to IIS on your local machine, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample4.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-135">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-135">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-136">若要在本機電腦上使用單鍵 [發行至 IIS]，您必須以系統管理員許可權執行 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="86e21-136">To use one-click publish to IIS on your local machine, you must be running Visual Studio with administrator permissions.</span></span> <span data-ttu-id="86e21-137">關閉 Visual Studio，然後以系統管理員許可權重新開機它。</span><span class="sxs-lookup"><span data-stu-id="86e21-137">Close Visual Studio and restart it with administrator permissions.</span></span>

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a><span data-ttu-id="86e21-138">無法連接到目的地電腦 。使用指定的進程</span><span class="sxs-lookup"><span data-stu-id="86e21-138">Could Not Connect to the Destination Computer ... Using the Specified Process</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-139">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-139">Scenario</span></span>

<span data-ttu-id="86e21-140">當您按一下 [Visual Studio 發佈] 按鈕來部署應用程式時，發行會失敗，而且 [**輸出**] 視窗會顯示類似下面的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="86e21-140">When you click the Visual Studio publish button to deploy an application, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample5.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-141">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-141">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-142">Proxy 伺服器正中斷與目的地伺服器的通訊。</span><span class="sxs-lookup"><span data-stu-id="86e21-142">A proxy server is interrupting communication with the destination server.</span></span> <span data-ttu-id="86e21-143">從 Windows [控制台] 或 Internet Explorer 中，選取 [**網際網路選項** **]，** 然後選取 [連線] 索引標籤。在 [**網際網路**內容] 對話方塊中，按一下 [ **LAN 設定**]。</span><span class="sxs-lookup"><span data-stu-id="86e21-143">From the Windows Control Panel or in Internet Explorer, select **Internet Options** and select the **Connections** tab. In the **Internet Properties** dialog box, click **LAN Settings**.</span></span> <span data-ttu-id="86e21-144">在 [**區域網路（LAN）設定**] 對話方塊中，清除 [**自動偵測設定**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="86e21-144">In the **Local Area Network (LAN) Settings** dialog box, clear the **Automatically detect settings** checkbox.</span></span> <span data-ttu-id="86e21-145">然後再次按一下 [發佈] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="86e21-145">Then click the publish button again.</span></span>

<span data-ttu-id="86e21-146">如果問題持續發生，請洽詢您的系統管理員，以判斷可以使用 proxy 或防火牆設定來完成的動作。</span><span class="sxs-lookup"><span data-stu-id="86e21-146">If the problem persists, contact your system administrator to determine what can be done with proxy or firewall settings.</span></span> <span data-ttu-id="86e21-147">發生此問題的原因是 Web Deploy 針對 Web 管理服務部署使用非標準埠（8172）;針對其他連接，Web Deploy 使用埠80。</span><span class="sxs-lookup"><span data-stu-id="86e21-147">The problem happens because Web Deploy uses a non-standard port for Web Management Service deployment (8172); for other connections, Web Deploy uses port 80.</span></span> <span data-ttu-id="86e21-148">當您要部署到協力廠商裝載提供者時，通常是使用 Web 管理服務。</span><span class="sxs-lookup"><span data-stu-id="86e21-148">When you are deploying to a third-party hosting provider, you are typically using the Web Management Service.</span></span>

## <a name="default-net-40-application-pool-does-not-exist"></a><span data-ttu-id="86e21-149">預設 .NET 4.0 應用程式集區不存在</span><span class="sxs-lookup"><span data-stu-id="86e21-149">Default .NET 4.0 Application Pool Does Not Exist</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-150">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-150">Scenario</span></span>

<span data-ttu-id="86e21-151">當您部署需要 .NET Framework 4 的應用程式時，您會看到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="86e21-151">When you deploy an application that requires the .NET Framework 4, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample6.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-152">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-152">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-153">IIS 中未安裝 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="86e21-153">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="86e21-154">如果您要部署的伺服器是您的開發電腦，且安裝了 Visual Studio 2010，則 ASP.NET 4 會安裝在電腦上，但可能不會安裝在 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="86e21-154">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="86e21-155">在您要部署的伺服器上，開啟提升許可權的命令提示字元，並執行下列命令，在 IIS 中安裝 ASP.NET 4：</span><span class="sxs-lookup"><span data-stu-id="86e21-155">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample7.cmd)]

<span data-ttu-id="86e21-156">您可能也需要手動設定預設應用程式集區的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="86e21-156">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="86e21-157">如需詳細資訊，請參閱[部署至 IIS 作為測試環境](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="86e21-157">For more information, see the [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) tutorial.</span></span>

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a><span data-ttu-id="86e21-158">初始化字串的格式不符合從索引0開始的規格。</span><span class="sxs-lookup"><span data-stu-id="86e21-158">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-159">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-159">Scenario</span></span>

<span data-ttu-id="86e21-160">當您使用單鍵發行來部署應用程式之後，當您執行存取資料庫的頁面時，會收到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="86e21-160">After you deploy an application using one-click publish, when you run a page that accesses the database you get the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample8.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-161">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-161">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-162">開啟已*部署網站中的 web.config*檔案，並檢查連接字串值是否以 `$(ReplaceableToken_`開頭，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="86e21-162">Open the *Web.config* file in the deployed site and check to see whether the connection string values begin with `$(ReplaceableToken_`, as in the following example:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample9.xml)]

<span data-ttu-id="86e21-163">如果連接字串看起來像這個範例，請編輯專案檔，並將下列屬性新增至所有組建設定的 `PropertyGroup` 元素：</span><span class="sxs-lookup"><span data-stu-id="86e21-163">If the connection strings look like this example, edit the project file and add the following property to the `PropertyGroup` element that is for all build configurations:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample10.xml)]

<span data-ttu-id="86e21-164">然後重新部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="86e21-164">Then redeploy the application.</span></span>

## <a name="http-500-internal-server-error"></a><span data-ttu-id="86e21-165">HTTP 500 內部伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="86e21-165">HTTP 500 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-166">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-166">Scenario</span></span>

<span data-ttu-id="86e21-167">當您執行部署的網站時，您會看到下列錯誤訊息，其中沒有指出錯誤原因的特定資訊：</span><span class="sxs-lookup"><span data-stu-id="86e21-167">When you run the deployed site, you see the following error message without specific information indicating the cause of the error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample11.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-168">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-168">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-169">500錯誤有許多原因，但如果您遵循這些教學課程，其中一個可能的原因是，您將 XML 元素放在其中一個 XML 轉換檔案中的錯誤位置。</span><span class="sxs-lookup"><span data-stu-id="86e21-169">There are many causes of 500 errors, but one possible cause if you are following these tutorials is that you put an XML element in the wrong place in one of the XML transformation files.</span></span> <span data-ttu-id="86e21-170">例如，如果您將轉換插入 `<system.web>` 之下的 `<location>` 專案，而不是直接在 `<configuration>`下，就會收到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="86e21-170">For example, you would get this error if you put the transformation that inserts a `<location>` element under `<system.web>` instead of directly under `<configuration>`.</span></span> <span data-ttu-id="86e21-171">在這種情況下，解決方法是更正 XML 轉換檔並重新部署。</span><span class="sxs-lookup"><span data-stu-id="86e21-171">The solution in that case is to correct the XML transformation file and redeploy.</span></span>

## <a name="http-50021-internal-server-error"></a><span data-ttu-id="86e21-172">HTTP 500.21 內部伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="86e21-172">HTTP 500.21 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-173">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-173">Scenario</span></span>

<span data-ttu-id="86e21-174">當您執行已部署的網站時，您會看到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="86e21-174">When you run the deployed site, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample12.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-175">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-175">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-176">您已部署的網站是以 ASP.NET 4 為目標，但 ASP.NET 4 並未在伺服器上的 IIS 中註冊。</span><span class="sxs-lookup"><span data-stu-id="86e21-176">The site you have deployed targets ASP.NET 4, but ASP.NET 4 is not registered in IIS on the server.</span></span> <span data-ttu-id="86e21-177">在伺服器上，開啟提升許可權的命令提示字元，並執行下列命令來註冊 ASP.NET 4：</span><span class="sxs-lookup"><span data-stu-id="86e21-177">On the server open an elevated command prompt and register ASP.NET 4 by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample13.cmd)]

<span data-ttu-id="86e21-178">您可能也需要手動設定預設應用程式集區的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="86e21-178">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="86e21-179">如需詳細資訊，請參閱[部署至 IIS 作為測試環境](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="86e21-179">For more information, see the [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) tutorial.</span></span>

## <a name="login-failed-opening-sql-server-express-database-in-app_data"></a><span data-ttu-id="86e21-180">登入無法在應用程式\_資料中開啟 SQL Server Express 資料庫</span><span class="sxs-lookup"><span data-stu-id="86e21-180">Login Failed Opening SQL Server Express Database in App\_Data</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-181">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-181">Scenario</span></span>

<span data-ttu-id="86e21-182">您已將*web.config*檔案連接字串更新為指向 SQL Server Express 資料庫，以作為*應用程式\_Data*資料夾中的 *.mdf*檔案，而且第一次執行應用程式時，您會看到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="86e21-182">You updated the *Web.config* file connection string to point to a SQL Server Express database as an *.mdf* file in your *App\_Data* folder, and the first time you run the application you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample14.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-183">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-183">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-184">*.Mdf*檔案的名稱不能與電腦上曾經存在的任何 SQL Server Express 資料庫名稱相符，即使您刪除了先前現有資料庫的 *.mdf*檔案也一樣。</span><span class="sxs-lookup"><span data-stu-id="86e21-184">The name of the *.mdf* file cannot match the name of any SQL Server Express database that has ever existed on your computer, even if you deleted the *.mdf* file of the previously existing database.</span></span> <span data-ttu-id="86e21-185">將 *.mdf*檔案的名稱變更為從未用來做為資料庫名稱的名稱，並將*web.config*檔案變更為使用新的名稱。</span><span class="sxs-lookup"><span data-stu-id="86e21-185">Change the name of the *.mdf* file to a name that has never been used as a database name and change the *Web.config* file to use the new name.</span></span> <span data-ttu-id="86e21-186">或者，您可以使用[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)來刪除先前現有 SQL Server Express 資料庫。</span><span class="sxs-lookup"><span data-stu-id="86e21-186">As an alternative, you can use [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete previously existing SQL Server Express databases.</span></span>

## <a name="model-compatibility-cannot-be-checked"></a><span data-ttu-id="86e21-187">無法檢查模型相容性</span><span class="sxs-lookup"><span data-stu-id="86e21-187">Model Compatibility Cannot be Checked</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-188">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-188">Scenario</span></span>

<span data-ttu-id="86e21-189">您已將*web.config*檔案連接字串更新為指向新的 SQL Server Express 資料庫，而且第一次執行應用程式時，您會看到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="86e21-189">You updated the *Web.config* file connection string to point to a new SQL Server Express database, and the first time you run the application you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample15.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-190">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-190">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-191">如果您放入 Web.config 檔案中的資料庫名稱在您的電腦之前曾經使用過，則資料庫中可能已經有一些資料表存在。</span><span class="sxs-lookup"><span data-stu-id="86e21-191">If the database name you put in the Web.config file was ever used before on your computer, a database might already exist with some tables in it.</span></span> <span data-ttu-id="86e21-192">選取先前尚未在電腦上使用的新名稱，並將*web.config*檔案變更為指向 [使用這個新的資料庫名稱]。</span><span class="sxs-lookup"><span data-stu-id="86e21-192">Select a new name that has not been used on your computer before and change the *Web.config* file to point to use this new database name.</span></span> <span data-ttu-id="86e21-193">或者，您可以使用[SQL Server Express 公用程式](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990)或[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)來刪除現有的資料庫。</span><span class="sxs-lookup"><span data-stu-id="86e21-193">As an alternative, you can use [SQL Server Express Utility](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) or [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete the existing database.</span></span>

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a><span data-ttu-id="86e21-194">腳本嘗試建立使用者或角色時發生 SQL 錯誤</span><span class="sxs-lookup"><span data-stu-id="86e21-194">SQL Error When a Script Attempts to Create Users or Roles</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-195">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-195">Scenario</span></span>

<span data-ttu-id="86e21-196">您正在使用 [**封裝/發行 SQL** ] 索引標籤上所設定的資料庫部署，在部署期間執行的 SQL 腳本包括 [建立使用者] 或 [建立角色] 命令，而執行這些命令時，腳本執行會失敗。</span><span class="sxs-lookup"><span data-stu-id="86e21-196">You are using database deployment configured on the **Package/Publish SQL** tab, SQL scripts that run during deployment include Create User or Create Role commands, and script execution fails when those commands are executed.</span></span> <span data-ttu-id="86e21-197">您可能會看到更詳細的訊息，如下所示：</span><span class="sxs-lookup"><span data-stu-id="86e21-197">You might see more detailed messages, such as the following:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample16.cmd)]

<span data-ttu-id="86e21-198">如果您在 [**發行 Web** ] 嚮導中設定資料庫部署，而不是 [**封裝/發行 SQL** ] 索引標籤，則會發生此錯誤，請在 [設定[及部署](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)] 論壇中建立執行緒，此解決方案將會新增至此 [疑難排解] 頁面。</span><span class="sxs-lookup"><span data-stu-id="86e21-198">If this error occurs when you have configured database deployment in the **Publish Web** wizard rather than the **Package/Publish SQL** tab, create a thread in the [Configuration and Deployment](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) forum, and the solution will be added to this troubleshooting page.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-199">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-199">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-200">您用來執行部署的使用者帳戶沒有建立使用者或角色的許可權。</span><span class="sxs-lookup"><span data-stu-id="86e21-200">The user account you are using to perform deployment does not have permission to create users or roles.</span></span> <span data-ttu-id="86e21-201">例如，主控公司可能會將 `db_datareader`、`db_datawriter`和 `db_ddladmin` 角色指派給它為您設定的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="86e21-201">For example, the hosting company might assign the `db_datareader`, `db_datawriter`, and `db_ddladmin` roles to the user account that it sets up for you.</span></span> <span data-ttu-id="86e21-202">這些就足以建立大部分的資料庫物件，而不是建立使用者或角色。</span><span class="sxs-lookup"><span data-stu-id="86e21-202">These are sufficient for creating most database objects, but not for creating users or roles.</span></span> <span data-ttu-id="86e21-203">避免錯誤的其中一種方法是從資料庫部署中排除使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="86e21-203">One way to avoid the error is by excluding users and roles from database deployment.</span></span> <span data-ttu-id="86e21-204">若要這麼做，您可以編輯資料庫自動產生之腳本的 `PreSource` 元素，使其包含下列屬性：</span><span class="sxs-lookup"><span data-stu-id="86e21-204">You can do this by editing the `PreSource` element for the database's automatically generated script so that it includes the following attributes:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample17.cmd)]

<span data-ttu-id="86e21-205">如需如何在專案檔中編輯 `PreSource` 元素的詳細資訊，請參閱[如何：編輯專案檔中的部署設定](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="86e21-205">For information about how to edit the `PreSource` element in the project file, see [How to: Edit Deployment Settings in the Project File](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx).</span></span> <span data-ttu-id="86e21-206">如果您的開發資料庫中的使用者或角色必須位於目的地資料庫中，請洽詢您的主機服務提供者以取得協助。</span><span class="sxs-lookup"><span data-stu-id="86e21-206">If the users or roles in your development database need to be in the destination database, contact your hosting provider for assistance.</span></span>

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a><span data-ttu-id="86e21-207">在部署期間執行自訂腳本時發生 SQL Server 逾時錯誤</span><span class="sxs-lookup"><span data-stu-id="86e21-207">SQL Server Timeout Error When Running Custom Scripts During Deployment</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-208">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-208">Scenario</span></span>

<span data-ttu-id="86e21-209">您已指定要在部署期間執行的自訂 SQL 腳本，而當 Web Deploy 執行時，它們會超時。</span><span class="sxs-lookup"><span data-stu-id="86e21-209">You have specified custom SQL scripts to run during deployment, and when Web Deploy runs them, they time out.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-210">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-210">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-211">執行多個具有不同交易模式的腳本可能會導致逾時錯誤。</span><span class="sxs-lookup"><span data-stu-id="86e21-211">Running multiple scripts that have different transaction modes can cause time-out errors.</span></span> <span data-ttu-id="86e21-212">根據預設，自動產生的腳本會在交易中執行，但是自訂腳本則不會。</span><span class="sxs-lookup"><span data-stu-id="86e21-212">By default, automatically generated scripts run in a transaction, but custom scripts do not.</span></span> <span data-ttu-id="86e21-213">如果您在 [**封裝/發行 SQL** ] 索引標籤上選取 [**從現有資料庫提取資料及/或架構**] 選項，而且加入自訂 SQL 腳本，則必須變更某些腳本的交易設定，讓所有腳本都使用相同的交易設定。</span><span class="sxs-lookup"><span data-stu-id="86e21-213">If you select the **Pull data and/or schema from an existing database** option on the **Package/Publish SQL** tab, and if you add a custom SQL script, you must change transaction settings on some scripts so that all scripts use the same transaction settings.</span></span> <span data-ttu-id="86e21-214">如需詳細資訊，請參閱[如何：使用 Web 應用程式專案部署資料庫](https://msdn.microsoft.com/library/dd465343.aspx)。</span><span class="sxs-lookup"><span data-stu-id="86e21-214">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343.aspx).</span></span>

<span data-ttu-id="86e21-215">如果您已設定交易設定，讓全部都相同，但仍然收到此錯誤，則可能的因應措施是分別執行腳本。</span><span class="sxs-lookup"><span data-stu-id="86e21-215">If you have configured transaction settings so that all are the same but still get this error, a possible workaround is to run the scripts separately.</span></span> <span data-ttu-id="86e21-216">在 [**封裝/發行**SQL] 索引標籤的 [**資料庫腳本**] 方格中，清除導致逾時錯誤之腳本的 [**包含**] 核取方塊，然後發佈專案。</span><span class="sxs-lookup"><span data-stu-id="86e21-216">In the **Database Scripts** grid in the **Package/Publish** SQL tab, clear the **Include** check box for the script that causes the timeout error, then publish the project.</span></span> <span data-ttu-id="86e21-217">然後回到 [**資料庫腳本**] 方格中，選取該腳本的 [**包含**] 核取方塊，並清除其他腳本的 [**包含**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="86e21-217">Then go back into the **Database Scripts** grid, select that script's **Include** check box, and clear the **Include** check boxes for the other scripts.</span></span> <span data-ttu-id="86e21-218">然後再次發行專案。</span><span class="sxs-lookup"><span data-stu-id="86e21-218">Then publish the project again.</span></span> <span data-ttu-id="86e21-219">這次當您發佈時，只有選取的自訂腳本會執行。</span><span class="sxs-lookup"><span data-stu-id="86e21-219">This time when you publish, only the selected custom script runs.</span></span>

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a><span data-ttu-id="86e21-220">尚未提供網站資訊清單的串流資料</span><span class="sxs-lookup"><span data-stu-id="86e21-220">Stream Data of Site Manifest Is Not Yet Available</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-221">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-221">Scenario</span></span>

<span data-ttu-id="86e21-222">當您使用*部署 .cmd*檔案搭配 `t` （測試）選項來安裝套件時，您會看到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="86e21-222">When you are installing a package using the *deploy.cmd* file with the `t` (test) option, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample18.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-223">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-223">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-224">錯誤訊息表示命令無法產生測試報告。</span><span class="sxs-lookup"><span data-stu-id="86e21-224">The error message means that the command cannot produce a test report.</span></span> <span data-ttu-id="86e21-225">不過，如果您使用 [`y` （實際安裝）] 選項，此命令可能會執行。</span><span class="sxs-lookup"><span data-stu-id="86e21-225">However, the command might run if you use the `y` (actual installation) option.</span></span> <span data-ttu-id="86e21-226">訊息只會指出在測試模式中執行命令時發生問題。</span><span class="sxs-lookup"><span data-stu-id="86e21-226">The message indicates only that there is a problem with running the command in test mode.</span></span>

## <a name="this-application-requires-managedruntimeversion-v40"></a><span data-ttu-id="86e21-227">此應用程式需要 ManagedRuntimeVersion v4。0</span><span class="sxs-lookup"><span data-stu-id="86e21-227">This Application Requires ManagedRuntimeVersion v4.0</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-228">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-228">Scenario</span></span>

<span data-ttu-id="86e21-229">當您嘗試部署時，您會看到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="86e21-229">When you attempt to deploy, you see the following error message:</span></span>

 <span data-ttu-id="86e21-230">錯誤： ' sitemanifest/dbFullSql [@path= ' C:\TEMP\AdventureWorksGrant.sql ']/sqlScript ' 的資料流程資料尚無法使用。</span><span class="sxs-lookup"><span data-stu-id="86e21-230">Error: The stream data of 'sitemanifest/dbFullSql[@path='C:\TEMP\AdventureWorksGrant.sql']/sqlScript' is not yet available.</span></span> <span data-ttu-id="86e21-231">您嘗試使用的應用程式集區，' managedRuntimeVersion ' 屬性設定為 ' v2.0 '。</span><span class="sxs-lookup"><span data-stu-id="86e21-231">The application pool that you are trying to use has the 'managedRuntimeVersion' property set to 'v2.0'.</span></span> <span data-ttu-id="86e21-232">此應用程式需要 ' v4.0 '。</span><span class="sxs-lookup"><span data-stu-id="86e21-232">This application requires 'v4.0'.</span></span> 

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-233">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-233">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-234">IIS 中未安裝 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="86e21-234">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="86e21-235">如果您要部署的伺服器是您的開發電腦，且安裝了 Visual Studio 2010，則 ASP.NET 4 會安裝在電腦上，但可能不會安裝在 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="86e21-235">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="86e21-236">在您要部署的伺服器上，開啟提升許可權的命令提示字元，並執行下列命令，在 IIS 中安裝 ASP.NET 4：</span><span class="sxs-lookup"><span data-stu-id="86e21-236">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample19.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a><span data-ttu-id="86e21-237">無法轉換 DeploymentProviderOptions。</span><span class="sxs-lookup"><span data-stu-id="86e21-237">Unable to cast Microsoft.Web.Deployment.DeploymentProviderOptions</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-238">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-238">Scenario</span></span>

<span data-ttu-id="86e21-239">當您部署套件時，您會看到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="86e21-239">When you are deploying a package, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample20.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-240">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-240">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-241">您正嘗試使用 Web Deploy 1.1 UI，從 IIS 管理員部署到已安裝 Web Deploy 2.0 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="86e21-241">You are trying to deploy from IIS Manager using the Web Deploy 1.1 UI to a server that has Web Deploy 2.0 installed.</span></span> <span data-ttu-id="86e21-242">如果您要透過匯入封裝來使用 IIS 遠端系統管理工具來進行部署，請在建立連線時，核取 [**可用的新功能**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="86e21-242">If you are using the IIS Remote Administration Tool to deploy by importing a package, check the **New Features Available** dialog box when you establish the connection.</span></span> <span data-ttu-id="86e21-243">（在第一次建立連接時，這個對話方塊可能只會顯示一次。</span><span class="sxs-lookup"><span data-stu-id="86e21-243">(This dialog box might only be shown once when the connection is first established.</span></span> <span data-ttu-id="86e21-244">若要清除連線並重新開始，請關閉 [IIS 管理員]，然後在命令提示字元中輸入 `inetmgr /reset`，再次啟動它。）如果列出的其中一個功能是**WEB DEPLOY UI**，而且其版本號碼低於8，則您要部署的伺服器可能會安裝1.1 和2.0 版的 Web Deploy。</span><span class="sxs-lookup"><span data-stu-id="86e21-244">To clear the connection and start over, close IIS Manager and start it up again by entering `inetmgr /reset` at the command prompt.) If one of the features listed is **Web Deploy UI**, and it has a version number lower than 8, the server you are deploying to might have both 1.1 and 2.0 versions of Web Deploy installed.</span></span> <span data-ttu-id="86e21-245">若要從已安裝2.0 的用戶端部署，伺服器必須只安裝 Web Deploy 2.0。</span><span class="sxs-lookup"><span data-stu-id="86e21-245">To deploy from a client that has 2.0 installed, the server must have only Web Deploy 2.0 installed.</span></span> <span data-ttu-id="86e21-246">您必須洽詢您的主機服務提供者，才能解決此問題。</span><span class="sxs-lookup"><span data-stu-id="86e21-246">You will have to contact your hosting provider to resolve this problem.</span></span>

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a><span data-ttu-id="86e21-247">無法載入 SQL Server Compact 的原生元件</span><span class="sxs-lookup"><span data-stu-id="86e21-247">Unable to load the native components of SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-248">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-248">Scenario</span></span>

<span data-ttu-id="86e21-249">當您執行已部署的網站時，您會看到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="86e21-249">When you run the deployed site, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample21.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-250">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-250">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-251">已部署的網站在應用程式的*bin*資料夾底下，沒有具有原生元件的*amd64*和*x86*子資料夾。</span><span class="sxs-lookup"><span data-stu-id="86e21-251">The deployed site does not have *amd64* and *x86* subfolders with the native assemblies in them under the application's *bin* folder.</span></span> <span data-ttu-id="86e21-252">在已安裝 SQL Server Compact 的電腦上，原生元件位於*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*。</span><span class="sxs-lookup"><span data-stu-id="86e21-252">On a computer that has SQL Server Compact installed, the native assemblies are located in *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*.</span></span> <span data-ttu-id="86e21-253">在 Visual Studio 專案的正確資料夾中取得正確檔案的最佳方式，是安裝 NuGet Entityframework.sqlservercompact 套件。</span><span class="sxs-lookup"><span data-stu-id="86e21-253">The best way to get the correct files into the correct folders in a Visual Studio project is to install the NuGet SqlServerCompact package.</span></span> <span data-ttu-id="86e21-254">套件安裝會加入後置組建腳本，將原生元件複製到*amd64*和*x86*。</span><span class="sxs-lookup"><span data-stu-id="86e21-254">Package installation adds a post-build script to copy the native assemblies into *amd64* and *x86*.</span></span> <span data-ttu-id="86e21-255">不過，為了要部署這些專案，您必須手動將它們包含在專案中。</span><span class="sxs-lookup"><span data-stu-id="86e21-255">In order for these to be deployed, however, you have to manually include them in the project.</span></span> <span data-ttu-id="86e21-256">如需詳細資訊，請參閱[部署 SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="86e21-256">For more information, see the [Deploying SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a><span data-ttu-id="86e21-257">部署 Entity Framework Code First 應用程式之後發生「路徑無效」錯誤</span><span class="sxs-lookup"><span data-stu-id="86e21-257">"Path is not valid" error after deploying an Entity Framework Code First application</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-258">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-258">Scenario</span></span>

<span data-ttu-id="86e21-259">您部署的應用程式會使用 Entity Framework Code First 移轉和 DBMS （例如 SQL Server Compact），將其資料庫儲存在應用程式\_Data 資料夾的檔案中。</span><span class="sxs-lookup"><span data-stu-id="86e21-259">You deploy an application that uses Entity Framework Code First Migrations and a DBMS such as SQL Server Compact which stores its database in a file in the App\_Data folder.</span></span> <span data-ttu-id="86e21-260">您已設定 Code First 移轉在第一次部署之後建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="86e21-260">You have Code First Migrations configured to create the database after your first deployment.</span></span> <span data-ttu-id="86e21-261">當您執行應用程式時，您會收到類似下列範例的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="86e21-261">When you run the application you get an error message like the following example:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample22.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-262">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-262">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-263">Code First 嘗試建立資料庫，但應用程式\_的資料檔案夾不存在。</span><span class="sxs-lookup"><span data-stu-id="86e21-263">Code First is attempting to create the database but the App\_Data folder does not exist.</span></span> <span data-ttu-id="86e21-264">當您部署時，*應用\_程式*中沒有任何檔案，或您在 [**專案屬性**] 視窗的 [**封裝/發行 Web** ] 索引標籤上選取了 [**排除應用程式\_資料**]，可能是您沒有任何檔案。</span><span class="sxs-lookup"><span data-stu-id="86e21-264">Either you didn't have any files in the *App\_Data* folder when you deployed, or you selected **Exclude App\_Data** on the **Package/Publish Web** tab of the **Project Properties** window.</span></span> <span data-ttu-id="86e21-265">如果資料夾中沒有要複製到伺服器的檔案，部署程式將不會在伺服器上建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="86e21-265">The deployment process won't create a folder on the server if there are no files in the folder to be copied to the server.</span></span> <span data-ttu-id="86e21-266">如果您已在網站中設定資料庫，則如果您在發行設定檔中選取 [**移除目的地的其他**檔案]，部署程式將會刪除檔案和*應用程式\_資料*資料夾本身。</span><span class="sxs-lookup"><span data-stu-id="86e21-266">If you already had the database set up in the site, the deployment process will delete the files and the *App\_Data* folder itself if you selected **Remove additional files at destination** in the publish profile.</span></span> <span data-ttu-id="86e21-267">若要解決此問題，請將預留位置檔案（例如 .txt 檔案）放在*應用程式\_Data*資料夾中，確定您未選取 [**排除應用程式]\_資料**，然後重新部署。</span><span class="sxs-lookup"><span data-stu-id="86e21-267">To solve the problem, put a placeholder file such as a .txt file in the *App\_Data* folder, make sure you do not have **Exclude App\_Data** selected, and redeploy.</span></span> 

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a><span data-ttu-id="86e21-268">「無法使用與基礎 RCW 分隔的 COM 物件」。</span><span class="sxs-lookup"><span data-stu-id="86e21-268">"COM object that has been separated from its underlying RCW cannot be used."</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-269">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-269">Scenario</span></span>

<span data-ttu-id="86e21-270">您已成功使用單鍵發行來部署您的應用程式，然後開始收到此錯誤：</span><span class="sxs-lookup"><span data-stu-id="86e21-270">You have been successfully using one-click publish to deploy your application and then you start getting this error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample23.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-271">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-271">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-272">關閉和重新開機 Visual Studio 通常是解決此錯誤所需的一切。</span><span class="sxs-lookup"><span data-stu-id="86e21-272">Closing and restarting Visual Studio is usually all that is required to resolve this error.</span></span>

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a><span data-ttu-id="86e21-273">部署失敗，因為用於發佈的使用者認證沒有 setACL 授權單位</span><span class="sxs-lookup"><span data-stu-id="86e21-273">Deployment Fails Because User Credentials Used for Publishing Don't Have setACL Authority</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-274">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-274">Scenario</span></span>

<span data-ttu-id="86e21-275">發行失敗並出現錯誤，指出您沒有設定資料夾許可權的授權單位（您所使用的使用者帳戶沒有 setACL 授權單位）。</span><span class="sxs-lookup"><span data-stu-id="86e21-275">Publishing fails with an error that indicates you don't have authority to set folder permissions (the user account you are using doesn't have setACL authority).</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-276">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-276">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-277">根據預設，Visual Studio 會設定網站根資料夾的讀取權限，以及應用程式\_Data 資料夾的寫入權限。</span><span class="sxs-lookup"><span data-stu-id="86e21-277">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="86e21-278">如果您知道網站資料夾的預設許可權是正確的，而且不需要設定，您可以藉由將 **&lt;IncludeSetACLProviderOn 目的地&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 新增至發行設定檔檔案（以影響單一設定檔）或對 wpp .targets 檔（影響所有設定檔），停用此行為。</span><span class="sxs-lookup"><span data-stu-id="86e21-278">If you know that the default permissions on site folders are correct and do not need to be set, you disable this behavior by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="86e21-279">如需如何編輯這些檔案的詳細資訊，請參閱[如何：編輯設定檔（. .pubxml）中的部署設定](https://msdn.microsoft.com/library/ff398069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="86e21-279">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span> 

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a><span data-ttu-id="86e21-280">應用程式嘗試寫入應用程式資料夾時發生拒絕存取的錯誤</span><span class="sxs-lookup"><span data-stu-id="86e21-280">Access Denied Errors when the Application Tries to Write to an Application Folder</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-281">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-281">Scenario</span></span>

<span data-ttu-id="86e21-282">您的應用程式在嘗試建立或編輯其中一個應用程式資料夾中的檔案時發生錯誤，因為它沒有該資料夾的寫入權限。</span><span class="sxs-lookup"><span data-stu-id="86e21-282">Your application errors when it tries to create or edit a file in one of the application folders, because it does not have write authority for that folder.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-283">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-283">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-284">根據預設，Visual Studio 會設定網站根資料夾的讀取權限，以及應用程式\_Data 資料夾的寫入權限。</span><span class="sxs-lookup"><span data-stu-id="86e21-284">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="86e21-285">如果您的應用程式需要子資料夾的寫入權限，您可以設定該資料夾的許可權，如[設定資料夾許可權](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)和[部署到生產環境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教學課程中所示。</span><span class="sxs-lookup"><span data-stu-id="86e21-285">If your application needs write access to a sub-folder, you can set permissions for that folder as shown in the [Setting Folder Permissions](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md) and [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorials.</span></span> <span data-ttu-id="86e21-286">如果您的應用程式需要網站根資料夾的寫入存取權，您必須將 **&lt;IncludeSetACLProviderOn 目的地&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 新增至發行設定檔檔案（以影響單一設定檔）或 wpp .targets 檔（以影響所有設定檔），以防止它在根資料夾上設定唯讀存取。</span><span class="sxs-lookup"><span data-stu-id="86e21-286">If your application needs write access to the root folder of the site, you have to prevent it from setting read-only access on the root folder by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="86e21-287">如需如何編輯這些檔案的詳細資訊，請參閱[如何：編輯設定檔（. .pubxml）中的部署設定](https://msdn.microsoft.com/library/ff398069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="86e21-287">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span> <a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a><span data-ttu-id="86e21-288">設定錯誤-targetFramework 屬性參考的版本比安裝的版本還要新 .NET Framework</span><span class="sxs-lookup"><span data-stu-id="86e21-288">Configuration Error - targetFramework attribute references a version that is later than the installed version of the .NET Framework</span></span>

### <a name="scenario"></a><span data-ttu-id="86e21-289">情節</span><span class="sxs-lookup"><span data-stu-id="86e21-289">Scenario</span></span>

<span data-ttu-id="86e21-290">您已成功發行以 ASP.NET 4.5 為目標的 Web 專案，但當您執行應用程式（並在 web.config 檔案中將 `customErrors` 模式設定為 "off"）時，會收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="86e21-290">You successfully published a web project that targets ASP.NET 4.5, but when you run the application (with the `customErrors` mode set to "off" in the Web.config file) you get the following error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample24.cmd)]

<span data-ttu-id="86e21-291">錯誤頁面的 [來源錯誤] 方塊會反白顯示 Web.config 中的下列這一行，做為錯誤的原因：</span><span class="sxs-lookup"><span data-stu-id="86e21-291">The Source Error box of the error page highlights the following line from Web.config as the cause of the error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample25.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="86e21-292">可能的原因和解決方案</span><span class="sxs-lookup"><span data-stu-id="86e21-292">Possible Cause and Solution</span></span>

<span data-ttu-id="86e21-293">伺服器不支援 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="86e21-293">The server does not support ASP.NET 4.5.</span></span> <span data-ttu-id="86e21-294">請洽詢主控提供者，以判斷何時及是否可新增 ASP.NET 4.5 的支援。</span><span class="sxs-lookup"><span data-stu-id="86e21-294">Contact the hosting provider to determine when and if support for ASP.NET 4.5 can be added.</span></span> <span data-ttu-id="86e21-295">如果無法選擇升級伺服器，您就必須改為部署以 ASP.NET 4 或更早版本為目標的 Web 專案。如果您將 ASP.NET 4 或舊版 Web 專案部署到相同的目的地，請在 [**發行 web** wizard] 的 [**設定**] 索引標籤上，選取 [**移除目的地的其他**檔案] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="86e21-295">If upgrading the server is not an option, you have to deploy a web project that targets ASP.NET 4 or earlier instead.If you deploy an ASP.NET 4 or earlier web project to the same destination, select the **Remove additional files at destination** check box on the **Settings** tab of the **Publish Web** wizard.</span></span> <span data-ttu-id="86e21-296">如果您未選取 [**移除目的地的其他**檔案]，將會繼續取得設定錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="86e21-296">If you don't select **Remove additional files at destination**, you will continue to get the Configuration Error page.</span></span>

<span data-ttu-id="86e21-297">[專案**屬性**] 視窗包含 [目標 framework] 下拉式清單，但您無法解決此問題，只需將 **.NET Framework 4.5**變更為 **.NET Framework 4**。</span><span class="sxs-lookup"><span data-stu-id="86e21-297">The project **Properties** windows includes a Target framework drop-down list, but you can't resolve this problem by just changing that from **.NET Framework 4.5** to **.NET Framework 4**.</span></span> <span data-ttu-id="86e21-298">如果您將目標 framework 變更為舊版架構，此專案仍會參考較新的 framework 版本元件，而且不會執行。</span><span class="sxs-lookup"><span data-stu-id="86e21-298">If you change the target framework to an earlier framework version, the project will still have references to the later framework version's assemblies and will not run.</span></span> <span data-ttu-id="86e21-299">您必須手動變更這些參考，或建立以 .NET Framework 4 或更早版本為目標的新專案。</span><span class="sxs-lookup"><span data-stu-id="86e21-299">You have to manually change those references or create a new project that targets .NET Framework 4 or earlier.</span></span> <span data-ttu-id="86e21-300">如需詳細資訊，請參閱[Web Sites 的 .NET Framework 目標](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="86e21-300">For more information, see [.NET Framework Targeting for Web Sites](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="86e21-301">上一篇</span><span class="sxs-lookup"><span data-stu-id="86e21-301">Previous</span></span>](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
