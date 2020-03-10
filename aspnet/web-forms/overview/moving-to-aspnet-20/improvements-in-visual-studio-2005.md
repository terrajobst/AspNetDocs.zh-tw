---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Visual Studio 2005 中的改進 |Microsoft Docs
author: microsoft
description: Visual Studio 2005 為 Web 應用程式開發人員提供一份很長的 Web 專案改良功能和增強功能。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: 64215d556ded0850537a13856fe69b094116ebca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575576"
---
# <a name="improvements-in-visual-studio-2005"></a><span data-ttu-id="a37da-103">Visual Studio 2005 中的改善</span><span class="sxs-lookup"><span data-stu-id="a37da-103">Improvements in Visual Studio 2005</span></span>

<span data-ttu-id="a37da-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a37da-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="a37da-105">Visual Studio 2005 為 Web 應用程式開發人員提供一份很長的 Web 專案改良功能和增強功能。</span><span class="sxs-lookup"><span data-stu-id="a37da-105">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span>

<span data-ttu-id="a37da-106">Visual Studio 2005 為 Web 應用程式開發人員提供一份很長的 Web 專案改良功能和增強功能。</span><span class="sxs-lookup"><span data-stu-id="a37da-106">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span> <span data-ttu-id="a37da-107">就像 Visual Studio .NET 2002 和2003的功能強大，Web 專案的處理方式有很多抱怨。</span><span class="sxs-lookup"><span data-stu-id="a37da-107">As powerful as Visual Studio .NET 2002 and 2003 are, there were many complaints in the way that Web projects were handled.</span></span> <span data-ttu-id="a37da-108">Visual Studio 2005 加入大量的新功能，以解決這些抱怨。</span><span class="sxs-lookup"><span data-stu-id="a37da-108">Visual Studio 2005 adds a significant number of new features in order to address these complaints.</span></span> <span data-ttu-id="a37da-109">針對偏好 Visual Studio .NET 2003 處理 Web 應用程式之編譯方式的人員，請參閱[Web 應用程式專案](https://go.microsoft.com/fwlink/?LinkId=57870)。</span><span class="sxs-lookup"><span data-stu-id="a37da-109">For those who prefer the way that Visual Studio .NET 2003 handled compilation of Web applications, see [Web Application Projects](https://go.microsoft.com/fwlink/?LinkId=57870).</span></span>

<span data-ttu-id="a37da-110">在此課程模組中，我們將探討 Web 專案建立、管理和開發方面的改進。</span><span class="sxs-lookup"><span data-stu-id="a37da-110">In this module, well cover improvements in Web project creation, management, and development.</span></span> <span data-ttu-id="a37da-111">在稍後的課程模組中，我們將進一步探討建立 Web 專案和部署它們的功能。</span><span class="sxs-lookup"><span data-stu-id="a37da-111">In a later module, well cover improvements in building Web projects and deploying them.</span></span>

## <a name="frontpage-server-extensions"></a><span data-ttu-id="a37da-112">FrontPage Server Extensions</span><span class="sxs-lookup"><span data-stu-id="a37da-112">FrontPage Server Extensions</span></span>

<span data-ttu-id="a37da-113">Visual Studio FrontPage Server Extensions 需要 .NET 2002 和2003，才能建立或建立 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="a37da-113">Visual Studio .NET 2002 and 2003 required FrontPage Server Extensions on the box in order to create or build Web projects.</span></span> <span data-ttu-id="a37da-114">開發人員可以選擇兩種不同的存取模式（FrontPage Server Extensions 或檔案存取模式），這兩者都用 FrontPage Server Extensions 來執行工作，例如在 IIS 中設定應用程式根目錄等等。</span><span class="sxs-lookup"><span data-stu-id="a37da-114">Developers did have a choice between two different access modes (FrontPage Server Extensions or File access mode), both used FrontPage Server Extensions to perform tasks such as setting the application root in IIS, etc.</span></span>

<span data-ttu-id="a37da-115">Visual Studio 2005 會移除對本機專案的 FrontPage Server Extensions 的依賴。</span><span class="sxs-lookup"><span data-stu-id="a37da-115">Visual Studio 2005 removes the reliance on FrontPage Server Extensions for local projects.</span></span> <span data-ttu-id="a37da-116">Visual Studio 2005 現在會直接存取 IIS 元資料庫，而不是使用 FrontPage Server Extensions。</span><span class="sxs-lookup"><span data-stu-id="a37da-116">Visual Studio 2005 now accesses the IIS metabase directly instead of using the FrontPage Server Extensions.</span></span> <span data-ttu-id="a37da-117">Visual Studio 2005 也新增了 FTP 的支援，允許遠端專案存取，而不需要 FrontPage Server Extensions。</span><span class="sxs-lookup"><span data-stu-id="a37da-117">Visual Studio 2005 also adds support for FTP which allows for remote project access without requiring FrontPage Server Extensions.</span></span>

<span data-ttu-id="a37da-118">對於想要在專案中使用 FrontPage Server Extensions 的開發人員而言，仍然可以使用此選項。</span><span class="sxs-lookup"><span data-stu-id="a37da-118">For those developers who want to use FrontPage Server Extensions in their projects, the option is still available.</span></span> <span data-ttu-id="a37da-119">不過，根據 ASP.NET 開發人員社區的強大意見反應，這不是必要條件。</span><span class="sxs-lookup"><span data-stu-id="a37da-119">However, based upon strong feedback from the ASP.NET developer community, it is not a requirement.</span></span>

> [!NOTE]
> <span data-ttu-id="a37da-120">遠端專案建立、開啟等等，仍然需要 FrontPage Server Extensions。</span><span class="sxs-lookup"><span data-stu-id="a37da-120">FrontPage Server Extensions are still required for remote project creation, opening, etc.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="a37da-121">ASP.NET 程式開發伺服器</span><span class="sxs-lookup"><span data-stu-id="a37da-121">ASP.NET Development Server</span></span>

<span data-ttu-id="a37da-122">Visual Studio 2005 隨附新的網頁伺服器，稱為 ASP.NET 程式開發伺服器。</span><span class="sxs-lookup"><span data-stu-id="a37da-122">Visual Studio 2005 ships with a new Web server called ASP.NET Development Server.</span></span> <span data-ttu-id="a37da-123">（此網頁伺服器先前稱為 Cassini）。</span><span class="sxs-lookup"><span data-stu-id="a37da-123">(This Web server was previously known as Cassini.)</span></span>

<span data-ttu-id="a37da-124">ASP.NET 程式開發伺服器有數個優點。</span><span class="sxs-lookup"><span data-stu-id="a37da-124">There are several benefits of the ASP.NET Development Server.</span></span>

- <span data-ttu-id="a37da-125">非系統管理員現在可以針對 Web 服務器進行開發和偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="a37da-125">It is now possible for non-Administrators to develop and debug against a Web server.</span></span>
- <span data-ttu-id="a37da-126">ASP.NET 程式開發伺服器會動態地將虛擬目錄對應至檔案系統中的任何位置，以允許彈性的專案位置。</span><span class="sxs-lookup"><span data-stu-id="a37da-126">The ASP.NET Development Server dynamically maps virtual directories to any location in the file system allowing for flexible project locations.</span></span>
- <span data-ttu-id="a37da-127">Windows XP Professional 上已使用 IIS 的使用者現在可以建立新的 Web 應用程式，而不會影響 IIS 中預設網站的檔案或資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="a37da-127">Users on Windows XP Professional who are already using IIS will now be able to create new Web applications that will not affect the file or folder structure of their Default Web Site in IIS.</span></span>

<span data-ttu-id="a37da-128">不需要特殊設定即可利用 ASP.NET 程式開發伺服器。</span><span class="sxs-lookup"><span data-stu-id="a37da-128">No special configuration is required to take advantage of the ASP.NET Development Server.</span></span> <span data-ttu-id="a37da-129">當調試或流覽檔案系統上主控的 Web 專案時，Visual Studio 2005 將會在隨機埠上自動啟動 ASP.NET 程式開發伺服器的實例，以服務要求。</span><span class="sxs-lookup"><span data-stu-id="a37da-129">When a Web project that is hosted on the file system is debugged or browsed, Visual Studio 2005 will automatically start an instance of the ASP.NET Development Server on a random port to service the request.</span></span>

<span data-ttu-id="a37da-130">本課程模組稍後的 ASP.NET 程式開發伺服器將涵蓋詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a37da-130">More information will be covered on the ASP.NET Development Server later in this module.</span></span>

## <a name="improved-file-management"></a><span data-ttu-id="a37da-131">改良的檔案管理</span><span class="sxs-lookup"><span data-stu-id="a37da-131">Improved File Management</span></span>

<span data-ttu-id="a37da-132">在 Visual Studio 2002 和2003中，專案檔（適用于 VB.NET 的 vbproj 和 .csproj C#）會儲存在 Web 應用程式中所有檔案的資訊。</span><span class="sxs-lookup"><span data-stu-id="a37da-132">In Visual Studio 2002 and 2003, a project file (.vbproj for VB.NET and .csproj for C#) stored information on all files in the Web application.</span></span> <span data-ttu-id="a37da-133">方案總管顯示是根據專案檔中的檔案資訊。</span><span class="sxs-lookup"><span data-stu-id="a37da-133">The Solution Explorer display is based upon the file information in the project file.</span></span> <span data-ttu-id="a37da-134">因此，在使用外部編輯器的情況下，方案總管通常會顯示不正確的資訊。</span><span class="sxs-lookup"><span data-stu-id="a37da-134">Because of this, the Solution Explorer would often display inaccurate information in cases where external editors were used.</span></span> <span data-ttu-id="a37da-135">Visual Studio 2002 和2003通常會覆寫檔案變更，或不會顯示最新版本的檔案。</span><span class="sxs-lookup"><span data-stu-id="a37da-135">Visual Studio 2002 and 2003 would often overwrite file changes or not display the most recent version of files.</span></span>

<span data-ttu-id="a37da-136">Visual Studio 2005 與專案檔相同。</span><span class="sxs-lookup"><span data-stu-id="a37da-136">Visual Studio 2005 does away with the project file.</span></span> <span data-ttu-id="a37da-137">相反地，它會直接從磁片讀取檔案和資料夾資訊，以精確顯示專案中的檔案。</span><span class="sxs-lookup"><span data-stu-id="a37da-137">Instead, it reads the file and folder information directly from the disk, resulting in an accurate display of the files in your project.</span></span> <span data-ttu-id="a37da-138">因為 Visual Studio 2002 和2003中的 [參考] 資料夾不代表 Web 應用程式中的實際資料夾，Visual Studio 2005 也會從方案總管移除 [參考] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a37da-138">Because the References folder in Visual Studio 2002 and 2003 does not represent an actual folder in your Web application, Visual Studio 2005 also removes the References folder from Solution Explorer.</span></span> <span data-ttu-id="a37da-139">若要存取 Visual Studio 2005 中專案的參考，您應該使用專案的屬性頁。</span><span class="sxs-lookup"><span data-stu-id="a37da-139">To access the references for your project in Visual Studio 2005, you should use the Property pages for the project.</span></span>

## <a name="creating-web-projects"></a><span data-ttu-id="a37da-140">建立 Web 專案</span><span class="sxs-lookup"><span data-stu-id="a37da-140">Creating Web Projects</span></span>

<span data-ttu-id="a37da-141">Web 開發人員有許多新選項可用於 Visual Studio 2005 中的專案建立。</span><span class="sxs-lookup"><span data-stu-id="a37da-141">Web developers have many new options available for project creation in Visual Studio 2005.</span></span> <span data-ttu-id="a37da-142">現在可以在檔案系統中的任何位置建立網站，然後使用新的 ASP.NET 程式開發伺服器來進行調試或流覽。</span><span class="sxs-lookup"><span data-stu-id="a37da-142">Web sites can now be created anywhere in the file system and can then be debugged or browsed using the new ASP.NET Development Server.</span></span> <span data-ttu-id="a37da-143">開發人員也可以使用 FTP 建立新的網站。</span><span class="sxs-lookup"><span data-stu-id="a37da-143">Developers can also create new Web sites using FTP.</span></span>

<span data-ttu-id="a37da-144">按一下這裡以觀看在 Visual Studio 2005 中建立 Web 專案的影片逐步解說。</span><span class="sxs-lookup"><span data-stu-id="a37da-144">Click here to view a video walkthrough of creating Web projects in Visual Studio 2005.</span></span>

![](improvements-in-visual-studio-2005/_static/image1.png)

[<span data-ttu-id="a37da-145">開啟全螢幕影片</span><span class="sxs-lookup"><span data-stu-id="a37da-145">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a><span data-ttu-id="a37da-146">檔案系統專案</span><span class="sxs-lookup"><span data-stu-id="a37da-146">File System Projects</span></span>

<span data-ttu-id="a37da-147">如您在影片逐步解說中所見，您可以選擇在檔案系統上，透過檔案共用在本機電腦或遠端位置上建立網站。</span><span class="sxs-lookup"><span data-stu-id="a37da-147">As you saw in the video walkthrough, you can choose to create Web sites on the file system either on the local machine or on a remote location via a file share.</span></span> <span data-ttu-id="a37da-148">在檔案系統上建立的網站會使用 ASP.NET 程式開發伺服器進行流覽和調試。</span><span class="sxs-lookup"><span data-stu-id="a37da-148">Web sites that are created on the file system are browsed and debugged using the ASP.NET Development Server.</span></span>

> [!NOTE]
> <span data-ttu-id="a37da-149">ASP.NET 程式開發伺服器可能會對客戶造成一些混淆。</span><span class="sxs-lookup"><span data-stu-id="a37da-149">The ASP.NET Development Server may cause some confusion for customers.</span></span> <span data-ttu-id="a37da-150">如果在檔案系統上的 IISs 目錄結構中建立 Web 專案（也就是 c：/inetpub/wwwroot），則在從 Visual Studio 2005 內啟動網站時，仍然會透過 ASP.NET 程式開發伺服器來流覽該網站。</span><span class="sxs-lookup"><span data-stu-id="a37da-150">If a Web project is created on the file system in IISs directory structure (i.e. c:/inetpub/wwwroot), the Web site will still be browsed via the ASP.NET Development Server when launched from within Visual Studio 2005.</span></span> <span data-ttu-id="a37da-151">因此，任何 IIS 設定（亦即驗證方法）都不適用。</span><span class="sxs-lookup"><span data-stu-id="a37da-151">Therefore, any IIS configuration (i.e. authentication methods) is not applicable.</span></span>

<span data-ttu-id="a37da-152">預設的 Web 專案也會藉由只包含 default.aspx 頁面、default.cs 檔和應用程式/_Data 資料夾來移除許多額外負荷。</span><span class="sxs-lookup"><span data-stu-id="a37da-152">The default web project also removes a lot of the overhead by only includes a Default.aspx page, default.cs file, and an App/_Data folder.</span></span> <span data-ttu-id="a37da-153">Web.config 和特殊資料夾（例如應用程式/_code）會視需要新增。</span><span class="sxs-lookup"><span data-stu-id="a37da-153">The web.config and special folders (i.e. app/_code) are added as they are needed.</span></span> <span data-ttu-id="a37da-154">您的 Web 專案只包含您需要的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="a37da-154">Your web project only includes the files and folders that you need.</span></span>

### <a name="http-projects"></a><span data-ttu-id="a37da-155">HTTP 專案</span><span class="sxs-lookup"><span data-stu-id="a37da-155">HTTP Projects</span></span>

<span data-ttu-id="a37da-156">HTTP 專案可以是在本機 IIS 網站或遠端網站上建立的專案。</span><span class="sxs-lookup"><span data-stu-id="a37da-156">HTTP projects can either be projects that are created on a local IIS Web site or on a remote Web site.</span></span> <span data-ttu-id="a37da-157">預設專案位置為 `http://localhost`。</span><span class="sxs-lookup"><span data-stu-id="a37da-157">The default project location is `http://localhost`.</span></span> <span data-ttu-id="a37da-158">如果您按一下 [流覽] 按鈕，則會有兩個 HTTP 選項： [本機 IIS] 和 [遠端網站]。</span><span class="sxs-lookup"><span data-stu-id="a37da-158">If you click the Browse button, there are two HTTP options: Local IIS and Remote Site.</span></span> <span data-ttu-id="a37da-159">這兩個選項的主要差異在於網站資訊顯示在 [選擇位置] 對話方塊中的方法，以及檔案複製到 Web 服務器的方式。</span><span class="sxs-lookup"><span data-stu-id="a37da-159">The main difference in these two options is the method in which the web site information is displayed in the Choose Location dialog and in how the files are copied to the Web server.</span></span>

<span data-ttu-id="a37da-160">本機 IIS 選項會從本機電腦上的設定檔讀取網站資訊，並使用檔案系統來複製檔案。</span><span class="sxs-lookup"><span data-stu-id="a37da-160">The Local IIS option reads the site information from the metabase on the local machine and files are copied using the file system.</span></span> <span data-ttu-id="a37da-161">[遠端網站] 選項會使用 FrontPage Server Extensions 並使用 HTTP 和 FrontPage Server Extensions RPC 呼叫來複製網站資訊和檔案。</span><span class="sxs-lookup"><span data-stu-id="a37da-161">The Remote Site option uses the FrontPage Server Extensions and the site information and files are copied using HTTP and FrontPage Server Extensions RPC calls.</span></span>

> [!NOTE]
> <span data-ttu-id="a37da-162">不再使用 vs # # #/_tmp .htm 檔案和 get/_aspx/_ver 來判斷版本資訊。</span><span class="sxs-lookup"><span data-stu-id="a37da-162">The vs###/_tmp.htm file and get/_aspx/_ver.aspx are no longer used to determine version information.</span></span>

<span data-ttu-id="a37da-163">預設的 HTTP 選項是 [本機 IIS]。</span><span class="sxs-lookup"><span data-stu-id="a37da-163">The default HTTP option is Local IIS.</span></span> <span data-ttu-id="a37da-164">此選項會讀取 IIS 的元資料庫，以判斷可用的網站和要在其中建立內容的位置。</span><span class="sxs-lookup"><span data-stu-id="a37da-164">This option reads the IIS Metabase to determine which sites are available and the location in which to create content.</span></span> <span data-ttu-id="a37da-165">您可以選取不同的資料夾或虛擬目錄，方法是在樹狀檢視中選取它。</span><span class="sxs-lookup"><span data-stu-id="a37da-165">You can select a different folder or virtual directory by selecting it in the tree view.</span></span> <span data-ttu-id="a37da-166">您也可以建立新的虛擬目錄、將資料夾標示為應用程式，以及從此對話方塊中刪除現有的虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="a37da-166">You can also create a new virtual directory, mark folders as applications, as well as delete existing virtual directories from this dialog box.</span></span>

![[選擇位置] 對話方塊](improvements-in-visual-studio-2005/_static/image1.gif)

<span data-ttu-id="a37da-168">**圖 1**： [選擇位置] 對話方塊</span><span class="sxs-lookup"><span data-stu-id="a37da-168">**Figure 1**: The Choose Location Dialog</span></span>

<span data-ttu-id="a37da-169">不同于舊版 Visual Studio，如果您核取 [**使用安全通訊端層**] 核取方塊，且 SSL 憑證不符合您要流覽的 URL，您會看到 [安全性警示] 對話方塊，詢問您是否要繼續。</span><span class="sxs-lookup"><span data-stu-id="a37da-169">Unlike in earlier versions of Visual Studio, if you check the **Use Secure Sockets Layer** checkbox and the SSL certificate does not match the URL you are browsing, you will be presented with a Security Alert dialog asking you if you would like to proceed.</span></span> <span data-ttu-id="a37da-170">使用 Visual Studio .NET 2003，如果憑證不相符，則建立專案會失敗。</span><span class="sxs-lookup"><span data-stu-id="a37da-170">Using Visual Studio .NET 2003, if the certificate was not a matching one, creating the project would fail.</span></span>

![關於 SSL 憑證的安全性警示](improvements-in-visual-studio-2005/_static/image2.gif)

<span data-ttu-id="a37da-172">**圖 2**：關於 SSL 憑證的安全性警示</span><span class="sxs-lookup"><span data-stu-id="a37da-172">**Figure 2**: Security Alert Regarding SSL Certificate</span></span>

### <a name="note-on-host-headers"></a><span data-ttu-id="a37da-173">主機標頭上的注意事項</span><span class="sxs-lookup"><span data-stu-id="a37da-173">Note on Host Headers</span></span>

<span data-ttu-id="a37da-174">如果您要在系結至特定 IP 的網站上建立 Web 應用程式，您將需要確定已設定主機標頭。</span><span class="sxs-lookup"><span data-stu-id="a37da-174">If you are creating a Web application on a site bound to a specific IP, you will need to ensure that a host header is configured.</span></span> <span data-ttu-id="a37da-175">否則，Visual Studio 會在 `http://localhost`建立網站，但在從 IDE 內流覽或調試網站時，IP 位址將無法正確解析。</span><span class="sxs-lookup"><span data-stu-id="a37da-175">Otherwise, Visual Studio will create the site at `http://localhost`, but the IP address will not resolve correctly when the site is browsed or debugged from within the IDE.</span></span>

<span data-ttu-id="a37da-176">如果您選取 [遠端網站] 選項，對話方塊會變更為，讓您輸入新網站的目的地 URL。</span><span class="sxs-lookup"><span data-stu-id="a37da-176">If you select the Remote Site option, the dialog changes to allow you to enter the destination URL for the new Web site.</span></span> <span data-ttu-id="a37da-177">此 URL 必須位於已啟用 FrontPage Server Extensions 的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="a37da-177">This URL must be on a server that has the FrontPage Server Extensions enabled.</span></span> <span data-ttu-id="a37da-178">如果您想要使用 FrontPage Server Extensions 來處理本機 Web 服務器，可以使用 [遠端網站] 選項，並指定本機 URL。</span><span class="sxs-lookup"><span data-stu-id="a37da-178">If you want to work with your local Web server using the FrontPage Server Extensions, you can use the Remote Site option and specify a local URL.</span></span>

![在遠端伺服器上建立網站](improvements-in-visual-studio-2005/_static/image1.jpg)

<span data-ttu-id="a37da-180">**圖 3**：在遠端伺服器上建立網站</span><span class="sxs-lookup"><span data-stu-id="a37da-180">**Figure 3**: Creating a Web Site on a Remote Server</span></span>

<span data-ttu-id="a37da-181">透過 SSL 在遠端網站上建立應用程式時，如果 SSL 憑證不相符，則 [確認] 對話方塊會與使用 [本機 IIS] 選項時所顯示的對話方塊略有不同。</span><span class="sxs-lookup"><span data-stu-id="a37da-181">When creating an application on a remote site via SSL, if the SSL certificate does not match, the confirmation dialog is slightly different than the dialog displayed when using the Local IIS option.</span></span>

![遠端網站安全性警示](improvements-in-visual-studio-2005/_static/image3.gif)

<span data-ttu-id="a37da-183">**圖 4**：遠端網站安全性警示</span><span class="sxs-lookup"><span data-stu-id="a37da-183">**Figure 4**: The Remote Site Security Alert</span></span>

<a id="_Toc116100243"></a>

#### <a name="ftp"></a><span data-ttu-id="a37da-184">FTP</span><span class="sxs-lookup"><span data-stu-id="a37da-184">FTP</span></span>

<span data-ttu-id="a37da-185">Visual Studio 2005 引進了透過 FTP 建立網站的選項。</span><span class="sxs-lookup"><span data-stu-id="a37da-185">Visual Studio 2005 introduces the option to create Web sites via FTP.</span></span> <span data-ttu-id="a37da-186">當您使用此選項時，IDE 會在使用者的 temp 資料夾中建立檔案，然後使用 FTP 將檔案移到 FTP 位置。</span><span class="sxs-lookup"><span data-stu-id="a37da-186">When you use this option, the IDE creates the files locally in the users temp folder and then uses FTP to move the files to the FTP location.</span></span>

> [!NOTE]
> <span data-ttu-id="a37da-187">暫存資料夾位置為 c：/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;應用程式名稱&gt;</span><span class="sxs-lookup"><span data-stu-id="a37da-187">The temp folder location is c:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="a37da-188">使用 FTP 選項時，您會看到 [選擇位置] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a37da-188">When using the FTP option, you will be presented with a Choose Location dialog.</span></span> <span data-ttu-id="a37da-189">您在此對話方塊中輸入必要的 FTP 連接資訊，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a37da-189">You enter the required FTP connection information into this dialog as shown below.</span></span>

![FTP 的 [選擇位置] 對話方塊](improvements-in-visual-studio-2005/_static/image2.jpg)

<span data-ttu-id="a37da-191">**圖 5**： FTP 的 [選擇位置] 對話方塊</span><span class="sxs-lookup"><span data-stu-id="a37da-191">**Figure 5**: The Choose Location Dialog for FTP</span></span>

## <a name="lab-setup-ftp-site-and-create-a-project"></a><span data-ttu-id="a37da-192">實驗室：設定 FTP 網站和建立專案</span><span class="sxs-lookup"><span data-stu-id="a37da-192">Lab: Setup FTP site and create a project</span></span>

<span data-ttu-id="a37da-193">下列步驟會設定 FTP 網站，讓使用者具有只能透過 FTP 上傳至的位置。</span><span class="sxs-lookup"><span data-stu-id="a37da-193">The following steps configure the FTP site so that a user has a location that only they can upload to via FTP.</span></span>

### <a name="install-the-ftp-service"></a><span data-ttu-id="a37da-194">安裝 FTP 服務</span><span class="sxs-lookup"><span data-stu-id="a37da-194">Install the FTP Service</span></span>

1. <span data-ttu-id="a37da-195">開啟 [新增] [移除程式]，選取 [新增/移除 Windows 元件]</span><span class="sxs-lookup"><span data-stu-id="a37da-195">Open Add Remove Programs, select Add/Remove Windows Components</span></span>
2. <span data-ttu-id="a37da-196">選取 [Internet Information Services （Windows 2003 上的應用程式伺服器）]，然後按一下 [**詳細資料**]。</span><span class="sxs-lookup"><span data-stu-id="a37da-196">Select Internet Information Services (Application Server on Windows 2003) and click **Details**.</span></span>
3. <span data-ttu-id="a37da-197">檢查**檔案傳輸通訊協定（FTP）服務**，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="a37da-197">Check **File Transfer Protocol (FTP) Service** and click **OK**.</span></span>
4. <span data-ttu-id="a37da-198">按 **[下一步]** 安裝 FTP 服務。</span><span class="sxs-lookup"><span data-stu-id="a37da-198">Click **Next** to install the FTP service.</span></span>

### <a name="create-a-new-folder-for-content"></a><span data-ttu-id="a37da-199">為內容建立新的資料夾</span><span class="sxs-lookup"><span data-stu-id="a37da-199">Create a New Folder for Content</span></span>

1. <span data-ttu-id="a37da-200">在 Windows Explorer 中，于 c：/inetpub/wwwroot 內建立名為**User1**的新資料夾。</span><span class="sxs-lookup"><span data-stu-id="a37da-200">In Windows Explorer, create a new folder called **User1** inside of c:/inetpub/wwwroot.</span></span>

#### <a name="configure-folders-and-permissions-on-folders"></a><span data-ttu-id="a37da-201">設定資料夾的資料夾和許可權。</span><span class="sxs-lookup"><span data-stu-id="a37da-201">Configure folders and permissions on folders.</span></span>

1. <span data-ttu-id="a37da-202">從 [系統管理工具] 開啟 [Internet Information Services] 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="a37da-202">Open the Internet Information Services snap-in from Administrative Tools.</span></span> <span data-ttu-id="a37da-203">您現在會在 [電腦名稱稱] 節點底下有一個 [FTP 網站] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a37da-203">You will now have an FTP Sites folder under the computer name node.</span></span>
2. <span data-ttu-id="a37da-204">展開 [ **FTP 網站**]。</span><span class="sxs-lookup"><span data-stu-id="a37da-204">Expand **FTP Sites**.</span></span>
3. <span data-ttu-id="a37da-205">以滑鼠右鍵按一下**預設的 FTP 網站**，依序選取 [**新增**]、[**虛擬目錄** **] 和 [下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="a37da-205">Right-click the **Default FTP Site**, select **New**, then **Virtual Directory**, then click **Next**.</span></span>
4. <span data-ttu-id="a37da-206">輸入**User1**作為虛擬目錄名稱，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="a37da-206">Enter **User1** for the virtual directory name and click **Next**.</span></span>
5. <span data-ttu-id="a37da-207">針對路徑輸入**c：/inetpub/wwwroot/User1** ，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="a37da-207">Enter **c:/inetpub/wwwroot/User1** for the path and click **Next**.</span></span>
6. <span data-ttu-id="a37da-208">按 **[下一步**]，然後按一下 **[完成**] 以完成嚮導。</span><span class="sxs-lookup"><span data-stu-id="a37da-208">Click **Next** and then **Finish** to complete the wizard.</span></span>
7. <span data-ttu-id="a37da-209">以滑鼠右鍵按一下 [預設 FTP 網站] 底下的**User1**虛擬目錄，然後選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="a37da-209">Right-click the **User1** virtual directory under Default FTP Site and select **Properties**.</span></span>
8. <span data-ttu-id="a37da-210">勾選 [**寫入**] 核取方塊，然後按一下 **[確定**] 以關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a37da-210">Check the **Write** checkbox and click **OK** to close the dialog.</span></span>
9. <span data-ttu-id="a37da-211">以滑鼠右鍵按一下 [**預設的 FTP 網站**]，然後選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="a37da-211">Right-click **Default FTP Site** and select **Properties**.</span></span>
10. <span data-ttu-id="a37da-212">在 [**安全性帳戶**] 索引標籤上，取消核取 [**允許匿名連接**]。</span><span class="sxs-lookup"><span data-stu-id="a37da-212">On the **Security Accounts** tab, uncheck **Allow Anonymous Connections**.</span></span>
11. <span data-ttu-id="a37da-213">在詢問您是否要繼續的對話方塊中按一下 **[是**]。</span><span class="sxs-lookup"><span data-stu-id="a37da-213">Click **Yes** in the dialog asking if you want to continue.</span></span>
12. <span data-ttu-id="a37da-214">按一下 **[確定]** 關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a37da-214">Click **OK** to close the dialog.</span></span>
13. <span data-ttu-id="a37da-215">在 [**網站**] 節點底下，展開 [**預設的網站**]。</span><span class="sxs-lookup"><span data-stu-id="a37da-215">Expand the **Default Web Site** under the **Web Sites** node.</span></span>
14. <span data-ttu-id="a37da-216">以滑鼠右鍵按一下**User1**目錄，然後選取 [**屬性**]</span><span class="sxs-lookup"><span data-stu-id="a37da-216">Right-click the **User1** directory and select **Properties**</span></span>
15. <span data-ttu-id="a37da-217">在 [**應用程式設定**] 區段中，按一下 [**建立**]，將資料夾標示為應用程式。</span><span class="sxs-lookup"><span data-stu-id="a37da-217">In the **Application Settings** section, click **Create** to mark the folder as an application.</span></span>
16. <span data-ttu-id="a37da-218">按一下 **[確定]** 關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a37da-218">Click **OK** to close the dialog.</span></span>
17. <span data-ttu-id="a37da-219">關閉 [Internet Information Services] 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="a37da-219">Close the Internet Information Services snap-in.</span></span>

### <a name="create-web-project"></a><span data-ttu-id="a37da-220">建立 Web 專案</span><span class="sxs-lookup"><span data-stu-id="a37da-220">Create web project</span></span>

1. <span data-ttu-id="a37da-221">開啟 Visual Studio 2005。</span><span class="sxs-lookup"><span data-stu-id="a37da-221">Open Visual Studio 2005.</span></span>
2. <span data-ttu-id="a37da-222">從 [**檔案**] 功能表中，選取 [**新網站**]。</span><span class="sxs-lookup"><span data-stu-id="a37da-222">From the **File** menu, select **New Web Site**.</span></span>
3. <span data-ttu-id="a37da-223">在 [**位置**] 下拉式清單中，選取 [ **FTP**]。</span><span class="sxs-lookup"><span data-stu-id="a37da-223">In the **Location** dropdown, select **FTP**.</span></span>
4. <span data-ttu-id="a37da-224">按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="a37da-224">Click **Browse**.</span></span>
5. <span data-ttu-id="a37da-225">在 [**伺服器**] 文字方塊中輸入**localhost** 。</span><span class="sxs-lookup"><span data-stu-id="a37da-225">Enter **localhost** in the **Server** textbox.</span></span>
6. <span data-ttu-id="a37da-226">在 [目錄] 文字方塊中，輸入**User1** 。</span><span class="sxs-lookup"><span data-stu-id="a37da-226">Enter **User1** in the Directory textbox.</span></span>
7. <span data-ttu-id="a37da-227">按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="a37da-227">Click **Open**.</span></span> <span data-ttu-id="a37da-228">FTP 位置會在 [新網站] 對話方塊中輸入。</span><span class="sxs-lookup"><span data-stu-id="a37da-228">The FTP location will be entered into the New Web Site dialog.</span></span>
8. <span data-ttu-id="a37da-229">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a37da-229">Click **OK**.</span></span>
9. <span data-ttu-id="a37da-230">取消核取 [FTP 登入] 對話方塊中的 [**匿名登入**]，輸入您的認證，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="a37da-230">Uncheck **Anonymous log on** in the FTP Log On dialog, enter your credentials, and click **OK**.</span></span>
10. <span data-ttu-id="a37da-231">專案的 URL 為何？</span><span class="sxs-lookup"><span data-stu-id="a37da-231">What is the URL for the project?</span></span> <span data-ttu-id="a37da-232">（專案的 URL 會顯示在方案總管中）。</span><span class="sxs-lookup"><span data-stu-id="a37da-232">(The URL for the project will be displayed in Solution Explorer.)</span></span>
11. <span data-ttu-id="a37da-233">從 [**建立**] 功能表中，選取 [**建立網站**] 或 [**組建方案**]。</span><span class="sxs-lookup"><span data-stu-id="a37da-233">From the **Build** menu, select **Build Web Site** or **Build Solution**.</span></span>
12. <span data-ttu-id="a37da-234">在方案總管中，以滑鼠右鍵按一下 default.aspx，然後**在瀏覽器中**選取 [View]。</span><span class="sxs-lookup"><span data-stu-id="a37da-234">Right-click on Default.aspx in Solution Explorer and select **View in Browser**.</span></span>
13. <span data-ttu-id="a37da-235">在 [需要網站 URL] 對話方塊中，輸入 URL 的 `http://localhost/user1`，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="a37da-235">In the Web Site URL Required dialog, enter `http://localhost/user1` for the URL and click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="a37da-236">如果您收到錯誤，指出無法載入類型/_Default，請確定您在網站上執行的是 ASP.NET 2.0，而不是在較舊的版本上執行。</span><span class="sxs-lookup"><span data-stu-id="a37da-236">If you get a error indicating an inability to load the type /_Default, make sure that you are running ASP.NET 2.0 on your Web site and not an earlier version.</span></span> <span data-ttu-id="a37da-237">您可以從 Internet Information Services 的 [ASP.NET] 索引標籤中執行此動作。</span><span class="sxs-lookup"><span data-stu-id="a37da-237">You can do that from the ASP.NET tab in Internet Information Services.</span></span>

## <a name="opening-web-projects"></a><span data-ttu-id="a37da-238">開啟 Web 專案</span><span class="sxs-lookup"><span data-stu-id="a37da-238">Opening Web Projects</span></span>

<span data-ttu-id="a37da-239">開啟 Web 專案類似于建立專案。</span><span class="sxs-lookup"><span data-stu-id="a37da-239">Opening Web projects is similar to creating projects.</span></span> <span data-ttu-id="a37da-240">下列各節會在 IDE 中工作時，呼叫要留意的區域。</span><span class="sxs-lookup"><span data-stu-id="a37da-240">The following sections call out areas to keep an eye out for while working within the IDE.</span></span> <span data-ttu-id="a37da-241">它也涵蓋如何使用 HTTP 和 FTP 來處理 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="a37da-241">It also covers working with Web projects using HTTP and FTP.</span></span>

<span data-ttu-id="a37da-242">若要開啟 Web 專案，請從 [檔案] 功能表中選取 [開啟網站]。</span><span class="sxs-lookup"><span data-stu-id="a37da-242">To open a Web project, select Open Web Site from the File menu.</span></span> <span data-ttu-id="a37da-243">系統會提示您提供先前所述的相同 [選擇位置] 對話方塊，而且您有相同的四個選項： [檔案系統]、[本機 IIS]、[FTP] 和 [遠端網站]。</span><span class="sxs-lookup"><span data-stu-id="a37da-243">You will be prompted with the same Choose Location dialog covered previously and you have the same four options available to you: File System, Local IIS, FTP, and Remote Site.</span></span>

<a id="_Toc116100245"></a>

## <a name="file-system"></a><span data-ttu-id="a37da-244">檔案系統</span><span class="sxs-lookup"><span data-stu-id="a37da-244">File System</span></span>

<span data-ttu-id="a37da-245">如先前在此課程模組中所述，Visual Studio 不再使用專案檔。</span><span class="sxs-lookup"><span data-stu-id="a37da-245">As indicated previously in this module, Visual Studio no longer uses a project file.</span></span> <span data-ttu-id="a37da-246">因此，如果您選擇從檔案系統開啟網站，則您實際上可以選擇想要的任何資料夾，即使您選擇的資料夾不是以 Visual Studio 一開始就建立為 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="a37da-246">Therefore, if you choose to open a Web site from the file system, you actually have the option of choosing any folder that you wish, even if the folder you choose was not created as a Web project initially in Visual Studio.</span></span> <span data-ttu-id="a37da-247">例如，您可以選擇開啟 [我的文件] 資料夾做為網站，Visual Studio 會很高興地開啟它並顯示您的檔案，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a37da-247">For example, you can choose to open the My Documents folder as a Web site and Visual Studio will happily open it and display your files as shown below.</span></span>

![我的檔開啟為網站](improvements-in-visual-studio-2005/_static/image3.jpg)

<span data-ttu-id="a37da-249">**圖 6**：*我的檔*開啟為網站</span><span class="sxs-lookup"><span data-stu-id="a37da-249">**Figure 6**: *My Documents* Opened As a Web Site</span></span>

<span data-ttu-id="a37da-250">因為 Visual Studio 只會在必要時建立額外的檔案和資料夾，所以不會在您開啟的位置新增任何其他檔案或資料夾。</span><span class="sxs-lookup"><span data-stu-id="a37da-250">Because Visual Studio only creates additional files and folders when necessary, no additional files or folders are added to the location you open.</span></span> <span data-ttu-id="a37da-251">此架構的副作用是它會讓您無法在檔案系統上建立網站的嵌套。</span><span class="sxs-lookup"><span data-stu-id="a37da-251">A side-effect of this architecture is that it prevents you from nesting Web sites on the file system.</span></span> <span data-ttu-id="a37da-252">例如，請考慮下列目錄結構。</span><span class="sxs-lookup"><span data-stu-id="a37da-252">For example, consider the following directory structure.</span></span>

<span data-ttu-id="a37da-253">Web 專案位於 C：/MyWebSite</span><span class="sxs-lookup"><span data-stu-id="a37da-253">Web project at C:/MyWebSite</span></span>

<span data-ttu-id="a37da-254">另一個位於 C：/MyWebSite/Nested 的 Web 專案</span><span class="sxs-lookup"><span data-stu-id="a37da-254">Another web project at C:/MyWebSite/Nested</span></span>

<span data-ttu-id="a37da-255">當您在 c：/MyWebSite 開啟網站時，此嵌套資料夾會顯示為該應用程式的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="a37da-255">When you open the Web site at c:/MyWebSite, the Nested folder will appear as a sub-folder of that application.</span></span>

<a id="_Toc116100246"></a>

## <a name="http"></a><span data-ttu-id="a37da-256">HTTP</span><span class="sxs-lookup"><span data-stu-id="a37da-256">HTTP</span></span>

<span data-ttu-id="a37da-257">透過 HTTP 開啟網站時，會從 IIS 元資料庫（本機 IIS）或使用 FrontPage Server Extensions （遠端網站）讀取設定。如果有嵌套的 web 應用程式，則會顯示它們，以及將其識別為應用程式的圖示。</span><span class="sxs-lookup"><span data-stu-id="a37da-257">When opening Web sites via HTTP, settings are read either from the IIS metabase (Local IIS) or using FrontPage Server Extensions (Remote Site.) If there are nested web applications, these are displayed as well with an icon identifying them as an application.</span></span> <span data-ttu-id="a37da-258">如果您熟悉在 FrontPage 中使用 web 應用程式，Visual Studio 2005 中的行為很類似。</span><span class="sxs-lookup"><span data-stu-id="a37da-258">If you are familiar with working with web applications in FrontPage, the behavior in Visual Studio 2005 is similar.</span></span>

<span data-ttu-id="a37da-259">即使 Visual Studio 將會顯示應用程式的圖示，而該應用程式位於目前在 IDE 中開啟的應用程式底下，但不允許您將其展開以查看其內容。</span><span class="sxs-lookup"><span data-stu-id="a37da-259">Even though Visual Studio will display an icon for applications that are nested beneath the application that is currently opened within the IDE, it will not allow you to expand them to see their content.</span></span> <span data-ttu-id="a37da-260">不過，您可以按兩下它們來開啟它們。</span><span class="sxs-lookup"><span data-stu-id="a37da-260">You can, however, double-click on them to open them.</span></span> <span data-ttu-id="a37da-261">當您這麼做時，您會看到一個對話方塊，提示您開啟 web 應用程式（並取代目前開啟的方案），或將 Web 應用程式新增至您目前的方案。</span><span class="sxs-lookup"><span data-stu-id="a37da-261">When you do, you will be presented with a dialog prompting you to either open the web application (and replace the currently open solution) or add the Web application to your current solution.</span></span>

![按兩下 [已嵌套的應用程式] 圖示會顯示此對話方塊](improvements-in-visual-studio-2005/_static/image4.jpg)

<span data-ttu-id="a37da-263">**圖 7**：按兩下 [已嵌套的應用程式] 圖示會顯示此對話方塊</span><span class="sxs-lookup"><span data-stu-id="a37da-263">**Figure 7**: Double-clicking a nested application icon presents you with this dialog</span></span>

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a><span data-ttu-id="a37da-264">FTP 站台</span><span class="sxs-lookup"><span data-stu-id="a37da-264">FTP Site</span></span>

<span data-ttu-id="a37da-265">當您透過 FTP 開啟網站時，檔案全部都會複製到您的暫存資料夾。</span><span class="sxs-lookup"><span data-stu-id="a37da-265">When you open a site via FTP, the files are all copied locally to your temp folder.</span></span> <span data-ttu-id="a37da-266">本機儲存位置的完整路徑會顯示在專案的 [屬性] 窗格中，並使用下列格式來建立。</span><span class="sxs-lookup"><span data-stu-id="a37da-266">The full path for the local storage location is displayed in the Properties pane for the project and is created using the following format.</span></span>

<span data-ttu-id="a37da-267">C：/Documents and Settings/&lt;使用者&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;應用程式名稱&gt;</span><span class="sxs-lookup"><span data-stu-id="a37da-267">C:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="a37da-268">使用 FTP 時，Visual Studio 需要指定專案的基底 URL，讓您可以流覽它，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a37da-268">When using FTP, Visual Studio will need to specify the base URL for your project so that you can browse it as shown below.</span></span> <span data-ttu-id="a37da-269">如果您未指定基底 URL，Visual Studio 會在您第一次嘗試流覽網站中的頁面時要求您。</span><span class="sxs-lookup"><span data-stu-id="a37da-269">If you do not specify a base URL, Visual Studio will ask you for it the first time you attempt to browse a page in the Web site.</span></span>

![指定 FTP 網站的基底 URL](improvements-in-visual-studio-2005/_static/image5.jpg)

<span data-ttu-id="a37da-271">**圖 8**：指定 FTP 網站的基底 URL</span><span class="sxs-lookup"><span data-stu-id="a37da-271">**Figure 8**: Specifying a Base URL for FTP Sites</span></span>

## <a name="improvements-in-compilation"></a><span data-ttu-id="a37da-272">編譯的改良功能</span><span class="sxs-lookup"><span data-stu-id="a37da-272">Improvements in Compilation</span></span>

<span data-ttu-id="a37da-273">在 Visual Studio 2005 中使用 Web 應用程式的速度，明顯比先前的版本更快。</span><span class="sxs-lookup"><span data-stu-id="a37da-273">Working with Web applications in Visual Studio 2005 is noticeably faster than previous versions.</span></span> <span data-ttu-id="a37da-274">這在編譯架構的變更中沒有任何小部分。</span><span class="sxs-lookup"><span data-stu-id="a37da-274">This is due in no small part to the changes in compilation architecture.</span></span>

<span data-ttu-id="a37da-275">在 Visual Studio 2002 和2003中，Web 應用程式已編譯成位於/bin 資料夾中的一個主要元件。</span><span class="sxs-lookup"><span data-stu-id="a37da-275">In Visual Studio 2002 and 2003, Web applications were compiled into one primary assembly residing in the /bin folder.</span></span> <span data-ttu-id="a37da-276">在 Visual Studio 2005 中，已新增應用程式/_Code 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a37da-276">In Visual Studio 2005, an App/_Code folder was added.</span></span> <span data-ttu-id="a37da-277">類別和其他非 UI 程式碼會新增至 App/_Code 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a37da-277">Classes and other non-UI code are added to the App/_Code folder.</span></span> <span data-ttu-id="a37da-278">當 Visual Studio 建立專案時，會將 App/_Code 資料夾中的所有檔案編譯成單一應用程式/_Code .dll 檔案。</span><span class="sxs-lookup"><span data-stu-id="a37da-278">When Visual Studio builds the project, all files in the App/_Code folder are compiled into a single App/_Code.dll file.</span></span> <span data-ttu-id="a37da-279">這項變更的結果是，後續組建的速度會比先前的版本快很多。</span><span class="sxs-lookup"><span data-stu-id="a37da-279">The result of this change is that subsequent builds are much faster than in previous versions.</span></span>

> [!NOTE]
> <span data-ttu-id="a37da-280">MSBuild 命令列公用程式也可以用來建立 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a37da-280">The MSBuild command line utility can also be used to build ASP.NET Web applications.</span></span> <span data-ttu-id="a37da-281">模組9將涵蓋該工具。</span><span class="sxs-lookup"><span data-stu-id="a37da-281">That tool will be covered in module 9.</span></span>

<span data-ttu-id="a37da-282">另一個編譯增強功能是 [建立] 功能表上的 [新增組建頁面] 選項。</span><span class="sxs-lookup"><span data-stu-id="a37da-282">Another compilation enhancement is the new Build Page option on the Build menu.</span></span> <span data-ttu-id="a37da-283">這項功能可讓開發人員只重建目前的頁面（當然還有相依性），以便更快速地編譯變更。</span><span class="sxs-lookup"><span data-stu-id="a37da-283">This feature allows a developer to rebuild only the current page (along with, of course, and dependencies) so that changes can be compiled more quickly.</span></span> <span data-ttu-id="a37da-284">由於C#不會針對更新 IntelliSense 等目的提供背景編譯等等，因此從這項功能可以獲益，因為它可讓 IntelliSense 快速地透過重建單一頁面來進行更新。</span><span class="sxs-lookup"><span data-stu-id="a37da-284">Because C# does not offer background compilation for purposes of updating IntelliSense, etc., they will benefit immensely from this feature because it will allow for IntelliSense to be updated quickly by simply rebuilding a single page.</span></span>

<span data-ttu-id="a37da-285">專案的組建屬性可讓您設定在執行啟動頁面之前所發生的組建類型。</span><span class="sxs-lookup"><span data-stu-id="a37da-285">The Build properties for a project allow you to configure the type of build that occurs before the startup page is executed.</span></span> <span data-ttu-id="a37da-286">開發人員可以選擇只建立目前的網頁，讓 Visual Studio 可以在程式碼變更之後，更快速地開始偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="a37da-286">Developers can choose to only build the current page so that Visual Studio can start debugging applications more quickly after code changes.</span></span>

![組建頁面啟動動作](improvements-in-visual-studio-2005/_static/image6.jpg)

<span data-ttu-id="a37da-288">**圖 9**：組建頁面啟動動作</span><span class="sxs-lookup"><span data-stu-id="a37da-288">**Figure 9**: The Build Page Start Action</span></span>

<span data-ttu-id="a37da-289">Visual Studio 和 ASP.NET 架構的另一個絕佳增強功能，是在 [編輯後繼續] 區域中。</span><span class="sxs-lookup"><span data-stu-id="a37da-289">Another great enhancement to Visual Studio and the ASP.NET architecture is in the area of edit and continue.</span></span> <span data-ttu-id="a37da-290">在 Visual Studio 2005 中，開發人員可以開始對專案進行偵錯工具，並在不中斷偵錯工具的情況下，對專案進行程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="a37da-290">In Visual Studio 2005, developers can start debugging a project and make code changes on the project without detaching the debugger.</span></span> <span data-ttu-id="a37da-291">事實上，您可以依實際情況開始對專案進行的偵錯工具、新增類別、將程式碼新增至該類別、將程式碼新增至您的頁面，以建立該類別的新實例並執行類別的方法，全都不需要卸離偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="a37da-291">In fact, you can literally start debugging a project, add a new class, add code to that class, add code to your page that creates a new instance of that class and execute a method of the class, all without detaching the debugger.</span></span> <span data-ttu-id="a37da-292">執行新的程式碼其實就像重新整理瀏覽器一樣簡單！</span><span class="sxs-lookup"><span data-stu-id="a37da-292">Executing the new code is literally as easy as refreshing the browser!</span></span>

<span data-ttu-id="a37da-293">按一下這裡以查看 Visual Studio 2005 中 [編輯後繼續] 功能的影片逐步解說。</span><span class="sxs-lookup"><span data-stu-id="a37da-293">Click here to see a video walkthrough of the edit and continue feature in Visual Studio 2005.</span></span>

![](improvements-in-visual-studio-2005/_static/image2.png)

[<span data-ttu-id="a37da-294">開啟全螢幕影片</span><span class="sxs-lookup"><span data-stu-id="a37da-294">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

<span data-ttu-id="a37da-295">ASP.NET 2.0 和 Visual Studio 2005 中的強大編輯和繼續功能，是因為 ASP.NET 應用程式的架構變更。</span><span class="sxs-lookup"><span data-stu-id="a37da-295">The robust edit and continue functionality in ASP.NET 2.0 and Visual Studio 2005 is due to an architectural change for ASP.NET applications.</span></span> <span data-ttu-id="a37da-296">在 ASP.NET 1.x 中，Visual Studio 2002/2003 中建立的應用程式會編譯成儲存在/bin 資料夾中的主要元件。</span><span class="sxs-lookup"><span data-stu-id="a37da-296">In ASP.NET 1.x, applications created in Visual Studio 2002/2003 were compiled into a primary assembly that was stored in the /bin folder.</span></span> <span data-ttu-id="a37da-297">應用程式的所有類別、頁面等等已編譯成該 DLL。</span><span class="sxs-lookup"><span data-stu-id="a37da-297">All classes, pages, etc. for the application were compiled into that one DLL.</span></span> <span data-ttu-id="a37da-298">然後在執行時間，ASP.NET 會在頁面中編譯所有的控制項、標記和 ASP.NET 程式碼，並將這些 Dll 複製到 ASP.NET 暫存資料夾中。</span><span class="sxs-lookup"><span data-stu-id="a37da-298">Then at runtime, ASP.NET would compile all of the controls, markup, and ASP.NET code within pages and copy those DLLs into the ASP.NET temporary folder.</span></span>

<span data-ttu-id="a37da-299">在使用 ASP.NET 2.0 的 Visual Studio 2005 中，上述兩種編譯模型（一個適用于 Visual Studio，一個用於執行時間的 ASP.NET）已合併為一個通用的編譯模型。</span><span class="sxs-lookup"><span data-stu-id="a37da-299">In Visual Studio 2005 using ASP.NET 2.0, the two compilation models outline above (one for Visual Studio and one for ASP.NET at runtime) have been merged into one common compilation model.</span></span> <span data-ttu-id="a37da-300">這表示現在會在開發階段（而不是在執行時間）攔截所有編譯問題。</span><span class="sxs-lookup"><span data-stu-id="a37da-300">That means that all compilation issues are now caught during the development stage instead of at runtime.</span></span> <span data-ttu-id="a37da-301">它也允許設計工具和 IntelliSense 支援的功能，例如使用者控制項和主版頁面。</span><span class="sxs-lookup"><span data-stu-id="a37da-301">It also allows for designer and IntelliSense support for features such as user controls and master pages.</span></span>

<span data-ttu-id="a37da-302">按一下這裡可查看提供使用者控制項設計工具支援的影片逐步解說。</span><span class="sxs-lookup"><span data-stu-id="a37da-302">Click here to see a video walkthrough of designer support for user controls.</span></span>

![](improvements-in-visual-studio-2005/_static/image3.png)

[<span data-ttu-id="a37da-303">開啟全螢幕影片</span><span class="sxs-lookup"><span data-stu-id="a37da-303">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> <span data-ttu-id="a37da-304">從頁面中移除使用者控制項時，@Register 指示詞會保留在標記中，而且應該手動移除，以避免在使用者控制項從網站中刪除時的剖析器錯誤。</span><span class="sxs-lookup"><span data-stu-id="a37da-304">When a user control is removed from a page, the @Register directive remains in the markup and should be removed manually in order to avoid parser errors if the user control is deleted from the Web site.</span></span>

<span data-ttu-id="a37da-305">Visual Studio 編譯模型的另一項改進是「發行網站」功能。</span><span class="sxs-lookup"><span data-stu-id="a37da-305">Another improvement in the Visual Studio compilation model is the Publish Web Site feature.</span></span> <span data-ttu-id="a37da-306">因為發佈功能會將網站預先編譯，所以開發人員可以享受增加的效能，而不需視需要編譯任何專案。</span><span class="sxs-lookup"><span data-stu-id="a37da-306">Because the Publish feature precompiles the Web site, developers can enjoy the added performance of not having to compile anything on demand.</span></span> <span data-ttu-id="a37da-307">它也會將 App/_Code 資料夾中的所有原始程式碼都預先編譯成 DLL，因此不需要部署任何原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="a37da-307">It also precompiles all source code in the App/_Code folder into a DLL so that no source code has to be deployed.</span></span>

![[發行網站] 對話方塊](improvements-in-visual-studio-2005/_static/image7.jpg)

<span data-ttu-id="a37da-309">**圖 10**： [發行網站] 對話方塊</span><span class="sxs-lookup"><span data-stu-id="a37da-309">**Figure 10**: The Publish Web Site Dialog</span></span>

> [!NOTE]
> <span data-ttu-id="a37da-310">Aspnet/_compile .exe 公用程式也可以用來預先編譯 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a37da-310">The aspnet/_compile.exe utility can also be used to pre-compile an ASP.NET Web application.</span></span> <span data-ttu-id="a37da-311">模組9將涵蓋該工具。</span><span class="sxs-lookup"><span data-stu-id="a37da-311">That tool will be covered in module 9.</span></span>

<span data-ttu-id="a37da-312">當您發行網站時，預先編譯的檔案會儲存在暫存的 ASP.NET Files 資料夾中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a37da-312">When you Publish a Web site, the precompiled files are stored in the Temporary ASP.NET Files folder as shown below.</span></span> <span data-ttu-id="a37da-313">副檔名*為 .xml*的檔案為 XML 檔案，可定義特定 dll 的相依性。</span><span class="sxs-lookup"><span data-stu-id="a37da-313">Files with a *.compiled* file extension are XML files that define dependencies for particular DLLs.</span></span> <span data-ttu-id="a37da-314">任何 Webform 或使用者控制項都會編譯成以*App/_Web/_* 開頭的隨機 dll。</span><span class="sxs-lookup"><span data-stu-id="a37da-314">Any Webform or user controls are compiled into random DLLs that begin with *App/_Web/_*.</span></span>

<span data-ttu-id="a37da-315">如果您將 [*允許此先行編譯的網站成為可更新*的] 核取方塊保持核取狀態，則 Webforms 和使用者控制項內的標記將不會預先編譯成 DLL，讓您在部署後進行變更。</span><span class="sxs-lookup"><span data-stu-id="a37da-315">If you leave the *Allow this precompiled site to be updatable* checkbox checked, markup inside of your Webforms and user controls will not be pre-compiled into a DLL allowing you to make changes after deployment.</span></span> <span data-ttu-id="a37da-316">如果您想要鎖定標記，而不允許變更已部署的內容，請取消核取此方塊。</span><span class="sxs-lookup"><span data-stu-id="a37da-316">If you would prefer to lock down the markup so that changes to the deployed content are not allowed, uncheck this box.</span></span>

<span data-ttu-id="a37da-317">[*使用固定命名和單一頁面元件*] 核取方塊可讓您停用批次編譯，讓每個頁面都編譯成固定名稱的元件。</span><span class="sxs-lookup"><span data-stu-id="a37da-317">The *Use fixed naming and single page assemblies* checkbox allows you to disable batch compilation so that each page is compiled into a fixed-named assembly.</span></span> <span data-ttu-id="a37da-318">未核取此方塊可讓您利用批次編譯。</span><span class="sxs-lookup"><span data-stu-id="a37da-318">Leaving this box unchecked allows you to take advantage of batch compilation.</span></span>

<span data-ttu-id="a37da-319">[在先行*編譯元件上啟用強式命名*] 核取方塊可讓您將先行編譯的元件強式名稱。</span><span class="sxs-lookup"><span data-stu-id="a37da-319">The *Enable strong naming on precompiled assemblies* checkbox allows you to strong-name your precompiled assemblies.</span></span>

> [!NOTE]
> <span data-ttu-id="a37da-320">在 ASP.NET 1.x 中，必須將強式名稱的元件安裝在全域組件快取（GAC）中。</span><span class="sxs-lookup"><span data-stu-id="a37da-320">In ASP.NET 1.x, strong-named assemblies had to be installed into the Global Assembly Cache (GAC).</span></span> <span data-ttu-id="a37da-321">在 ASP.NET 2.0 中，您不需要將強式名稱的元件安裝到 GAC 中。</span><span class="sxs-lookup"><span data-stu-id="a37da-321">In ASP.NET 2.0, you are not required to install strong-named assemblies into the GAC.</span></span>

![ASP.NET 應用程式預先編譯的檔案](improvements-in-visual-studio-2005/_static/image8.jpg)

<span data-ttu-id="a37da-323">**圖 11**： ASP.NET 應用程式預先編譯的檔案</span><span class="sxs-lookup"><span data-stu-id="a37da-323">**Figure 11**: An ASP.NET Applications Pre-Compiled Files</span></span>

> [!NOTE]
> <span data-ttu-id="a37da-324">在上述應用程式中，沒有 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="a37da-324">In the application above, there was no web.config file.</span></span> <span data-ttu-id="a37da-325">如果已經存在，則會在發佈網站進程之後被稱為*PrecompiledApp。*</span><span class="sxs-lookup"><span data-stu-id="a37da-325">If there had been, it would have been called *PrecompiledApp.config* after the Publish Web site process.</span></span>

## <a name="improvements-in-deployment"></a><span data-ttu-id="a37da-326">部署的改良功能</span><span class="sxs-lookup"><span data-stu-id="a37da-326">Improvements in Deployment</span></span>

<span data-ttu-id="a37da-327">如同 Visual Studio 2002 和2003，Visual Studio 2005 提供複製專案功能。</span><span class="sxs-lookup"><span data-stu-id="a37da-327">As with Visual Studio 2002 and 2003, Visual Studio 2005 offers a Copy Project feature.</span></span> <span data-ttu-id="a37da-328">不過，此功能已在 Visual Studio 2005 中過增強，現在稱為「複製網站」。</span><span class="sxs-lookup"><span data-stu-id="a37da-328">However, the feature has been beefed up in Visual Studio 2005 and is now called Copy Web Site.</span></span>

<span data-ttu-id="a37da-329">[複製網站] 對話方塊會分割成左框架和右框架。</span><span class="sxs-lookup"><span data-stu-id="a37da-329">The Copy Web Site dialog is split into a left frame and a right frame.</span></span> <span data-ttu-id="a37da-330">左側的框架稱為「來源網站」，而右邊的框架稱為「遠端網站」。</span><span class="sxs-lookup"><span data-stu-id="a37da-330">The left frame is called the Source Web Site and the right frame is called the Remote Web Site.</span></span> <span data-ttu-id="a37da-331">有些開發人員可能會造成混淆，那就是在右側畫面中顯示的網站不一定是遠端網站。</span><span class="sxs-lookup"><span data-stu-id="a37da-331">One thing that may confuse some developers is that the site displayed in the right frame is not necessarily a remote site.</span></span> <span data-ttu-id="a37da-332">它可以是本機檔案系統上或 IIS 本機實例上的網站。</span><span class="sxs-lookup"><span data-stu-id="a37da-332">It could be a site on the local file system or on the local instance of IIS.</span></span> <span data-ttu-id="a37da-333">此外，在左邊框中顯示的網站不一定是來源網站，因為此對話方塊可讓您從遠端網站發行*至*來源網站。</span><span class="sxs-lookup"><span data-stu-id="a37da-333">Additionally, the site displayed in the left frame is not necessarily the source Web site because the dialog allows you to publish from the remote Web site *to* the source Web site.</span></span>

<span data-ttu-id="a37da-334">如果您要將專案複製到遠端網站，該網站上必須安裝 FrontPage Server Extensions。</span><span class="sxs-lookup"><span data-stu-id="a37da-334">If you are copying a project to a remote Web site, that site must have the FrontPage Server Extensions installed on it.</span></span> <span data-ttu-id="a37da-335">如果不是，您就必須使用 FTP 進行連接。</span><span class="sxs-lookup"><span data-stu-id="a37da-335">If it does not, you will need to connect using FTP.</span></span> <span data-ttu-id="a37da-336">另一方面，如果您要將專案複製到本機 IIS 實例，則不需要 FrontPage Server Extensions。</span><span class="sxs-lookup"><span data-stu-id="a37da-336">On the other hand, if you are copying a project to the local IIS instance, FrontPage Server Extensions are not required.</span></span>

> [!NOTE]
> <span data-ttu-id="a37da-337">如果您嘗試在本機 IIS 實例上建立新的網站，而且已安裝 FrontPage 2002 伺服器延伸模組，您會收到一則錯誤訊息，告訴您 SharePoint 伺服器上不支援建立網站。</span><span class="sxs-lookup"><span data-stu-id="a37da-337">If you try to create a new Web site on the local IIS instance and the FrontPage 2002 Server Extensions are installed, you will get an error message telling you that creating Web sites is not supported on a SharePoint server.</span></span> <span data-ttu-id="a37da-338">在此情況下，您可以選擇安裝 FrontPage 2000 伺服器擴充功能或移除 FrontPage Server Extensions。</span><span class="sxs-lookup"><span data-stu-id="a37da-338">In that case, you have the option of installing the FrontPage 2000 Server Extensions or removing the FrontPage Server Extensions.</span></span>

<span data-ttu-id="a37da-339">按一下這裡以取得複製網站功能的影片逐步解說。</span><span class="sxs-lookup"><span data-stu-id="a37da-339">Click here for a video walkthrough of the Copy Web Site feature.</span></span>

![](improvements-in-visual-studio-2005/_static/image4.png)

[<span data-ttu-id="a37da-340">開啟全螢幕影片</span><span class="sxs-lookup"><span data-stu-id="a37da-340">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a><span data-ttu-id="a37da-341">對調試功能的改善</span><span class="sxs-lookup"><span data-stu-id="a37da-341">Improvements in Debugging</span></span>

<span data-ttu-id="a37da-342">Visual Studio 2005 中的調試功能有四項重要的改良。</span><span class="sxs-lookup"><span data-stu-id="a37da-342">There are four key improvements in debugging in Visual Studio 2005.</span></span>

- <span data-ttu-id="a37da-343">以非系統管理員的身分在本機進行調試，可能是現成的。</span><span class="sxs-lookup"><span data-stu-id="a37da-343">Debugging locally as a non-administrator is possible out of the box.</span></span>
- <span data-ttu-id="a37da-344">編譯專案的 Debug 屬性現在預設為 false。</span><span class="sxs-lookup"><span data-stu-id="a37da-344">The Debug attribute for the Compilation element is now false by default.</span></span>
- <span data-ttu-id="a37da-345">遠端偵錯程式的安裝和設定比以前更容易。</span><span class="sxs-lookup"><span data-stu-id="a37da-345">Remote debugging setup and configuration is easier than before.</span></span>
- <span data-ttu-id="a37da-346">您現在可以將透過 FTP 位置開啟的網站進行偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="a37da-346">You can now debug a Web site opened via an FTP location.</span></span>

## <a name="debugging-as-a-non-administrator"></a><span data-ttu-id="a37da-347">以非系統管理員的身分進行調試</span><span class="sxs-lookup"><span data-stu-id="a37da-347">Debugging as a Non-Administrator</span></span>

<span data-ttu-id="a37da-348">新增 ASP.NET 程式開發伺服器可讓非系統管理員輕鬆地立即 ASP.NET 現成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a37da-348">The addition of the ASP.NET Development Server allows non-administrators to easily debug ASP.NET applications right out of the box.</span></span> <span data-ttu-id="a37da-349">在本機檔案系統上執行的 ASP.NET 應用程式進行調試時，Visual Studio 會在登入使用者的內容下啟動 ASP.NET 程式開發伺服器。</span><span class="sxs-lookup"><span data-stu-id="a37da-349">When an ASP.NET application running on the local file system is debugged, Visual Studio launches the ASP.NET Development Server under the context of the logged-on user.</span></span> <span data-ttu-id="a37da-350">之後，該使用者就可以在不進行任何額外設定的情況下，進行應用程式的</span><span class="sxs-lookup"><span data-stu-id="a37da-350">That user can then debug that application without any additional configuration.</span></span>

## <a name="debug-is-false-by-default"></a><span data-ttu-id="a37da-351">Debug 預設為 False</span><span class="sxs-lookup"><span data-stu-id="a37da-351">Debug is False by Default</span></span>

<span data-ttu-id="a37da-352">在 ASP.NET 1.x 中，web.config 檔案之*編譯*元素中的*debug*屬性預設會設定為*true* 。</span><span class="sxs-lookup"><span data-stu-id="a37da-352">In ASP.NET 1.x, the *debug* attribute in the *compilation* element of the web.config file was set to *true* by default.</span></span> <span data-ttu-id="a37da-353">建議開發人員在將應用程式部署到生產環境之前，將此屬性設定為*false* ，但因為大部分的開發人員都不會完全瞭解將 debug 屬性設定為 true 的結果，所以它們只是保持不存在。</span><span class="sxs-lookup"><span data-stu-id="a37da-353">It has always been recommended that developers set this attribute to *false* before deploying an application to production, but because most developers don't fully understand the consequences of leaving the debug attribute set to true, they simply left it as-is.</span></span>

<span data-ttu-id="a37da-354">將 debug 屬性設為 true 的最嚴重問題，就是它會停用神經網路批次編譯模型。</span><span class="sxs-lookup"><span data-stu-id="a37da-354">The most severe problem with having the debug attribute set to true is that it disables ASP.NETs batch compilation model.</span></span> <span data-ttu-id="a37da-355">因此，每個頁面都會編譯成個別的 DLL。</span><span class="sxs-lookup"><span data-stu-id="a37da-355">Therefore, each page is compiled into a separate DLL.</span></span> <span data-ttu-id="a37da-356">如果 Web 應用程式是由數千頁組成（不是由任何方法前所未聞），這表示該應用程式會建立數千個小型的 Dll。</span><span class="sxs-lookup"><span data-stu-id="a37da-356">If a Web application consists of thousands of pages (not unheard of by any means), that means several thousand small DLLs will be created by that application.</span></span> <span data-ttu-id="a37da-357">雖然這些 Dll 的大小很小，但是它們不會載入記憶體中的任何特定位置。</span><span class="sxs-lookup"><span data-stu-id="a37da-357">While these DLLs are small in size, they are not loaded into any particular location in memory.</span></span> <span data-ttu-id="a37da-358">因此，它們會造成系統記憶體分散，而且可能會導致 OutOfMemoryException 發生。</span><span class="sxs-lookup"><span data-stu-id="a37da-358">Therefore, they cause fragmentation in system memory and can contribute to OutOfMemoryException occurrences.</span></span>

<span data-ttu-id="a37da-359">在 ASP.NET 2.0 中，debug 屬性預設會設定為 false。</span><span class="sxs-lookup"><span data-stu-id="a37da-359">In ASP.NET 2.0, the debug attribute is set to false by default.</span></span> <span data-ttu-id="a37da-360">如您所見，當開發人員在 Visual Studio 2005 中調試 ASP.NET 應用程式時，系統會提示他們新增已啟用偵測的 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="a37da-360">As you have already seen, when a developer debugs an ASP.NET application in Visual Studio 2005, they are prompted to add a web.config file with debugging enabled.</span></span> <span data-ttu-id="a37da-361">這麼做會產生與 ASP.NET 1.x 中相同的缺點，但現在，開發人員會在將應用程式移至生產環境之前，清楚警告屬性應該重設為 false。</span><span class="sxs-lookup"><span data-stu-id="a37da-361">Doing so incurs the same drawbacks that were present in ASP.NET 1.x, but now the developer is clearly warned that the attribute should be reset to false before moving the application to production.</span></span>

## <a name="remote-debugging-setup-and-configuration"></a><span data-ttu-id="a37da-362">遠端偵錯程式安裝和設定</span><span class="sxs-lookup"><span data-stu-id="a37da-362">Remote Debugging Setup and Configuration</span></span>

<span data-ttu-id="a37da-363">在 Visual Studio 2002/2003 中，遠端偵錯程式依賴機器偵錯工具（mdm）和 vs7jit 處理。</span><span class="sxs-lookup"><span data-stu-id="a37da-363">In Visual Studio 2002/2003, remote debugging relied on the Machine Debug Manager (mdm.exe) and the vs7jit.exe process.</span></span> <span data-ttu-id="a37da-364">因此，針對遠端偵錯程式問題進行疑難排解通常是客戶的黑色方塊，而對於 PSS 而言，這通常不是那麼好。</span><span class="sxs-lookup"><span data-stu-id="a37da-364">Because of that, troubleshooting remote debugging problems was often a black box for customers and it was often not much better for PSS.</span></span>

<span data-ttu-id="a37da-365">Visual Studio 2005 會移除對 wsdl.exe 和 vs7jit 處理的依賴。</span><span class="sxs-lookup"><span data-stu-id="a37da-365">Visual Studio 2005 removes the reliance on the mdm.exe and vs7jit.exe processes.</span></span> <span data-ttu-id="a37da-366">相反地，它現在會使用遠端偵錯「監視」服務（msvsmon）。</span><span class="sxs-lookup"><span data-stu-id="a37da-366">Instead, it now uses the Remote Debug Monitor service (msvsmon.exe.)</span></span>

<span data-ttu-id="a37da-367">從遠端在 Visual Studio 2005 中進行調試的需求相當簡單。</span><span class="sxs-lookup"><span data-stu-id="a37da-367">The requirement for debugging in Visual Studio 2005 remotely is quite simple.</span></span> <span data-ttu-id="a37da-368">您必須先在遠端伺服器上執行 msvsmon，然後再進行調試。</span><span class="sxs-lookup"><span data-stu-id="a37da-368">You need to run msvsmon.exe on the remote server prior to debugging.</span></span> <span data-ttu-id="a37da-369">您可以從 Visual Studio CD 安裝遠端偵錯時間監視器，也可以直接從共用執行 msvsmon，而不需要在 Web 服務器上安裝任何專案。</span><span class="sxs-lookup"><span data-stu-id="a37da-369">You can install the Remote Debug Monitor from the Visual Studio CD or you can simply run msvsmon.exe from a share without installing anything at all on the Web server.</span></span>

<span data-ttu-id="a37da-370">當您執行 msvsmon 時，可能會抱怨封鎖埠以進行遠端偵錯程式。</span><span class="sxs-lookup"><span data-stu-id="a37da-370">When you run msvsmon.exe, it is likely that it will complain about ports being blocked for remote debugging.</span></span> <span data-ttu-id="a37da-371">幸好，您可以輕鬆地在警告對話方塊中直接解除封鎖埠，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a37da-371">Fortunately, you can easily unblock the ports from right within the warning dialog as shown below.</span></span>

![Windows 防火牆封鎖遠端偵錯程式的通知](improvements-in-visual-studio-2005/_static/image9.jpg)

<span data-ttu-id="a37da-373">**圖 12**： Windows 防火牆封鎖遠端偵錯程式的通知</span><span class="sxs-lookup"><span data-stu-id="a37da-373">**Figure 12**: Notification that Windows Firewall is Blocking Remote Debugging</span></span>

<span data-ttu-id="a37da-374">一旦您解除了偵錯工具所需的通訊埠，就會看到如下所示的遠端偵錯監視。</span><span class="sxs-lookup"><span data-stu-id="a37da-374">Once you have unblocked the ports necessary for debugging, you will see the Remote Debugging Monitor as shown below.</span></span> <span data-ttu-id="a37da-375">您可以從這個介面輕鬆地監視連接和變更調試許可權。</span><span class="sxs-lookup"><span data-stu-id="a37da-375">From this interface, you can monitor connections and change debugging permissions easily.</span></span>

![遠端偵錯監視](improvements-in-visual-studio-2005/_static/image10.jpg)

<span data-ttu-id="a37da-377">**圖 13**：遠端偵錯監視</span><span class="sxs-lookup"><span data-stu-id="a37da-377">**Figure 13**: The Remote Debugging Monitor</span></span>

<span data-ttu-id="a37da-378">您也可以從遠端偵測透過 FTP 開啟的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a37da-378">It is also possible to remotely debug a Web application opened via FTP.</span></span> <span data-ttu-id="a37da-379">這些步驟與先前涵蓋的步驟相同。</span><span class="sxs-lookup"><span data-stu-id="a37da-379">The steps are the same as those previously covered.</span></span> <span data-ttu-id="a37da-380">不過，您必須指定用來流覽 FTP 專案的基底 URL，如本課程模組稍早所述。</span><span class="sxs-lookup"><span data-stu-id="a37da-380">However, you will need to specify a base URL for browsing the FTP project as outlined earlier in this module.</span></span>

## <a name="lab-2"></a><span data-ttu-id="a37da-381">實驗室2</span><span class="sxs-lookup"><span data-stu-id="a37da-381">Lab 2</span></span>

## <a name="remote-debugging-with-visual-studio-2005"></a><span data-ttu-id="a37da-382">使用 Visual Studio 2005 進行遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="a37da-382">Remote Debugging with Visual Studio 2005</span></span>

<span data-ttu-id="a37da-383">此實驗室將逐步引導您使用 Visual Studio 2005 進行遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="a37da-383">This lab will walk you through remote debugging with Visual Studio 2005.</span></span>

<span data-ttu-id="a37da-384">按一下這裡以取得此實驗室的影片逐步解說。</span><span class="sxs-lookup"><span data-stu-id="a37da-384">Click here for a video walkthrough of this lab.</span></span>

![](improvements-in-visual-studio-2005/_static/image5.png)

[<span data-ttu-id="a37da-385">開啟全螢幕影片</span><span class="sxs-lookup"><span data-stu-id="a37da-385">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

<span data-ttu-id="a37da-386">此實驗室需要您擁有兩部電腦，一個執行 Visual Studio 2005，另一個執行中的 IIS 5 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a37da-386">This lab requires you to have two machines, one running Visual Studio 2005 and the other running IIS 5 or greater.</span></span>

1. <span data-ttu-id="a37da-387">開啟 Visual Studio 2005，並在遠端伺服器上建立新的網站。</span><span class="sxs-lookup"><span data-stu-id="a37da-387">Open Visual Studio 2005 and create a new Web site on the remote server.</span></span>

> [!NOTE]
> <span data-ttu-id="a37da-388">您可以在遠端 IIS 實例上或透過 FTP 來建立網站。</span><span class="sxs-lookup"><span data-stu-id="a37da-388">You can create the Web site on a remote IIS instance or via FTP.</span></span>

1. <span data-ttu-id="a37da-389">從遠端 Web 服務器，使用 UNC 路徑找出在開發電腦上的 msvsmon，然後加以執行。</span><span class="sxs-lookup"><span data-stu-id="a37da-389">From the remote Web server, locate msvsmon.exe on the development machine using a UNC path and execute it.</span></span>  
 <span data-ttu-id="a37da-390">Msvsmon 的預設位置是//server/c $/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote 偵錯工具/x86。</span><span class="sxs-lookup"><span data-stu-id="a37da-390">The default location for msvsmon.exe is //server/c$/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86.</span></span>
2. <span data-ttu-id="a37da-391">如果系統提示您解除封鎖埠以進行遠端偵錯程式，請執行此動作。</span><span class="sxs-lookup"><span data-stu-id="a37da-391">If prompted to unblock ports for remote debugging, do so.</span></span>
3. <span data-ttu-id="a37da-392">在開發電腦上，開啟 default.aspx 的程式碼後置，並在 Page/_Load 方法中設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="a37da-392">From the development machine, open the code-behind for Default.aspx and set a breakpoint in the Page/_Load method.</span></span>
4. <span data-ttu-id="a37da-393">從開發電腦開始進行調試。</span><span class="sxs-lookup"><span data-stu-id="a37da-393">Start debugging from the development machine.</span></span>

<span data-ttu-id="a37da-394">您應該會如預期般到達中斷點。</span><span class="sxs-lookup"><span data-stu-id="a37da-394">You should hit the breakpoint as expected.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="a37da-395">ASP.NET 程式開發伺服器</span><span class="sxs-lookup"><span data-stu-id="a37da-395">ASP.NET Development Server</span></span>

<span data-ttu-id="a37da-396">如先前所討論，Visual Studio 2005 隨附名為 ASP.NET 程式開發伺服器的 Web 服務器。</span><span class="sxs-lookup"><span data-stu-id="a37da-396">As we've already discussed, Visual Studio 2005 ships with a Web server called the ASP.NET Development Server.</span></span> <span data-ttu-id="a37da-397">（ASP.NET 程式開發伺服器有時稱為 Cassini）。這個 Web 服務器是流覽和偵錯工具在檔案系統上執行之 Web 應用程式的便利方法。</span><span class="sxs-lookup"><span data-stu-id="a37da-397">(The ASP.NET Development Server is sometimes referred to as Cassini.) This Web server is a convenient means to browse and debug Web applications running on the file system.</span></span>

<span data-ttu-id="a37da-398">ASP.NET 程式開發伺服器是受限制的 Web 服務器。</span><span class="sxs-lookup"><span data-stu-id="a37da-398">The ASP.NET Development Server is a restricted Web server.</span></span> <span data-ttu-id="a37da-399">它不允許遠端連線，它不允許來自啟動 Web 服務器的使用者以外的任何使用者提出任何要求。</span><span class="sxs-lookup"><span data-stu-id="a37da-399">It does not allow remote connections, it does not allow any requests from any user other than the user who started the Web server.</span></span> <span data-ttu-id="a37da-400">它也沒有提供 ASP 網頁的功能。</span><span class="sxs-lookup"><span data-stu-id="a37da-400">It also does not have the capability of serving ASP pages.</span></span> <span data-ttu-id="a37da-401">只會提供 ASP.NET 資源和 HTML 資源（包括影像、CSS 檔案等）。</span><span class="sxs-lookup"><span data-stu-id="a37da-401">Only ASP.NET resources and HTML resources (including images, CSS files, etc.) are served.</span></span>

<span data-ttu-id="a37da-402">ASP.NET 程式開發伺服器可以透過命令列來啟動，方法是執行位於 c：/Windows/Microsoft .net/Framework/v2.0./ */* / */* /\* 的 webdev.webserver.exe。</span><span class="sxs-lookup"><span data-stu-id="a37da-402">The ASP.NET Development Server can be launched via the command line by running the WebDev.WebServer.exe file located at c:/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/\*.</span></span> <span data-ttu-id="a37da-403">下列對話方塊會顯示可用的參數。</span><span class="sxs-lookup"><span data-stu-id="a37da-403">The following dialog displays the parameters that are available.</span></span>

![](improvements-in-visual-studio-2005/_static/image11.jpg)

<span data-ttu-id="a37da-404">**圖14**</span><span class="sxs-lookup"><span data-stu-id="a37da-404">**Figure 14**</span></span>

> [!NOTE]
> <span data-ttu-id="a37da-405">透過命令列明確啟動時，不支援 ASP.NET 程式開發伺服器。</span><span class="sxs-lookup"><span data-stu-id="a37da-405">The ASP.NET Development Server is not supported when launched explicitly via the command line.</span></span>
