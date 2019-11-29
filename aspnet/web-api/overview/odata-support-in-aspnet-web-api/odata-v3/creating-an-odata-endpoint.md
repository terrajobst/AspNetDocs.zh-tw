---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: 使用 Web API 2 建立 OData v3 端點 |Microsoft Docs
author: MikeWasson
description: 開放式資料通訊協定（OData）是 web 的資料存取通訊協定。 OData 提供統一的方式來結構資料、查詢資料，以及運算元據 。
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: e68a454398f109dfd089be9c9a44d3fe662acc2f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600424"
---
# <a name="creating-an-odata-v3-endpoint-with-web-api-2"></a><span data-ttu-id="3a7b3-104">使用 Web API 2 建立 OData v3 端點</span><span class="sxs-lookup"><span data-stu-id="3a7b3-104">Creating an OData v3 Endpoint with Web API 2</span></span>

<span data-ttu-id="3a7b3-105">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3a7b3-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="3a7b3-106">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="3a7b3-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="3a7b3-107">[開放式資料通訊協定](http://www.odata.org/)（OData）是 web 的資料存取通訊協定。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-107">The [Open Data Protocol](http://www.odata.org/) (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="3a7b3-108">OData 提供統一的方式來結構資料、查詢資料，以及透過 CRUD 作業（建立、讀取、更新和刪除）來運算元據集。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-108">OData provides a uniform way to structure data, query the data, and manipulate the data set through CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="3a7b3-109">OData 同時支援 AtomPub （XML）和 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-109">OData supports both AtomPub (XML) and JSON formats.</span></span> <span data-ttu-id="3a7b3-110">OData 也會定義公開資料相關中繼資料的方式。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-110">OData also defines a way to expose metadata about the data.</span></span> <span data-ttu-id="3a7b3-111">用戶端可以使用中繼資料來探索資料集的類型資訊和關聯性。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-111">Clients can use the metadata to discover the type information and relationships for the data set.</span></span>
>
> <span data-ttu-id="3a7b3-112">ASP.NET Web API 可讓您輕鬆地建立資料集的 OData 端點。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-112">ASP.NET Web API makes it easy to create an OData endpoint for a data set.</span></span> <span data-ttu-id="3a7b3-113">您可以完全控制端點所支援的 OData 作業。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-113">You can control exactly which OData operations the endpoint supports.</span></span> <span data-ttu-id="3a7b3-114">您可以將多個 OData 端點與非 OData 端點一起裝載。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-114">You can host multiple OData endpoints, alongside non-OData endpoints.</span></span> <span data-ttu-id="3a7b3-115">您可以完全掌控您的資料模型、後端商務邏輯和資料層。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-115">You have full control over your data model, back-end business logic, and data layer.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3a7b3-116">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="3a7b3-116">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="3a7b3-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3a7b3-117">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="3a7b3-118">Web API 2</span><span class="sxs-lookup"><span data-stu-id="3a7b3-118">Web API 2</span></span>
> - <span data-ttu-id="3a7b3-119">OData 第3版</span><span class="sxs-lookup"><span data-stu-id="3a7b3-119">OData Version 3</span></span>
> - <span data-ttu-id="3a7b3-120">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="3a7b3-120">Entity Framework 6</span></span>
> - [<span data-ttu-id="3a7b3-121">Fiddler Web 調試的 Proxy （選擇性）</span><span class="sxs-lookup"><span data-stu-id="3a7b3-121">Fiddler Web Debugging Proxy (Optional)</span></span>](http://www.fiddler2.com)
>
> <span data-ttu-id="3a7b3-122">已在[ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)中新增 Web API OData 支援。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-122">Web API OData support was added in [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="3a7b3-123">不過，本教學課程使用 Visual Studio 2013 中新增的樣板。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-123">However, this tutorial uses scaffolding that was added in Visual Studio 2013.</span></span>

<span data-ttu-id="3a7b3-124">在本教學課程中，您將建立用戶端可以查詢的簡單 OData 端點。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-124">In this tutorial, you will create a simple OData endpoint that clients can query.</span></span> <span data-ttu-id="3a7b3-125">您也會建立端點C#的用戶端。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-125">You will also create a C# client for the endpoint.</span></span> <span data-ttu-id="3a7b3-126">完成本教學課程之後，下一組教學課程會示範如何新增更多功能，包括實體關聯、動作和 $expand/$select。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-126">After you complete this tutorial, the next set of tutorials show how to add more functionality, including entity relations, actions, and $expand/$select.</span></span>

- [<span data-ttu-id="3a7b3-127">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="3a7b3-127">Create the Visual Studio Project</span></span>](#create-project)
- [<span data-ttu-id="3a7b3-128">新增實體模型</span><span class="sxs-lookup"><span data-stu-id="3a7b3-128">Add an Entity Model</span></span>](#add-model)
- [<span data-ttu-id="3a7b3-129">新增 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="3a7b3-129">Add an OData Controller</span></span>](#add-controller)
- [<span data-ttu-id="3a7b3-130">加入 EDM 和 Route</span><span class="sxs-lookup"><span data-stu-id="3a7b3-130">Add the EDM and Route</span></span>](#edm)
- [<span data-ttu-id="3a7b3-131">植入資料庫（選擇性）</span><span class="sxs-lookup"><span data-stu-id="3a7b3-131">Seed the Database (Optional)</span></span>](#seed-db)
- [<span data-ttu-id="3a7b3-132">探索 OData 端點</span><span class="sxs-lookup"><span data-stu-id="3a7b3-132">Exploring the OData Endpoint</span></span>](#explore)
- [<span data-ttu-id="3a7b3-133">OData 序列化格式</span><span class="sxs-lookup"><span data-stu-id="3a7b3-133">OData Serialization Formats</span></span>](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a><span data-ttu-id="3a7b3-134">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="3a7b3-134">Create the Visual Studio Project</span></span>

<span data-ttu-id="3a7b3-135">在本教學課程中，您將建立支援基本 CRUD 作業的 OData 端點。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-135">In this tutorial, you will create an OData endpoint that supports basic CRUD operations.</span></span> <span data-ttu-id="3a7b3-136">端點會公開單一資源，也就是一份產品清單。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-136">The endpoint will expose a single resource, a list of products.</span></span> <span data-ttu-id="3a7b3-137">稍後的教學課程會新增更多功能。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-137">Later tutorials will add more features.</span></span>

<span data-ttu-id="3a7b3-138">啟動 Visual Studio，然後從 [開始] 頁面選取 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-138">Start Visual Studio and select **New Project** from the Start page.</span></span> <span data-ttu-id="3a7b3-139">或者，**從 [檔案**] 功能表選取 [**新增**]，然後選取 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-139">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="3a7b3-140">在 [**範本**] 窗格中，選取 [**已安裝**的C#範本]，然後展開視覺效果節點。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-140">In the **Templates** pane, select **Installed Templates** and expand the Visual C# node.</span></span> <span data-ttu-id="3a7b3-141">在 **[ C#視覺效果**] 底下，選取 [ **Web**]。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-141">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="3a7b3-142">選取 **[ASP.NET Web 應用程式**] 範本。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-142">Select **the ASP.NET Web Application** template.</span></span>

![](creating-an-odata-endpoint/_static/image1.png)

<span data-ttu-id="3a7b3-143">在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [**空白**] 範本。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-143">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="3a7b3-144">在 [&quot;新增&quot;的資料夾和核心參考] 底下，檢查 [ **WEB API**]。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-144">Under &quot;Add folders and core references for...&quot;, check **Web API**.</span></span> <span data-ttu-id="3a7b3-145">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-145">Click **OK**.</span></span>

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a><span data-ttu-id="3a7b3-146">新增實體模型</span><span class="sxs-lookup"><span data-stu-id="3a7b3-146">Add an Entity Model</span></span>

<span data-ttu-id="3a7b3-147">「模型」是代表應用程式中資料的物件。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-147">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="3a7b3-148">在本教學課程中，我們需要代表產品的模型。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-148">For this tutorial, we need a model that represents a product.</span></span> <span data-ttu-id="3a7b3-149">模型會對應至我們的 OData 實體類型。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-149">The model corresponds to our OData entity type.</span></span>

<span data-ttu-id="3a7b3-150">在方案總管中，以滑鼠右鍵按一下 [模型] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-150">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="3a7b3-151">從內容功能表中，選取 [**新增**]，然後選取 [**類別**]。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-151">From the context menu, select **Add** then select **Class**.</span></span>

![](creating-an-odata-endpoint/_static/image3.png)

<span data-ttu-id="3a7b3-152">在 [**加入新**專案] 對話方塊中，將類別命名為 &quot;產品&quot;。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-152">In the **Add New** Item dialog, name the class &quot;Product&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="3a7b3-153">依照慣例，模型類別會放在 [模型] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-153">By convention, model classes are placed in the Models folder.</span></span> <span data-ttu-id="3a7b3-154">您不需要在自己的專案中遵循此慣例，但我們將在本教學課程中使用它。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-154">You don't have to follow this convention in your own projects, but we'll use it for this tutorial.</span></span>

<span data-ttu-id="3a7b3-155">在 Product.cs 檔案中，新增下列類別定義：</span><span class="sxs-lookup"><span data-stu-id="3a7b3-155">In the Product.cs file, add the following class definition:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

<span data-ttu-id="3a7b3-156">ID 屬性將會是實體索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-156">The ID property will be the entity key.</span></span> <span data-ttu-id="3a7b3-157">用戶端可以依識別碼查詢產品。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-157">Clients can query products by ID.</span></span> <span data-ttu-id="3a7b3-158">此欄位也會是後端資料庫中的主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-158">This field would also be the primary key in the back-end database.</span></span>

<span data-ttu-id="3a7b3-159">立即建立專案。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-159">Build the project now.</span></span> <span data-ttu-id="3a7b3-160">在下一個步驟中，我們將使用一些使用反映的 Visual Studio 樣板來尋找產品類型。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-160">In the next step, we'll use some Visual Studio scaffolding that uses reflection to find the Product type.</span></span>

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a><span data-ttu-id="3a7b3-161">新增 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="3a7b3-161">Add an OData Controller</span></span>

<span data-ttu-id="3a7b3-162">*控制器*是處理 HTTP 要求的類別。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-162">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="3a7b3-163">您可以針對 OData 服務中的每個實體集定義個別的控制器。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-163">You define a separate controller for each entity set in you OData service.</span></span> <span data-ttu-id="3a7b3-164">在本教學課程中，我們將建立單一控制器。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-164">In this tutorial, we'll create a single controller.</span></span>

<span data-ttu-id="3a7b3-165">在方案總管中，以滑鼠右鍵按一下 [控制器] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-165">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="3a7b3-166">選取 [**新增**]，然後選取 [**控制器**]。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-166">Select **Add** and then select **Controller**.</span></span>

![](creating-an-odata-endpoint/_static/image5.png)

<span data-ttu-id="3a7b3-167">在 **新增 Scaffold**  對話方塊中，選取 使用 Entity Framework&quot;&quot;具有動作的 Web API 2 OData 控制器。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-167">In the **Add Scaffold** dialog, select &quot;Web API 2 OData Controller with actions, using Entity Framework&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image6.png)

<span data-ttu-id="3a7b3-168">在 [**新增控制器**] 對話方塊中，將控制器命名為 "productscontroller.cs"。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-168">In the **Add Controller** dialog, name the controller "ProductsController".</span></span> <span data-ttu-id="3a7b3-169">選取 [&quot;使用非同步控制器動作&quot;] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-169">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="3a7b3-170">在 [**模型**] 下拉式清單中，選取 [Product] 類別。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-170">In the **Model** drop-down list, select the Product class.</span></span>

![](creating-an-odata-endpoint/_static/image7.png)

<span data-ttu-id="3a7b3-171">按一下 [**新增資料內容 ...** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-171">Click the **New data context...** button.</span></span> <span data-ttu-id="3a7b3-172">保留 [資料內容類型] 的預設名稱，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-172">Leave the default name for the data context type, and click **Add**.</span></span>

![](creating-an-odata-endpoint/_static/image8.png)

<span data-ttu-id="3a7b3-173">按一下 [新增控制器] 對話方塊中的 [新增]，以新增控制器。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-173">Click Add in the Add Controller dialog to add the controller.</span></span>

![](creating-an-odata-endpoint/_static/image9.png)

<span data-ttu-id="3a7b3-174">注意：如果您收到錯誤訊息，指出 &quot;取得類型 ...&quot;時發生錯誤，請確定您在新增 Product 類別之後，已建立 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-174">Note: If you get an error message that says &quot;There was an error getting the type...&quot;, make sure that you built the Visual Studio project after you added the Product class.</span></span> <span data-ttu-id="3a7b3-175">此樣板會使用反映來尋找類別。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-175">The scaffolding uses reflection to find the class.</span></span>

![](creating-an-odata-endpoint/_static/image10.png)

<span data-ttu-id="3a7b3-176">此架構會將兩個程式碼檔案加入至專案：</span><span class="sxs-lookup"><span data-stu-id="3a7b3-176">The scaffolding adds two code files to the project:</span></span>

- <span data-ttu-id="3a7b3-177">Products.cs 會定義用來執行 OData 端點的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-177">Products.cs defines the Web API controller that implements the OData endpoint.</span></span>
- <span data-ttu-id="3a7b3-178">ProductServiceCoNtext.cs 提供使用 Entity Framework 查詢基礎資料庫的方法。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-178">ProductServiceContext.cs provides methods to query the underlying database, using Entity Framework.</span></span>

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a><span data-ttu-id="3a7b3-179">加入 EDM 和 Route</span><span class="sxs-lookup"><span data-stu-id="3a7b3-179">Add the EDM and Route</span></span>

<span data-ttu-id="3a7b3-180">在方案總管中，展開應用程式\_開始 資料夾，然後開啟名為 WebApiConfig.cs 的檔案。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-180">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="3a7b3-181">此類別會保存 Web API 的設定程式碼。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-181">This class holds configuration code for Web API.</span></span> <span data-ttu-id="3a7b3-182">將此程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="3a7b3-182">Replace this code with the following:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

<span data-ttu-id="3a7b3-183">這段程式碼會執行兩項工作：</span><span class="sxs-lookup"><span data-stu-id="3a7b3-183">This code does two things:</span></span>

- <span data-ttu-id="3a7b3-184">建立 OData 端點的實體資料模型（EDM）。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-184">Creates an Entity Data Model (EDM) for the OData endpoint.</span></span>
- <span data-ttu-id="3a7b3-185">加入端點的路由。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-185">Adds a route for the endpoint.</span></span>

<span data-ttu-id="3a7b3-186">EDM 是資料的抽象模型。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-186">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="3a7b3-187">EDM 是用來建立元資料檔案，並定義服務的 Uri。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-187">The EDM is used to create the metadata document and define the URIs for the service.</span></span> <span data-ttu-id="3a7b3-188">**ODataConventionModelBuilder**會使用一組預設的命名慣例 edm 來建立 EDM。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-188">The **ODataConventionModelBuilder** creates an EDM by using a set of default naming conventions EDM.</span></span> <span data-ttu-id="3a7b3-189">這種方法需要最少的程式碼。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-189">This approach requires the least code.</span></span> <span data-ttu-id="3a7b3-190">如果您想要更充分掌控 EDM，您可以使用**用**類別來明確地新增屬性、索引鍵和導覽屬性來建立 edm。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-190">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="3a7b3-191">**EntitySet**方法會將實體集加入至 EDM：</span><span class="sxs-lookup"><span data-stu-id="3a7b3-191">The **EntitySet** method adds an entity set to the EDM:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

<span data-ttu-id="3a7b3-192">"Products" 字串會定義實體集的名稱。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-192">The string "Products" defines the name of the entity set.</span></span> <span data-ttu-id="3a7b3-193">控制器的名稱必須符合實體集的名稱。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-193">The name of the controller must match the name of the entity set.</span></span> <span data-ttu-id="3a7b3-194">在本教學課程中，實體集命名為 "Products"，而控制器的名稱為 `ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-194">In this tutorial, the entity set is named "Products" and the controller is named `ProductsController`.</span></span> <span data-ttu-id="3a7b3-195">如果您將實體集命名為 "ProductSet"，則會將控制器命名為 `ProductSetController`。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-195">If you named the entity set "ProductSet", you would name the controller `ProductSetController`.</span></span> <span data-ttu-id="3a7b3-196">請注意，端點可以有多個實體集。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-196">Note that an endpoint can have multiple entity sets.</span></span> <span data-ttu-id="3a7b3-197">針對每個實體集呼叫**EntitySet&lt;t&gt;** ，然後定義對應的控制器。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-197">Call **EntitySet&lt;T&gt;** for each entity set, and then define a corresponding controller.</span></span>

<span data-ttu-id="3a7b3-198">**MapODataRoute**方法會加入 OData 端點的路由。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-198">The **MapODataRoute** method adds a route for the OData endpoint.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

<span data-ttu-id="3a7b3-199">第一個參數是路由的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-199">The first parameter is a friendly name for the route.</span></span> <span data-ttu-id="3a7b3-200">您服務的用戶端看不到此名稱。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-200">Clients of your service do not see this name.</span></span> <span data-ttu-id="3a7b3-201">第二個參數是端點的 URI 前置詞。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-201">The second parameter is the URI prefix for the endpoint.</span></span> <span data-ttu-id="3a7b3-202">假設有此程式碼，Products 實體集的 URI 為 HTTP://<em>hostname</em>/odata/Products。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-202">Given this code, the URI for the Products entity set is http://<em>hostname</em>/odata/Products.</span></span> <span data-ttu-id="3a7b3-203">您的應用程式可以有一個以上的 OData 端點。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-203">Your application can have more than one OData endpoint.</span></span> <span data-ttu-id="3a7b3-204">針對每個端點，呼叫<strong>MapODataRoute</strong>並提供唯一的路由名稱和唯一的 URI 前置詞。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-204">For each endpoint, call <strong>MapODataRoute</strong> and provide a unique route name and a unique URI prefix.</span></span>

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a><span data-ttu-id="3a7b3-205">植入資料庫（選擇性）</span><span class="sxs-lookup"><span data-stu-id="3a7b3-205">Seed the Database (Optional)</span></span>

<span data-ttu-id="3a7b3-206">在此步驟中，您將使用 Entity Framework 來植入具有一些測試資料的資料庫。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-206">In this step, you will use Entity Framework to seed the database with some test data.</span></span> <span data-ttu-id="3a7b3-207">此步驟是選擇性的，但可讓您立即測試您的 OData 端點。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-207">This step is optional, but it lets you test out your OData endpoint right away.</span></span>

<span data-ttu-id="3a7b3-208">從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-208">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="3a7b3-209">在 [套件管理員主控台] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="3a7b3-209">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

<span data-ttu-id="3a7b3-210">這會新增名為「遷移」的資料夾和名為 Configuration.cs 的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-210">This adds a folder named Migrations and a code file named Configuration.cs.</span></span>

![](creating-an-odata-endpoint/_static/image12.png)

<span data-ttu-id="3a7b3-211">開啟此檔案，並將下列程式碼新增至 `Configuration.Seed` 方法。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-211">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

<span data-ttu-id="3a7b3-212">在 [套件管理員主控台] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="3a7b3-212">In the Package Manager Console Window, enter the following commands:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

<span data-ttu-id="3a7b3-213">這些命令會產生建立資料庫的程式碼，然後執行該程式碼。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-213">These commands generate code that creates the database, and then executes that code.</span></span>

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a><span data-ttu-id="3a7b3-214">探索 OData 端點</span><span class="sxs-lookup"><span data-stu-id="3a7b3-214">Exploring the OData Endpoint</span></span>

<span data-ttu-id="3a7b3-215">在本節中，我們將使用[Fiddler Web 調試的 Proxy](http://www.fiddler2.com) ，將要求傳送至端點，並檢查回應訊息。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-215">In this section, we'll use the [Fiddler Web Debugging Proxy](http://www.fiddler2.com) to send requests to the endpoint and examine the response messages.</span></span> <span data-ttu-id="3a7b3-216">這可協助您瞭解 OData 端點的功能。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-216">This will help you to understand the capabilities of an OData endpoint.</span></span>

<span data-ttu-id="3a7b3-217">在 Visual Studio 中，按 F5 開始進行調試。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-217">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="3a7b3-218">根據預設，Visual Studio 會開啟您的瀏覽器以 `http://localhost:*port*`，其中*port*是在專案設定中設定的埠號碼。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-218">By default, Visual Studio opens your browser to `http://localhost:*port*`, where *port* is the port number configured in the project settings.</span></span>

<span data-ttu-id="3a7b3-219">您可以在專案設定中變更埠號碼。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-219">You can change the port number in the project settings.</span></span> <span data-ttu-id="3a7b3-220">在方案總管中，以滑鼠右鍵按一下專案，然後選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-220">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="3a7b3-221">在 [屬性] 視窗中，選取 [ **Web**]。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-221">In the properties window, select **Web**.</span></span> <span data-ttu-id="3a7b3-222">在 [**專案 Url**] 底下輸入埠號碼。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-222">Enter the port number under **Project Url**.</span></span>

### <a name="service-document"></a><span data-ttu-id="3a7b3-223">服務檔</span><span class="sxs-lookup"><span data-stu-id="3a7b3-223">Service Document</span></span>

<span data-ttu-id="3a7b3-224">*服務檔*包含 OData 端點的實體集清單。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-224">The *service document* contains a list of the entity sets for the OData endpoint.</span></span> <span data-ttu-id="3a7b3-225">若要取得服務檔，請將 GET 要求傳送至服務的根 URI。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-225">To get the service document, send a GET request to the root URI of the service.</span></span>

<span data-ttu-id="3a7b3-226">使用 Fiddler，在 [**編輯器**] 索引標籤中輸入下列 URI： [`http://localhost:port/odata/`]，其中*port*是埠號碼。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-226">Using Fiddler, enter the following URI in the **Composer** tab: `http://localhost:port/odata/`, where *port* is the port number.</span></span>

![](creating-an-odata-endpoint/_static/image13.png)

<span data-ttu-id="3a7b3-227">按一下 [**執行**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-227">Click the **Execute** button.</span></span> <span data-ttu-id="3a7b3-228">Fiddler 會將 HTTP GET 要求傳送至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-228">Fiddler sends an HTTP GET request to your application.</span></span> <span data-ttu-id="3a7b3-229">您應該會在 [Web 會話] 清單中看到回應。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-229">You should see the response in the Web Sessions list.</span></span> <span data-ttu-id="3a7b3-230">如果所有專案都正常運作，狀態碼將會是200。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-230">If everything is working, the status code will be 200.</span></span>

![](creating-an-odata-endpoint/_static/image14.png)

<span data-ttu-id="3a7b3-231">在 [Web 會話] 清單中按兩下回應，以在 [偵測器] 索引標籤中查看回應訊息的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-231">Double-click the response in the Web Sessions list to see the details of the response message in the Inspectors tab.</span></span>

![](creating-an-odata-endpoint/_static/image15.png)

<span data-ttu-id="3a7b3-232">原始 HTTP 回應訊息看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="3a7b3-232">The raw HTTP response message should look similar to the following:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

<span data-ttu-id="3a7b3-233">根據預設，Web API 會以 AtomPub 格式傳回服務檔。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-233">By default, Web API returns the service document in AtomPub format.</span></span> <span data-ttu-id="3a7b3-234">若要要求 JSON，請將下列標頭新增至 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="3a7b3-234">To request JSON, add the following header to the HTTP request:</span></span>

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

<span data-ttu-id="3a7b3-235">現在 HTTP 回應包含 JSON 承載：</span><span class="sxs-lookup"><span data-stu-id="3a7b3-235">Now the HTTP response contains a JSON payload:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a><span data-ttu-id="3a7b3-236">服務元資料檔案</span><span class="sxs-lookup"><span data-stu-id="3a7b3-236">Service Metadata Document</span></span>

<span data-ttu-id="3a7b3-237">*服務元資料檔案*會使用稱為概念結構定義語言（CSDL）的 XML 語言來描述服務的資料模型。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-237">The *service metadata document* describes the data model of the service, using an XML language called the Conceptual Schema Definition Language (CSDL).</span></span> <span data-ttu-id="3a7b3-238">元資料檔案會顯示服務中的資料結構，而且可用來產生用戶端程式代碼。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-238">The metadata document shows the structure of the data in the service, and can be used to generate client code.</span></span>

<span data-ttu-id="3a7b3-239">若要取得元資料檔案，請將 GET 要求傳送至 `http://localhost:port/odata/$metadata`。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-239">To get the metadata document, send a GET request to `http://localhost:port/odata/$metadata`.</span></span> <span data-ttu-id="3a7b3-240">以下是本教學課程中所顯示之端點的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-240">Here is the metadata for the endpoint shown in this tutorial.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a><span data-ttu-id="3a7b3-241">實體集</span><span class="sxs-lookup"><span data-stu-id="3a7b3-241">Entity Set</span></span>

<span data-ttu-id="3a7b3-242">若要取得 Products 實體集，請將 GET 要求傳送至 `http://localhost:port/odata/Products`。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-242">To get the Products entity set, send a GET request to `http://localhost:port/odata/Products`.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a><span data-ttu-id="3a7b3-243">實體</span><span class="sxs-lookup"><span data-stu-id="3a7b3-243">Entity</span></span>

<span data-ttu-id="3a7b3-244">若要取得個別產品，請將 GET 要求傳送至 `http://localhost:port/odata/Products(1)`，其中 "1" 是產品識別碼。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-244">To get an individual product, send a GET request to `http://localhost:port/odata/Products(1)`, where "1" is the product ID.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a><span data-ttu-id="3a7b3-245">OData 序列化格式</span><span class="sxs-lookup"><span data-stu-id="3a7b3-245">OData Serialization Formats</span></span>

<span data-ttu-id="3a7b3-246">OData 支援數種序列化格式：</span><span class="sxs-lookup"><span data-stu-id="3a7b3-246">OData supports several serialization formats:</span></span>

- <span data-ttu-id="3a7b3-247">Atom Pub （XML）</span><span class="sxs-lookup"><span data-stu-id="3a7b3-247">Atom Pub (XML)</span></span>
- <span data-ttu-id="3a7b3-248">JSON 「light」（在 OData v3 中引進）</span><span class="sxs-lookup"><span data-stu-id="3a7b3-248">JSON "light" (introduced in OData v3)</span></span>
- <span data-ttu-id="3a7b3-249">JSON 「詳細資訊」（OData v2）</span><span class="sxs-lookup"><span data-stu-id="3a7b3-249">JSON "verbose" (OData v2)</span></span>

<span data-ttu-id="3a7b3-250">根據預設，Web API 會使用 AtomPubJSON "light" 格式。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-250">By default, Web API uses AtomPubJSON "light" format.</span></span>

<span data-ttu-id="3a7b3-251">若要取得 AtomPub 格式，請將 Accept 標頭設為 "application/atom + xml"。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-251">To get AtomPub format, set the Accept header to "application/atom+xml".</span></span> <span data-ttu-id="3a7b3-252">以下是範例回應主體：</span><span class="sxs-lookup"><span data-stu-id="3a7b3-252">Here is an example response body:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

<span data-ttu-id="3a7b3-253">您可以看到 Atom 格式的一個明顯缺點：比 JSON 光線更多的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-253">You can see one obvious disadvantage of the Atom format: It's a lot more verbose than the JSON light.</span></span> <span data-ttu-id="3a7b3-254">不過，如果您有了解 AtomPub 的用戶端，用戶端可能會偏好該格式超過 JSON。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-254">However, if you have a client that understands AtomPub, the client might prefer that format over JSON.</span></span>

<span data-ttu-id="3a7b3-255">以下是相同實體的 JSON light 版本：</span><span class="sxs-lookup"><span data-stu-id="3a7b3-255">Here is the JSON light version of the same entity:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

<span data-ttu-id="3a7b3-256">JSON light 格式是在 OData 通訊協定的第3版中引進。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-256">The JSON light format was introduced in version 3 of the OData protocol.</span></span> <span data-ttu-id="3a7b3-257">為了回溯相容性，用戶端可以要求較舊的「詳細資訊」 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-257">For backward compatibility, a client can request the older "verbose" JSON format.</span></span> <span data-ttu-id="3a7b3-258">若要要求詳細資訊 JSON，請將 Accept 標頭設為 `application/json;odata=verbose`。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-258">To request verbose JSON, set the Accept header to `application/json;odata=verbose`.</span></span> <span data-ttu-id="3a7b3-259">詳細資訊版本如下：</span><span class="sxs-lookup"><span data-stu-id="3a7b3-259">Here is the verbose version:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

<span data-ttu-id="3a7b3-260">此格式會在回應本文中傳達更多的中繼資料，這可能會在整個會話上增加相當大的負擔。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-260">This format conveys more metadata in the response body, which can add considerable overhead over an entire session.</span></span> <span data-ttu-id="3a7b3-261">此外，它也會將物件包裝在名為 "d" 的屬性中，藉此加入間接取值層級。</span><span class="sxs-lookup"><span data-stu-id="3a7b3-261">Also, it adds a level of indirection by wrapping the object in a property named "d".</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a7b3-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3a7b3-262">Next Steps</span></span>

- [<span data-ttu-id="3a7b3-263">新增實體關聯</span><span class="sxs-lookup"><span data-stu-id="3a7b3-263">Add Entity Relations</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="3a7b3-264">新增 OData 動作</span><span class="sxs-lookup"><span data-stu-id="3a7b3-264">Add OData Actions</span></span>](odata-actions.md)
- [<span data-ttu-id="3a7b3-265">從 .NET 用戶端呼叫 OData 服務</span><span class="sxs-lookup"><span data-stu-id="3a7b3-265">Call the OData Service From a .NET Client</span></span>](calling-an-odata-service-from-a-net-client.md)
