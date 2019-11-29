---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
title: 成員資格和管理 |Microsoft Docs
author: Erikre
description: 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們建立 ASP.NET Web Forms 應用程式的基本概念 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 732a2316-e49f-4f72-becd-0cd72f14457e
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
msc.type: authoredcontent
ms.openlocfilehash: ab00bc90bfc767d06e747be6dfb973245b5aae88
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615463"
---
# <a name="membership-and-administration"></a><span data-ttu-id="127da-103">成員資格及系統管理</span><span class="sxs-lookup"><span data-stu-id="127da-103">Membership and Administration</span></span>

<span data-ttu-id="127da-104">依[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="127da-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="127da-105">[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="127da-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="127da-106">本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 建立 ASP.NET Web Forms 應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="127da-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="127da-107">本教學課程系列隨附有[ C#原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案。</span><span class="sxs-lookup"><span data-stu-id="127da-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="127da-108">本教學課程說明如何更新 Wingtip 玩具範例應用程式，以新增自訂角色並使用 ASP.NET Identity。</span><span class="sxs-lookup"><span data-stu-id="127da-108">This tutorial shows you how to update the Wingtip Toys sample application to add a custom role and use ASP.NET Identity.</span></span> <span data-ttu-id="127da-109">它也會示範如何執行系統管理頁面，其中具有自訂角色的使用者可以從網站新增和移除產品。</span><span class="sxs-lookup"><span data-stu-id="127da-109">It also shows you how to implement an administration page from which the user with a custom role can add and remove products from the website.</span></span>

<span data-ttu-id="127da-110">[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)是用來建立 ASP.NET web 應用程式的成員資格系統，並可在 ASP.NET 4.5 中取得。</span><span class="sxs-lookup"><span data-stu-id="127da-110">[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md) is the membership system used to build ASP.NET web application and is available in ASP.NET 4.5.</span></span> <span data-ttu-id="127da-111">ASP.NET Identity 用於 Visual Studio 2013 Web form 專案範本，以及用來[ASP.NET MVC](../../../../mvc/index.md)、 [ASP.NET Web API](../../../../web-api/index.md)和[ASP.NET 單一頁面應用程式](../../../../single-page-application/index.md)的範本。</span><span class="sxs-lookup"><span data-stu-id="127da-111">ASP.NET Identity is used in the Visual Studio 2013 Web Forms project template, as well as the templates for [ASP.NET MVC](../../../../mvc/index.md), [ASP.NET Web API](../../../../web-api/index.md), and [ASP.NET Single Page Application](../../../../single-page-application/index.md).</span></span> <span data-ttu-id="127da-112">當您開始使用空白 Web 應用程式時，也可以使用 NuGet 來特別安裝 ASP.NET Identity 系統。</span><span class="sxs-lookup"><span data-stu-id="127da-112">You can also specifically install the ASP.NET Identity system using NuGet when you start with an empty Web application.</span></span> <span data-ttu-id="127da-113">不過，在本教學課程系列中，您會使用**Web Forms**projecttemplate，其中包含 ASP.NET Identity 系統。</span><span class="sxs-lookup"><span data-stu-id="127da-113">However, in this tutorial series you use the **Web Forms**projecttemplate, which includes the ASP.NET Identity system.</span></span> <span data-ttu-id="127da-114">ASP.NET Identity 可讓您輕鬆地整合使用者特定的設定檔資料與應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="127da-114">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="127da-115">此外，ASP.NET Identity 可讓您選擇應用程式中使用者設定檔的持續性模型。</span><span class="sxs-lookup"><span data-stu-id="127da-115">Also, ASP.NET Identity allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="127da-116">您可以將資料儲存在 SQL Server 資料庫或其他資料存放區中，包括*NoSQL*資料存放區，例如 Windows Azure 儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="127da-116">You can store the data in a SQL Server database or another data store, including *NoSQL* data stores such as Windows Azure Storage Tables.</span></span>

<span data-ttu-id="127da-117">本教學課程是以先前的教學課程為基礎，在 Wingtip 玩具教學課程系列中的「簽出與使用 PayPal 付款」。</span><span class="sxs-lookup"><span data-stu-id="127da-117">This tutorial builds on the previous tutorial titled "Checkout and Payment with PayPal" in the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="127da-118">您將瞭解的內容：</span><span class="sxs-lookup"><span data-stu-id="127da-118">What you'll learn:</span></span>

- <span data-ttu-id="127da-119">如何使用程式碼將自訂角色和使用者新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="127da-119">How to use code to add a custom role and a user to the application.</span></span>
- <span data-ttu-id="127da-120">如何限制對管理資料夾和頁面的存取。</span><span class="sxs-lookup"><span data-stu-id="127da-120">How to restrict access to the administration folder and page.</span></span>
- <span data-ttu-id="127da-121">如何為屬於自訂角色的使用者提供導覽。</span><span class="sxs-lookup"><span data-stu-id="127da-121">How to provide navigation for the user that belongs to the custom role.</span></span>
- <span data-ttu-id="127da-122">如何使用模型系結來填入具有產品類別目錄的[DropDownList](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist(v=vs.110).aspx)控制項。</span><span class="sxs-lookup"><span data-stu-id="127da-122">How to use model binding to populate a [DropDownList](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist(v=vs.110).aspx) control with product categories.</span></span>
- <span data-ttu-id="127da-123">如何使用[FileUpload](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload(v=vs.110).aspx)控制項將檔案上傳至 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="127da-123">How to upload a file to the web application using the [FileUpload](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload(v=vs.110).aspx) control.</span></span>
- <span data-ttu-id="127da-124">如何使用驗證控制項來執行輸入驗證。</span><span class="sxs-lookup"><span data-stu-id="127da-124">How to use validation controls to implement input validation.</span></span>
- <span data-ttu-id="127da-125">如何在應用程式中新增和移除產品。</span><span class="sxs-lookup"><span data-stu-id="127da-125">How to add and remove products from the application.</span></span>

## <a name="these-features-are-included-in-the-tutorial"></a><span data-ttu-id="127da-126">這些功能包含在教學課程中：</span><span class="sxs-lookup"><span data-stu-id="127da-126">These features are included in the tutorial:</span></span>

- <span data-ttu-id="127da-127">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="127da-127">ASP.NET Identity</span></span>
- <span data-ttu-id="127da-128">設定和授權</span><span class="sxs-lookup"><span data-stu-id="127da-128">Configuration and Authorization</span></span>
- <span data-ttu-id="127da-129">模型繫結</span><span class="sxs-lookup"><span data-stu-id="127da-129">Model Binding</span></span>
- <span data-ttu-id="127da-130">不顯眼的驗證</span><span class="sxs-lookup"><span data-stu-id="127da-130">Unobtrusive Validation</span></span>

<span data-ttu-id="127da-131">ASP.NET Web Forms 提供成員資格功能。</span><span class="sxs-lookup"><span data-stu-id="127da-131">ASP.NET Web Forms provides membership capabilities.</span></span> <span data-ttu-id="127da-132">藉由使用預設範本，您可以在應用程式執行時立即使用內建的成員資格功能。</span><span class="sxs-lookup"><span data-stu-id="127da-132">By using the default template, you have built-in membership functionality that you can immediately use when the application runs.</span></span> <span data-ttu-id="127da-133">本教學課程說明如何使用 ASP.NET Identity 新增自訂角色，並將使用者指派給該角色。</span><span class="sxs-lookup"><span data-stu-id="127da-133">This tutorial shows you how to use ASP.NET Identity to add a custom role and assign a user to that role.</span></span> <span data-ttu-id="127da-134">您將瞭解如何限制系統管理資料夾的存取權。</span><span class="sxs-lookup"><span data-stu-id="127da-134">You will learn how to restrict access to the administration folder.</span></span> <span data-ttu-id="127da-135">您將會在 [系統管理] 資料夾中新增一個頁面，讓具有自訂角色的使用者新增和移除產品，以及在新增產品後進行預覽。</span><span class="sxs-lookup"><span data-stu-id="127da-135">You'll add a page to the administration folder that allows a user with a custom role to add and remove products, and to preview a product after it has been added.</span></span>

## <a name="adding-a-custom-role"></a><span data-ttu-id="127da-136">新增自訂角色</span><span class="sxs-lookup"><span data-stu-id="127da-136">Adding a Custom Role</span></span>

<span data-ttu-id="127da-137">使用 ASP.NET Identity，您可以加入自訂角色，並使用程式碼將使用者指派給該角色。</span><span class="sxs-lookup"><span data-stu-id="127da-137">Using ASP.NET Identity, you can add a custom role and assign a user to that role using code.</span></span>

1. <span data-ttu-id="127da-138">在**方案總管**中，以滑鼠右鍵按一下*邏輯*資料夾，然後建立新的類別。</span><span class="sxs-lookup"><span data-stu-id="127da-138">In **Solution Explorer**, right-click on the *Logic* folder and create a new class.</span></span>
2. <span data-ttu-id="127da-139">將新類別命名為*RoleActions.cs*。</span><span class="sxs-lookup"><span data-stu-id="127da-139">Name the new class *RoleActions.cs*.</span></span>
3. <span data-ttu-id="127da-140">修改程式碼，使其看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="127da-140">Modify the code so that it appears as follows:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample1.cs?highlight=8)]
4. <span data-ttu-id="127da-141">在**方案總管**中，開啟*Global.asax.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="127da-141">In **Solution Explorer**, open the *Global.asax.cs* file.</span></span>
5. <span data-ttu-id="127da-142">藉由新增黃色反白顯示的程式碼來修改*Global.asax.cs*檔案，讓它看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="127da-142">Modify the *Global.asax.cs* file by adding the code highlighted in yellow so that it appears as follows:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample2.cs?highlight=11,26-28)]
6. <span data-ttu-id="127da-143">請注意，`AddUserAndRole` 會以紅色加上底線。</span><span class="sxs-lookup"><span data-stu-id="127da-143">Notice that `AddUserAndRole` is underlined in red.</span></span> <span data-ttu-id="127da-144">按兩下 [AddUserAndRole] 程式碼。</span><span class="sxs-lookup"><span data-stu-id="127da-144">Double-click the AddUserAndRole code.</span></span>  
   <span data-ttu-id="127da-145">反白顯示方法開頭的字母 "A" 會加上底線。</span><span class="sxs-lookup"><span data-stu-id="127da-145">The letter "A" at the beginning of the highlighted method will be underlined.</span></span>
