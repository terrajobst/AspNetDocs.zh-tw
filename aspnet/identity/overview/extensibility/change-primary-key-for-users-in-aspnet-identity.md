---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: 在 ASP.NET Identity-ASP.NET 4.x 中變更使用者的主要金鑰
author: Rick-Anderson
description: 在 Visual Studio 2013 中，預設 web 應用程式會使用字串值作為使用者帳戶的金鑰。 ASP.NET Identity 可讓您變更的類型 。
ms.author: riande
ms.date: 09/30/2014
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0afea8eacfc646f1489b87629fdb2d437815d88c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584459"
---
# <a name="change-primary-key-for-users-in-aspnet-identity"></a><span data-ttu-id="d6786-104">變更 ASP.NET Identity 中的使用者主索引鍵</span><span class="sxs-lookup"><span data-stu-id="d6786-104">Change Primary Key for Users in ASP.NET Identity</span></span>

<span data-ttu-id="d6786-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d6786-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d6786-106">在 Visual Studio 2013 中，預設 web 應用程式會使用字串值作為使用者帳戶的金鑰。</span><span class="sxs-lookup"><span data-stu-id="d6786-106">In Visual Studio 2013, the default web application uses a string value for the key for user accounts.</span></span> <span data-ttu-id="d6786-107">ASP.NET Identity 可讓您變更金鑰的類型，以符合您的資料需求。</span><span class="sxs-lookup"><span data-stu-id="d6786-107">ASP.NET Identity enables you to change the type of the key to meet your data requirements.</span></span> <span data-ttu-id="d6786-108">例如，您可以將索引鍵的類型從字串變更為整數。</span><span class="sxs-lookup"><span data-stu-id="d6786-108">For example, you can change the type of the key from a string to an integer.</span></span>
> 
> <span data-ttu-id="d6786-109">本主題說明如何從預設 web 應用程式開始，並將使用者帳戶金鑰變更為整數。</span><span class="sxs-lookup"><span data-stu-id="d6786-109">This topic shows how to start with the default web application and change the user account key to an integer.</span></span> <span data-ttu-id="d6786-110">您可以使用相同的修改來在您的專案中執行任何類型的金鑰。</span><span class="sxs-lookup"><span data-stu-id="d6786-110">You can use the same modifications to implement any type of key in your project.</span></span> <span data-ttu-id="d6786-111">它會示範如何在預設 web 應用程式中進行這些變更，但您可以對自訂應用程式套用類似的修改。</span><span class="sxs-lookup"><span data-stu-id="d6786-111">It shows how to make these changes in the default web application, but you could apply similar modifications to a customized application.</span></span> <span data-ttu-id="d6786-112">它會顯示使用 MVC 或 Web Forms 時所需的變更。</span><span class="sxs-lookup"><span data-stu-id="d6786-112">It shows the changes needed when working with MVC or Web Forms.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d6786-113">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="d6786-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="d6786-114">Update 2 （或更新版本）的 Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d6786-114">Visual Studio 2013 with Update 2 (or later)</span></span>
> - <span data-ttu-id="d6786-115">ASP.NET Identity 2.1 或更新版本</span><span class="sxs-lookup"><span data-stu-id="d6786-115">ASP.NET Identity 2.1 or later</span></span>

<span data-ttu-id="d6786-116">若要執行本教學課程中的步驟，您必須擁有 Visual Studio 2013 Update 2 （或更新版本），以及從 ASP.NET Web 應用程式範本建立的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6786-116">To perform the steps in this tutorial, you must have Visual Studio 2013 Update 2 (or later), and a web application created from the ASP.NET Web Application template.</span></span> <span data-ttu-id="d6786-117">在 Update 3 中變更的範本。</span><span class="sxs-lookup"><span data-stu-id="d6786-117">The template changed in Update 3.</span></span> <span data-ttu-id="d6786-118">本主題說明如何在 Update 2 和 Update 3 中變更範本。</span><span class="sxs-lookup"><span data-stu-id="d6786-118">This topic shows how to change the template in Update 2 and Update 3.</span></span>

