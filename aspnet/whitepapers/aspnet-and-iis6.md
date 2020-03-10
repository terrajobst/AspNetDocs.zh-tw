---
uid: whitepapers/aspnet-and-iis6
title: 執行具有 IIS 6.0 的 ASP.NET 1.1 |Microsoft Docs
author: rick-anderson
description: 雖然 Windows Server 2003 同時包含 IIS 6.0 和 ASP.NET 1.1，但這些元件預設為停用。 本白皮書說明如何啟用 IIS 6.0 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 2e7812f34481afe9a71927c0d9ba2a9abc9632e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523307"
---
# <a name="running-aspnet-11-with-iis-60"></a><span data-ttu-id="7300f-104">執行 ASP.NET 1.1 與 IIS 6.0</span><span class="sxs-lookup"><span data-stu-id="7300f-104">Running ASP.NET 1.1 with IIS 6.0</span></span>

> <span data-ttu-id="7300f-105">雖然 Windows Server 2003 同時包含 IIS 6.0 和 ASP.NET 1.1，但這些元件預設為停用。</span><span class="sxs-lookup"><span data-stu-id="7300f-105">While Windows Server 2003 includes both IIS 6.0 and ASP.NET 1.1, these components are disabled by default.</span></span> <span data-ttu-id="7300f-106">本白皮書說明如何啟用 IIS 6.0 和 ASP.NET 1.1，並建議數個設定，以從 IIS 和 ASP.NET 取得最佳效能。</span><span class="sxs-lookup"><span data-stu-id="7300f-106">This whitepaper describes how to enable IIS 6.0 and ASP.NET 1.1, and recommends several configuration settings to get the optimal performance from IIS and ASP.NET.</span></span>
> 
> <span data-ttu-id="7300f-107">適用于 ASP.NET 1.1 和 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="7300f-107">Applies to ASP.NET 1.1 and IIS 6.0.</span></span>

<span data-ttu-id="7300f-108">ASP.NET 1.1 隨附于 Windows Server 2003，其中也包含最新版的 Internet Information Server （IIS）版本6.0。</span><span class="sxs-lookup"><span data-stu-id="7300f-108">ASP.NET 1.1 ships with Windows Server 2003, which also includes the latest version of Internet Information Server (IIS) version 6.0.</span></span> <span data-ttu-id="7300f-109">IIS 6.0 和 ASP.NET 1.1 是設計用來順暢地整合，而 ASP.NET 現在預設為新的 IIS 6.0 工作者進程模型。</span><span class="sxs-lookup"><span data-stu-id="7300f-109">IIS 6.0 and ASP.NET 1.1 are designed to integrate seamlessly and ASP.NET now defaults to the new IIS 6.0 worker process model.</span></span>

## <a name="aspnet-11-is-not-installed-by-default"></a><span data-ttu-id="7300f-110">預設不會安裝 ASP.NET 1。1</span><span class="sxs-lookup"><span data-stu-id="7300f-110">ASP.NET 1.1 is not installed by default</span></span>

<span data-ttu-id="7300f-111">與舊版的 Microsoft 伺服器作業系統不同的是，預設不會啟用 Internet Information Server （IIS）;也不是 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="7300f-111">Unlike previous versions of Microsoft's server operating systems, Internet Information Server (IIS) is not enabled by default; nor is ASP.NET 1.1.</span></span> <span data-ttu-id="7300f-112">有兩個選項可啟用 IIS：</span><span class="sxs-lookup"><span data-stu-id="7300f-112">There are two options for enabling IIS:</span></span>

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a><span data-ttu-id="7300f-113">啟用 IIS，選項 #1-設定您的伺服器 Wizard</span><span class="sxs-lookup"><span data-stu-id="7300f-113">Enabling IIS, option #1 - Configure Your Server Wizard</span></span>