7. <span data-ttu-id="127da-146">將滑鼠停留在字母 "A" 上，然後按一下 UI，讓您為 `AddUserAndRole` 方法產生方法 stub。</span><span class="sxs-lookup"><span data-stu-id="127da-146">Hover over the letter "A" and click the UI that allows you to generate a method stub for the `AddUserAndRole` method.</span></span> 

    ![成員資格和管理-產生方法 Stub](membership-and-administration/_static/image1.png)
8. <span data-ttu-id="127da-148">按一下標題為的選項：</span><span class="sxs-lookup"><span data-stu-id="127da-148">Click the option titled:</span></span>  
    `Generate method stub for "AddUserAndRole" in "WingtipToys.Logic.RoleActions"`
9. <span data-ttu-id="127da-149">從*邏輯*資料夾中開啟*RoleActions.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="127da-149">Open the *RoleActions.cs* file from the *Logic* folder.</span></span>  
   <span data-ttu-id="127da-150">`AddUserAndRole` 方法已新增至類別檔案。</span><span class="sxs-lookup"><span data-stu-id="127da-150">The `AddUserAndRole` method has been added to the class file.</span></span>
10. <span data-ttu-id="127da-151">移除 `NotImplementedException` 並新增以黃色反白顯示的程式碼，以修改*RoleActions.cs*檔，使其看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="127da-151">Modify the *RoleActions.cs* file by removing the `NotImplementedException` and adding the code highlighted in yellow, so that it appears as follows:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample3.cs?highlight=5-7,15-51)]

<span data-ttu-id="127da-152">上述程式碼會先建立成員資格資料庫的資料庫內容。</span><span class="sxs-lookup"><span data-stu-id="127da-152">The above code first establishes a database context for the membership database.</span></span> <span data-ttu-id="127da-153">成員資格資料庫也會儲存為*應用程式\_Data*資料夾中的 *.mdf*檔案。</span><span class="sxs-lookup"><span data-stu-id="127da-153">The membership database is also stored as an *.mdf* file in the *App\_Data* folder.</span></span> <span data-ttu-id="127da-154">當第一位使用者登入此 web 應用程式之後，您就能夠看到此資料庫。</span><span class="sxs-lookup"><span data-stu-id="127da-154">You will be able to view this database once the first user has signed in to this web application.</span></span> 

> [!NOTE] 
> 
> <span data-ttu-id="127da-155">如果您想要儲存成員資格資料和產品資料，您可以考慮使用您用來在上述程式碼中儲存產品資料的相同**DbCoNtext** 。</span><span class="sxs-lookup"><span data-stu-id="127da-155">If you wish to store the membership data along with the product data, you can consider using the same **DbContext** that you used to store the product data in the above code.</span></span>

 <span data-ttu-id="127da-156">*Internal*關鍵字是類型（例如類別）和類型成員（例如方法或屬性）的存取修飾詞。</span><span class="sxs-lookup"><span data-stu-id="127da-156">The *internal* keyword is an access modifier for types (such as classes) and type members (such as methods or properties).</span></span> <span data-ttu-id="127da-157">內部類型或成員只能在包含于相同元件 *（.dll*檔案）中的檔案內進行存取。</span><span class="sxs-lookup"><span data-stu-id="127da-157">Internal types or members are accessible only within files contained in the same assembly *(.dll* file).</span></span> <span data-ttu-id="127da-158">當您建立應用程式時，會建立元件檔 *（.dll*），其中包含執行應用程式時所執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="127da-158">When you build your application, an assembly file *(.dll*) is created that contains the code that is executed when you run your application.</span></span> 

