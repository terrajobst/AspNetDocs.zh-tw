---
uid: web-api/overview/older-versions/self-host-a-web-api
title: 自我裝載 ASP.NET Web API 1 （C#）-ASP.NET 4。x
author: MikeWasson
description: 教學課程示範如何在主控台應用程式中裝載 Web API。
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: bae1737ba5b16bc67fa0ed0474ff04df0add1b3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525085"
---
# <a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="33255-103">自我裝載 ASP.NET Web API 1 （C#）</span><span class="sxs-lookup"><span data-stu-id="33255-103">Self-Host ASP.NET Web API 1 (C#)</span></span>

<span data-ttu-id="33255-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="33255-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="33255-105">本教學課程說明如何在主控台應用程式中裝載 Web API。</span><span class="sxs-lookup"><span data-stu-id="33255-105">This tutorial shows how to host a web API inside a console application.</span></span> <span data-ttu-id="33255-106">ASP.NET Web API 不需要 IIS。</span><span class="sxs-lookup"><span data-stu-id="33255-106">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="33255-107">您可以在自己的主機進程中自我裝載 Web API。</span><span class="sxs-lookup"><span data-stu-id="33255-107">You can self-host a web API in your own host process.</span></span> 
> 
> <span data-ttu-id="33255-108">**新的應用程式應該使用 OWIN 來自我裝載 Web API。**</span><span class="sxs-lookup"><span data-stu-id="33255-108">**New applications should use OWIN to self-host Web API.**</span></span> <span data-ttu-id="33255-109">請參閱[使用 OWIN 至自我裝載 ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="33255-109">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="33255-110">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="33255-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="33255-111">Web API 1</span><span class="sxs-lookup"><span data-stu-id="33255-111">Web API 1</span></span>
> - <span data-ttu-id="33255-112">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="33255-112">Visual Studio 2012</span></span>

## <a name="create-the-console-application-project"></a><span data-ttu-id="33255-113">建立主控台應用程式專案</span><span class="sxs-lookup"><span data-stu-id="33255-113">Create the Console Application Project</span></span>

<span data-ttu-id="33255-114">啟動 Visual Studio，然後從 [**開始**] 頁面選取 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="33255-114">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="33255-115">或者，**從 [檔案**] 功能表選取 [**新增**]，然後選取 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="33255-115">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="33255-116">在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。</span><span class="sxs-lookup"><span data-stu-id="33255-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="33255-117">在 **[ C#視覺效果**] 底下，選取 [ **Windows**]。</span><span class="sxs-lookup"><span data-stu-id="33255-117">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="33255-118">在專案範本清單中，選取 [**主控台應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="33255-118">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="33255-119">將專案命名為 &quot;SelfHost&quot; 然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="33255-119">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="33255-120">設定目標 Framework （Visual Studio 2010）</span><span class="sxs-lookup"><span data-stu-id="33255-120">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="33255-121">如果您使用 Visual Studio 2010，請將目標 framework 變更為 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="33255-121">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="33255-122">（根據預設，專案範本會以[.Net Framework 用戶端設定檔](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile)為目標）。</span><span class="sxs-lookup"><span data-stu-id="33255-122">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="33255-123">在方案總管中，以滑鼠右鍵按一下專案，然後選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="33255-123">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="33255-124">在 [**目標 framework** ] 下拉式清單中，將 [目標 framework] 變更為 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="33255-124">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="33255-125">當系統提示您套用變更時，按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="33255-125">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="33255-126">安裝 NuGet 套件管理員</span><span class="sxs-lookup"><span data-stu-id="33255-126">Install NuGet Package Manager</span></span>

<span data-ttu-id="33255-127">NuGet 套件管理員是將 Web API 元件新增至 non-ASP.NET 專案的最簡單方式。</span><span class="sxs-lookup"><span data-stu-id="33255-127">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="33255-128">若要檢查是否已安裝 NuGet 套件管理員，請按一下 Visual Studio 中的 [**工具**] 功能表。</span><span class="sxs-lookup"><span data-stu-id="33255-128">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="33255-129">如果您看到名為 [ **Nuget 套件管理員**] 的功能表項目，則您會有 Nuget 套件管理員。</span><span class="sxs-lookup"><span data-stu-id="33255-129">If you see a menu item called **NuGet Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="33255-130">若要安裝 NuGet 套件管理員：</span><span class="sxs-lookup"><span data-stu-id="33255-130">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="33255-131">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="33255-131">Start Visual Studio.</span></span>
2. <span data-ttu-id="33255-132">從 [工具] 功能表中，選取 [擴充功能和更新]。</span><span class="sxs-lookup"><span data-stu-id="33255-132">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="33255-133">在 [**擴充功能和更新**] 對話方塊中，選取 [**線上**]。</span><span class="sxs-lookup"><span data-stu-id="33255-133">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="33255-134">如果您沒有看到「NuGet 套件管理員」，請在搜尋方塊中輸入「nuget 套件管理員」。</span><span class="sxs-lookup"><span data-stu-id="33255-134">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="33255-135">選取 [NuGet 套件管理員]，然後按一下 [**下載**]。</span><span class="sxs-lookup"><span data-stu-id="33255-135">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="33255-136">下載完成之後，系統會提示您安裝。</span><span class="sxs-lookup"><span data-stu-id="33255-136">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="33255-137">安裝完成之後，系統可能會提示您重新開機 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="33255-137">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="33255-138">新增 Web API NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="33255-138">Add the Web API NuGet Package</span></span>

<span data-ttu-id="33255-139">安裝 NuGet 套件管理員之後，請將 Web API 自我裝載封裝新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="33255-139">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="33255-140">從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]。</span><span class="sxs-lookup"><span data-stu-id="33255-140">From the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="33255-141">*注意*：如果您看不到此功能表項目，請確定已正確安裝 NuGet 套件管理員。</span><span class="sxs-lookup"><span data-stu-id="33255-141">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="33255-142">選取 [**管理解決方案的 NuGet 套件**]</span><span class="sxs-lookup"><span data-stu-id="33255-142">Select **Manage NuGet Packages for Solution**</span></span>
3. <span data-ttu-id="33255-143">在 [**管理 NugGet 封裝**] 對話方塊中，選取 [**線上**]。</span><span class="sxs-lookup"><span data-stu-id="33255-143">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="33255-144">在搜尋方塊中，輸入 &quot;WebApi. SelfHost&quot;。</span><span class="sxs-lookup"><span data-stu-id="33255-144">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="33255-145">選取 ASP.NET Web API 的自我裝載套件，然後按一下 [**安裝**]。</span><span class="sxs-lookup"><span data-stu-id="33255-145">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="33255-146">安裝套件之後，按一下 [**關閉**] 以關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="33255-146">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="33255-147">請務必安裝名為 WebApi. SelfHost，而不是 AspNetWebApi. SelfHost 的套件。</span><span class="sxs-lookup"><span data-stu-id="33255-147">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="33255-148">建立模型和控制器</span><span class="sxs-lookup"><span data-stu-id="33255-148">Create the Model and Controller</span></span>