<span data-ttu-id="d6786-119">本主題包含下列各節：</span><span class="sxs-lookup"><span data-stu-id="d6786-119">This topic contains the following sections:</span></span>

- [<span data-ttu-id="d6786-120">變更身分識別使用者類別中的金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-120">Change the type of the key in the Identity user class</span></span>](#userclass)
- [<span data-ttu-id="d6786-121">新增使用金鑰類型的自訂身分識別類別</span><span class="sxs-lookup"><span data-stu-id="d6786-121">Add customized Identity classes that use the key type</span></span>](#customclass)
- [<span data-ttu-id="d6786-122">將內容類別和使用者管理員變更為使用金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-122">Change the context class and user manager to use the key type</span></span>](#context)
- [<span data-ttu-id="d6786-123">變更啟動設定以使用金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-123">Change start-up configuration to use the key type</span></span>](#startup)
- [<span data-ttu-id="d6786-124">針對含 Update 2 的 MVC，請將 AccountController 變更為傳遞金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-124">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="d6786-125">針對包含 Update 3 的 MVC，請變更 AccountController 和 ManageController 以傳遞金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-125">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="d6786-126">針對含 Update 2 的 Web form，變更帳戶頁面以傳遞金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-126">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="d6786-127">針對包含 Update 3 的 Web form，變更帳戶頁面以傳遞金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-127">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)
- [<span data-ttu-id="d6786-128">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="d6786-128">Run application</span></span>](#run)
- [<span data-ttu-id="d6786-129">其他資源</span><span class="sxs-lookup"><span data-stu-id="d6786-129">Other resources</span></span>](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a><span data-ttu-id="d6786-130">變更身分識別使用者類別中的金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-130">Change the type of the key in the Identity user class</span></span>

<span data-ttu-id="d6786-131">在您從 ASP.NET Web 應用程式範本建立的專案中，指定 ApplicationUser 類別針對使用者帳戶的索引鍵使用整數。</span><span class="sxs-lookup"><span data-stu-id="d6786-131">In your project created from the ASP.NET Web Application template, specify that the ApplicationUser class uses an integer for the key for user accounts.</span></span> <span data-ttu-id="d6786-132">在 IdentityModels.cs 中，變更 ApplicationUser 類別，使其繼承自 TKey 泛型參數類型為**int**的 IdentityUser。</span><span class="sxs-lookup"><span data-stu-id="d6786-132">In IdentityModels.cs, change the ApplicationUser class to inherit from IdentityUser that has a type of **int** for the TKey generic parameter.</span></span> <span data-ttu-id="d6786-133">您也會傳遞您尚未實行之三個自訂類別的名稱。</span><span class="sxs-lookup"><span data-stu-id="d6786-133">You also pass the names of three customized class which you have not implemented yet.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

<span data-ttu-id="d6786-134">您已變更金鑰的類型，但根據預設，應用程式的其餘部分仍會假設索引鍵為字串。</span><span class="sxs-lookup"><span data-stu-id="d6786-134">You have changed the type of the key, but, by default, the rest of the application still assumes the key is a string.</span></span> <span data-ttu-id="d6786-135">您必須在採用字串的程式碼中明確指出金鑰的類型。</span><span class="sxs-lookup"><span data-stu-id="d6786-135">You must explicitly indicate the type of the key in code that assumes a string.</span></span>

<span data-ttu-id="d6786-136">在**ApplicationUser**類別中，將**GenerateUserIdentityAsync**方法變更為包含 int，如下列反白顯示的程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="d6786-136">In the **ApplicationUser** class, change the **GenerateUserIdentityAsync** method to include int, as shown in the highlighted code below.</span></span> <span data-ttu-id="d6786-137">具有 Update 3 範本的 Web form 專案不需要進行這種變更。</span><span class="sxs-lookup"><span data-stu-id="d6786-137">This change is not necessary for Web Forms projects with the Update 3 template.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a><span data-ttu-id="d6786-138">新增使用金鑰類型的自訂身分識別類別</span><span class="sxs-lookup"><span data-stu-id="d6786-138">Add customized Identity classes that use the key type</span></span>

<span data-ttu-id="d6786-139">其他身分識別類別，例如 IdentityUserRole、IdentityUserClaim、IdentityUserLogin、IdentityRole、UserStore、RoleStore，仍然會設定為使用字串索引鍵。</span><span class="sxs-lookup"><span data-stu-id="d6786-139">The other Identity classes, such as IdentityUserRole, IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore, are still set up to use a string key.</span></span> <span data-ttu-id="d6786-140">建立這些類別的新版本，以指定索引鍵的整數。</span><span class="sxs-lookup"><span data-stu-id="d6786-140">Create new versions of these classes that specify an integer for the key.</span></span> <span data-ttu-id="d6786-141">您不需要在這些類別中提供大量的實作為程式碼，您主要只是將 int 設定為索引鍵。</span><span class="sxs-lookup"><span data-stu-id="d6786-141">You do not need to provide much implementation code in these classes, you are primarily just setting int as the key.</span></span>

<span data-ttu-id="d6786-142">將下列類別新增至您的 IdentityModels.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="d6786-142">Add the following classes to your IdentityModels.cs file.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a><span data-ttu-id="d6786-143">將內容類別和使用者管理員變更為使用金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-143">Change the context class and user manager to use the key type</span></span>

<span data-ttu-id="d6786-144">在 IdentityModels.cs 中，變更 **[applicationdbcoNtext]** 類別的定義，以使用新的自訂類別和金鑰的**int** ，如反白顯示的程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="d6786-144">In IdentityModels.cs, change the definition of the **ApplicationDbContext** class to use your new customized classes and an **int** for the key, as shown in the highlighted code.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

<span data-ttu-id="d6786-145">ThrowIfV1Schema 參數在此函式中已不再有效。</span><span class="sxs-lookup"><span data-stu-id="d6786-145">The ThrowIfV1Schema parameter is no longer valid in the constructor.</span></span> <span data-ttu-id="d6786-146">變更此函式，使其不會傳遞 ThrowIfV1Schema 值。</span><span class="sxs-lookup"><span data-stu-id="d6786-146">Change the constructor so it does not pass a ThrowIfV1Schema value.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

<span data-ttu-id="d6786-147">開啟 IdentityConfig.cs，然後變更**ApplicationUserManger**類別，以使用新的使用者存放區類別來保存資料，並將金鑰設為**int** 。</span><span class="sxs-lookup"><span data-stu-id="d6786-147">Open IdentityConfig.cs, and change the **ApplicationUserManger** class to use your new user store class for persisting data and an **int** for the key.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

<span data-ttu-id="d6786-148">在 Update 3 範本中，您必須變更 ApplicationSignInManager 類別。</span><span class="sxs-lookup"><span data-stu-id="d6786-148">In the Update 3 template, you must change the ApplicationSignInManager class.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a><span data-ttu-id="d6786-149">變更啟動設定以使用金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-149">Change start-up configuration to use the key type</span></span>

<span data-ttu-id="d6786-150">在 Startup.Auth.cs 中，取代 OnValidateIdentity 程式碼，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d6786-150">In Startup.Auth.cs, replace the OnValidateIdentity code, as highlighted below.</span></span> <span data-ttu-id="d6786-151">請注意，getUserIdCallback 定義會將字串值剖析成整數。</span><span class="sxs-lookup"><span data-stu-id="d6786-151">Notice that the getUserIdCallback definition, parses the string value into an integer.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

<span data-ttu-id="d6786-152">如果您的專案無法辨識**GetUserId**方法的一般執行，您可能需要將 ASP.NET Identity NuGet 套件更新為2.1 版</span><span class="sxs-lookup"><span data-stu-id="d6786-152">If your project does not recognize the generic implementation of the **GetUserId** method, you may need to update the ASP.NET Identity NuGet package to version 2.1</span></span>

<span data-ttu-id="d6786-153">您對 ASP.NET Identity 所使用的基礎結構類別進行了許多變更。</span><span class="sxs-lookup"><span data-stu-id="d6786-153">You have made a lot of changes to the infrastructure classes used by ASP.NET Identity.</span></span> <span data-ttu-id="d6786-154">如果您嘗試編譯專案，您會發現很多錯誤。</span><span class="sxs-lookup"><span data-stu-id="d6786-154">If you try compiling the project, you will notice a lot of errors.</span></span> <span data-ttu-id="d6786-155">幸運的是，其餘的錯誤全都很類似。</span><span class="sxs-lookup"><span data-stu-id="d6786-155">Fortunately, the remaining errors are all similar.</span></span> <span data-ttu-id="d6786-156">識別類別的索引鍵必須是整數，但控制器（或 Web Form）會傳遞字串值。</span><span class="sxs-lookup"><span data-stu-id="d6786-156">The Identity class expects an integer for the key, but the controller (or Web Form) is passing a string value.</span></span> <span data-ttu-id="d6786-157">在每個案例中，您都需要呼叫**GetUserId&lt;int&gt;** ，從字串轉換為和整數。</span><span class="sxs-lookup"><span data-stu-id="d6786-157">In each case, you need to convert from a string to and integer by calling **GetUserId&lt;int&gt;**.</span></span> <span data-ttu-id="d6786-158">您可以從編譯完成錯誤清單，或遵循下列變更。</span><span class="sxs-lookup"><span data-stu-id="d6786-158">You can either work through the error list from compilation or follow the changes below.</span></span>

<span data-ttu-id="d6786-159">其餘的變更取決於您要建立的專案類型，以及您在 Visual Studio 中安裝的更新。</span><span class="sxs-lookup"><span data-stu-id="d6786-159">The remaining changes depend on the type of project you are creating and which update you have installed in Visual Studio.</span></span> <span data-ttu-id="d6786-160">您可以透過下列連結直接前往相關章節</span><span class="sxs-lookup"><span data-stu-id="d6786-160">You can go directly to the relevant section through the following links</span></span>

- [<span data-ttu-id="d6786-161">針對含 Update 2 的 MVC，請將 AccountController 變更為傳遞金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-161">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="d6786-162">針對包含 Update 3 的 MVC，請變更 AccountController 和 ManageController 以傳遞金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-162">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="d6786-163">針對含 Update 2 的 Web form，變更帳戶頁面以傳遞金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-163">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="d6786-164">針對包含 Update 3 的 Web form，變更帳戶頁面以傳遞金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-164">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a><span data-ttu-id="d6786-165">針對含 Update 2 的 MVC，請將 AccountController 變更為傳遞金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-165">For MVC with Update 2, change the AccountController to pass the key type</span></span>

<span data-ttu-id="d6786-166">開啟 AccountController.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="d6786-166">Open the AccountController.cs file.</span></span> <span data-ttu-id="d6786-167">您需要變更下列方法。</span><span class="sxs-lookup"><span data-stu-id="d6786-167">You need to change the following methods.</span></span>

<span data-ttu-id="d6786-168">**ConfirmEmail**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-168">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

<span data-ttu-id="d6786-169">取消**關聯**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-169">**Disassociate** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

<span data-ttu-id="d6786-170">**管理（ManageUserViewModel）** 方法</span><span class="sxs-lookup"><span data-stu-id="d6786-170">**Manage(ManageUserViewModel)** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

<span data-ttu-id="d6786-171">**LinkLoginCallback**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-171">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

<span data-ttu-id="d6786-172">**RemoveAccountList**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-172">**RemoveAccountList** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

<span data-ttu-id="d6786-173">**HasPassword**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-173">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

<span data-ttu-id="d6786-174">您現在可以[執行應用程式](#run)，並註冊新的使用者。</span><span class="sxs-lookup"><span data-stu-id="d6786-174">You can now [run the application](#run) and register a new user.</span></span>

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a><span data-ttu-id="d6786-175">針對包含 Update 3 的 MVC，請變更 AccountController 和 ManageController 以傳遞金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-175">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>

<span data-ttu-id="d6786-176">開啟 AccountController.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="d6786-176">Open the AccountController.cs file.</span></span> <span data-ttu-id="d6786-177">您需要變更下列方法。</span><span class="sxs-lookup"><span data-stu-id="d6786-177">You need to change the following method.</span></span>

<span data-ttu-id="d6786-178">**ConfirmEmail**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-178">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

<span data-ttu-id="d6786-179">**SendCode**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-179">**SendCode** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

<span data-ttu-id="d6786-180">開啟 ManageController.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="d6786-180">Open the ManageController.cs file.</span></span> <span data-ttu-id="d6786-181">您需要變更下列方法。</span><span class="sxs-lookup"><span data-stu-id="d6786-181">You need to change the following methods.</span></span>

<span data-ttu-id="d6786-182">**Index**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-182">**Index** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

<span data-ttu-id="d6786-183">**RemoveLogin**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-183">**RemoveLogin** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

<span data-ttu-id="d6786-184">**AddPhoneNumber**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-184">**AddPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

<span data-ttu-id="d6786-185">**EnableTwoFactorAuthentication**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-185">**EnableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

<span data-ttu-id="d6786-186">**DisableTwoFactorAuthentication**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-186">**DisableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

<span data-ttu-id="d6786-187">**VerifyPhoneNumber**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-187">**VerifyPhoneNumber** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

<span data-ttu-id="d6786-188">**RemovePhoneNumber**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-188">**RemovePhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

<span data-ttu-id="d6786-189">**ChangePassword**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-189">**ChangePassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

<span data-ttu-id="d6786-190">**SetPassword**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-190">**SetPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

<span data-ttu-id="d6786-191">**ManageLogins**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-191">**ManageLogins** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

<span data-ttu-id="d6786-192">**LinkLoginCallback**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-192">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

<span data-ttu-id="d6786-193">**HasPassword**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-193">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

<span data-ttu-id="d6786-194">**HasPhoneNumber**方法</span><span class="sxs-lookup"><span data-stu-id="d6786-194">**HasPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

<span data-ttu-id="d6786-195">您現在可以[執行應用程式](#run)，並註冊新的使用者。</span><span class="sxs-lookup"><span data-stu-id="d6786-195">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="d6786-196">針對含 Update 2 的 Web form，變更帳戶頁面以傳遞金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-196">For Web Forms with Update 2, change Account pages to pass the key type</span></span>

<span data-ttu-id="d6786-197">針對含 Update 2 的 Web form，您必須變更下列頁面。</span><span class="sxs-lookup"><span data-stu-id="d6786-197">For Web Forms with Update 2, you need to change the following pages.</span></span>

<span data-ttu-id="d6786-198">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="d6786-198">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

<span data-ttu-id="d6786-199">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="d6786-199">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

<span data-ttu-id="d6786-200">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="d6786-200">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

<span data-ttu-id="d6786-201">您現在可以[執行應用程式](#run)，並註冊新的使用者。</span><span class="sxs-lookup"><span data-stu-id="d6786-201">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="d6786-202">針對包含 Update 3 的 Web form，變更帳戶頁面以傳遞金鑰類型</span><span class="sxs-lookup"><span data-stu-id="d6786-202">For Web Forms with Update 3, change Account pages to pass the key type</span></span>

<span data-ttu-id="d6786-203">針對具有 Update 3 的 Web form，您必須變更下列頁面。</span><span class="sxs-lookup"><span data-stu-id="d6786-203">For Web Forms with Update 3, you need to change the following pages.</span></span>

<span data-ttu-id="d6786-204">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="d6786-204">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

<span data-ttu-id="d6786-205">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="d6786-205">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

<span data-ttu-id="d6786-206">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="d6786-206">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

<span data-ttu-id="d6786-207">**VerifyPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="d6786-207">**VerifyPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

<span data-ttu-id="d6786-208">**AddPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="d6786-208">**AddPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

<span data-ttu-id="d6786-209">**ManagePassword.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="d6786-209">**ManagePassword.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

<span data-ttu-id="d6786-210">**ManageLogins.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="d6786-210">**ManageLogins.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

<span data-ttu-id="d6786-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="d6786-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a><span data-ttu-id="d6786-212">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="d6786-212">Run application</span></span>

<span data-ttu-id="d6786-213">您已完成預設 Web 應用程式範本所需的所有變更。</span><span class="sxs-lookup"><span data-stu-id="d6786-213">You have finished all of the required changes to the default Web Application template.</span></span> <span data-ttu-id="d6786-214">執行應用程式，並註冊新的使用者。</span><span class="sxs-lookup"><span data-stu-id="d6786-214">Run the application and register a new user.</span></span> <span data-ttu-id="d6786-215">註冊使用者之後，您會注意到 AspNetUsers 資料表的識別碼資料行是整數。</span><span class="sxs-lookup"><span data-stu-id="d6786-215">After registering the user, you will notice that the AspNetUsers table has an Id column that is an integer.</span></span>

![新的主要金鑰](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

<span data-ttu-id="d6786-217">如果您先前已使用不同的主鍵建立 ASP.NET Identity 資料表，您需要進行一些額外的變更。</span><span class="sxs-lookup"><span data-stu-id="d6786-217">If you have previously created the ASP.NET Identity tables with a different primary key, you need to make some additional changes.</span></span> <span data-ttu-id="d6786-218">可能的話，只要刪除現有的資料庫即可。</span><span class="sxs-lookup"><span data-stu-id="d6786-218">If possible, just delete the existing database.</span></span> <span data-ttu-id="d6786-219">當您執行 web 應用程式並加入新的使用者時，將會使用正確的設計來重新建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="d6786-219">The database will be re-created with the correct design when you run the web application and add a new user.</span></span> <span data-ttu-id="d6786-220">如果無法刪除，請執行 code first 遷移來變更資料表。</span><span class="sxs-lookup"><span data-stu-id="d6786-220">If deletion is not possible, run code first migrations to change the tables.</span></span> <span data-ttu-id="d6786-221">不過，新的整數主鍵不會設定為資料庫中的 SQL 識別屬性。</span><span class="sxs-lookup"><span data-stu-id="d6786-221">However, the new integer primary key will not be set up as a SQL IDENTITY property in the database.</span></span> <span data-ttu-id="d6786-222">您必須以手動方式將 Id 資料行設定為身分識別。</span><span class="sxs-lookup"><span data-stu-id="d6786-222">You must manually set the Id column as an IDENTITY.</span></span>

<a id="other"></a>
## <a name="other-resources"></a><span data-ttu-id="d6786-223">其他資源</span><span class="sxs-lookup"><span data-stu-id="d6786-223">Other resources</span></span>

- [<span data-ttu-id="d6786-224">ASP.NET Identity 的自訂儲存體提供者概觀</span><span class="sxs-lookup"><span data-stu-id="d6786-224">Overview of Custom Storage Providers for ASP.NET Identity</span></span>](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [<span data-ttu-id="d6786-225">將現有的網站從 SQL 成員資格移轉至 ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="d6786-225">Migrating an Existing Website from SQL Membership to ASP.NET Identity</span></span>](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [<span data-ttu-id="d6786-226">將成員資格和使用者設定檔的通用提供者資料移轉至 ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="d6786-226">Migrating Universal Provider Data for Membership and User Profiles to ASP.NET Identity</span></span>](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- <span data-ttu-id="d6786-227">具有變更之主要金鑰的[範例應用程式](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK)</span><span class="sxs-lookup"><span data-stu-id="d6786-227">[Sample application](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) with changed primary key</span></span>