<span data-ttu-id="127da-159">提供角色管理的 `RoleStore` 物件會根據資料庫內容來建立。</span><span class="sxs-lookup"><span data-stu-id="127da-159">A `RoleStore` object, which provides role management, is created based on the database context.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="127da-160">請注意，建立 `RoleStore` 物件時，它會使用泛型 `IdentityRole` 類型。</span><span class="sxs-lookup"><span data-stu-id="127da-160">Notice that when the `RoleStore` object is created it uses a Generic `IdentityRole` type.</span></span> <span data-ttu-id="127da-161">這表示 `RoleStore` 只允許包含 `IdentityRole` 物件。</span><span class="sxs-lookup"><span data-stu-id="127da-161">This means that the `RoleStore` is only allowed to contain `IdentityRole` objects.</span></span> <span data-ttu-id="127da-162">此外，藉由使用泛型，記憶體中的資源會以更好的方式處理。</span><span class="sxs-lookup"><span data-stu-id="127da-162">Also by using Generics, resources in memory are handled better.</span></span>

<span data-ttu-id="127da-163">接下來，會根據您剛才建立的 `RoleStore` 物件來建立 `RoleManager` 物件。</span><span class="sxs-lookup"><span data-stu-id="127da-163">Next, the `RoleManager` object, is created based on the `RoleStore` object that you just created.</span></span> <span data-ttu-id="127da-164">`RoleManager` 物件會公開角色相關的 API，可用來自動將變更儲存至 `RoleStore`。</span><span class="sxs-lookup"><span data-stu-id="127da-164">the `RoleManager` object exposes role related API which can be used to automatically save changes to the `RoleStore`.</span></span> <span data-ttu-id="127da-165">`RoleManager` 只允許包含 `IdentityRole` 物件，因為程式碼會使用 `<IdentityRole>` 的泛型型別。</span><span class="sxs-lookup"><span data-stu-id="127da-165">The `RoleManager` is only allowed to contain `IdentityRole` objects because the code uses the `<IdentityRole>` Generic type.</span></span>

<span data-ttu-id="127da-166">您可以呼叫 `RoleExists` 方法，判斷成員資格資料庫中是否有 "canEdit" 角色。</span><span class="sxs-lookup"><span data-stu-id="127da-166">You call the `RoleExists` method to determine if the "canEdit" role is present in the membership database.</span></span> <span data-ttu-id="127da-167">如果不是，您可以建立角色。</span><span class="sxs-lookup"><span data-stu-id="127da-167">If it is not, you create the role.</span></span>

<span data-ttu-id="127da-168">建立 `UserManager` 物件比 `RoleManager` 控制項更複雜，但幾乎相同。</span><span class="sxs-lookup"><span data-stu-id="127da-168">Creating the `UserManager` object appears to be more complicated than the `RoleManager` control, however it is nearly the same.</span></span> <span data-ttu-id="127da-169">它只會在一行上進行編碼，而不是數個。</span><span class="sxs-lookup"><span data-stu-id="127da-169">It is just coded on one line rather than several.</span></span> <span data-ttu-id="127da-170">在這裡，您要傳遞的參數會具現化為括弧中包含的新物件。</span><span class="sxs-lookup"><span data-stu-id="127da-170">Here, the parameter that you are passing is instantiating as a new object contained in the parenthesis.</span></span>

<span data-ttu-id="127da-171">接下來，建立新的 `ApplicationUser` 物件來建立 "canEditUser" 使用者。</span><span class="sxs-lookup"><span data-stu-id="127da-171">Next you create the "canEditUser" user by creating a new `ApplicationUser` object.</span></span> <span data-ttu-id="127da-172">然後，如果您成功建立使用者，請將使用者新增至新角色。</span><span class="sxs-lookup"><span data-stu-id="127da-172">Then, if you successfully create the user, you add the user to the new role.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="127da-173">錯誤處理將會在本教學課程系列稍後的「ASP.NET 錯誤處理」教學課程中更新。</span><span class="sxs-lookup"><span data-stu-id="127da-173">The error handling will be updated during the "ASP.NET Error Handling" tutorial later in this tutorial series.</span></span>

