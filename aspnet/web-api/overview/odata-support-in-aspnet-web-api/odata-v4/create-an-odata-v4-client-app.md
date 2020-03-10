---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: 建立 OData v4 用戶端應用程式C#（） |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: a0016cf2cc7bffe6268664395ccb38e140090310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556291"
---
# <a name="create-an-odata-v4-client-app-c"></a><span data-ttu-id="b1751-102">建立 OData v4 用戶端應用程式 (C#)</span><span class="sxs-lookup"><span data-stu-id="b1751-102">Create an OData v4 Client App (C#)</span></span>

<span data-ttu-id="b1751-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b1751-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b1751-104">在上一個教學課程中，您已建立支援 CRUD 作業的基本 OData 服務。</span><span class="sxs-lookup"><span data-stu-id="b1751-104">In the previous tutorial, you created a basic OData service that supports CRUD operations.</span></span> <span data-ttu-id="b1751-105">現在讓我們建立服務的用戶端。</span><span class="sxs-lookup"><span data-stu-id="b1751-105">Now let's create a client for the service.</span></span>

<span data-ttu-id="b1751-106">啟動 Visual Studio 的新實例，然後建立新的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="b1751-106">Start a new instance of Visual Studio and create a new console application project.</span></span> <span data-ttu-id="b1751-107">在 [**新增專案**] 對話方塊中，選取 [**已安裝**] &gt; [&gt; **Visual C#**  &gt; **Windows 桌面**的**範本**]，然後選取 [**主控台應用程式**] 範本。</span><span class="sxs-lookup"><span data-stu-id="b1751-107">In the **New Project** dialog, select **Installed** &gt; **Templates** &gt; **Visual C#** &gt; **Windows Desktop**, and select the **Console Application** template.</span></span> <span data-ttu-id="b1751-108">將專案命名為 &quot;ProductsApp&quot;。</span><span class="sxs-lookup"><span data-stu-id="b1751-108">Name the project &quot;ProductsApp&quot;.</span></span>

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="b1751-109">您也可以將主控台應用程式新增至包含 OData 服務的相同 Visual Studio 解決方案。</span><span class="sxs-lookup"><span data-stu-id="b1751-109">You can also add the console app to the same Visual Studio solution that contains the OData service.</span></span>

## <a name="install-the-odata-client-code-generator"></a><span data-ttu-id="b1751-110">安裝 OData 用戶端程式代碼產生器</span><span class="sxs-lookup"><span data-stu-id="b1751-110">Install the OData Client Code Generator</span></span>

<span data-ttu-id="b1751-111">從 [工具] 功能表中，選取 [擴充功能和更新]。</span><span class="sxs-lookup"><span data-stu-id="b1751-111">From the **Tools** menu, select **Extensions and Updates**.</span></span> <span data-ttu-id="b1751-112">選取 [**線上**&gt; **Visual Studio 資源庫**]。</span><span class="sxs-lookup"><span data-stu-id="b1751-112">Select **Online** &gt; **Visual Studio Gallery**.</span></span> <span data-ttu-id="b1751-113">在搜尋方塊中，搜尋 &quot;OData 用戶端程式代碼產生器&quot;。</span><span class="sxs-lookup"><span data-stu-id="b1751-113">In the search box, search for &quot;OData Client Code Generator&quot;.</span></span> <span data-ttu-id="b1751-114">按一下 [**下載**] 以安裝 VSIX。</span><span class="sxs-lookup"><span data-stu-id="b1751-114">Click **Download** to install the VSIX.</span></span> <span data-ttu-id="b1751-115">系統可能會提示您重新開機 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b1751-115">You might be prompted to restart Visual Studio.</span></span>

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a><span data-ttu-id="b1751-116">在本機執行 OData 服務</span><span class="sxs-lookup"><span data-stu-id="b1751-116">Run the OData Service Locally</span></span>

<span data-ttu-id="b1751-117">從 Visual Studio 執行 ProductService 專案。</span><span class="sxs-lookup"><span data-stu-id="b1751-117">Run the ProductService project from Visual Studio.</span></span> <span data-ttu-id="b1751-118">根據預設，Visual Studio 會將瀏覽器啟動至應用程式根目錄。</span><span class="sxs-lookup"><span data-stu-id="b1751-118">By default, Visual Studio launches a browser to the application root.</span></span> <span data-ttu-id="b1751-119">請記下 URI;在下一個步驟中，您將需要此項。</span><span class="sxs-lookup"><span data-stu-id="b1751-119">Note the URI; you will need this in the next step.</span></span> <span data-ttu-id="b1751-120">繼續執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1751-120">Leave the application running.</span></span>

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="b1751-121">如果您將這兩個專案放在相同的方案中，請務必執行 ProductService 專案而不進行調試。</span><span class="sxs-lookup"><span data-stu-id="b1751-121">If you put both projects in the same solution, make sure to run the ProductService project without debugging.</span></span> <span data-ttu-id="b1751-122">在下一個步驟中，您將需要在修改主控台應用程式專案時，讓服務保持執行狀態。</span><span class="sxs-lookup"><span data-stu-id="b1751-122">In the next step, you will need to keep the service running while you modify the console application project.</span></span>

## <a name="generate-the-service-proxy"></a><span data-ttu-id="b1751-123">產生服務 Proxy</span><span class="sxs-lookup"><span data-stu-id="b1751-123">Generate the Service Proxy</span></span>

<span data-ttu-id="b1751-124">服務 proxy 是一個 .NET 類別，可定義存取 OData 服務的方法。</span><span class="sxs-lookup"><span data-stu-id="b1751-124">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="b1751-125">Proxy 會將方法呼叫轉譯為 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="b1751-125">The proxy translates method calls into HTTP requests.</span></span> <span data-ttu-id="b1751-126">您將藉由執行[T4 範本](https://msdn.microsoft.com/library/bb126445.aspx)來建立 proxy 類別。</span><span class="sxs-lookup"><span data-stu-id="b1751-126">You will create the proxy class by running a [T4 template](https://msdn.microsoft.com/library/bb126445.aspx).</span></span>

<span data-ttu-id="b1751-127">以滑鼠右鍵按一下專案。</span><span class="sxs-lookup"><span data-stu-id="b1751-127">Right-click the project.</span></span> <span data-ttu-id="b1751-128">選取 **[** **新增 &gt; 新專案**]。</span><span class="sxs-lookup"><span data-stu-id="b1751-128">Select **Add** &gt; **New Item**.</span></span>

![](create-an-odata-v4-client-app/_static/image5.png)

<span data-ttu-id="b1751-129">在 [**加入新專案**] 對話方塊中，選取 [&gt; 程式**代碼**&gt; **OData 用戶端**] 的 [**視覺C#專案**]。</span><span class="sxs-lookup"><span data-stu-id="b1751-129">In the **Add New Item** dialog, select **Visual C# Items** &gt; **Code** &gt; **OData Client**.</span></span> <span data-ttu-id="b1751-130">將範本命名 &quot;ProductClient.tt&quot;。</span><span class="sxs-lookup"><span data-stu-id="b1751-130">Name the template &quot;ProductClient.tt&quot;.</span></span> <span data-ttu-id="b1751-131">按一下 [**新增**]，然後按一下 [安全性警告]。</span><span class="sxs-lookup"><span data-stu-id="b1751-131">Click **Add** and click through the security warning.</span></span>

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

<span data-ttu-id="b1751-132">此時，您會收到錯誤，您可以忽略它。</span><span class="sxs-lookup"><span data-stu-id="b1751-132">At this point, you'll get an error, which you can ignore.</span></span> <span data-ttu-id="b1751-133">Visual Studio 會自動執行範本，但範本需要先進行一些設定。</span><span class="sxs-lookup"><span data-stu-id="b1751-133">Visual Studio automatically runs the template, but the template needs some configuration settings first.</span></span>

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

<span data-ttu-id="b1751-134">開啟檔案 ProductClient。在 `Parameter` 元素中，貼上 ProductService 專案（上一個步驟）中的 URI。</span><span class="sxs-lookup"><span data-stu-id="b1751-134">Open the file ProductClient.odata.config. In the `Parameter` element, paste in the URI from the ProductService project (previous step).</span></span> <span data-ttu-id="b1751-135">例如:</span><span class="sxs-lookup"><span data-stu-id="b1751-135">For example:</span></span>

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

<span data-ttu-id="b1751-136">再次執行範本。</span><span class="sxs-lookup"><span data-stu-id="b1751-136">Run the template again.</span></span> <span data-ttu-id="b1751-137">在方案總管中，以滑鼠右鍵按一下 ProductClient.tt 檔案，然後選取 [**執行自訂工具**]。</span><span class="sxs-lookup"><span data-stu-id="b1751-137">In Solution Explorer, right click the ProductClient.tt file and select **Run Custom Tool**.</span></span>

<span data-ttu-id="b1751-138">此範本會建立名為 ProductClient.cs 的程式碼檔案，以定義 proxy。</span><span class="sxs-lookup"><span data-stu-id="b1751-138">The template creates a code file named ProductClient.cs that defines the proxy.</span></span> <span data-ttu-id="b1751-139">當您開發應用程式時，如果您變更 OData 端點，請再次執行範本來更新 proxy。</span><span class="sxs-lookup"><span data-stu-id="b1751-139">As you develop your app, if you change the OData endpoint, run the template again to update the proxy.</span></span>

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a><span data-ttu-id="b1751-140">使用服務 Proxy 呼叫 OData 服務</span><span class="sxs-lookup"><span data-stu-id="b1751-140">Use the Service Proxy to Call the OData Service</span></span>

<span data-ttu-id="b1751-141">開啟檔案 Program.cs，並以下列程式碼取代重複使用的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b1751-141">Open the file Program.cs and replace the boilerplate code with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

<span data-ttu-id="b1751-142">將*serviceUri*的值取代為先前的服務 URI。</span><span class="sxs-lookup"><span data-stu-id="b1751-142">Replace the value of *serviceUri* with the service URI from earlier.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

<span data-ttu-id="b1751-143">當您執行應用程式時，它應該會輸出下列內容：</span><span class="sxs-lookup"><span data-stu-id="b1751-143">When you run the app, it should output the following:</span></span>

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]