<span data-ttu-id="7300f-114">Windows Server 2003 隨附新的「設定您的伺服器嚮導」，協助您在所需的模式下正確設定伺服器。</span><span class="sxs-lookup"><span data-stu-id="7300f-114">Windows Server 2003 ships a new 'Configure Your Server Wizard' to help you properly configure your server in the desired mode.</span></span>

<span data-ttu-id="7300f-115">若要啟動精靈-請注意，若要執行 wizard，您必須以系統管理員的身分登入-前往： Start |程式 |[系統管理工具]，然後選取 [設定您的伺服器]。</span><span class="sxs-lookup"><span data-stu-id="7300f-115">To start the wizard - note, to run the wizard you must be logged in as an administrator - go to: Start | Programs | Administrative Tools and select 'Configure Your Server'.</span></span>

<span data-ttu-id="7300f-116">選取之後，您應該會看到 [設定您的伺服器 Wizard] 開啟畫面：</span><span class="sxs-lookup"><span data-stu-id="7300f-116">Once selected you should see the 'Configure Your Server Wizard' opening screen:</span></span>

![](aspnet-and-iis6/_static/image1.jpg)

<span data-ttu-id="7300f-117">按一下 [下一步 &gt;]：</span><span class="sxs-lookup"><span data-stu-id="7300f-117">Click 'Next &gt;':</span></span>

![](aspnet-and-iis6/_static/image2.jpg)

<span data-ttu-id="7300f-118">按一下 [下一步 &gt;]</span><span class="sxs-lookup"><span data-stu-id="7300f-118">Click 'Next &gt;'</span></span>

![](aspnet-and-iis6/_static/image3.jpg)

<span data-ttu-id="7300f-119">在此畫面上，您將需要選取 [應用程式伺服器（IIS，ASP.NET）] 做為要設定的選項。</span><span class="sxs-lookup"><span data-stu-id="7300f-119">On this screen you will need to select 'Application server (IIS, ASP.NET) as the options to configure.</span></span>

<span data-ttu-id="7300f-120">按一下 [下一步 &gt;]。</span><span class="sxs-lookup"><span data-stu-id="7300f-120">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image4.jpg)

<span data-ttu-id="7300f-121">選取將伺服器設定為應用程式伺服器之後，將會顯示此畫面，提示您應安裝的其他功能。</span><span class="sxs-lookup"><span data-stu-id="7300f-121">After selecting to configure the server as an Application Server, this screen will be displayed prompting what additional capabilities should be installed.</span></span> <span data-ttu-id="7300f-122">預設不會選取任何選項。</span><span class="sxs-lookup"><span data-stu-id="7300f-122">Neither option is selected by default.</span></span> <span data-ttu-id="7300f-123">若要自動啟用 ASP.NET，您必須選取 [啟用 ASP]。NET '。</span><span class="sxs-lookup"><span data-stu-id="7300f-123">To enable ASP.NET automatically, you need to select 'Enable ASP.NET'.</span></span>

<span data-ttu-id="7300f-124">按一下 [下一步 &gt;]。</span><span class="sxs-lookup"><span data-stu-id="7300f-124">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image5.jpg)

<span data-ttu-id="7300f-125">此畫面會顯示要安裝的選項。</span><span class="sxs-lookup"><span data-stu-id="7300f-125">This screen displays what options are to be installed.</span></span>

<span data-ttu-id="7300f-126">按一下 [下一步 &gt;]。</span><span class="sxs-lookup"><span data-stu-id="7300f-126">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image6.jpg)

<span data-ttu-id="7300f-127">您在安裝選取的選項時，將會看到此畫面。</span><span class="sxs-lookup"><span data-stu-id="7300f-127">You will see this screen while the options you selected are being installed.</span></span> <span data-ttu-id="7300f-128">在安裝服務時，通常會看到其他對話方塊出現。</span><span class="sxs-lookup"><span data-stu-id="7300f-128">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="7300f-129">系統可能會另外提示您輸入 Windows 2003 Server 安裝光碟的位置。</span><span class="sxs-lookup"><span data-stu-id="7300f-129">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="7300f-130">完成時，請按一下 [下一步 &gt;]。</span><span class="sxs-lookup"><span data-stu-id="7300f-130">Click 'Next &gt;' when complete.</span></span>