<span data-ttu-id="127da-174">下次應用程式啟動時，名為 "canEditUser" 的使用者會新增為應用程式名稱為 "canEdit" 的角色。</span><span class="sxs-lookup"><span data-stu-id="127da-174">The next time the application starts, the user named "canEditUser" will be added as the role named "canEdit" of the application.</span></span> <span data-ttu-id="127da-175">稍後在本教學課程中，您將以「canEditUser」使用者的身分登入，以顯示您將在本教學課程中新增的其他功能。</span><span class="sxs-lookup"><span data-stu-id="127da-175">Later in this tutorial, you will login as the "canEditUser" user to display additional capabilities that you will added during this tutorial.</span></span> <span data-ttu-id="127da-176">如需有關 ASP.NET Identity 的 API 詳細資料，請參閱[Microsoft AspNet. Identity 命名空間](https://msdn.microsoft.com/library/microsoft.aspnet.identity(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="127da-176">For API details about ASP.NET Identity, see the [Microsoft.AspNet.Identity Namespace](https://msdn.microsoft.com/library/microsoft.aspnet.identity(v=vs.111).aspx).</span></span> <span data-ttu-id="127da-177">如需有關初始化 ASP.NET Identity 系統的其他詳細資訊，請參閱[AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample/blob/master/AspnetIdentitySample/App_Start/IdentityConfig.cs)。</span><span class="sxs-lookup"><span data-stu-id="127da-177">For additional details about initializing the ASP.NET Identity system, see the [AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample/blob/master/AspnetIdentitySample/App_Start/IdentityConfig.cs).</span></span>

### <a name="restricting-access-to-the-administration-page"></a><span data-ttu-id="127da-178">限制系統管理頁面的存取權</span><span class="sxs-lookup"><span data-stu-id="127da-178">Restricting Access to the Administration Page</span></span>

<span data-ttu-id="127da-179">Wingtip 玩具範例應用程式可讓匿名使用者和已登入的使用者查看和購買產品。</span><span class="sxs-lookup"><span data-stu-id="127da-179">The Wingtip Toys sample application allows both anonymous users and logged-in users to view and purchase products.</span></span> <span data-ttu-id="127da-180">不過，具有自訂 "canEdit" 角色的登入使用者可以存取受限制的頁面，以便新增和移除產品。</span><span class="sxs-lookup"><span data-stu-id="127da-180">However, the logged-in user that has the custom "canEdit" role can access a restricted page in order to add and remove products.</span></span>

#### <a name="add-an-administration-folder-and-page"></a><span data-ttu-id="127da-181">新增系統管理資料夾和頁面</span><span class="sxs-lookup"><span data-stu-id="127da-181">Add an Administration Folder and Page</span></span>

<span data-ttu-id="127da-182">接下來，您將為屬於 Wingtip 玩具範例應用程式自訂角色的 "canEditUser" 使用者建立名為*Admin*的資料夾。</span><span class="sxs-lookup"><span data-stu-id="127da-182">Next, you will create a folder named *Admin* for the "canEditUser" user belonging to the custom role of the Wingtip Toys sample application.</span></span>

1. <span data-ttu-id="127da-183">在**方案總管**中，以滑鼠右鍵按一下專案名稱（**Wingtip 玩具**），**然後選取 [** 新增 -&gt;**新資料夾**]。</span><span class="sxs-lookup"><span data-stu-id="127da-183">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add** -&gt; **New Folder**.</span></span>
2. <span data-ttu-id="127da-184">將新資料夾命名為*Admin*。</span><span class="sxs-lookup"><span data-stu-id="127da-184">Name the new folder *Admin*.</span></span>
3. <span data-ttu-id="127da-185">在 [系統*管理*] 資料夾上按一下滑鼠右鍵，**然後選取 [** 新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="127da-185">Right-click the *Admin* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="127da-186">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="127da-186">The **Add New Item** dialog box is displayed.</span></span>
4. <span data-ttu-id="127da-187">選取左側的 [ <strong>Visual C#</strong> -&gt; <strong>Web</strong>範本] 群組。</span><span class="sxs-lookup"><span data-stu-id="127da-187">Select the <strong>Visual C#</strong>-&gt; <strong>Web</strong> templates group on the left.</span></span> <span data-ttu-id="127da-188">從中間清單中，選取 [<strong>具有主版的 Web 表單</strong>]，將它命名為<em>AdminPage .aspx</em><strong>，</strong>然後選取 [<strong>新增</strong>]。</span><span class="sxs-lookup"><span data-stu-id="127da-188">From the middle list, select <strong>Web Form with Master Page</strong>,name it <em>AdminPage.aspx</em><strong>,</strong> and then select <strong>Add</strong>.</span></span>
5. <span data-ttu-id="127da-189">選取*網站*檔案作為主版頁面，然後選擇 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="127da-189">Select the *Site.Master* file as the master page, and then choose **OK**.</span></span>

#### <a name="add-a-webconfig-file"></a><span data-ttu-id="127da-190">新增 Web.config 檔案</span><span class="sxs-lookup"><span data-stu-id="127da-190">Add a Web.config File</span></span>

<span data-ttu-id="127da-191">藉由將*web.config*檔案新增至*Admin*資料夾，您可以限制對資料夾中所含頁面的存取。</span><span class="sxs-lookup"><span data-stu-id="127da-191">By adding a *Web.config* file to the *Admin* folder, you can restrict access to the page contained in the folder.</span></span>

1. <span data-ttu-id="127da-192">以滑鼠右鍵按一下 [系統*管理*] 資料夾，**然後選取 [** 新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="127da-192">Right-click the *Admin* folder and select **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="127da-193">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="127da-193">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="127da-194">從C#視覺 web 範本清單中，從中間清單選取 [ <strong>web 設定檔</strong>]，接受 web.config 的預設名稱<strong>，然後</strong>選取 [<strong>新增</strong>]。</span><span class="sxs-lookup"><span data-stu-id="127da-194">From the list of Visual C# web templates, select <strong>Web Configuration File</strong>from the middle list, accept the default name of <em>Web.config</em><strong>,</strong> and then select <strong>Add</strong>.</span></span>
3. <span data-ttu-id="127da-195">將*web.config*檔案中的現有 XML 內容取代為下列各項：</span><span class="sxs-lookup"><span data-stu-id="127da-195">Replace the existing XML content in the *Web.config* file with the following:</span></span>  

    [!code-xml[Main](membership-and-administration/samples/sample4.xml)]

<span data-ttu-id="127da-196">儲存 web.config*檔案*。</span><span class="sxs-lookup"><span data-stu-id="127da-196">Save the *Web.config* file.</span></span> <span data-ttu-id="127da-197">Web.config*檔案*會指定只有屬於應用程式 "canEdit" 角色的使用者才能存取*Admin*資料夾中包含的頁面。</span><span class="sxs-lookup"><span data-stu-id="127da-197">The *Web.config* file specifies that only user belonging to the "canEdit" role of the application can access the page contained in the *Admin* folder.</span></span>

### <a name="including-custom-role-navigation"></a><span data-ttu-id="127da-198">包括自訂角色導覽</span><span class="sxs-lookup"><span data-stu-id="127da-198">Including Custom Role Navigation</span></span>

<span data-ttu-id="127da-199">若要讓自訂 "canEdit" 角色的使用者流覽至應用程式的 [管理] 區段，您必須新增 [*網站*] 頁面的連結。</span><span class="sxs-lookup"><span data-stu-id="127da-199">To enable the user of the custom "canEdit" role to navigate to the administration section of the application, you must add a link to the *Site.Master* page.</span></span> <span data-ttu-id="127da-200">只有屬於 "canEdit" 角色的使用者才能夠看到系統**管理員**連結並存取 [管理] 區段。</span><span class="sxs-lookup"><span data-stu-id="127da-200">Only users that belong to the "canEdit" role will be able to see the **Admin** link and access the administration section.</span></span>

1. <span data-ttu-id="127da-201">在方案總管中，尋找並開啟 [*網站*] 頁面。</span><span class="sxs-lookup"><span data-stu-id="127da-201">In Solution Explorer, find and open the *Site.Master* page.</span></span>
2. <span data-ttu-id="127da-202">若要為 "canEdit" 角色的使用者建立連結，請將以黃色反白顯示的標記新增至下列未排序清單 `<ul>` 元素，讓清單顯示如下：</span><span class="sxs-lookup"><span data-stu-id="127da-202">To create a link for the user of the "canEdit" role, add the markup highlighted in yellow to the following unordered list `<ul>` element so that the list appears as follows:</span></span>  

    [!code-html[Main](membership-and-administration/samples/sample5.html?highlight=2-3)]
3. <span data-ttu-id="127da-203">開啟*Site.Master.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="127da-203">Open the *Site.Master.cs* file.</span></span> <span data-ttu-id="127da-204">將以黃色反白顯示的程式碼新增至 `Page_Load` 處理常式，讓系統**管理員**連結只對 "canEditUser" 使用者顯示。</span><span class="sxs-lookup"><span data-stu-id="127da-204">Make the **Admin** link visible only to the "canEditUser" user by adding the code highlighted in yellow to the `Page_Load` handler.</span></span> <span data-ttu-id="127da-205">`Page_Load` 處理常式將會如下所示：</span><span class="sxs-lookup"><span data-stu-id="127da-205">The `Page_Load` handler will appear as follows:</span></span>   

    [!code-csharp[Main](membership-and-administration/samples/sample6.cs?highlight=3-6)]

<span data-ttu-id="127da-206">當頁面載入時，程式碼會檢查登入的使用者是否具有 "canEdit" 的角色。</span><span class="sxs-lookup"><span data-stu-id="127da-206">When the page loads, the code checks whether the logged-in user has the role of "canEdit".</span></span> <span data-ttu-id="127da-207">如果使用者屬於 "canEdit" 角色，則會顯示包含*AdminPage*頁面連結的 span 元素（以及範圍內的連結）。</span><span class="sxs-lookup"><span data-stu-id="127da-207">If the user belongs to the "canEdit" role, the span element containing the link to the *AdminPage.aspx* page (and consequently the link inside the span) is made visible.</span></span>

### <a name="enabling-product-administration"></a><span data-ttu-id="127da-208">啟用產品管理</span><span class="sxs-lookup"><span data-stu-id="127da-208">Enabling Product Administration</span></span>

<span data-ttu-id="127da-209">到目前為止，您已建立「canEdit」角色，並新增了「canEditUser」使用者、「管理」資料夾和管理頁面。</span><span class="sxs-lookup"><span data-stu-id="127da-209">So far, you have created the "canEdit" role and added an "canEditUser" user, an administration folder, and an administration page.</span></span> <span data-ttu-id="127da-210">您已設定 [系統管理] 資料夾和頁面的存取權限，並已將 "canEdit" 角色的使用者導覽連結新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="127da-210">You have set access rights for the administration folder and page, and have added a navigation link for the user of the "canEdit" role to the application.</span></span> <span data-ttu-id="127da-211">接下來，您會將標記加入至*AdminPage* ，並將程式碼新增至*AdminPage.aspx.cs*程式碼後置檔案，讓具有 "canEdit" 角色的使用者可以新增和移除產品。</span><span class="sxs-lookup"><span data-stu-id="127da-211">Next, you will add markup to the *AdminPage.aspx* page and code to the *AdminPage.aspx.cs* code-behind file that will enable the user with the "canEdit" role to add and remove products.</span></span>

1. <span data-ttu-id="127da-212">在**方案總管**中，從 [系統*管理*] 資料夾開啟*AdminPage .aspx*檔案。</span><span class="sxs-lookup"><span data-stu-id="127da-212">In **Solution Explorer**, open the *AdminPage.aspx* file from the *Admin* folder.</span></span>
2. <span data-ttu-id="127da-213">以下列內容取代現有的標記：</span><span class="sxs-lookup"><span data-stu-id="127da-213">Replace the existing markup with the following:</span></span>  

    [!code-aspx[Main](membership-and-administration/samples/sample7.aspx)]
3. <span data-ttu-id="127da-214">接下來，開啟*AdminPage.aspx.cs*程式碼後置檔案，方法是以滑鼠右鍵按一下*AdminPage* ，然後按一下 [ **View code**]。</span><span class="sxs-lookup"><span data-stu-id="127da-214">Next, open the *AdminPage.aspx.cs* code-behind file by right-clicking the *AdminPage.aspx* and clicking **View Code**.</span></span>
4. <span data-ttu-id="127da-215">將*AdminPage.aspx.cs*程式碼後置檔案中的現有程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="127da-215">Replace the existing code in the *AdminPage.aspx.cs* code-behind file with the following code:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample8.cs)]

<span data-ttu-id="127da-216">在您為*AdminPage.aspx.cs*程式碼後置檔案輸入的程式碼中，名為 `AddProducts` 的類別會執行將產品新增至資料庫的實際工作。</span><span class="sxs-lookup"><span data-stu-id="127da-216">In the code that you entered for the *AdminPage.aspx.cs* code-behind file, a class called `AddProducts` does the actual work of adding products to the database.</span></span> <span data-ttu-id="127da-217">此類別尚不存在，因此您現在將會建立它。</span><span class="sxs-lookup"><span data-stu-id="127da-217">This class doesn't exist yet, so you will create it now.</span></span>

1. <span data-ttu-id="127da-218">在**方案總管**中，以滑鼠右鍵按一下*邏輯*資料夾，然後**選取 [** 新增 -&gt;**新專案**]。</span><span class="sxs-lookup"><span data-stu-id="127da-218">In **Solution Explorer**, right-click the *Logic* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="127da-219">隨即顯示 [ 新增項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="127da-219">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="127da-220">選取左側的 [ **Visual C#**  -&gt; 程式**代碼**範本] 群組。</span><span class="sxs-lookup"><span data-stu-id="127da-220">Select the **Visual C#** -&gt; **Code** templates group on the left.</span></span> <span data-ttu-id="127da-221">然後，從中間清單中選取 [**類別**]，並將其命名為*AddProducts.cs*。</span><span class="sxs-lookup"><span data-stu-id="127da-221">Then, select **Class**from the middle list and name it *AddProducts.cs*.</span></span>   
   <span data-ttu-id="127da-222">隨即顯示新的類別檔案。</span><span class="sxs-lookup"><span data-stu-id="127da-222">The new class file is displayed.</span></span>
3. <span data-ttu-id="127da-223">將現有的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="127da-223">Replace the existing code with the following:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample9.cs)]

<span data-ttu-id="127da-224">*AdminPage*可以讓屬於 "canEdit" 角色的使用者新增和移除產品。</span><span class="sxs-lookup"><span data-stu-id="127da-224">The *AdminPage.aspx* page allows the user belonging to the "canEdit" role to add and remove products.</span></span> <span data-ttu-id="127da-225">新增產品時，會驗證產品的詳細資料，然後將其輸入至資料庫。</span><span class="sxs-lookup"><span data-stu-id="127da-225">When a new product is added, the details about the product are validated and then entered into the database.</span></span> <span data-ttu-id="127da-226">新產品會立即提供給 web 應用程式的所有使用者使用。</span><span class="sxs-lookup"><span data-stu-id="127da-226">The new product is immediately available to all users of the web application.</span></span>

#### <a name="unobtrusive-validation"></a><span data-ttu-id="127da-227">不顯眼的驗證</span><span class="sxs-lookup"><span data-stu-id="127da-227">Unobtrusive Validation</span></span>

<span data-ttu-id="127da-228">使用者在*AdminPage .aspx*頁面上提供的產品詳細資料，會使用驗證控制項（`RequiredFieldValidator` 和 `RegularExpressionValidator`）進行驗證。</span><span class="sxs-lookup"><span data-stu-id="127da-228">The product details that the user provides on the *AdminPage.aspx* page are validated using validation controls (`RequiredFieldValidator` and `RegularExpressionValidator`).</span></span> <span data-ttu-id="127da-229">這些控制項會自動使用不顯眼的驗證。</span><span class="sxs-lookup"><span data-stu-id="127da-229">These controls automatically use unobtrusive validation.</span></span> <span data-ttu-id="127da-230">不顯眼的驗證可讓驗證控制項針對用戶端驗證邏輯使用 JavaScript，這表示頁面不需要通過伺服器的驗證。</span><span class="sxs-lookup"><span data-stu-id="127da-230">Unobtrusive validation allows the validation controls to use JavaScript for client-side validation logic, which means the page does not require a trip to the server to be validated.</span></span> <span data-ttu-id="127da-231">根據預設，不顯眼的驗證會包含*在 web.config 檔案*中，以下列設定為基礎：</span><span class="sxs-lookup"><span data-stu-id="127da-231">By default, unobtrusive validation is included in the *Web.config* file based on the following configuration setting:</span></span>

[!code-xml[Main](membership-and-administration/samples/sample10.xml)]

#### <a name="regular-expressions"></a><span data-ttu-id="127da-232">規則運算式</span><span class="sxs-lookup"><span data-stu-id="127da-232">Regular Expressions</span></span>

<span data-ttu-id="127da-233">[ *AdminPage* ] 頁面上的產品價格會使用**RegularExpressionValidator**控制項進行驗證。</span><span class="sxs-lookup"><span data-stu-id="127da-233">The product price on the *AdminPage.aspx* page is validated using a **RegularExpressionValidator** control.</span></span> <span data-ttu-id="127da-234">此控制項會驗證相關聯的輸入控制項值（"AddProductPrice" TextBox）是否符合正則運算式所指定的模式。</span><span class="sxs-lookup"><span data-stu-id="127da-234">This control validates whether the value of the associated input control (the "AddProductPrice" TextBox) matches the pattern specified by the regular expression.</span></span> <span data-ttu-id="127da-235">正則運算式是模式比對標記法，可讓您快速尋找並比對特定的字元模式。</span><span class="sxs-lookup"><span data-stu-id="127da-235">A regular expression is a pattern-matching notation that enables you to quickly find and match specific character patterns.</span></span> <span data-ttu-id="127da-236">**RegularExpressionValidator**控制項包含名為 `ValidationExpression` 的屬性，其中包含用來驗證價格輸入的正則運算式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="127da-236">The **RegularExpressionValidator** control includes a property named `ValidationExpression` that contains the regular expression used to validate price input, as shown below:</span></span>

[!code-aspx[Main](membership-and-administration/samples/sample11.aspx)]

#### <a name="fileupload-control"></a><span data-ttu-id="127da-237">FileUpload 控制項</span><span class="sxs-lookup"><span data-stu-id="127da-237">FileUpload Control</span></span>

<span data-ttu-id="127da-238">除了 [輸入] 和 [驗證] 控制項以外，您還將**FileUpload**控制項新增至 [ *AdminPage* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="127da-238">In addition to the input and validation controls, you added the **FileUpload** control to the *AdminPage.aspx* page.</span></span> <span data-ttu-id="127da-239">此控制項提供上傳檔案的功能。</span><span class="sxs-lookup"><span data-stu-id="127da-239">This control provides the capability to upload files.</span></span> <span data-ttu-id="127da-240">在此情況下，您只允許上傳影像檔案。</span><span class="sxs-lookup"><span data-stu-id="127da-240">In this case, you are only allowing image files to be uploaded.</span></span> <span data-ttu-id="127da-241">在程式碼後置檔案（*AdminPage.aspx.cs*）中，按一下 `AddProductButton` 時，程式碼會檢查**FileUpload**控制項的 `HasFile` 屬性。</span><span class="sxs-lookup"><span data-stu-id="127da-241">In the code-behind file (*AdminPage.aspx.cs*), when the `AddProductButton` is clicked, the code checks the `HasFile` property of the **FileUpload** control.</span></span> <span data-ttu-id="127da-242">如果控制項有檔案，而且允許檔案類型（以副檔名為依據），則會將影像儲存至應用程式的*images*資料夾和*images/拇指*資料夾。</span><span class="sxs-lookup"><span data-stu-id="127da-242">If the control has a file and if the file type (based on file extension) is allowed, the image is saved to the *Images* folder and the *Images/Thumbs* folder of the application.</span></span>

#### <a name="model-binding"></a><span data-ttu-id="127da-243">模型繫結</span><span class="sxs-lookup"><span data-stu-id="127da-243">Model Binding</span></span>

<span data-ttu-id="127da-244">稍早在本教學課程中，您已使用模型系結來填入**ListView**控制項、 **FormsView**控制項、 **GridView**控制項和**detailview 之**控制項。</span><span class="sxs-lookup"><span data-stu-id="127da-244">Earlier in this tutorial series you used model binding to populate a **ListView** control, a **FormsView** control, a **GridView** control, and a **DetailView** control.</span></span> <span data-ttu-id="127da-245">在本教學課程中，您會使用模型系結，以產品類別目錄清單填入**DropDownList**控制項。</span><span class="sxs-lookup"><span data-stu-id="127da-245">In this tutorial, you use model binding to populate a **DropDownList** control with a list of product categories.</span></span>

<span data-ttu-id="127da-246">您新增至*AdminPage .aspx*檔案的標記包含名為 `DropDownAddCategory`的**DropDownList**控制項：</span><span class="sxs-lookup"><span data-stu-id="127da-246">The markup that you added to the *AdminPage.aspx* file contains a **DropDownList** control called `DropDownAddCategory`:</span></span>

[!code-aspx[Main](membership-and-administration/samples/sample12.aspx)]

<span data-ttu-id="127da-247">您可以使用模型系結來填入這個**DropDownList** ，方法是設定 `ItemType` 屬性和 `SelectMethod` 屬性。</span><span class="sxs-lookup"><span data-stu-id="127da-247">You use model binding to populate this **DropDownList** by setting the `ItemType` attribute and the `SelectMethod` attribute.</span></span> <span data-ttu-id="127da-248">`ItemType` 屬性指定在填入控制項時使用 `WingtipToys.Models.Category` 類型。</span><span class="sxs-lookup"><span data-stu-id="127da-248">The `ItemType` attribute specifies that you use the `WingtipToys.Models.Category` type when populating the control.</span></span> <span data-ttu-id="127da-249">您已在本教學課程系列的開頭定義此型別，方法是建立 `Category` 類別（如下所示）。</span><span class="sxs-lookup"><span data-stu-id="127da-249">You defined this type at the beginning of this tutorial series by creating the `Category` class (shown below).</span></span> <span data-ttu-id="127da-250">`Category` 類別位於*Category.cs*檔案內的 [*模型*] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="127da-250">The `Category` class is in the *Models* folder inside the *Category.cs* file.</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample13.cs)]

<span data-ttu-id="127da-251">**DropDownList**控制項的 `SelectMethod` 屬性會指定您使用程式碼後置檔案（*AdminPage.aspx.cs*）中所包含的 `GetCategories` 方法（如下所示）。</span><span class="sxs-lookup"><span data-stu-id="127da-251">The `SelectMethod` attribute of the **DropDownList** control specifies that you use the `GetCategories` method (shown below) that is included in the code-behind file (*AdminPage.aspx.cs*).</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample14.cs)]

