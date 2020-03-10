---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: 使用 ASP.NET Web API 2.2 建立 OData v4 端點 |Microsoft Docs
author: MikeWasson
description: 開放式資料通訊協定（OData）是 web 的資料存取通訊協定。 OData 透過 CRUD 作業提供統一的方式來查詢和運算元據集 。
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 81d134cbd3231b9a0d5537ccbd1bbfe6419254af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598732"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a><span data-ttu-id="93cb9-104">使用 ASP.NET Web API 建立 OData v4 端點</span><span class="sxs-lookup"><span data-stu-id="93cb9-104">Create an OData v4 Endpoint Using ASP.NET Web API</span></span> 

> <span data-ttu-id="93cb9-105">開放式資料通訊協定（OData）是 web 的資料存取通訊協定。</span><span class="sxs-lookup"><span data-stu-id="93cb9-105">The Open Data Protocol (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="93cb9-106">OData 透過 CRUD 作業（建立、讀取、更新和刪除）提供統一的方式來查詢和運算元據集。</span><span class="sxs-lookup"><span data-stu-id="93cb9-106">OData provides a uniform way to query and manipulate data sets through CRUD operations (create, read, update, and delete).</span></span>
>
> <span data-ttu-id="93cb9-107">ASP.NET Web API 支援通訊協定的 v3 和 v4。</span><span class="sxs-lookup"><span data-stu-id="93cb9-107">ASP.NET Web API supports both v3 and v4 of the protocol.</span></span> <span data-ttu-id="93cb9-108">您甚至可以有一個與 v3 端點並存執行的 v4 端點。</span><span class="sxs-lookup"><span data-stu-id="93cb9-108">You can even have a v4 endpoint that runs side-by-side with a v3 endpoint.</span></span>
>
> <span data-ttu-id="93cb9-109">本教學課程說明如何建立支援 CRUD 作業的 OData v4 端點。</span><span class="sxs-lookup"><span data-stu-id="93cb9-109">This tutorial shows how to create an OData v4 endpoint that supports CRUD operations.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="93cb9-110">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="93cb9-110">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="93cb9-111">Web API 5。2</span><span class="sxs-lookup"><span data-stu-id="93cb9-111">Web API 5.2</span></span>
> - <span data-ttu-id="93cb9-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="93cb9-112">OData v4</span></span>
> - <span data-ttu-id="93cb9-113">Visual Studio 2017 （請[在這裡](https://visualstudio.microsoft.com/downloads/)下載 Visual Studio 2017）</span><span class="sxs-lookup"><span data-stu-id="93cb9-113">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/))</span></span>
> - <span data-ttu-id="93cb9-114">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="93cb9-114">Entity Framework 6</span></span>
> - <span data-ttu-id="93cb9-115">.NET 4.7。2</span><span class="sxs-lookup"><span data-stu-id="93cb9-115">.NET 4.7.2</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="93cb9-116">教學課程版本</span><span class="sxs-lookup"><span data-stu-id="93cb9-116">Tutorial versions</span></span>
>
> <span data-ttu-id="93cb9-117">針對 OData 第3版，請參閱[建立 odata V3 端點](../odata-v3/creating-an-odata-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="93cb9-117">For the OData Version 3, see [Creating an OData v3 Endpoint](../odata-v3/creating-an-odata-endpoint.md).</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="93cb9-118">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="93cb9-118">Create the Visual Studio Project</span></span>

<span data-ttu-id="93cb9-119">在 Visual Studio 中，從 **[檔案**] 功能表選取 [**新增**&gt;**專案**]。</span><span class="sxs-lookup"><span data-stu-id="93cb9-119">In Visual Studio, from the **File** menu, select **New** &gt; **Project**.</span></span>

<span data-ttu-id="93cb9-120">展開 **已安裝** &gt; **Visual C#**  &gt; **web**，然後選取  **ASP.NET Web 應用程式（.NET Framework）**  範本。</span><span class="sxs-lookup"><span data-stu-id="93cb9-120">Expand **Installed** &gt; **Visual C#** &gt; **Web**, and select the **ASP.NET Web Application (.NET Framework)** template.</span></span> <span data-ttu-id="93cb9-121">將專案命名為 &quot;ProductService&quot;。</span><span class="sxs-lookup"><span data-stu-id="93cb9-121">Name the project &quot;ProductService&quot;.</span></span>

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

<span data-ttu-id="93cb9-122">選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="93cb9-122">Select **OK**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

<span data-ttu-id="93cb9-123">選取 [空白] 範本。</span><span class="sxs-lookup"><span data-stu-id="93cb9-123">Select the **Empty** template.</span></span> <span data-ttu-id="93cb9-124">在 [**新增資料夾和核心參考：** ] 底下，選取 [ **Web API**]。</span><span class="sxs-lookup"><span data-stu-id="93cb9-124">Under **Add folders and core references for:**, select **Web API**.</span></span> <span data-ttu-id="93cb9-125">選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="93cb9-125">Select **OK**.</span></span>

## <a name="install-the-odata-packages"></a><span data-ttu-id="93cb9-126">安裝 OData 封裝</span><span class="sxs-lookup"><span data-stu-id="93cb9-126">Install the OData packages</span></span>

<span data-ttu-id="93cb9-127">從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**] &gt; [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="93cb9-127">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="93cb9-128">在 [套件管理員主控台] 視窗中，輸入：</span><span class="sxs-lookup"><span data-stu-id="93cb9-128">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

<span data-ttu-id="93cb9-129">此命令會安裝最新的 OData NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="93cb9-129">This command installs the latest OData NuGet packages.</span></span>

## <a name="add-a-model-class"></a><span data-ttu-id="93cb9-130">新增模型類別</span><span class="sxs-lookup"><span data-stu-id="93cb9-130">Add a model class</span></span>

<span data-ttu-id="93cb9-131">「*模型*」是代表您應用程式中資料實體的物件。</span><span class="sxs-lookup"><span data-stu-id="93cb9-131">A *model* is an object that represents a data entity in your application.</span></span>

<span data-ttu-id="93cb9-132">在 [方案總管] 中，於 Models 資料夾上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="93cb9-132">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="93cb9-133">從內容功能表中，選取 [**新增**&gt;**類別**]。</span><span class="sxs-lookup"><span data-stu-id="93cb9-133">From the context menu, select **Add** &gt; **Class**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="93cb9-134">依照慣例，模型類別會放在 [模型] 資料夾中，但您不需要在自己的專案中遵循此慣例。</span><span class="sxs-lookup"><span data-stu-id="93cb9-134">By convention, model classes are placed in the Models folder, but you don't have to follow this convention in your own projects.</span></span>

<span data-ttu-id="93cb9-135">將類別命名為 `Product`。</span><span class="sxs-lookup"><span data-stu-id="93cb9-135">Name the class `Product`.</span></span> <span data-ttu-id="93cb9-136">在 Product.cs 檔案中，將重複使用的程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="93cb9-136">In the Product.cs file, replace the boilerplate code with the following:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

<span data-ttu-id="93cb9-137">`Id` 屬性是實體索引鍵。</span><span class="sxs-lookup"><span data-stu-id="93cb9-137">The `Id` property is the entity key.</span></span> <span data-ttu-id="93cb9-138">用戶端可以依索引鍵查詢實體。</span><span class="sxs-lookup"><span data-stu-id="93cb9-138">Clients can query entities by key.</span></span> <span data-ttu-id="93cb9-139">例如，若要取得識別碼為5的產品，則 URI 為 `/Products(5)`。</span><span class="sxs-lookup"><span data-stu-id="93cb9-139">For example, to get the product with ID of 5, the URI is `/Products(5)`.</span></span> <span data-ttu-id="93cb9-140">`Id` 屬性也會是後端資料庫中的主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="93cb9-140">The `Id` property will also be the primary key in the back-end database.</span></span>

## <a name="enable-entity-framework"></a><span data-ttu-id="93cb9-141">啟用 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="93cb9-141">Enable Entity Framework</span></span>

<span data-ttu-id="93cb9-142">在本教學課程中，我們將使用 Entity Framework （EF） Code First 來建立後端資料庫。</span><span class="sxs-lookup"><span data-stu-id="93cb9-142">For this tutorial, we'll use Entity Framework (EF) Code First to create the back-end database.</span></span>

> [!NOTE]
> <span data-ttu-id="93cb9-143">Web API OData 不需要 EF。</span><span class="sxs-lookup"><span data-stu-id="93cb9-143">Web API OData does not require EF.</span></span> <span data-ttu-id="93cb9-144">使用可將資料庫實體轉譯成模型的任何資料存取層。</span><span class="sxs-lookup"><span data-stu-id="93cb9-144">Use any data-access layer that can translate database entities into models.</span></span>

<span data-ttu-id="93cb9-145">首先，安裝 EF 的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="93cb9-145">First, install the NuGet package for EF.</span></span> <span data-ttu-id="93cb9-146">從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**] &gt; [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="93cb9-146">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="93cb9-147">在 [套件管理員主控台] 視窗中，輸入：</span><span class="sxs-lookup"><span data-stu-id="93cb9-147">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

<span data-ttu-id="93cb9-148">開啟 web.config 檔案，並在**configSections**元素後面的**configuration**元素內新增下列區段。</span><span class="sxs-lookup"><span data-stu-id="93cb9-148">Open the Web.config file, and add the following section inside the **configuration** element, after the **configSections** element.</span></span>

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

<span data-ttu-id="93cb9-149">此設定會加入 LocalDB 資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="93cb9-149">This setting adds a connection string for a LocalDB database.</span></span> <span data-ttu-id="93cb9-150">當您在本機執行應用程式時，將會使用此資料庫。</span><span class="sxs-lookup"><span data-stu-id="93cb9-150">This database will be used when you run the app locally.</span></span>

<span data-ttu-id="93cb9-151">接下來，將名為 `ProductsContext` 的類別新增至 [模型] 資料夾：</span><span class="sxs-lookup"><span data-stu-id="93cb9-151">Next, add a class named `ProductsContext` to the Models folder:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

<span data-ttu-id="93cb9-152">在此函數中，`"name=ProductsContext"` 會提供連接字串的名稱。</span><span class="sxs-lookup"><span data-stu-id="93cb9-152">In the constructor, `"name=ProductsContext"` gives the name of the connection string.</span></span>

## <a name="configure-the-odata-endpoint"></a><span data-ttu-id="93cb9-153">設定 OData 端點</span><span class="sxs-lookup"><span data-stu-id="93cb9-153">Configure the OData endpoint</span></span>

<span data-ttu-id="93cb9-154">開啟檔案應用程式\_Start/WebApiConfig. cs。</span><span class="sxs-lookup"><span data-stu-id="93cb9-154">Open the file App\_Start/WebApiConfig.cs.</span></span> <span data-ttu-id="93cb9-155">新增下列**using**語句：</span><span class="sxs-lookup"><span data-stu-id="93cb9-155">Add the following **using** statements:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

<span data-ttu-id="93cb9-156">然後將下列程式碼新增至**Register**方法：</span><span class="sxs-lookup"><span data-stu-id="93cb9-156">Then add the following code to the **Register** method:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

<span data-ttu-id="93cb9-157">這段程式碼會執行兩項工作：</span><span class="sxs-lookup"><span data-stu-id="93cb9-157">This code does two things:</span></span>

- <span data-ttu-id="93cb9-158">建立實體資料模型（EDM）。</span><span class="sxs-lookup"><span data-stu-id="93cb9-158">Creates an Entity Data Model (EDM).</span></span>
- <span data-ttu-id="93cb9-159">新增路由。</span><span class="sxs-lookup"><span data-stu-id="93cb9-159">Adds a route.</span></span>

<span data-ttu-id="93cb9-160">EDM 是資料的抽象模型。</span><span class="sxs-lookup"><span data-stu-id="93cb9-160">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="93cb9-161">EDM 是用來建立服務元資料檔案。</span><span class="sxs-lookup"><span data-stu-id="93cb9-161">The EDM is used to create the service metadata document.</span></span> <span data-ttu-id="93cb9-162">**ODataConventionModelBuilder**類別會使用預設命名慣例來建立 EDM。</span><span class="sxs-lookup"><span data-stu-id="93cb9-162">The **ODataConventionModelBuilder** class creates an EDM by using default naming conventions.</span></span> <span data-ttu-id="93cb9-163">這種方法需要最少的程式碼。</span><span class="sxs-lookup"><span data-stu-id="93cb9-163">This approach requires the least code.</span></span> <span data-ttu-id="93cb9-164">如果您想要更充分掌控 EDM，您可以使用**用**類別來明確地新增屬性、索引鍵和導覽屬性來建立 edm。</span><span class="sxs-lookup"><span data-stu-id="93cb9-164">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="93cb9-165">*路由*會告知 Web API 如何將 HTTP 要求路由傳送至端點。</span><span class="sxs-lookup"><span data-stu-id="93cb9-165">A *route* tells Web API how to route HTTP requests to the endpoint.</span></span> <span data-ttu-id="93cb9-166">若要建立 OData v4 路由，請呼叫**MapODataServiceRoute**擴充方法。</span><span class="sxs-lookup"><span data-stu-id="93cb9-166">To create an OData v4 route, call the **MapODataServiceRoute** extension method.</span></span>

<span data-ttu-id="93cb9-167">如果您的應用程式有多個 OData 端點，請為每個端點建立個別的路由。</span><span class="sxs-lookup"><span data-stu-id="93cb9-167">If your application has multiple OData endpoints, create a separate route for each.</span></span> <span data-ttu-id="93cb9-168">為每個路由提供唯一的路由名稱和前置詞。</span><span class="sxs-lookup"><span data-stu-id="93cb9-168">Give each route a unique route name and prefix.</span></span>

## <a name="add-the-odata-controller"></a><span data-ttu-id="93cb9-169">新增 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="93cb9-169">Add the OData controller</span></span>

<span data-ttu-id="93cb9-170">*控制器*是處理 HTTP 要求的類別。</span><span class="sxs-lookup"><span data-stu-id="93cb9-170">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="93cb9-171">您會針對 OData 服務中的每個實體集建立個別的控制器。</span><span class="sxs-lookup"><span data-stu-id="93cb9-171">You create a separate controller for each entity set in your OData service.</span></span> <span data-ttu-id="93cb9-172">在本教學課程中，您將為 `Product` 實體建立一個控制器。</span><span class="sxs-lookup"><span data-stu-id="93cb9-172">In this tutorial, you will create one controller, for the `Product` entity.</span></span>

<span data-ttu-id="93cb9-173">在方案總管中，以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [**新增**&gt;**類別**]。</span><span class="sxs-lookup"><span data-stu-id="93cb9-173">In Solution Explorer, right-click the Controllers folder and select **Add** &gt; **Class**.</span></span> <span data-ttu-id="93cb9-174">將類別命名為 `ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="93cb9-174">Name the class `ProductsController`.</span></span>

> [!NOTE]
> <span data-ttu-id="93cb9-175">此 OData v3 教學課程的版本會使用「**新增控制器**」架構。</span><span class="sxs-lookup"><span data-stu-id="93cb9-175">The version of this tutorial for OData v3 uses the **Add Controller** scaffolding.</span></span> <span data-ttu-id="93cb9-176">目前沒有 OData v4 的樣板。</span><span class="sxs-lookup"><span data-stu-id="93cb9-176">Currently, there is no scaffolding for OData v4.</span></span>

<span data-ttu-id="93cb9-177">將 ProductsController.cs 中的重複使用程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="93cb9-177">Replace the boilerplate code in ProductsController.cs with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

<span data-ttu-id="93cb9-178">控制器會使用 `ProductsContext` 類別，以使用 EF 來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="93cb9-178">The controller uses the `ProductsContext` class to access the database using EF.</span></span> <span data-ttu-id="93cb9-179">請注意，控制器會覆寫**dispose**方法來處置**ProductsCoNtext**。</span><span class="sxs-lookup"><span data-stu-id="93cb9-179">Notice that the controller overrides the **Dispose** method to dispose of the **ProductsContext**.</span></span>

<span data-ttu-id="93cb9-180">這是控制器的起點。</span><span class="sxs-lookup"><span data-stu-id="93cb9-180">This is the starting point for the controller.</span></span> <span data-ttu-id="93cb9-181">接下來，我們將新增所有 CRUD 作業的方法。</span><span class="sxs-lookup"><span data-stu-id="93cb9-181">Next, we'll add methods for all of the CRUD operations.</span></span>

## <a name="query-the-entity-set"></a><span data-ttu-id="93cb9-182">查詢實體集</span><span class="sxs-lookup"><span data-stu-id="93cb9-182">Query the entity set</span></span>

<span data-ttu-id="93cb9-183">將下列方法新增至 `ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="93cb9-183">Add the following methods to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

<span data-ttu-id="93cb9-184">`Get` 方法的無參數版本會傳回整個產品集合。</span><span class="sxs-lookup"><span data-stu-id="93cb9-184">The parameterless version of the `Get` method returns the entire Products collection.</span></span> <span data-ttu-id="93cb9-185">具有索引*鍵*參數的 `Get` 方法會依其索引鍵（在此案例中為 `Id` 屬性）查閱產品。</span><span class="sxs-lookup"><span data-stu-id="93cb9-185">The `Get` method with a *key* parameter looks up a product by its key (in this case, the `Id` property).</span></span>

<span data-ttu-id="93cb9-186">**[EnableQuery]** 屬性可讓用戶端使用查詢選項（例如 $filter、$sort 和 $page）來修改查詢。</span><span class="sxs-lookup"><span data-stu-id="93cb9-186">The **[EnableQuery]** attribute enables clients to modify the query, by using query options such as $filter, $sort, and $page.</span></span> <span data-ttu-id="93cb9-187">如需詳細資訊，請參閱[支援 OData 查詢選項](../supporting-odata-query-options.md)。</span><span class="sxs-lookup"><span data-stu-id="93cb9-187">For more information, see [Supporting OData Query Options](../supporting-odata-query-options.md).</span></span>

## <a name="add-an-entity-to-the-entity-set"></a><span data-ttu-id="93cb9-188">將實體新增至實體集</span><span class="sxs-lookup"><span data-stu-id="93cb9-188">Add an entity to the entity set</span></span>

<span data-ttu-id="93cb9-189">若要讓用戶端將新產品新增至資料庫，請將下列方法新增至 `ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="93cb9-189">To enable clients to add a new product to the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a><span data-ttu-id="93cb9-190">更新實體</span><span class="sxs-lookup"><span data-stu-id="93cb9-190">Update an entity</span></span>

<span data-ttu-id="93cb9-191">OData 支援兩種不同的語義來更新實體、PATCH 和 PUT。</span><span class="sxs-lookup"><span data-stu-id="93cb9-191">OData supports two different semantics for updating an entity, PATCH and PUT.</span></span>

- <span data-ttu-id="93cb9-192">PATCH 會執行部分更新。</span><span class="sxs-lookup"><span data-stu-id="93cb9-192">PATCH performs a partial update.</span></span> <span data-ttu-id="93cb9-193">用戶端只會指定要更新的屬性。</span><span class="sxs-lookup"><span data-stu-id="93cb9-193">The client specifies just the properties to update.</span></span>
- <span data-ttu-id="93cb9-194">PUT 會取代整個實體。</span><span class="sxs-lookup"><span data-stu-id="93cb9-194">PUT replaces the entire entity.</span></span>

<span data-ttu-id="93cb9-195">PUT 的缺點是用戶端必須傳送實體中所有屬性的值，包括不會變更的值。</span><span class="sxs-lookup"><span data-stu-id="93cb9-195">The disadvantage of PUT is that the client must send values for all of the properties in the entity, including values that are not changing.</span></span> <span data-ttu-id="93cb9-196">[OData 規格](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719)會指出建議的修補程式。</span><span class="sxs-lookup"><span data-stu-id="93cb9-196">The [OData spec](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) states that PATCH is preferred.</span></span>

<span data-ttu-id="93cb9-197">在任何情況下，以下是 PATCH 和 PUT 方法的程式碼：</span><span class="sxs-lookup"><span data-stu-id="93cb9-197">In any case, here is the code for both PATCH and PUT methods:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

<span data-ttu-id="93cb9-198">在修補程式的情況下，控制器會使用**差異&lt;t&gt;** 類型來追蹤變更。</span><span class="sxs-lookup"><span data-stu-id="93cb9-198">In the case of PATCH, the controller uses the **Delta&lt;T&gt;** type to track the changes.</span></span>

## <a name="delete-an-entity"></a><span data-ttu-id="93cb9-199">刪除實體</span><span class="sxs-lookup"><span data-stu-id="93cb9-199">Delete an entity</span></span>

<span data-ttu-id="93cb9-200">若要讓用戶端從資料庫中刪除產品，請將下列方法新增至 `ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="93cb9-200">To enable clients to delete a product from the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
