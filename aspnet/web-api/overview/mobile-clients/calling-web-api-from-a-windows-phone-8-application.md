---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: 從 Windows Phone 8 應用程式呼叫 Web API （C#）-ASP.NET 4。x
author: rmcmurray
description: 教學課程與程式碼：在 ASP.NET 4.x 中建立 ASP.NET Web API 應用程式，以提供 Windows Phone 8 應用程式的書籍目錄。
ms.author: riande
ms.date: 10/09/2013
ms.custom: seoapril2019
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: c5da14a6856f551343b6fb14f0aedc659e792f6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614734"
---
# <a name="calling-web-api-from-a-windows-phone-8-application-c"></a><span data-ttu-id="53136-103">從 Windows Phone 8 應用程式呼叫 Web API (C#)</span><span class="sxs-lookup"><span data-stu-id="53136-103">Calling Web API from a Windows Phone 8 Application (C#)</span></span>

<span data-ttu-id="53136-104">依[Robert McMurray](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="53136-104">by [Robert McMurray](https://github.com/rmcmurray)</span></span>

<span data-ttu-id="53136-105">在本教學課程中，您將瞭解如何建立完整的端對端案例，其中包含 ASP.NET Web API 應用程式，可提供 Windows Phone 8 應用程式的書籍目錄。</span><span class="sxs-lookup"><span data-stu-id="53136-105">In this tutorial, you will learn how to create a complete end-to-end scenario consisting of an ASP.NET Web API application that provides a catalog of books to a Windows Phone 8 application.</span></span>

### <a name="overview"></a><span data-ttu-id="53136-106">概觀</span><span class="sxs-lookup"><span data-stu-id="53136-106">Overview</span></span>

<span data-ttu-id="53136-107">RESTful 服務（例如 ASP.NET Web API）藉由抽象化伺服器端和用戶端應用程式的架構，簡化開發人員的 HTTP 型應用程式建立。</span><span class="sxs-lookup"><span data-stu-id="53136-107">RESTful services like ASP.NET Web API simplify the creation of HTTP-based applications for developers by abstracting the architecture for server-side and client-side applications.</span></span> <span data-ttu-id="53136-108">Web API 開發人員不會建立用於通訊的專屬通訊端型通訊協定，而是只需要針對其應用程式發佈必要的 HTTP 方法（例如： GET、POST、PUT、DELETE），而用戶端應用程式開發人員只需要使用其應用程式所需的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="53136-108">Instead of creating a proprietary socket-based protocol for communication, Web API developers simply need to publish the requisite HTTP methods for their application, (for example: GET, POST, PUT, DELETE), and client application developers only need to consume the HTTP methods that are necessary for their application.</span></span>

<span data-ttu-id="53136-109">在此端對端教學課程中，您將瞭解如何使用 Web API 來建立下列專案：</span><span class="sxs-lookup"><span data-stu-id="53136-109">In this end-to-end tutorial, you will learn how to use Web API to create the following projects:</span></span>

- <span data-ttu-id="53136-110">在[本教學課程的第一個部分](#STEP1)中，您將建立支援所有建立、讀取、更新和刪除（CRUD）作業的 ASP.NET Web API 應用程式，以管理書籍目錄。</span><span class="sxs-lookup"><span data-stu-id="53136-110">In the [first part of this tutorial](#STEP1), you will create an ASP.NET Web API application that supports all of the Create, Read, Update, and Delete (CRUD) operations to manage a book catalog.</span></span> <span data-ttu-id="53136-111">此應用程式將使用 MSDN 的[範例 XML 檔（books.xml）](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="53136-111">This application will use the [Sample XML File (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) from MSDN.</span></span>
- <span data-ttu-id="53136-112">在[本教學課程的第二個部分](#STEP2)中，您將建立互動式 Windows Phone 8 應用程式，以從您的 Web API 應用程式抓取資料。</span><span class="sxs-lookup"><span data-stu-id="53136-112">In the [second part of this tutorial](#STEP2), you will create an interactive Windows Phone 8 application that retrieves the data from your Web API application.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="53136-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="53136-113">Prerequisites</span></span>

- <span data-ttu-id="53136-114">已安裝 Windows Phone 8 SDK 的 Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="53136-114">Visual Studio 2013 with the Windows Phone 8 SDK installed</span></span>
- <span data-ttu-id="53136-115">安裝 Hyper-v 之64位系統上的 Windows 8 或更新版本</span><span class="sxs-lookup"><span data-stu-id="53136-115">Windows 8 or later on a 64-bit system with Hyper-V installed</span></span>
- <span data-ttu-id="53136-116">如需其他需求的清單，請參閱[WINDOWS PHONE SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471)下載頁面上的*系統需求*一節。</span><span class="sxs-lookup"><span data-stu-id="53136-116">For a list of additional requirements, see the *System Requirements* section on the [Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) download page.</span></span>

> [!NOTE]
> <span data-ttu-id="53136-117">如果您要在本機系統上測試 Web API 與 Windows Phone 8 專案之間的連線，您必須遵循將 *[Windows Phone 8 模擬器連線到本機電腦上的 WEB API 應用程式](https://go.microsoft.com/fwlink/?LinkId=324014)* 一文中的指示，以設定您的測試環境。</span><span class="sxs-lookup"><span data-stu-id="53136-117">If you are going to test the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a><span data-ttu-id="53136-118">步驟1：建立 Web API 書店專案</span><span class="sxs-lookup"><span data-stu-id="53136-118">Step 1: Creating the Web API Bookstore Project</span></span>

<span data-ttu-id="53136-119">本端對端教學課程的第一個步驟，是建立支援所有 CRUD 作業的 Web API 專案;請注意，您會在本教學課程的[步驟 2](#STEP2)中，將 Windows Phone 應用程式專案新增至此方案。</span><span class="sxs-lookup"><span data-stu-id="53136-119">The first step of this end-to-end tutorial is to create a Web API project that supports all of the CRUD operations; note that you will add the Windows Phone application project to this solution in [Step 2](#STEP2) of this tutorial.</span></span>

1. <span data-ttu-id="53136-120">開啟**Visual Studio 2013**。</span><span class="sxs-lookup"><span data-stu-id="53136-120">Open **Visual Studio 2013**.</span></span>
2. <span data-ttu-id="53136-121">依**序按一下 [** 檔案]、[**新增**] 和 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="53136-121">Click **File**, then **New**, and then **Project**.</span></span>
3. <span data-ttu-id="53136-122">當 [**新增專案**] 對話方塊顯示時，依序展開 [**已安裝**]、[**範本**]、[**視覺C#效果**] 和 [ **Web**]。</span><span class="sxs-lookup"><span data-stu-id="53136-122">When the **New Project** dialog box is displayed, expand **Installed**, then **Templates**, then **Visual C#**, and then **Web**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="53136-123">按一下影像以展開</span><span class="sxs-lookup"><span data-stu-id="53136-123">Click image to expand</span></span>                                                                |

4. <span data-ttu-id="53136-124">反白顯示**ASP.NET Web 應用程式**，輸入**書店**作為專案名稱，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="53136-124">Highlight **ASP.NET Web Application**, enter **BookStore** for the project name, and then click **OK**.</span></span>
5. <span data-ttu-id="53136-125">當 [**新增 ASP.NET 專案**] 對話方塊顯示時，請選取 [ **Web API** ] 範本，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="53136-125">When the **New ASP.NET Project** dialog box is displayed, select the **Web API** template, and then click **OK**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="53136-126">按一下影像以展開</span><span class="sxs-lookup"><span data-stu-id="53136-126">Click image to expand</span></span>                                                                |

6. <span data-ttu-id="53136-127">當 Web API 專案開啟時，從專案中移除範例控制器：</span><span class="sxs-lookup"><span data-stu-id="53136-127">When the Web API project opens, remove the sample controller from the project:</span></span>

    1. <span data-ttu-id="53136-128">在 [方案瀏覽器] 中展開 [**控制器**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="53136-128">Expand the **Controllers** folder in the solution explorer.</span></span>
    2. <span data-ttu-id="53136-129">以滑鼠右鍵按一下**ValuesController.cs**檔案，然後按一下 [**刪除**]。</span><span class="sxs-lookup"><span data-stu-id="53136-129">Right-click the **ValuesController.cs** file, and then click **Delete**.</span></span>
    3. <span data-ttu-id="53136-130">當系統提示您確認刪除時，請按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="53136-130">Click **OK** when prompted to confirm the deletion.</span></span>
7. <span data-ttu-id="53136-131">將 XML 資料檔案新增至 Web API 專案;此檔案包含書店目錄的內容：</span><span class="sxs-lookup"><span data-stu-id="53136-131">Add an XML data file to the Web API project; this file contains the contents of the bookstore catalog:</span></span>

   1. <span data-ttu-id="53136-132">以滑鼠右鍵按一下 [solution explorer] 中的**應用程式\_[Data** ] 資料夾，然後按一下 [新增]，**再按一下 [** **新專案**]。</span><span class="sxs-lookup"><span data-stu-id="53136-132">Right-click the **App\_Data** folder in the solution explorer, then click **Add**, and then click **New Item**.</span></span>
   2. <span data-ttu-id="53136-133">當 [**加入新專案**] 對話方塊顯示時，請反白顯示**XML**檔案範本。</span><span class="sxs-lookup"><span data-stu-id="53136-133">When the **Add New Item** dialog box is displayed, highlight the **XML File** template.</span></span>
   3. <span data-ttu-id="53136-134">將檔案名命名為**books.xml**，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="53136-134">Name the file **Books.xml**, and then click **Add**.</span></span>
   4. <span data-ttu-id="53136-135">當開啟**books.xml**檔案時，請將檔案中的程式碼取代為 MSDN 上的範例**書籍 .xml**檔案中的 xml：</span><span class="sxs-lookup"><span data-stu-id="53136-135">When the **Books.xml** file is opened, replace the code in the file with the XML from the sample **books.xml** file on MSDN:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. <span data-ttu-id="53136-136">儲存並關閉 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="53136-136">Save and close the XML file.</span></span>

8. <span data-ttu-id="53136-137">將書店模型新增至 Web API 專案;此模型包含適用于書店應用程式的建立、讀取、更新和刪除（CRUD）邏輯：</span><span class="sxs-lookup"><span data-stu-id="53136-137">Add the bookstore model to the Web API project; this model contains the Create, Read, Update, and Delete (CRUD) logic for the bookstore application:</span></span>

   1. <span data-ttu-id="53136-138">以滑鼠右鍵按一下 [方案瀏覽器] 中的 [**模型**] 資料夾，然後按一下 [**新增**]，再按一下 [**類別**]。</span><span class="sxs-lookup"><span data-stu-id="53136-138">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   2. <span data-ttu-id="53136-139">當 [新增**專案**] 對話方塊顯示時，將類別檔案命名為**BookDetails.cs**，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="53136-139">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   3. <span data-ttu-id="53136-140">開啟**BookDetails.cs**檔案時，請將檔案中的程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="53136-140">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. <span data-ttu-id="53136-141">儲存並關閉**BookDetails.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="53136-141">Save and close the **BookDetails.cs** file.</span></span>

9. <span data-ttu-id="53136-142">將書店控制器新增至 Web API 專案：</span><span class="sxs-lookup"><span data-stu-id="53136-142">Add the bookstore controller to the Web API project:</span></span>

   1. <span data-ttu-id="53136-143">以滑鼠右鍵按一下 [solution explorer] 中的 [**控制器**] 資料夾，然後按一下 [**新增**]，再按一下 [**控制器**]。</span><span class="sxs-lookup"><span data-stu-id="53136-143">Right-click the **Controllers** folder in the solution explorer, then click **Add**, and then click **Controller**.</span></span>
   2. <span data-ttu-id="53136-144">顯示 [**新增 Scaffold** ] 對話方塊時，反白顯示 [ **Web API 2 控制器-空白**]，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="53136-144">When the **Add Scaffold** dialog box is displayed, highlight **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
   3. <span data-ttu-id="53136-145">顯示 [**新增控制器**] 對話方塊時，將控制器命名為**BooksController**，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="53136-145">When the **Add Controller** dialog box is displayed, name the controller **BooksController**, and then click **Add**.</span></span>
   4. <span data-ttu-id="53136-146">開啟**BooksController.cs**檔案時，請將檔案中的程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="53136-146">When the **BooksController.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. <span data-ttu-id="53136-147">儲存並關閉**BooksController.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="53136-147">Save and close the **BooksController.cs** file.</span></span>

10. <span data-ttu-id="53136-148">建立 Web API 應用程式來檢查是否有錯誤。</span><span class="sxs-lookup"><span data-stu-id="53136-148">Build the Web API application to check for errors.</span></span>

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a><span data-ttu-id="53136-149">步驟2：新增 Windows Phone 8 書店目錄專案</span><span class="sxs-lookup"><span data-stu-id="53136-149">Step 2: Adding the Windows Phone 8 Bookstore Catalog Project</span></span>

<span data-ttu-id="53136-150">此端對端案例的下一個步驟是建立 Windows Phone 8 的目錄應用程式。</span><span class="sxs-lookup"><span data-stu-id="53136-150">The next step of this end-to-end scenario is to create the catalog application for Windows Phone 8.</span></span> <span data-ttu-id="53136-151">此應用程式會使用預設使用者介面的*Windows Phone 資料*系結應用程式範本，並使用您在本教學課程的[步驟 1](#STEP1)中建立的 Web API 應用程式做為資料來源。</span><span class="sxs-lookup"><span data-stu-id="53136-151">This application will use the *Windows Phone Databound App* template for the default user interface, and it will use the Web API application that you created in [Step 1](#STEP1) of this tutorial as the data source.</span></span>

1. <span data-ttu-id="53136-152">在 [方案瀏覽器] 中，以滑鼠右鍵按一下 [**書店**] 方案，然後依序按一下 [**加入**] 和 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="53136-152">Right-click the **BookStore** solution in the in the solution explorer, then click **Add**, and then **New Project**.</span></span>
2. <span data-ttu-id="53136-153">當 **新增專案** 對話方塊顯示時，依序展開 **已安裝** 和 **視覺效果C#** ，然後**Windows Phone**。</span><span class="sxs-lookup"><span data-stu-id="53136-153">When the **New Project** dialog box is displayed, expand **Installed**, then **Visual C#**, and then **Windows Phone**.</span></span>
3. <span data-ttu-id="53136-154">反白顯示 Windows Phone 的資料系結**應用程式**，輸入**BookCatalog**作為 [名稱]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="53136-154">Highlight **Windows Phone Databound App**, enter **BookCatalog** for the name, and then click **OK**.</span></span>
4. <span data-ttu-id="53136-155">將 Json.NET NuGet 套件新增至**BookCatalog**專案：</span><span class="sxs-lookup"><span data-stu-id="53136-155">Add the Json.NET NuGet package to the **BookCatalog** project:</span></span>

    1. <span data-ttu-id="53136-156">以滑鼠右鍵按一下 [方案瀏覽器] 中**BookCatalog**專案的 [**參考**]，然後按一下 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="53136-156">Right-click **References** for the **BookCatalog** project in the solution explorer, and then click **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="53136-157">顯示 [**管理 NuGet 封裝**] 對話方塊時，展開 [**線上**] 區段，並反白顯示 [ **nuget.org**]。</span><span class="sxs-lookup"><span data-stu-id="53136-157">When the **Manage NuGet Packages** dialog box is displayed, expand the **Online** section, and highlight **nuget.org**.</span></span>
    3. <span data-ttu-id="53136-158">在搜尋欄位中輸入**Json.NET** ，然後按一下 [搜尋] 圖示。</span><span class="sxs-lookup"><span data-stu-id="53136-158">Enter **Json.NET** in the search field and click the search icon.</span></span>
    4. <span data-ttu-id="53136-159">反白顯示搜尋結果中的**Json.NET** ，然後按一下 [**安裝**]。</span><span class="sxs-lookup"><span data-stu-id="53136-159">Highlight **Json.NET** in the search results, and then click **Install**.</span></span>
    5. <span data-ttu-id="53136-160">當安裝完成時，按一下 [**關閉**]。</span><span class="sxs-lookup"><span data-stu-id="53136-160">When the installation has completed, click **Close**.</span></span>
5. <span data-ttu-id="53136-161">將**BookDetails**模型加入至**BookCatalog**專案;這包含書店類別的一般模型：</span><span class="sxs-lookup"><span data-stu-id="53136-161">Add the **BookDetails** model to the **BookCatalog** project; this contains a generic model of the bookstore class:</span></span>

   1. <span data-ttu-id="53136-162">以滑鼠右鍵按一下 [方案瀏覽器] 中的**BookCatalog**專案，然後按一下 [**加入**]，再按一下 [**新增資料夾**]。</span><span class="sxs-lookup"><span data-stu-id="53136-162">Right-click the **BookCatalog** project in the solution explorer, then click **Add**, and then click **New Folder**.</span></span>
   2. <span data-ttu-id="53136-163">將新資料夾命名為**模型**。</span><span class="sxs-lookup"><span data-stu-id="53136-163">Name the new folder **Models**.</span></span>
   3. <span data-ttu-id="53136-164">以滑鼠右鍵按一下 [方案瀏覽器] 中的 [**模型**] 資料夾，然後按一下 [**新增**]，再按一下 [**類別**]。</span><span class="sxs-lookup"><span data-stu-id="53136-164">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   4. <span data-ttu-id="53136-165">當 [新增**專案**] 對話方塊顯示時，將類別檔案命名為**BookDetails.cs**，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="53136-165">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   5. <span data-ttu-id="53136-166">開啟**BookDetails.cs**檔案時，請將檔案中的程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="53136-166">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. <span data-ttu-id="53136-167">儲存並關閉**BookDetails.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="53136-167">Save and close the **BookDetails.cs** file.</span></span>

6. <span data-ttu-id="53136-168">更新**MainViewModel.cs**類別，以包含與書店 Web API 應用程式通訊的功能：</span><span class="sxs-lookup"><span data-stu-id="53136-168">Update the **MainViewModel.cs** class to include the functionality to communicate with the BookStore Web API application:</span></span>

   1. <span data-ttu-id="53136-169">展開 [方案瀏覽器] 中的 [ **viewmodel** ] 資料夾，然後按兩下 [ **MainViewModel.cs** ] 檔案。</span><span class="sxs-lookup"><span data-stu-id="53136-169">Expand the **ViewModels** folder in the solution explorer, and then double-click the **MainViewModel.cs** file.</span></span>
   2. <span data-ttu-id="53136-170">開啟**MainViewModel.cs**檔案時，請將檔案中的程式碼取代為下列程式碼：請注意，您將需要使用 Web API 的實際 URL 來更新 `apiUrl` 常數的值：</span><span class="sxs-lookup"><span data-stu-id="53136-170">When the **MainViewModel.cs** file is opened, replace the code in the file with the following; note that you will need to update the value of the `apiUrl` constant with the actual URL of your Web API:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. <span data-ttu-id="53136-171">儲存並關閉**MainViewModel.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="53136-171">Save and close the **MainViewModel.cs** file.</span></span>

7. <span data-ttu-id="53136-172">更新**MainPage** ，以自訂應用程式名稱：</span><span class="sxs-lookup"><span data-stu-id="53136-172">Update the **MainPage.xaml** file to customize the application name:</span></span>

   1. <span data-ttu-id="53136-173">按兩下 [方案 MainPage] 中的 [ **xaml** ] 檔案。</span><span class="sxs-lookup"><span data-stu-id="53136-173">Double-click the **MainPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="53136-174">當**MainPage 開啟 xaml**檔案時，請找出下列幾行程式碼：</span><span class="sxs-lookup"><span data-stu-id="53136-174">When the **MainPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. <span data-ttu-id="53136-175">以下列內容取代這幾行：</span><span class="sxs-lookup"><span data-stu-id="53136-175">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. <span data-ttu-id="53136-176">儲存並關閉**MainPage. xaml**檔案。</span><span class="sxs-lookup"><span data-stu-id="53136-176">Save and close the **MainPage.xaml** file.</span></span>

8. <span data-ttu-id="53136-177">更新**DetailsPage**檔案，以自訂顯示的專案：</span><span class="sxs-lookup"><span data-stu-id="53136-177">Update the **DetailsPage.xaml** file to customize the displayed items:</span></span>

   1. <span data-ttu-id="53136-178">按兩下 [方案 DetailsPage] 中的 [ **xaml** ] 檔案。</span><span class="sxs-lookup"><span data-stu-id="53136-178">Double-click the **DetailsPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="53136-179">當**DetailsPage 開啟 xaml**檔案時，請找出下列幾行程式碼：</span><span class="sxs-lookup"><span data-stu-id="53136-179">When the **DetailsPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. <span data-ttu-id="53136-180">以下列內容取代這幾行：</span><span class="sxs-lookup"><span data-stu-id="53136-180">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. <span data-ttu-id="53136-181">儲存並關閉**DetailsPage. xaml**檔案。</span><span class="sxs-lookup"><span data-stu-id="53136-181">Save and close the **DetailsPage.xaml** file.</span></span>

9. <span data-ttu-id="53136-182">建立 Windows Phone 應用程式，以檢查是否有錯誤。</span><span class="sxs-lookup"><span data-stu-id="53136-182">Build the Windows Phone application to check for errors.</span></span>

### <a name="step-3-testing-the-end-to-end-solution"></a><span data-ttu-id="53136-183">步驟3：測試端對端解決方案</span><span class="sxs-lookup"><span data-stu-id="53136-183">Step 3: Testing the End-to-End Solution</span></span>

<span data-ttu-id="53136-184">如本教學*課程的必要條件*一節中所述，當您在本機系統上測試 Web API 與 Windows Phone 8 專案之間的連線時，必須遵循將 *[Windows Phone 8 模擬器連線到本機電腦上的 Web API 應用程式](https://go.microsoft.com/fwlink/?LinkId=324014)* 一文中的指示，以設定您的測試環境。</span><span class="sxs-lookup"><span data-stu-id="53136-184">As mentioned in the *Prerequisites* section of this tutorial, when you are testing the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<span data-ttu-id="53136-185">設定測試環境之後，您必須將 Windows Phone 應用程式設為啟始專案。</span><span class="sxs-lookup"><span data-stu-id="53136-185">Once you have the testing environment configured, you will need to set the Windows Phone application as the startup project.</span></span> <span data-ttu-id="53136-186">若要這樣做，請在 [方案瀏覽器] 中反白顯示**BookCatalog**應用程式，然後按一下 [**設定為啟始專案**]：</span><span class="sxs-lookup"><span data-stu-id="53136-186">To do so, highlight the **BookCatalog** application in the solution explorer, and then click **Set as StartUp Project**:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| <span data-ttu-id="53136-187">按一下影像以展開</span><span class="sxs-lookup"><span data-stu-id="53136-187">Click image to expand</span></span> |

<span data-ttu-id="53136-188">當您按下 F5 時，Visual Studio 會同時啟動 Windows Phone 模擬器，這會在從您的 Web API 抓取應用程式資料時，顯示 &quot;請等候&quot; 訊息：</span><span class="sxs-lookup"><span data-stu-id="53136-188">When you press F5, Visual Studio will start both the Windows Phone Emulator, which will display a &quot;Please Wait&quot; message while the application data is retrieved from your Web API:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| <span data-ttu-id="53136-189">按一下影像以展開</span><span class="sxs-lookup"><span data-stu-id="53136-189">Click image to expand</span></span> |

<span data-ttu-id="53136-190">如果所有專案都成功，您應該會看到顯示的類別目錄：</span><span class="sxs-lookup"><span data-stu-id="53136-190">If everything is successful, you should see the catalog displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| <span data-ttu-id="53136-191">按一下影像以展開</span><span class="sxs-lookup"><span data-stu-id="53136-191">Click image to expand</span></span> |

<span data-ttu-id="53136-192">如果您在任何書籍標題上按一下，應用程式將會顯示書籍描述：</span><span class="sxs-lookup"><span data-stu-id="53136-192">If you tap on any book title, the application will display the book description:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| <span data-ttu-id="53136-193">按一下影像以展開</span><span class="sxs-lookup"><span data-stu-id="53136-193">Click image to expand</span></span> |

<span data-ttu-id="53136-194">如果應用程式無法與您的 Web API 通訊，將會顯示錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="53136-194">If the application cannot communicate with your Web API, an error message will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| <span data-ttu-id="53136-195">按一下影像以展開</span><span class="sxs-lookup"><span data-stu-id="53136-195">Click image to expand</span></span> |

<span data-ttu-id="53136-196">如果您按一下錯誤訊息，將會顯示有關錯誤的任何其他詳細資料：</span><span class="sxs-lookup"><span data-stu-id="53136-196">If you tap on the error message, any additional details about the error will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 <span data-ttu-id="53136-197">按一下影像以展開</span><span class="sxs-lookup"><span data-stu-id="53136-197">Click image to expand</span></span>                                                                 |