<span data-ttu-id="127da-252">這個方法會指定使用 `IQueryable` 介面來評估 `Category` 類型的查詢。</span><span class="sxs-lookup"><span data-stu-id="127da-252">This method specifies that an `IQueryable` interface is used to evaluate a query against a `Category` type.</span></span> <span data-ttu-id="127da-253">傳回的值會用來填入頁面標記中的**DropDownList** （*AdminPage .aspx*）。</span><span class="sxs-lookup"><span data-stu-id="127da-253">The returned value is used to populate the **DropDownList** in the markup of the page (*AdminPage.aspx*).</span></span>

<span data-ttu-id="127da-254">針對清單中的每個專案所顯示的文字，是藉由設定 `DataTextField` 屬性來指定。</span><span class="sxs-lookup"><span data-stu-id="127da-254">The text displayed for each item in the list is specified by setting the `DataTextField` attribute.</span></span> <span data-ttu-id="127da-255">`DataTextField` 屬性會使用 `Category` 類別（如上所示）的 `CategoryName`，在**DropDownList**控制項中顯示每個類別目錄。</span><span class="sxs-lookup"><span data-stu-id="127da-255">The `DataTextField` attribute uses the `CategoryName` of the `Category` class (shown above) to display each category in the **DropDownList** control.</span></span> <span data-ttu-id="127da-256">在**DropDownList**控制項中選取專案時所傳遞的實際值是以 `DataValueField` 屬性為基礎。</span><span class="sxs-lookup"><span data-stu-id="127da-256">The actual value that is passed when an item is selected in the **DropDownList** control is based on the `DataValueField` attribute.</span></span> <span data-ttu-id="127da-257">`DataValueField` 屬性會設定為 `CategoryID`，做為 `Category` 類別中的定義（如上所示）。</span><span class="sxs-lookup"><span data-stu-id="127da-257">The `DataValueField` attribute is set to the `CategoryID` as define in the `Category` class (shown above).</span></span>

