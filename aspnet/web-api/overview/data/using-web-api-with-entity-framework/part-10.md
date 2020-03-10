---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: 將應用程式發佈至 Azure Azure App Service |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: a9a7b74a07c71b47253c0af304c7a26ffa4eaae5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622385"
---
# <a name="publish-the-app-to-azure-azure-app-service"></a><span data-ttu-id="5b3af-102">將應用程式發佈至 Azure Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5b3af-102">Publish the App to Azure Azure App Service</span></span>

<span data-ttu-id="5b3af-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5b3af-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="5b3af-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="5b3af-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="5b3af-105">在最後一個步驟中，您會將應用程式發行至 Azure。</span><span class="sxs-lookup"><span data-stu-id="5b3af-105">As the last step, you will publish the application to Azure.</span></span> <span data-ttu-id="5b3af-106">在方案總管中，以滑鼠右鍵按一下專案，然後選取 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="5b3af-106">In Solution Explorer, right-click the project and select **Publish**.</span></span>

![](part-10/_static/image1.png)

<span data-ttu-id="5b3af-107">按一下 [**發佈**] 會叫用 [**發行 Web** ] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5b3af-107">Clicking **Publish** invokes the **Publish Web** dialog.</span></span> <span data-ttu-id="5b3af-108">如果您在第一次建立專案時已核取 [**主機在雲端**]，則已設定連接和設定。</span><span class="sxs-lookup"><span data-stu-id="5b3af-108">If you checked **Host in Cloud** when you first created the project, then the connection and settings are already configured.</span></span> <span data-ttu-id="5b3af-109">在此情況下，只需按一下 [**設定**] 索引標籤，然後檢查 &quot;執行 Code First 移轉&quot;。</span><span class="sxs-lookup"><span data-stu-id="5b3af-109">In that case, just click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="5b3af-110">（如果您在一開始就沒有檢查**雲端主機**，請遵循[下一節](#new-website)中的步驟。）</span><span class="sxs-lookup"><span data-stu-id="5b3af-110">(If you didn't check **Host in Cloud** at the beginning, then follow the steps in the [next section](#new-website).)</span></span>

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

<span data-ttu-id="5b3af-111">若要部署應用程式，請按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="5b3af-111">To deploy the app, click **Publish**.</span></span> <span data-ttu-id="5b3af-112">您可以在 [ **Web 發行活動**] 視窗中查看發行進度。</span><span class="sxs-lookup"><span data-stu-id="5b3af-112">You can view the publishing progress in the **Web Publish Activity** window.</span></span> <span data-ttu-id="5b3af-113">（從 [ **View** ] 功能表選取 [**其他視窗**]，然後選取 [ **Web 發行活動**]）。</span><span class="sxs-lookup"><span data-stu-id="5b3af-113">(From the **View** menu, select **Other Windows**, then select **Web Publish Activity**.)</span></span>

![](part-10/_static/image4.png)

<span data-ttu-id="5b3af-114">當 Visual Studio 完成部署應用程式時，預設瀏覽器會自動開啟至已部署網站的 URL，而您建立的應用程式現在正在雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="5b3af-114">When Visual Studio finishes deploying the app, the default browser automatically opens to the URL of the deployed website, and the application that you created is now running in the cloud.</span></span> <span data-ttu-id="5b3af-115">瀏覽器網址列中的 URL 會顯示正在從網際網路載入網站。</span><span class="sxs-lookup"><span data-stu-id="5b3af-115">The URL in the browser address bar shows that the site is being loaded from the Internet.</span></span>

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a><span data-ttu-id="5b3af-116">部署至新網站</span><span class="sxs-lookup"><span data-stu-id="5b3af-116">Deploying to a New Website</span></span>

<span data-ttu-id="5b3af-117">如果您在第一次建立專案時未檢查**雲端主機**，您可以立即設定新的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b3af-117">If you did not check **Host in Cloud** when you first created the project, you can configure a new web app now.</span></span> <span data-ttu-id="5b3af-118">在方案總管中，以滑鼠右鍵按一下專案，然後選取 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="5b3af-118">In Solution Explorer, right-click the project and select **Publish**.</span></span> <span data-ttu-id="5b3af-119">選取 [**設定檔**] 索引標籤，然後按一下 [ **Microsoft Azure 網站**]。</span><span class="sxs-lookup"><span data-stu-id="5b3af-119">Select the **Profile** tab and click **Microsoft Azure Websites**.</span></span> <span data-ttu-id="5b3af-120">如果您目前未登入 Azure，系統會提示您登入。</span><span class="sxs-lookup"><span data-stu-id="5b3af-120">If you aren't currently signed in to Azure, you will be prompted to sign in.</span></span>

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

<span data-ttu-id="5b3af-121">在 [**現有網站**] 對話方塊中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="5b3af-121">In the **Existing Websites** dialog, click **New**.</span></span>

![](part-10/_static/image9.png)

<span data-ttu-id="5b3af-122">輸入 [網站名稱]。</span><span class="sxs-lookup"><span data-stu-id="5b3af-122">Enter a site name.</span></span> <span data-ttu-id="5b3af-123">選取您的 Azure 訂用帳戶和區域。</span><span class="sxs-lookup"><span data-stu-id="5b3af-123">Select your Azure subscription and the region.</span></span> <span data-ttu-id="5b3af-124">在 [**資料庫伺服器**] 底下，選取 [**建立新的伺服器**]，或選取現有的伺服器。</span><span class="sxs-lookup"><span data-stu-id="5b3af-124">Under **Database server**, select **Create New Server**, or select an existing server.</span></span> <span data-ttu-id="5b3af-125">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5b3af-125">Click **Create**.</span></span>

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

<span data-ttu-id="5b3af-126">按一下 [**設定**] 索引標籤，然後勾選 [&quot;執行 Code First 移轉&quot;]。</span><span class="sxs-lookup"><span data-stu-id="5b3af-126">Click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="5b3af-127">然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="5b3af-127">Then click **Publish**.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5b3af-128">上一篇</span><span class="sxs-lookup"><span data-stu-id="5b3af-128">Previous</span></span>](part-9.md)
