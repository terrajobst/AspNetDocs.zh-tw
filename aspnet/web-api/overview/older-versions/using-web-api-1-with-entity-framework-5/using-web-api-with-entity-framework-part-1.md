---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: 第1部分：總覽和建立專案 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: a76a18f2bd95969358452085ef342fdca8a386e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556074"
---
# <a name="part-1-overview-and-creating-the-project"></a><span data-ttu-id="a4a62-102">第1部分：總覽和建立專案</span><span class="sxs-lookup"><span data-stu-id="a4a62-102">Part 1: Overview and Creating the Project</span></span>

<span data-ttu-id="a4a62-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a4a62-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="a4a62-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="a4a62-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

<span data-ttu-id="a4a62-105">Entity Framework 是物件/關聯式對應架構。</span><span class="sxs-lookup"><span data-stu-id="a4a62-105">Entity Framework is an object/relational mapping framework.</span></span> <span data-ttu-id="a4a62-106">它會將程式碼中的網域物件對應至關係資料庫中的實體。</span><span class="sxs-lookup"><span data-stu-id="a4a62-106">It maps the domain objects in your code to entities in a relational database.</span></span> <span data-ttu-id="a4a62-107">在大部分的情況下，您不需要擔心資料庫層，因為 Entity Framework 會為您處理。</span><span class="sxs-lookup"><span data-stu-id="a4a62-107">For the most part, you do not have to worry about the database layer, because Entity Framework takes care of it for you.</span></span> <span data-ttu-id="a4a62-108">您的程式碼會操控物件，而變更會保存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="a4a62-108">Your code manipulates the objects, and changes are persisted to a database.</span></span>

## <a name="about-the-tutorial"></a><span data-ttu-id="a4a62-109">關於教學課程</span><span class="sxs-lookup"><span data-stu-id="a4a62-109">About the Tutorial</span></span>

<span data-ttu-id="a4a62-110">在本教學課程中，您將建立簡單的存放區應用程式。</span><span class="sxs-lookup"><span data-stu-id="a4a62-110">In this tutorial, you will create a simple store application.</span></span> <span data-ttu-id="a4a62-111">應用程式有兩個主要部分。</span><span class="sxs-lookup"><span data-stu-id="a4a62-111">There are two main parts to the application.</span></span> <span data-ttu-id="a4a62-112">一般使用者可以查看產品並建立訂單：</span><span class="sxs-lookup"><span data-stu-id="a4a62-112">Normal users can view products and create orders:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

<span data-ttu-id="a4a62-113">系統管理員可以建立、刪除或編輯產品：</span><span class="sxs-lookup"><span data-stu-id="a4a62-113">Administrators can create, delete, or edit products:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="a4a62-114">您要學習的技術</span><span class="sxs-lookup"><span data-stu-id="a4a62-114">Skills You'll Learn</span></span>

<span data-ttu-id="a4a62-115">以下是您要學習的內容：</span><span class="sxs-lookup"><span data-stu-id="a4a62-115">Here's what you'll learn:</span></span>

- <span data-ttu-id="a4a62-116">如何搭配 ASP.NET Web API 使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="a4a62-116">How to use Entity Framework with ASP.NET Web API.</span></span>
- <span data-ttu-id="a4a62-117">如何使用挖的 .js 建立動態用戶端 UI。</span><span class="sxs-lookup"><span data-stu-id="a4a62-117">How to use knockout.js to create a dynamic client UI.</span></span>
- <span data-ttu-id="a4a62-118">如何使用 Web API 的表單驗證來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="a4a62-118">How to use forms authentication with Web API to authenticate users.</span></span>

<span data-ttu-id="a4a62-119">雖然本教學課程是獨立的，但您可能會想要先閱讀下列教學課程：</span><span class="sxs-lookup"><span data-stu-id="a4a62-119">Although this tutorial is self-contained, you might want to read the following tutorials first:</span></span>