![](aspnet-and-iis6/_static/image7.jpg)

<span data-ttu-id="7300f-131">按一下 [完成]-Windows Server 2003 現在已設定為支援 IIS 6.0 和 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="7300f-131">Click 'Finish' - the Windows Server 2003 is now configured to support IIS 6.0 and ASP.NET 1.1.</span></span>

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a><span data-ttu-id="7300f-132">啟用 IIS，選項 #2-手動設定 IIS 和 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7300f-132">Enabling IIS, option #2 - Manually configuring IIS and ASP.NET</span></span>

<span data-ttu-id="7300f-133">如果您不想使用「設定您的伺服器嚮導」，您可以選擇性地使用 [控制台] 中的 [新增或移除程式] 來安裝 IIS 6.0 和 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="7300f-133">If you do not wish to use the 'Configure Your Server Wizard' you can optionally install IIS 6.0 and ASP.NET 1.1 using 'Add or Remove Programs' from the Control Panel.</span></span>

<span data-ttu-id="7300f-134">首先開啟 [控制台]：</span><span class="sxs-lookup"><span data-stu-id="7300f-134">First open the Control Panel:</span></span>

![](aspnet-and-iis6/_static/image8.jpg)

<span data-ttu-id="7300f-135">接下來，按一下 [新增/移除 Windows 元件]，這會開啟 [Windows 元件嚮導]：</span><span class="sxs-lookup"><span data-stu-id="7300f-135">Next, click on 'Add/Remove Windows Components' which will open the 'Windows Components Wizard':</span></span>

![](aspnet-and-iis6/_static/image9.jpg)

<span data-ttu-id="7300f-136">反白顯示並勾選 [應用程式伺服器]，然後按一下 [詳細資料？]</span><span class="sxs-lookup"><span data-stu-id="7300f-136">Highlight and check 'Application Server' and then click the 'Details?'</span></span> <span data-ttu-id="7300f-137">button</span><span class="sxs-lookup"><span data-stu-id="7300f-137">button:</span></span>

![](aspnet-and-iis6/_static/image10.jpg)

<span data-ttu-id="7300f-138">若要安裝 ASP.NET，請核取 [ASP]。NET '。</span><span class="sxs-lookup"><span data-stu-id="7300f-138">To install ASP.NET, check 'ASP.NET'.</span></span>

<span data-ttu-id="7300f-139">按一下 [確定] 以返回 Windows 元件嚮導。</span><span class="sxs-lookup"><span data-stu-id="7300f-139">Click 'OK' to return to the Windows Component Wizard.</span></span> <span data-ttu-id="7300f-140">按一下 Windows 元件嚮導中的 [下一步 &gt;] 開始安裝：</span><span class="sxs-lookup"><span data-stu-id="7300f-140">Click 'Next &gt;' from the Windows Component Wizard to begin installing:</span></span>

![](aspnet-and-iis6/_static/image11.jpg)

<span data-ttu-id="7300f-141">在安裝服務時，通常會看到其他對話方塊出現。</span><span class="sxs-lookup"><span data-stu-id="7300f-141">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="7300f-142">系統可能會另外提示您輸入 Windows 2003 Server 安裝光碟的位置。</span><span class="sxs-lookup"><span data-stu-id="7300f-142">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="7300f-143">當安裝完成時，您會看到 Windows 元件嚮導的最後一個畫面：</span><span class="sxs-lookup"><span data-stu-id="7300f-143">When installation is complete you will see the last screen of the Windows Component Wizard:</span></span>

![](aspnet-and-iis6/_static/image12.jpg)