### <a name="how-the-application-will-work"></a><span data-ttu-id="127da-258">應用程式的工作方式</span><span class="sxs-lookup"><span data-stu-id="127da-258">How the Application Will Work</span></span>

<span data-ttu-id="127da-259">當屬於 "canEdit" 角色的使用者第一次流覽至頁面時，會如上面所述填入 `DropDownAddCategory`**DropDownList**控制項。</span><span class="sxs-lookup"><span data-stu-id="127da-259">When the user belonging to the "canEdit" role navigates to the page for the first time, the `DropDownAddCategory`**DropDownList** control is populated as described above.</span></span> <span data-ttu-id="127da-260">`DropDownRemoveProduct`**DropDownList**控制項也會使用相同的方法填入產品。</span><span class="sxs-lookup"><span data-stu-id="127da-260">The `DropDownRemoveProduct`**DropDownList** control is also populated with products using the same approach.</span></span> <span data-ttu-id="127da-261">屬於 "canEdit" 角色的使用者會選取類別目錄類型，並新增產品詳細資料（**名稱**、**描述**、**價格**和**影像檔**案）。</span><span class="sxs-lookup"><span data-stu-id="127da-261">The user belonging to the "canEdit" role selects the category type and adds product details (**Name**, **Description**, **Price**, and **Image File**).</span></span> <span data-ttu-id="127da-262">當屬於 "canEdit" 角色的使用者按一下 [**加入產品**] 按鈕時，就會觸發 `AddProductButton_Click` 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="127da-262">When the user belonging to the "canEdit" role clicks the **Add Product** button, the `AddProductButton_Click` event handler is triggered.</span></span> <span data-ttu-id="127da-263">位於程式碼後置檔案（*AdminPage.aspx.cs*）中的 `AddProductButton_Click` 事件處理常式會檢查影像檔案，確認它符合允許的檔案類型 *（.gif*、 *.png*、 *jpeg*或 *.jpg*）。</span><span class="sxs-lookup"><span data-stu-id="127da-263">The `AddProductButton_Click` event handler located in the code-behind file (*AdminPage.aspx.cs*) checks the image file to make sure it matches the allowed file types *(.gif*, *.png*, *.jpeg*, or *.jpg*).</span></span> <span data-ttu-id="127da-264">然後，影像檔案會儲存到 Wingtip 玩具範例應用程式的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="127da-264">Then, the image file is saved into a folder of the Wingtip Toys sample application.</span></span> <span data-ttu-id="127da-265">接下來，新的產品會新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="127da-265">Next, the new product is added to the database.</span></span> <span data-ttu-id="127da-266">為了完成新產品的加入，會建立 `AddProducts` 類別的新實例，並將其命名為 products。</span><span class="sxs-lookup"><span data-stu-id="127da-266">To accomplish adding a new product, a new instance of the `AddProducts` class is created and named products.</span></span> <span data-ttu-id="127da-267">`AddProducts` 類別具有名為 `AddProduct`的方法，而 products 物件會呼叫這個方法，將產品加入至資料庫。</span><span class="sxs-lookup"><span data-stu-id="127da-267">The `AddProducts` class has a method named `AddProduct`, and the products object calls this method to add products to the database.</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample15.cs)]