- [<span data-ttu-id="a4a62-120">您的第一個 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="a4a62-120">Your First ASP.NET Web API</span></span>](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [<span data-ttu-id="a4a62-121">建立支援 CRUD 作業的 Web API</span><span class="sxs-lookup"><span data-stu-id="a4a62-121">Creating a Web API that Supports CRUD Operations</span></span>](../creating-a-web-api-that-supports-crud-operations.md)

<span data-ttu-id="a4a62-122">[ASP.NET MVC](../../../../mvc/index.md)的某些知識也很有説明。</span><span class="sxs-lookup"><span data-stu-id="a4a62-122">Some knowledge of [ASP.NET MVC](../../../../mvc/index.md) is also helpful.</span></span>

## <a name="overview"></a><span data-ttu-id="a4a62-123">概觀</span><span class="sxs-lookup"><span data-stu-id="a4a62-123">Overview</span></span>

<span data-ttu-id="a4a62-124">概括而言，以下是應用程式的架構：</span><span class="sxs-lookup"><span data-stu-id="a4a62-124">At a high level, here is the architecture of the application:</span></span>

- <span data-ttu-id="a4a62-125">ASP.NET MVC 會產生用戶端的 HTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="a4a62-125">ASP.NET MVC generates the HTML pages for the client.</span></span>
- <span data-ttu-id="a4a62-126">ASP.NET Web API 會對資料（產品和訂單）公開 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="a4a62-126">ASP.NET Web API exposes CRUD operations on the data (products and orders).</span></span>
- <span data-ttu-id="a4a62-127">Entity Framework 會將C# Web API 所使用的模型轉譯成資料庫實體。</span><span class="sxs-lookup"><span data-stu-id="a4a62-127">Entity Framework translates the C# models used by Web API into database entities.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

<span data-ttu-id="a4a62-128">下圖顯示網域物件在應用程式的各個層級中的呈現方式：資料庫層、物件模型，最後是電傳格式，這是用來透過 HTTP 將資料傳輸至用戶端。</span><span class="sxs-lookup"><span data-stu-id="a4a62-128">The following diagram shows how the domain objects are represented at various layers of the application: The database layer, the object model, and finally the wire format, which is used to transmit data to the client via HTTP.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="a4a62-129">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="a4a62-129">Create the Visual Studio Project</span></span>

<span data-ttu-id="a4a62-130">您可以使用 Visual Web Developer Express 或完整版的 Visual Studio 來建立教學課程專案。</span><span class="sxs-lookup"><span data-stu-id="a4a62-130">You can create the tutorial project using either Visual Web Developer Express or the full version of Visual Studio.</span></span>

<span data-ttu-id="a4a62-131">在 [**開始**] 頁面上，按一下 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="a4a62-131">From the **Start** page, click **New Project**.</span></span>

<span data-ttu-id="a4a62-132">在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。</span><span class="sxs-lookup"><span data-stu-id="a4a62-132">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="a4a62-133">在 **[ C#視覺效果**] 底下，選取 [ **Web**]。</span><span class="sxs-lookup"><span data-stu-id="a4a62-133">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="a4a62-134">在專案範本清單中，選取 [ **ASP.NET MVC 4 Web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="a4a62-134">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="a4a62-135">將專案命名為 "ProductStore"，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="a4a62-135">Name the project "ProductStore" and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

<span data-ttu-id="a4a62-136">在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="a4a62-136">In the **New ASP.NET MVC 4 Project** dialog, select **Internet Application** and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

<span data-ttu-id="a4a62-137">「網際網路應用程式」範本會建立支援表單驗證的 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a4a62-137">The "Internet Application" template creates an ASP.NET MVC application that supports forms authentication.</span></span> <span data-ttu-id="a4a62-138">如果您現在執行應用程式，它已經有一些功能：</span><span class="sxs-lookup"><span data-stu-id="a4a62-138">If you run the application now, it already has some features:</span></span>

- <span data-ttu-id="a4a62-139">新使用者可以按一下右上角的 [註冊] 連結進行註冊。</span><span class="sxs-lookup"><span data-stu-id="a4a62-139">New users can register by clicking the "Register" link in the upper right corner.</span></span>
- <span data-ttu-id="a4a62-140">已註冊的使用者可以按一下 [登入] 連結來進行登入。</span><span class="sxs-lookup"><span data-stu-id="a4a62-140">Registered users can log in by clicking the "Log in" link.</span></span>

<span data-ttu-id="a4a62-141">成員資格資訊會保存在自動建立的資料庫中。</span><span class="sxs-lookup"><span data-stu-id="a4a62-141">Membership information is persisted in a database that gets created automatically.</span></span> <span data-ttu-id="a4a62-142">如需 ASP.NET MVC 中表單驗證的詳細資訊，請參閱[逐步解說：在 ASP.NET mvc 中使用表單驗](https://msdn.microsoft.com/library/ff398049(VS.98).aspx)證。</span><span class="sxs-lookup"><span data-stu-id="a4a62-142">For more information about forms authentication in ASP.NET MVC, see [Walkthrough: Using Forms Authentication in ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span></span>

## <a name="update-the-css-file"></a><span data-ttu-id="a4a62-143">更新 CSS 檔案</span><span class="sxs-lookup"><span data-stu-id="a4a62-143">Update the CSS File</span></span>

<span data-ttu-id="a4a62-144">此步驟是表面的，但它會使頁面呈現起來像先前的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="a4a62-144">This step is cosmetic, but it will make the pages render like the earlier screen shots.</span></span>

<span data-ttu-id="a4a62-145">在方案總管中，展開 [內容] 資料夾，然後開啟名為 [網站 .css] 的檔案。</span><span class="sxs-lookup"><span data-stu-id="a4a62-145">In Solution Explorer, expand the Content folder and open the file named Site.css.</span></span> <span data-ttu-id="a4a62-146">新增下列 CSS 樣式：</span><span class="sxs-lookup"><span data-stu-id="a4a62-146">Add the following CSS styles:</span></span>

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [<span data-ttu-id="a4a62-147">下一個</span><span class="sxs-lookup"><span data-stu-id="a4a62-147">Next</span></span>](using-web-api-with-entity-framework-part-2.md)