<span data-ttu-id="7300f-144">現在已設定並可使用 IIS 6.0 和 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="7300f-144">IIS 6.0 and ASP.NET 1.1 are now configured and available.</span></span>

## <a name="recommended-settings"></a><span data-ttu-id="7300f-145">建議的設定</span><span class="sxs-lookup"><span data-stu-id="7300f-145">Recommended Settings</span></span>

<span data-ttu-id="7300f-146">執行具有 IIS 6.0 的 ASP.NET 1.1 時，有數個設定建議，以取得 ASP.NET 的最佳效能：</span><span class="sxs-lookup"><span data-stu-id="7300f-146">When running ASP.NET 1.1 with IIS 6.0 there are several configuration settings that are recommended to get the optimal performance from ASP.NET:</span></span>

- <span data-ttu-id="7300f-147">設定工作者進程記憶體限制</span><span class="sxs-lookup"><span data-stu-id="7300f-147">Configuring worker process memory limits</span></span>
- <span data-ttu-id="7300f-148">設定工作者進程回收</span><span class="sxs-lookup"><span data-stu-id="7300f-148">Configuring worker process recycling</span></span>

### <a name="configuring-worker-process-memory-limits"></a><span data-ttu-id="7300f-149">設定工作者進程記憶體限制</span><span class="sxs-lookup"><span data-stu-id="7300f-149">Configuring worker process memory limits</span></span>

<span data-ttu-id="7300f-150">根據預設，IIS 6.0 不會設定 IIS 允許使用的記憶體數量限制。</span><span class="sxs-lookup"><span data-stu-id="7300f-150">By default IIS 6.0 does not set a limit on the amount of memory that IIS is allowed to use.</span></span> <span data-ttu-id="7300f-151">ASP.NET 的快取功能依賴記憶體的限制，因此快取可以主動從記憶體中移除未使用的專案。</span><span class="sxs-lookup"><span data-stu-id="7300f-151">ASP.NET's Cache feature relies on a limitation of memory so the Cache can proactively remove unused items from memory.</span></span>

<span data-ttu-id="7300f-152">建議您設定 IIS 6.0 的記憶體回收功能。</span><span class="sxs-lookup"><span data-stu-id="7300f-152">It is recommended that you configure the memory recycling feature of IIS 6.0.</span></span> <span data-ttu-id="7300f-153">若要設定這個開啟的 Internet Information Services 管理員（開始 |程式 |系統管理工具 |Internet Information Services）。</span><span class="sxs-lookup"><span data-stu-id="7300f-153">To configure this open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="7300f-154">開啟之後，展開 [應用程式集區] 資料夾：</span><span class="sxs-lookup"><span data-stu-id="7300f-154">Once open, expand the 'Application Pools' folder:</span></span>

<span data-ttu-id="7300f-155">針對每個應用程式集區：</span><span class="sxs-lookup"><span data-stu-id="7300f-155">For each application pool:</span></span>

![](aspnet-and-iis6/_static/image13.jpg)

1. <span data-ttu-id="7300f-156">以滑鼠右鍵按一下應用程式集區（例如 ' DefaultAppPool '），然後選取 [屬性]：</span><span class="sxs-lookup"><span data-stu-id="7300f-156">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image14.jpg)