<span data-ttu-id="127da-268">如果程式碼成功將新產品加入至資料庫，則會使用查詢字串值 `ProductAction=add`重載該頁面。</span><span class="sxs-lookup"><span data-stu-id="127da-268">If the code successfully adds the new product to the database, the page is reloaded with the query string value `ProductAction=add`.</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample16.cs)]

<span data-ttu-id="127da-269">當頁面重載時，查詢字串會包含在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="127da-269">When the page reloads, the query string is included in the URL.</span></span> <span data-ttu-id="127da-270">藉由重載頁面，屬於 "canEdit" 角色的使用者可以立即在*AdminPage*頁面上看到**DropDownList**控制項中的更新。</span><span class="sxs-lookup"><span data-stu-id="127da-270">By reloading the page, the user belonging to the "canEdit" role can immediately see the updates in the **DropDownList** controls on the *AdminPage.aspx* page.</span></span> <span data-ttu-id="127da-271">此外，藉由包含 URL 的查詢字串，頁面可以向屬於 "canEdit" 角色的使用者顯示成功訊息。</span><span class="sxs-lookup"><span data-stu-id="127da-271">Also, by including the query string with the URL, the page can display a success message to the user belonging to the "canEdit" role.</span></span>

<span data-ttu-id="127da-272">當*AdminPage 載入 .aspx*頁面時，會呼叫 `Page_Load` 事件。</span><span class="sxs-lookup"><span data-stu-id="127da-272">When the *AdminPage.aspx* page reloads, the `Page_Load` event is called.</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample17.cs)]

<span data-ttu-id="127da-273">`Page_Load` 事件處理常式會檢查查詢字串值，並決定是否要顯示成功訊息。</span><span class="sxs-lookup"><span data-stu-id="127da-273">The `Page_Load` event handler checks the query string value and determines whether to show a success message.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="127da-274">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="127da-274">Running the Application</span></span>

<span data-ttu-id="127da-275">您可以立即執行應用程式，以瞭解如何在「購物車」中新增、刪除及更新專案。</span><span class="sxs-lookup"><span data-stu-id="127da-275">You can run the application now to see how you can add, delete, and update items in the shopping cart.</span></span> <span data-ttu-id="127da-276">購物車總計會反映購物車中所有專案的總成本。</span><span class="sxs-lookup"><span data-stu-id="127da-276">The shopping cart total will reflect the total cost of all items in the shopping cart.</span></span>

