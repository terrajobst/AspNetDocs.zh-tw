---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 第2部分：資料存取層 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第2部分涵蓋加入資料存取層。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 342d2c54dfba5d052570e890f85dcf9739f9884f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78573245"
---
# <a name="part-2-data-access-layer"></a><span data-ttu-id="8013a-104">第2部分：資料存取層</span><span class="sxs-lookup"><span data-stu-id="8013a-104">Part 2: Data Access Layer</span></span>

<span data-ttu-id="8013a-105">依[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="8013a-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="8013a-106">Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。</span><span class="sxs-lookup"><span data-stu-id="8013a-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="8013a-107">它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。</span><span class="sxs-lookup"><span data-stu-id="8013a-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="8013a-108">本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="8013a-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="8013a-109">第2部分涵蓋加入資料存取層。</span><span class="sxs-lookup"><span data-stu-id="8013a-109">Part 2 covers adding the data access layer.</span></span>

## <a id="_Toc260221668"></a><span data-ttu-id="8013a-110">加入資料存取層</span><span class="sxs-lookup"><span data-stu-id="8013a-110">Adding the Data Access Layer</span></span>

<span data-ttu-id="8013a-111">我們的電子商務應用程式將取決於兩個資料庫。</span><span class="sxs-lookup"><span data-stu-id="8013a-111">Our ecommerce application will depend on two databases.</span></span>

<span data-ttu-id="8013a-112">針對客戶資訊，我們將使用標準 ASP.NET 成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="8013a-112">For customer information we'll use the standard ASP.NET Membership database.</span></span> <span data-ttu-id="8013a-113">針對我們的購物車和產品目錄，我們將會執行 SQL Express 資料庫，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8013a-113">For our shopping cart and product catalog we'll implement a SQL Express database as follows.</span></span>

![](tailspin-spyworks-part-2/_static/image1.jpg)

<span data-ttu-id="8013a-114">在應用程式的應用程式中建立資料庫（Commerce .mdf）\_Data 資料夾中，我們可以使用 .NET Entity Framework 繼續建立我們的資料存取層。</span><span class="sxs-lookup"><span data-stu-id="8013a-114">Having created the database (Commerce.mdf) in the application's App\_Data folder we can proceed to create our Data Access Layer using the .NET Entity Framework.</span></span>

<span data-ttu-id="8013a-115">我們將建立名為「資料\_存取」的資料夾，並以滑鼠右鍵按一下該資料夾，然後選取 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="8013a-115">We'll create a folder named "Data\_Access" and them right click on that folder and select "Add New Item".</span></span>

<span data-ttu-id="8013a-116">在 [已安裝的範本] 專案中，然後選取 [ADO.NET 實體資料模型] 輸入 EDM\_Commerce .edmx 作為名稱，然後按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8013a-116">In the "Installed Templates" item and then select "ADO.NET Entity Data Model" enter EDM\_Commerce.edmx as the name and click the "Add" button.</span></span>

![](tailspin-spyworks-part-2/_static/image2.jpg)

<span data-ttu-id="8013a-117">選擇 [從資料庫產生]。</span><span class="sxs-lookup"><span data-stu-id="8013a-117">Choose "Generate from Database".</span></span>

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

<span data-ttu-id="8013a-118">儲存並建立。</span><span class="sxs-lookup"><span data-stu-id="8013a-118">Save and build.</span></span>

<span data-ttu-id="8013a-119">現在，我們已準備好新增我們的第一個功能– [產品類別] 功能表。</span><span class="sxs-lookup"><span data-stu-id="8013a-119">Now we are ready to add our first feature – a product category menu.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8013a-120">[上一頁](tailspin-spyworks-part-1.md)
> [下一頁](tailspin-spyworks-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="8013a-120">[Previous](tailspin-spyworks-part-1.md)
[Next](tailspin-spyworks-part-3.md)</span></span>