2. <span data-ttu-id="7300f-157">接下來，按一下 [使用的記憶體上限（以 mb 為單位）：] 來啟用記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="7300f-157">Next, enable Memory recycling by clicking on either 'Maximum used memory (in megabytes):'.</span></span> <span data-ttu-id="7300f-158">此值不能超過伺服器上的實體（非虛擬）記憶體量，良好近似值是實體記憶體的60%，亦即，如果是具有512MB 實體記憶體的伺服器，請選取310。</span><span class="sxs-lookup"><span data-stu-id="7300f-158">The value should not be more than the amount of physical (not virtual) memory on the server, a good approximation is 60% of the physical memory, i.e. for a server with 512MB of physical memory select 310.</span></span> <span data-ttu-id="7300f-159">此外，也建議您在使用2GB 位址空間時，最大值不能超過800MB。</span><span class="sxs-lookup"><span data-stu-id="7300f-159">It is also recommended that the maximum not exceed 800MB when using a 2GB address space.</span></span> <span data-ttu-id="7300f-160">如果伺服器的記憶體位址空間是3GB，則工作者進程的最大記憶體限制可以是1，800MB：</span><span class="sxs-lookup"><span data-stu-id="7300f-160">If the memory address space of the server is 3GB, the maximum memory limit for the worker process can be as high as 1,800MB:</span></span>

![](aspnet-and-iis6/_static/image15.jpg)

<span data-ttu-id="7300f-161">按一下 [套用] 和 [確定] 以結束 [屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7300f-161">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="7300f-162">針對所有可用的應用程式集區重複此動作。</span><span class="sxs-lookup"><span data-stu-id="7300f-162">Repeat this for all available application pools.</span></span>

### <a name="configuring-worker-recycling"></a><span data-ttu-id="7300f-163">設定工作者回收</span><span class="sxs-lookup"><span data-stu-id="7300f-163">Configuring worker recycling</span></span>

<span data-ttu-id="7300f-164">根據預設，IIS 6.0 已設定為每隔29小時回收其工作者進程。</span><span class="sxs-lookup"><span data-stu-id="7300f-164">By default IIS 6.0 is configured to recycle its worker process every 29 hours.</span></span> <span data-ttu-id="7300f-165">這對執行 ASP.NET 的應用程式會有點積極，因此建議停用自動背景工作進程回收。</span><span class="sxs-lookup"><span data-stu-id="7300f-165">This is a bit aggressive for an application running ASP.NET and it is recommended that automatic worker process recycling is disabled.</span></span>

<span data-ttu-id="7300f-166">若要停用自動工作者進程回收，請先開啟 Internet Information Services 管理員（[開始] |程式 |系統管理工具 |Internet Information Services）。</span><span class="sxs-lookup"><span data-stu-id="7300f-166">To disable automatic worker process recycling, first open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="7300f-167">開啟之後，展開 [應用程式集區] 資料夾：</span><span class="sxs-lookup"><span data-stu-id="7300f-167">Once open, expand the 'Application Pools' folder:</span></span>

![](aspnet-and-iis6/_static/image16.jpg)

<span data-ttu-id="7300f-168">針對每個應用程式集區：</span><span class="sxs-lookup"><span data-stu-id="7300f-168">For each application pool:</span></span>

1. <span data-ttu-id="7300f-169">以滑鼠右鍵按一下應用程式集區（例如 ' DefaultAppPool '），然後選取 [屬性]：</span><span class="sxs-lookup"><span data-stu-id="7300f-169">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image17.jpg)

2. <span data-ttu-id="7300f-170">取消核取 [回收背景工作進程（分鐘）：]：</span><span class="sxs-lookup"><span data-stu-id="7300f-170">Uncheck 'Recycle worker process (in minutes):':</span></span>

![](aspnet-and-iis6/_static/image18.jpg)