<span data-ttu-id="33255-149">本教學課程使用與[消費者入門](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教學課程相同的模型和控制器類別。</span><span class="sxs-lookup"><span data-stu-id="33255-149">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="33255-150">新增名為 `Product`的公用類別。</span><span class="sxs-lookup"><span data-stu-id="33255-150">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="33255-151">新增名為 `ProductsController`的公用類別。</span><span class="sxs-lookup"><span data-stu-id="33255-151">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="33255-152">從**ApiController**衍生這個類別。</span><span class="sxs-lookup"><span data-stu-id="33255-152">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="33255-153">如需此控制器中程式碼的詳細資訊，請參閱[消費者入門](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="33255-153">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="33255-154">此控制器會定義三個 GET 動作：</span><span class="sxs-lookup"><span data-stu-id="33255-154">This controller defines three GET actions:</span></span>

| <span data-ttu-id="33255-155">URI</span><span class="sxs-lookup"><span data-stu-id="33255-155">URI</span></span> | <span data-ttu-id="33255-156">說明</span><span class="sxs-lookup"><span data-stu-id="33255-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="33255-157">/api/products</span><span class="sxs-lookup"><span data-stu-id="33255-157">/api/products</span></span> | <span data-ttu-id="33255-158">取得所有產品的清單。</span><span class="sxs-lookup"><span data-stu-id="33255-158">Get a list of all products.</span></span> |
| <span data-ttu-id="33255-159">/api/products/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="33255-159">/api/products/*id*</span></span> | <span data-ttu-id="33255-160">依識別碼取得產品。</span><span class="sxs-lookup"><span data-stu-id="33255-160">Get a product by ID.</span></span> |
| <span data-ttu-id="33255-161">/api/products/？ category =*category*</span><span class="sxs-lookup"><span data-stu-id="33255-161">/api/products/?category=*category*</span></span> | <span data-ttu-id="33255-162">依類別取得產品清單。</span><span class="sxs-lookup"><span data-stu-id="33255-162">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="33255-163">裝載 Web API</span><span class="sxs-lookup"><span data-stu-id="33255-163">Host the Web API</span></span>

<span data-ttu-id="33255-164">開啟檔案 Program.cs，並新增下列 using 語句：</span><span class="sxs-lookup"><span data-stu-id="33255-164">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="33255-165">將下列程式碼新增至**Program**類別。</span><span class="sxs-lookup"><span data-stu-id="33255-165">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="33255-166">選擇性新增 HTTP URL 命名空間保留</span><span class="sxs-lookup"><span data-stu-id="33255-166">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="33255-167">此應用程式會接聽 `http://localhost:8080/`。</span><span class="sxs-lookup"><span data-stu-id="33255-167">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="33255-168">根據預設，接聽特定 HTTP 位址時需要系統管理員許可權。</span><span class="sxs-lookup"><span data-stu-id="33255-168">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="33255-169">當您執行本教學課程時，您可能會收到下列錯誤：「HTTP 無法登錄 URL http://+:8080/」，有兩種方式可避免此錯誤：</span><span class="sxs-lookup"><span data-stu-id="33255-169">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="33255-170">以提升的系統管理員許可權執行 Visual Studio，或</span><span class="sxs-lookup"><span data-stu-id="33255-170">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="33255-171">使用 Netsh 來授與您的帳戶許可權以保留 URL。</span><span class="sxs-lookup"><span data-stu-id="33255-171">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="33255-172">若要使用 Netsh，請使用系統管理員許可權開啟命令提示字元，並輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="33255-172">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="33255-173">其中*machine\username*是您的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="33255-173">where *machine\username* is your user account.</span></span>

<span data-ttu-id="33255-174">當您完成自我裝載時，請務必刪除保留：</span><span class="sxs-lookup"><span data-stu-id="33255-174">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="33255-175">從用戶端應用程式呼叫 Web API （C#）</span><span class="sxs-lookup"><span data-stu-id="33255-175">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="33255-176">讓我們撰寫一個簡單的主控台應用程式，以呼叫 Web API。</span><span class="sxs-lookup"><span data-stu-id="33255-176">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="33255-177">將新的主控台應用程式專案新增至方案：</span><span class="sxs-lookup"><span data-stu-id="33255-177">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="33255-178">在方案總管中，以滑鼠右鍵按一下方案，然後選取 [**加入新專案**]。</span><span class="sxs-lookup"><span data-stu-id="33255-178">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="33255-179">建立名為 &quot;ClientApp&quot;的新主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="33255-179">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="33255-180">使用 NuGet 套件管理員來新增 ASP.NET Web API 核心程式庫套件：</span><span class="sxs-lookup"><span data-stu-id="33255-180">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="33255-181">從 [工具] 功能表中，選取 [ **NuGet 套件管理員**]。</span><span class="sxs-lookup"><span data-stu-id="33255-181">From the Tools menu, select **NuGet Package Manager**.</span></span>
- <span data-ttu-id="33255-182">選取 [**管理解決方案的 NuGet 套件**]</span><span class="sxs-lookup"><span data-stu-id="33255-182">Select **Manage NuGet Packages for Solution**</span></span>
- <span data-ttu-id="33255-183">在 [**管理 NuGet 套件**] 對話方塊中，選取 [**線上**]。</span><span class="sxs-lookup"><span data-stu-id="33255-183">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="33255-184">在搜尋方塊中，輸入 &quot;WebApi. 用戶端&quot;。</span><span class="sxs-lookup"><span data-stu-id="33255-184">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="33255-185">選取 [Microsoft ASP.NET Web API 用戶端程式庫] 套件，然後按一下 [**安裝**]。</span><span class="sxs-lookup"><span data-stu-id="33255-185">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="33255-186">將 ClientApp 中的參考新增至 SelfHost 專案：</span><span class="sxs-lookup"><span data-stu-id="33255-186">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="33255-187">在方案總管中，以滑鼠右鍵按一下 [ClientApp] 專案。</span><span class="sxs-lookup"><span data-stu-id="33255-187">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="33255-188">選取 [新增參考]。</span><span class="sxs-lookup"><span data-stu-id="33255-188">Select **Add Reference**.</span></span>
- <span data-ttu-id="33255-189">在 [**參考管理員**] 對話方塊中，選取 [**方案**] 底下的 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="33255-189">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="33255-190">選取 [SelfHost] 專案。</span><span class="sxs-lookup"><span data-stu-id="33255-190">Select the SelfHost project.</span></span>
- <span data-ttu-id="33255-191">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="33255-191">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="33255-192">開啟用戶端/程式 .cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="33255-192">Open the Client/Program.cs file.</span></span> <span data-ttu-id="33255-193">加入下列 **using** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="33255-193">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="33255-194">新增靜態**HttpClient**實例：</span><span class="sxs-lookup"><span data-stu-id="33255-194">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="33255-195">新增下列方法以列出所有產品、依識別碼列出產品，以及依類別列出產品。</span><span class="sxs-lookup"><span data-stu-id="33255-195">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="33255-196">所有這些方法都會遵循相同的模式：</span><span class="sxs-lookup"><span data-stu-id="33255-196">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="33255-197">呼叫**HttpClient. GetAsync** ，將 GET 要求傳送至適當的 URI。</span><span class="sxs-lookup"><span data-stu-id="33255-197">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="33255-198">呼叫**HttpResponseMessage. EnsureSuccessStatusCode**。</span><span class="sxs-lookup"><span data-stu-id="33255-198">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="33255-199">如果 HTTP 回應狀態為錯誤碼，這個方法就會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="33255-199">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="33255-200">呼叫**ReadAsAsync&lt;t&gt;** ，將 CLR 類型從 HTTP 回應還原序列化。</span><span class="sxs-lookup"><span data-stu-id="33255-200">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="33255-201">這個方法是在**HttpContentExtensions**中定義的擴充方法。</span><span class="sxs-lookup"><span data-stu-id="33255-201">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="33255-202">**GetAsync**和**ReadAsAsync**方法都是非同步。</span><span class="sxs-lookup"><span data-stu-id="33255-202">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="33255-203">它們會傳回代表非同步作業的**Task**物件。</span><span class="sxs-lookup"><span data-stu-id="33255-203">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="33255-204">取得**Result**屬性會封鎖執行緒，直到作業完成為止。</span><span class="sxs-lookup"><span data-stu-id="33255-204">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="33255-205">如需使用 HttpClient 的詳細資訊，包括如何進行非封鎖式呼叫，請參閱[從 .Net 用戶端呼叫 WEB API](../advanced/calling-a-web-api-from-a-net-client.md)。</span><span class="sxs-lookup"><span data-stu-id="33255-205">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="33255-206">在呼叫這些方法之前，請先將 HttpClient 實例上的 BaseAddress 屬性設定為 "`http://localhost:8080`"。</span><span class="sxs-lookup"><span data-stu-id="33255-206">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="33255-207">例如:</span><span class="sxs-lookup"><span data-stu-id="33255-207">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="33255-208">這應該會輸出下列各項。</span><span class="sxs-lookup"><span data-stu-id="33255-208">This should output the following.</span></span> <span data-ttu-id="33255-209">（請記得先執行 SelfHost 應用程式）。</span><span class="sxs-lookup"><span data-stu-id="33255-209">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