1. <span data-ttu-id="127da-277">在方案總管中，按**F5**執行 Wingtip 玩具範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="127da-277">In Solution Explorer, press **F5** to run the Wingtip Toys sample application.</span></span>  
   <span data-ttu-id="127da-278">瀏覽器會開啟並顯示*default.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="127da-278">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="127da-279">按一下頁面頂端的 [**登入**] 連結。</span><span class="sxs-lookup"><span data-stu-id="127da-279">Click the **Log in** link at the top of the page.</span></span> 

    ![成員資格和管理-登入連結](membership-and-administration/_static/image2.png)

   <span data-ttu-id="127da-281">[*登入 .aspx* ] 頁面隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="127da-281">The *Login.aspx* page is displayed.</span></span>
3. <span data-ttu-id="127da-282">使用下列使用者名稱和密碼：</span><span class="sxs-lookup"><span data-stu-id="127da-282">Use the following user name and password:</span></span>  
   <span data-ttu-id="127da-283">使用者名稱： canEditUser@wingtiptoys.com</span><span class="sxs-lookup"><span data-stu-id="127da-283">User name: canEditUser@wingtiptoys.com</span></span>  
   <span data-ttu-id="127da-284">密碼： Pa $ $word 1</span><span class="sxs-lookup"><span data-stu-id="127da-284">Password: Pa$$word1</span></span> 

    ![成員資格和管理-登入頁面](membership-and-administration/_static/image3.png)
4. <span data-ttu-id="127da-286">按一下靠近頁面底部的 [**登入**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="127da-286">Click the **Log in** button near the bottom of the page.</span></span>
5. <span data-ttu-id="127da-287">在下一個頁面的頂端，選取 [**管理**] 連結以流覽至 [ *AdminPage* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="127da-287">At the top of the next page, select the **Admin** link to navigate to the *AdminPage.aspx* page.</span></span> 

    ![成員資格和管理-系統管理員連結](membership-and-administration/_static/image4.png)
6. <span data-ttu-id="127da-289">若要測試輸入驗證，請按一下 [**新增產品**] 按鈕，而不新增任何產品詳細資料。</span><span class="sxs-lookup"><span data-stu-id="127da-289">To test the input validation, click the **Add Product** button without adding any product details.</span></span> 

    ![成員資格和管理-系統管理頁面](membership-and-administration/_static/image5.png)

   <span data-ttu-id="127da-291">請注意，會顯示必要的欄位訊息。</span><span class="sxs-lookup"><span data-stu-id="127da-291">Notice that the required field messages are displayed.</span></span>
7. <span data-ttu-id="127da-292">新增新產品的詳細資料，然後按一下 [**新增產品**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="127da-292">Add the details for a new product, and then click the **Add Product** button.</span></span> 

    ![成員資格和管理-新增產品](membership-and-administration/_static/image6.png)
8. <span data-ttu-id="127da-294">從頂端導覽功能表中選取 [**產品**]，以查看您新增的新產品。</span><span class="sxs-lookup"><span data-stu-id="127da-294">Select **Products** from the top navigation menu to view the new product you added.</span></span> 

    ![成員資格和管理-顯示新產品](membership-and-administration/_static/image7.png)
9. <span data-ttu-id="127da-296">按一下 [系統**管理員**] 連結以返回 [管理] 頁面。</span><span class="sxs-lookup"><span data-stu-id="127da-296">Click the **Admin** link to return to the administration page.</span></span>
10. <span data-ttu-id="127da-297">在頁面的 [**移除產品**] 區段中，選取您在**DropDownListBox**中新增的新產品。</span><span class="sxs-lookup"><span data-stu-id="127da-297">In the **Remove Product** section of the page, select the new product you added in the **DropDownListBox**.</span></span>
11. <span data-ttu-id="127da-298">按一下 [**移除產品**] 按鈕，從應用程式中移除新的產品。</span><span class="sxs-lookup"><span data-stu-id="127da-298">Click the **Remove Product** button to remove the new product from the application.</span></span> 

    ![成員資格和管理-移除產品](membership-and-administration/_static/image8.png)
12. <span data-ttu-id="127da-300">從頂端導覽功能表中選取 [**產品**]，確認已移除產品。</span><span class="sxs-lookup"><span data-stu-id="127da-300">Select **Products** from the top navigation menu to confirm that the product has been removed.</span></span>
13. <span data-ttu-id="127da-301">按一下 **[登出]** 以存在系統管理模式。</span><span class="sxs-lookup"><span data-stu-id="127da-301">Click **Log off** to exist administration mode.</span></span>   
    <span data-ttu-id="127da-302">請注意，上方流覽窗格不會再顯示 [**管理**] 功能表項目。</span><span class="sxs-lookup"><span data-stu-id="127da-302">Notice that the top navigation pane no longer shows the **Admin** menu item.</span></span>

## <a name="summary"></a><span data-ttu-id="127da-303">總結</span><span class="sxs-lookup"><span data-stu-id="127da-303">Summary</span></span>

<span data-ttu-id="127da-304">在本教學課程中，您已新增自訂角色和屬於自訂角色的使用者、限制存取管理資料夾和頁面，並為屬於自訂角色的使用者提供導覽。</span><span class="sxs-lookup"><span data-stu-id="127da-304">In this tutorial, you added a custom role and a user belonging to the custom role, restricted access to the administration folder and page, and provided navigation for the user belonging to the custom role.</span></span> <span data-ttu-id="127da-305">您已使用模型系結來填入具有資料的**DropDownList**控制項。</span><span class="sxs-lookup"><span data-stu-id="127da-305">You used model binding to populate a **DropDownList** control with data.</span></span> <span data-ttu-id="127da-306">您已執行**FileUpload**控制項和驗證控制項。</span><span class="sxs-lookup"><span data-stu-id="127da-306">You implemented the **FileUpload** control and validation controls.</span></span> <span data-ttu-id="127da-307">此外，您也已瞭解如何從資料庫新增和移除產品。</span><span class="sxs-lookup"><span data-stu-id="127da-307">Also, you have learned how to add and remove products from a database.</span></span> <span data-ttu-id="127da-308">在下一個教學課程中，您將瞭解如何執行 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="127da-308">In the next tutorial, you'll learn how to implement ASP.NET routing.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="127da-309">其他資源</span><span class="sxs-lookup"><span data-stu-id="127da-309">Additional Resources</span></span>

<span data-ttu-id="127da-310">[Web.config-authorization 元素](https://msdn.microsoft.com/library/8d82143t(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="127da-310">[Web.config - authorization Element](https://msdn.microsoft.com/library/8d82143t(v=vs.100).aspx)</span></span>  
[<span data-ttu-id="127da-311">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="127da-311">ASP.NET Identity</span></span>](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)  
[<span data-ttu-id="127da-312">將具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET Web Forms 應用程式部署至 Azure 網站</span><span class="sxs-lookup"><span data-stu-id="127da-312">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to an Azure Web Site</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="127da-313">Microsoft Azure 免費試用</span><span class="sxs-lookup"><span data-stu-id="127da-313">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> <span data-ttu-id="127da-314">[上一頁](checkout-and-payment-with-paypal.md)
> [下一頁](url-routing.md)</span><span class="sxs-lookup"><span data-stu-id="127da-314">[Previous](checkout-and-payment-with-paypal.md)
[Next](url-routing.md)</span></span>