<span data-ttu-id="7300f-171">按一下 [套用] 和 [確定] 以結束 [屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7300f-171">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="7300f-172">針對所有可用的應用程式集區重複此動作。</span><span class="sxs-lookup"><span data-stu-id="7300f-172">Repeat this for all available application pools.</span></span>

## <a name="granting-write-access-to-the-file-system"></a><span data-ttu-id="7300f-173">授與檔案系統的寫入權限</span><span class="sxs-lookup"><span data-stu-id="7300f-173">Granting write access to the file system</span></span>

<span data-ttu-id="7300f-174">如果您的應用程式需要檔案系統的寫入權限，而且您使用 NTFS，則必須修改資料夾或檔案上的存取控制清單（ACL），以授與的 ASP.NET 存取權。</span><span class="sxs-lookup"><span data-stu-id="7300f-174">If your application requires write access to the file system and you are using NTFS you will need to modify an Access Control List (ACL) on the folder or file to grant ASP.NET access to.</span></span>

<span data-ttu-id="7300f-175">例如，若要將 ASP.NET 寫入存取權授與 c:\inetpub\wwwroot，請先開啟瀏覽器並流覽至目錄：</span><span class="sxs-lookup"><span data-stu-id="7300f-175">For example, to grant ASP.NET write access to the c:\inetpub\wwwroot first open explorer and navigate to the directory:</span></span>

![](aspnet-and-iis6/_static/image19.jpg)

<span data-ttu-id="7300f-176">接下來，以滑鼠右鍵按一下目錄，例如 [wwwroot]，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="7300f-176">Next, right-click on the directory, e.g. 'wwwroot' and select properties.</span></span> <span data-ttu-id="7300f-177">在 [屬性] 對話方塊開啟之後，選取 [安全性] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="7300f-177">After the properties dialog opens, select the 'Security' tab:</span></span>

![](aspnet-and-iis6/_static/image20.jpg)

<span data-ttu-id="7300f-178">C:\inetpub\wwwroot\ 目錄是特殊的目錄，其中已授與特殊的 IIS 6.0 群組 ' IIS\_WPG ' 讀取 &amp; 執行、列出資料夾內容和讀取權限。</span><span class="sxs-lookup"><span data-stu-id="7300f-178">The c:\inetpub\wwwroot\ directory is a special directory in that the special IIS 6.0 group 'IIS\_WPG' is already granted Read &amp; Execute, List Folder Contents, and Read permissions.</span></span> <span data-ttu-id="7300f-179">不過，若要授與寫入權限，您必須按一下 [允許] 核取方塊以進行寫入：</span><span class="sxs-lookup"><span data-stu-id="7300f-179">However, to grant Write permission, you need to click the Allow checkbox for Write:</span></span>

![](aspnet-and-iis6/_static/image21.jpg)

<span data-ttu-id="7300f-180">IIS 6.0 現在具有此資料夾的寫入權限。</span><span class="sxs-lookup"><span data-stu-id="7300f-180">IIS 6.0 now has write permission on this folder.</span></span> <span data-ttu-id="7300f-181">若要授與其他資料夾的寫入權限，請遵循下列步驟-請注意，您可能需要新增 IIS\_WPG 群組（如果尚未存在的話）。</span><span class="sxs-lookup"><span data-stu-id="7300f-181">To grant write permissions on other folders, follow these steps - note, you may need to add the IIS\_WPG group if it does not already exist.</span></span>

> [!CAUTION]
> <span data-ttu-id="7300f-182">將寫入權限授與 IIS\_WPG，可讓任何 ASP.NET 應用程式寫入此目錄。</span><span class="sxs-lookup"><span data-stu-id="7300f-182">Granting write permission to IIS\_WPG will allow any ASP.NET application to write to this directory.</span></span>

## <a name="supporting-integrated-authentication-with-sql-server"></a><span data-ttu-id="7300f-183">支援 SQL Server 的整合式驗證</span><span class="sxs-lookup"><span data-stu-id="7300f-183">Supporting integrated authentication with SQL Server</span></span>

<span data-ttu-id="7300f-184">整合式驗證可讓 SQL Server 利用 Windows NT 驗證來驗證 SQL Server 的登入帳戶。</span><span class="sxs-lookup"><span data-stu-id="7300f-184">Integrated authentication allows for SQL Server to leverage Windows NT authentication to validate SQL Server logon accounts.</span></span> <span data-ttu-id="7300f-185">這可讓使用者略過標準的 SQL Server 登入程式。</span><span class="sxs-lookup"><span data-stu-id="7300f-185">This allows the user to bypass the standard SQL Server logon process.</span></span> <span data-ttu-id="7300f-186">透過這種方法，網路使用者可以存取 SQL Server 資料庫，而不需提供個別的登入識別或密碼，因為 SQL Server 會從 Windows NT 網路安全性程式取得使用者和密碼資訊。</span><span class="sxs-lookup"><span data-stu-id="7300f-186">With this approach, a network user can access a SQL Server database without supplying a separate logon identification or password because SQL Server obtains the user and password information from the Windows NT network security process.</span></span>

<span data-ttu-id="7300f-187">選擇 ASP.NET 應用程式的整合式驗證是不錯的選擇，因為您的應用程式連接字串中不會儲存任何認證。</span><span class="sxs-lookup"><span data-stu-id="7300f-187">Choosing integrated authentication for ASP.NET applications is a good choice because no credentials are ever stored within your connection string for your application.</span></span> <span data-ttu-id="7300f-188">相反地，用來連接到 SQL 的連接字串看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="7300f-188">Rather the connection string used to connect to SQL will look as follows:</span></span>

`"server=localhost; database=Northwind;Trusted_Connection=true"`

<span data-ttu-id="7300f-189">此連接字串會告訴 SQL Server 使用嘗試存取 SQL Server 之應用程式的 Windows 認證。</span><span class="sxs-lookup"><span data-stu-id="7300f-189">This connection string tells SQL Server to use the Windows credentials of the application attempting to access SQL Server.</span></span> <span data-ttu-id="7300f-190">在 ASP.NET/IIS 6 的案例中，這會是 IIS\_WPG 群組中的帳戶。</span><span class="sxs-lookup"><span data-stu-id="7300f-190">In the case of ASP.NET/IIS 6 this would be an account in the IIS\_WPG group.</span></span>

<span data-ttu-id="7300f-191">若要啟用 SQL Server 和 ASP.NET 之間的整合式驗證，您必須先確定已針對整合式驗證或混合模式驗證設定 SQL Server-請洽詢您的 DBA 以判斷此情況。</span><span class="sxs-lookup"><span data-stu-id="7300f-191">To enable integrated authentication between SQL Server and ASP.NET, you will need to first ensure that SQL Server is configured for either Integrated authentication or Mixed-Mode authentication - check with your DBA to determine this.</span></span> <span data-ttu-id="7300f-192">如果 SQL Server 是這兩種模式的其中一種，您可以使用整合式驗證。</span><span class="sxs-lookup"><span data-stu-id="7300f-192">If SQL Server is in one of these two modes, you can use integrated authentication.</span></span>

<span data-ttu-id="7300f-193">開啟 SQL Server Enterprise Manager （開始 |程式 |Microsoft SQL Server |Enterprise Manager）中，選取適當的伺服器，然後展開 [安全性] 資料夾：</span><span class="sxs-lookup"><span data-stu-id="7300f-193">Open SQL Server Enterprise Manager (Start | Programs | Microsoft SQL Server | Enterprise Manager), select the appropriate server, and expand the Security folder:</span></span>

![](aspnet-and-iis6/_static/image22.jpg)

<span data-ttu-id="7300f-194">如果未列出 ' BUILTINT\IIS\_WPG ' 群組，請以滑鼠右鍵按一下 登入，然後選取 新增 Login '：</span><span class="sxs-lookup"><span data-stu-id="7300f-194">If 'BUILTINT\IIS\_WPG' group is not listed, right-click on Logins and select 'New Login':</span></span>

![](aspnet-and-iis6/_static/image23.jpg)

<span data-ttu-id="7300f-195">在 [名稱：] 文字方塊中，輸入 ' [Server/Domain Name] \IIS\_WPG '，或按一下省略號按鈕以開啟 [Windows NT 使用者/群組選擇器]：</span><span class="sxs-lookup"><span data-stu-id="7300f-195">In the 'Name:' textbox either enter '[Server/Domain Name]\IIS\_WPG' or click on the ellipses button to open the Windows NT user/group picker:</span></span>

![](aspnet-and-iis6/_static/image24.jpg)

<span data-ttu-id="7300f-196">選取目前電腦的 IIS\_WPG 群組，然後按一下 [新增] 和 [確定] 關閉選擇器。</span><span class="sxs-lookup"><span data-stu-id="7300f-196">Select the current machine's IIS\_WPG group and click 'Add' and OK to close the picker.</span></span>

<span data-ttu-id="7300f-197">接著，您也需要設定預設資料庫和存取資料庫的許可權。</span><span class="sxs-lookup"><span data-stu-id="7300f-197">You then need to also set the default database and the permissions to access the database.</span></span> <span data-ttu-id="7300f-198">若要設定預設資料庫，請從下拉式清單中選擇，例如在 [Northwind] 底下選取：</span><span class="sxs-lookup"><span data-stu-id="7300f-198">To set the default database choose from the drop down list, e.g. below Northwind is selected:</span></span>

![](aspnet-and-iis6/_static/image25.jpg)

<span data-ttu-id="7300f-199">接下來，按一下 [資料庫存取] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="7300f-199">Next, click on the Database Access tab:</span></span>

![](aspnet-and-iis6/_static/image26.jpg)

<span data-ttu-id="7300f-200">針對您想要允許存取的每個資料庫，按一下 [允許] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7300f-200">Click on the Permit checkbox for every database that you wish to allow access to.</span></span> <span data-ttu-id="7300f-201">您也必須選取資料庫角色，檢查 db\_擁有者將確保您的登入具有管理和使用選取之資料庫的所有必要許可權。</span><span class="sxs-lookup"><span data-stu-id="7300f-201">You will also need to select database roles, checking db\_owner will ensure your login has all necessary permissions to manage and use the selected database.</span></span>

<span data-ttu-id="7300f-202">按一下 [確定] 以結束 [屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7300f-202">Click OK to exit the property dialog.</span></span> <span data-ttu-id="7300f-203">您的 ASP.NET 應用程式現在已設定為支援整合式 SQL Server 驗證。</span><span class="sxs-lookup"><span data-stu-id="7300f-203">Your ASP.NET application is now configured to support integrated SQL Server authentication.</span></span>

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a><span data-ttu-id="7300f-204">不要在 IIS 6.0 原生模式中執行 ASP.NET 1。0</span><span class="sxs-lookup"><span data-stu-id="7300f-204">Don't run ASP.NET 1.0 in IIS 6.0 native mode</span></span>

<span data-ttu-id="7300f-205">Iis 6.0 上的 ASP.NET 1.0 只有在 IIS 5 相容性模式下才支援。</span><span class="sxs-lookup"><span data-stu-id="7300f-205">ASP.NET 1.0 on IIS 6.0 is only supported in IIS 5 compatibility mode.</span></span>

<span data-ttu-id="7300f-206">若要設定 ASP.NET 1.0 在 IIS 5.0 相容性模式中執行，請開啟網際網路服務管理員並以滑鼠右鍵按一下 [網站]，然後選取 [屬性]：</span><span class="sxs-lookup"><span data-stu-id="7300f-206">To configure ASP.NET 1.0 to run in IIS 5.0 compatibility mode, open Internet Services Manager and right click Web Sites and select properties:</span></span>

![](aspnet-and-iis6/_static/image27.jpg)

<span data-ttu-id="7300f-207">切換至 [服務] 索引標籤並檢查嗎？在 IIS 5.0 隔離模式中執行 WWW 服務？：</span><span class="sxs-lookup"><span data-stu-id="7300f-207">Switch to the Service Tab and check ?Run WWW Service in IIS 5.0 Isolation Mode?:</span></span>

![](aspnet-and-iis6/_static/image28.jpg)
