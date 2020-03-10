---
uid: whitepapers/denied-access-to-iis-directories
title: ASP.NET 拒絕存取 IIS 目錄 |Microsoft Docs
author: rick-anderson
description: 本白皮書說明當 ASP.NET 應用程式的要求傳回錯誤「拒絕存取 DirectoryName 目錄」時，您必須執行的動作。 無法進行 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: a3a53aa88abbe1bcaaea7d691406800c8f9b988b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638499"
---
# <a name="aspnet-denied-access-to-iis-directories"></a><span data-ttu-id="bb7ef-104">ASP.NET 拒絕存取 IIS 目錄</span><span class="sxs-lookup"><span data-stu-id="bb7ef-104">ASP.NET Denied Access to IIS Directories</span></span>

> <span data-ttu-id="bb7ef-105">本白皮書說明當 ASP.NET 應用程式的要求傳回錯誤「拒絕存取*DirectoryName*目錄」時，您必須執行的動作。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-105">This whitepaper describes what you must do if a request to your ASP.NET application returns the error, "Denied Access to *DirectoryName* directory.</span></span> <span data-ttu-id="bb7ef-106">無法開始監視目錄變更。」</span><span class="sxs-lookup"><span data-stu-id="bb7ef-106">Failed to start monitoring directory changes."</span></span>
> 
> <span data-ttu-id="bb7ef-107">適用于 ASP.NET 1.0 和 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-107">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="bb7ef-108">ASP.NET V1 RTM 現在會使用較低許可權的 windows 帳戶（在本機電腦上註冊為「ASPNET」帳戶）來執行。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-108">ASP.NET V1 RTM now runs using a less privileged windows account - registered as the "ASPNET" account on a local machine.</span></span>

<span data-ttu-id="bb7ef-109">在某些鎖定的系統上，此帳戶預設可能不會擁有網站內容目錄、應用程式根目錄或網站根目錄的讀取安全性存取權。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-109">On some locked down systems, this account may not by default have read security access to a website's content directories, the application root directory, or the web site root directory.</span></span> <span data-ttu-id="bb7ef-110">在此情況下，當您從指定的 web 應用程式要求頁面時，您會收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="bb7ef-110">In this case you will receive the following error when requesting pages from a given web application:</span></span>

![](denied-access-to-iis-directories/_static/image1.jpg)

<span data-ttu-id="bb7ef-111">若要修正此問題，您將需要變更適當目錄的安全性許可權。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-111">To fix this you will need to change the security permissions on the appropriate directories.</span></span>

<span data-ttu-id="bb7ef-112">具體來說，ASP.NET 需要網站根目錄（例如： c:\inetpub\wwwroot 或您在 IIS 中設定的任何替代網站目錄）的 ASPNET 帳戶的讀取、執行和列出存取權，也就是內容目錄和應用程式根目錄以監視設定檔案的變更。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-112">Specifically, ASP.NET requires read, execute, and list access for the ASPNET account for the web site root (for example: c:\inetpub\wwwroot or any alternative site directory you may have configured in IIS), the content directory and the application root directory in order to monitor for configuration file changes.</span></span> <span data-ttu-id="bb7ef-113">應用程式根目錄會對應到 IIS 管理工具（inetmgr）中與應用程式虛擬目錄相關聯的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-113">The application root corresponds to the folder path associated with the application virtual directory in the IIS Administration tool (inetmgr).</span></span>

<span data-ttu-id="bb7ef-114">例如，請考慮 [wwwroot] 資料夾下的下列應用程式階層。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-114">For example, consider the following application hierarchy under the wwwroot folder.</span></span>

`C:\inetpub\wwwroot\myapp\default.aspx`

<span data-ttu-id="bb7ef-115">在此範例中，ASPNET 帳戶需要針對 myapp 和 wwwroot 目錄中的內容所定義的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-115">For this example, the ASPNET account needs the read permissions defined above for content in both the myapp and the wwwroot directory.</span></span> <span data-ttu-id="bb7ef-116">根資料夾上的單一繼承 ACL 也可以選擇性地用於這兩個目錄（如果它們是嵌套的）。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-116">A single inherited ACL on the root folder can also be optionally used for both directories if they're nested.</span></span>

<span data-ttu-id="bb7ef-117">若要將許可權新增至目錄，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bb7ef-117">To add permissions to a directory, perform the following steps:</span></span>

- <span data-ttu-id="bb7ef-118">使用 Windows explorer 流覽至目錄</span><span class="sxs-lookup"><span data-stu-id="bb7ef-118">Using the Windows explorer, navigate to the directory</span></span>
- <span data-ttu-id="bb7ef-119">以滑鼠右鍵按一下目錄資料夾，然後選擇 [屬性]</span><span class="sxs-lookup"><span data-stu-id="bb7ef-119">Right click on the directory folder and choose "Properties"</span></span>
- <span data-ttu-id="bb7ef-120">流覽至 [屬性] 對話方塊上的 [安全性] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="bb7ef-120">Navigate to the "Security" tab on the property dialog</span></span>
- <span data-ttu-id="bb7ef-121">按一下 [新增] 按鈕，然後輸入電腦名稱稱，後面接著 ASPNET 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-121">Click the "Add" button and enter the machine name followed by the ASPNET account name.</span></span> <span data-ttu-id="bb7ef-122">例如，在名為 "webdev.webserver.exe" 的電腦上，您會輸入 webdev\ASPNET，然後點擊 [確定]。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-122">For example, on a machine named "webdev", you would enter webdev\ASPNET and hit "OK".</span></span>
- <span data-ttu-id="bb7ef-123">確定 ASPNET 帳戶已核取 [讀取 &amp; 執行]、[列出資料夾內容] 和 [讀取] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-123">Ensure that the ASPNET account has the "Read &amp; Execute", "List Folder Contents", and "Read" checkboxes checked.</span></span>
- <span data-ttu-id="bb7ef-124">按 [確定] 以關閉對話方塊並儲存變更。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-124">Hit OK to dismiss the dialog and save the changes.</span></span>

![](denied-access-to-iis-directories/_static/image2.jpg)

<span data-ttu-id="bb7ef-125">如有需要，您可以使用腳本或 Windows 隨附的「cacls .exe」工具來自動化這些變更。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-125">If desired, these changes can be automated using scripts or the "cacls.exe" tool that ships with Windows.</span></span> <span data-ttu-id="bb7ef-126">如需 ASPNET 帳戶的詳細資訊，請參閱[常見問題檔](https://go.microsoft.com/fwlink/?LinkId=5828)。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-126">For more information on the ASPNET account, please see the [FAQ document](https://go.microsoft.com/fwlink/?LinkId=5828).</span></span>

<span data-ttu-id="bb7ef-127">如果指定的 web 應用程式依賴對特定資料夾或檔案的寫入或修改許可權，則可以遵循相同程式並勾選 [寫入] 和/或 [修改] 核取方塊來授與。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-127">If a given web application relies on having write or modify permissions to a particular folder or file, this can be granted by following the same procedure and checking the "Write" and/or "Modify" checkboxes.</span></span>

<span data-ttu-id="bb7ef-128">在允許 Everyone 或 Users 群組讀取這些目錄（這是預設設定）的電腦上，將不會發生任何問題，也不需要執行上述步驟。</span><span class="sxs-lookup"><span data-stu-id="bb7ef-128">On machines that allow Everyone or the Users group read access to these directories (which is the default configuration), no issues will be encountered and the above steps will not be required.</span></span>
