---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: 第6部分： ASP.NET 成員資格 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第6部分新增 ASP.NET 成員資格。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: b0caa89dc9ffb5bb7451fa2d9d346c7db2bf1466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78564180"
---
# <a name="part-6-aspnet-membership"></a><span data-ttu-id="f1b58-104">第6部分： ASP.NET 成員資格</span><span class="sxs-lookup"><span data-stu-id="f1b58-104">Part 6: ASP.NET Membership</span></span>

<span data-ttu-id="f1b58-105">依[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="f1b58-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="f1b58-106">Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。</span><span class="sxs-lookup"><span data-stu-id="f1b58-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="f1b58-107">它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。</span><span class="sxs-lookup"><span data-stu-id="f1b58-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="f1b58-108">本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="f1b58-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="f1b58-109">第6部分新增 ASP.NET 成員資格。</span><span class="sxs-lookup"><span data-stu-id="f1b58-109">Part 6 adds ASP.NET Membership.</span></span>

## <a id="_Toc260221672"></a><span data-ttu-id="f1b58-110">使用 ASP.NET 成員資格</span><span class="sxs-lookup"><span data-stu-id="f1b58-110">Working with ASP.NET Membership</span></span>

![](tailspin-spyworks-part-6/_static/image1.png)

<span data-ttu-id="f1b58-111">按一下 [安全性]</span><span class="sxs-lookup"><span data-stu-id="f1b58-111">Click Security</span></span>

![](tailspin-spyworks-part-6/_static/image1.jpg)

<span data-ttu-id="f1b58-112">請確定我們使用的是表單驗證。</span><span class="sxs-lookup"><span data-stu-id="f1b58-112">Make sure that we are using forms authentication.</span></span>

![](tailspin-spyworks-part-6/_static/image2.jpg)

<span data-ttu-id="f1b58-113">使用 [建立使用者] 連結來建立幾個使用者。</span><span class="sxs-lookup"><span data-stu-id="f1b58-113">Use the "Create User" link to create a couple of users.</span></span>

![](tailspin-spyworks-part-6/_static/image3.jpg)

<span data-ttu-id="f1b58-114">完成時，請參閱 [方案總管] 視窗，並重新整理此視圖。</span><span class="sxs-lookup"><span data-stu-id="f1b58-114">When done, refer to the Solution Explorer window and refresh the view.</span></span>

![](tailspin-spyworks-part-6/_static/image2.png)

<span data-ttu-id="f1b58-115">請注意，ASPNETDB.MDF。MDF 已建立良好。</span><span class="sxs-lookup"><span data-stu-id="f1b58-115">Note that the ASPNETDB.MDF fine has been created.</span></span> <span data-ttu-id="f1b58-116">此檔案包含支援核心 ASP.NET 服務（例如成員資格）的資料表。</span><span class="sxs-lookup"><span data-stu-id="f1b58-116">This file contains the tables to support the core ASP.NET services like membership.</span></span>

<span data-ttu-id="f1b58-117">現在我們可以開始執行結帳程式。</span><span class="sxs-lookup"><span data-stu-id="f1b58-117">Now we can begin implementing the checkout process.</span></span>

<span data-ttu-id="f1b58-118">一開始先建立一個 [CheckOut] 頁面。</span><span class="sxs-lookup"><span data-stu-id="f1b58-118">Begin by creating a CheckOut.aspx page.</span></span>

<span data-ttu-id="f1b58-119">只有登入的使用者才能使用 [CheckOut] 頁面，因此我們會限制登入使用者的存取權，並將未登入的使用者重新導向至登入頁面。</span><span class="sxs-lookup"><span data-stu-id="f1b58-119">The CheckOut.aspx page should only be available to users who are logged in so we will restrict access to logged in users and redirect users who are not logged in to the LogIn page.</span></span>

<span data-ttu-id="f1b58-120">為此，我們會將下列內容新增至 web.config 檔案的 [設定] 區段。</span><span class="sxs-lookup"><span data-stu-id="f1b58-120">To do this we'll add the following to the configuration section of our web.config file.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

<span data-ttu-id="f1b58-121">ASP.NET Web Forms 應用程式的範本會自動將驗證區段新增至我們的 web.config 檔案，並建立預設登入頁面。</span><span class="sxs-lookup"><span data-stu-id="f1b58-121">The template for ASP.NET Web Forms applications automatically added an authentication section to our web.config file and established the default login page.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

<span data-ttu-id="f1b58-122">當使用者登入時，我們必須修改登入 .aspx 程式碼後置檔案，以遷移匿名購物車。</span><span class="sxs-lookup"><span data-stu-id="f1b58-122">We must modify the Login.aspx code behind file to migrate an anonymous shopping cart when the user logs in.</span></span> <span data-ttu-id="f1b58-123">變更頁面\_載入事件，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f1b58-123">Change the Page\_Load event as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

<span data-ttu-id="f1b58-124">然後，新增 "LoggedIn" 事件處理常式（如下所示），將會話名稱設定為新登入的使用者，並藉由呼叫 MyShoppingCart 類別中的 MigrateCart 方法，將購物車中的暫時會話識別碼變更為使用者。</span><span class="sxs-lookup"><span data-stu-id="f1b58-124">Then add a "LoggedIn" event handler like this to set the session name to the newly logged in user and change the temporary session id in the shopping cart to that of the user by calling the MigrateCart method in our MyShoppingCart class.</span></span> <span data-ttu-id="f1b58-125">（實作為 .cs 檔案）</span><span class="sxs-lookup"><span data-stu-id="f1b58-125">(Implemented in the .cs file)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

<span data-ttu-id="f1b58-126">執行 MigrateCart （）方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f1b58-126">Implement the MigrateCart() method like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

<span data-ttu-id="f1b58-127">在 checkout 中，我們將使用 [簽出] 頁面中的 EntityDataSource 和 GridView，與我們在 [購物車] 頁面中所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="f1b58-127">In checkout.aspx we'll use an EntityDataSource and a GridView in our check out page much as we did in our shopping cart page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

<span data-ttu-id="f1b58-128">請注意，GridView 控制項會指定名為 MyList\_RowDataBound 的 "ondatabound" 事件處理常式，讓我們來執行此事件處理常式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f1b58-128">Note that our GridView control specifies an "ondatabound" event handler named MyList\_RowDataBound so let's implement that event handler like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

<span data-ttu-id="f1b58-129">此方法會在每個資料列被系結時，保留購物車的執行總計，並更新 GridView 的底部資料列。</span><span class="sxs-lookup"><span data-stu-id="f1b58-129">This method keeps a running total of the shopping cart as each row is bound and updates the bottom row of the GridView.</span></span>

<span data-ttu-id="f1b58-130">在這個階段，我們已針對要放置的訂單，執行「評論」簡報。</span><span class="sxs-lookup"><span data-stu-id="f1b58-130">At this stage we have implemented a "review" presentation of the order to be placed.</span></span>

<span data-ttu-id="f1b58-131">讓我們藉由將幾行程式碼新增至頁面\_載入事件來處理空的購物車案例：</span><span class="sxs-lookup"><span data-stu-id="f1b58-131">Let's handle an empty cart scenario by adding a few lines of code to our Page\_Load event:</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

<span data-ttu-id="f1b58-132">當使用者按一下 [Submit （提交）] 按鈕時，我們會在 [提交] 按鈕的 Click 事件處理常式中執行下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="f1b58-132">When the user clicks on the "Submit" button we will execute the following code in the Submit Button Click Event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

<span data-ttu-id="f1b58-133">訂單提交程式的「肉」是在我們的 MyShoppingCart 類別的 SubmitOrder （）方法中執行。</span><span class="sxs-lookup"><span data-stu-id="f1b58-133">The "meat" of the order submission process is to be implemented in the SubmitOrder() method of our MyShoppingCart class.</span></span>

<span data-ttu-id="f1b58-134">SubmitOrder 將會：</span><span class="sxs-lookup"><span data-stu-id="f1b58-134">SubmitOrder will:</span></span>

- <span data-ttu-id="f1b58-135">接受購物車中的所有明細專案，並使用它們來建立新的訂單記錄和相關聯的 OrderDetails 記錄。</span><span class="sxs-lookup"><span data-stu-id="f1b58-135">Take all the line items in the shopping cart and use them to create a new Order Record and the associated OrderDetails records.</span></span>
- <span data-ttu-id="f1b58-136">計算出貨日期。</span><span class="sxs-lookup"><span data-stu-id="f1b58-136">Calculate Shipping Date.</span></span>
- <span data-ttu-id="f1b58-137">清除 [購物車]。</span><span class="sxs-lookup"><span data-stu-id="f1b58-137">Clear the shopping cart.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

<span data-ttu-id="f1b58-138">基於此範例應用程式的目的，我們將計算出貨日期，只要在目前日期加上兩天。</span><span class="sxs-lookup"><span data-stu-id="f1b58-138">For the purposes of this sample application we'll calculate a ship date by simply adding two days to the current date.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

<span data-ttu-id="f1b58-139">現在執行應用程式可讓我們從開始到結束測試購物流程。</span><span class="sxs-lookup"><span data-stu-id="f1b58-139">Running the application now will permit us to test the shopping process from start to finish.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f1b58-140">[上一頁](tailspin-spyworks-part-5.md)
> [下一頁](tailspin-spyworks-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="f1b58-140">[Previous](tailspin-spyworks-part-5.md)
[Next](tailspin-spyworks-part-7.md)</span></span>
