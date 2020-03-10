---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
title: 使用表單驗證驗證使用者（VB） |Microsoft Docs
author: microsoft
description: 瞭解如何使用 [授權] 屬性來保護 MVC 應用程式中的特定頁面。 您也會瞭解如何使用網站管理 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 4341f5b1-6fe5-44c5-8b8a-18fa84f80177
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: a2c2140631d59a7f8b21aa73613a92ea5c7a91d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615574"
---
# <a name="authenticating-users-with-forms-authentication-vb"></a><span data-ttu-id="8cd97-104">使用表單驗證驗證使用者 (VB)</span><span class="sxs-lookup"><span data-stu-id="8cd97-104">Authenticating Users with Forms Authentication (VB)</span></span>

<span data-ttu-id="8cd97-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8cd97-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="8cd97-106">瞭解如何使用 [授權] 屬性來保護 MVC 應用程式中的特定頁面。</span><span class="sxs-lookup"><span data-stu-id="8cd97-106">Learn how to use the [Authorize] attribute to password protect particular pages in your MVC application.</span></span> <span data-ttu-id="8cd97-107">您將瞭解如何使用網站管理工具來建立及管理使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="8cd97-107">You learn how to use the Web Site Administration Tool to create and manage users and roles.</span></span> <span data-ttu-id="8cd97-108">您也會瞭解如何設定儲存使用者帳戶和角色資訊的位置。</span><span class="sxs-lookup"><span data-stu-id="8cd97-108">You also learn how to configure where user account and role information is stored.</span></span>

<span data-ttu-id="8cd97-109">本教學課程的目的是要說明如何使用表單驗證來保護 ASP.NET MVC 應用程式中的觀點。</span><span class="sxs-lookup"><span data-stu-id="8cd97-109">The goal of this tutorial is to explain how you can use Forms authentication to password protect the views in your ASP.NET MVC applications.</span></span> <span data-ttu-id="8cd97-110">您將瞭解如何使用網站管理工具來建立使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="8cd97-110">You learn how to use the Web Site Administration Tool to create users and roles.</span></span> <span data-ttu-id="8cd97-111">您也將瞭解如何防止未經授權的使用者叫用控制器動作。</span><span class="sxs-lookup"><span data-stu-id="8cd97-111">You also learn how to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="8cd97-112">最後，您將瞭解如何設定儲存使用者名稱和密碼的位置。</span><span class="sxs-lookup"><span data-stu-id="8cd97-112">Finally, you learn how to configure where user names and passwords are stored.</span></span>

#### <a name="using-the-web-site-administration-tool"></a><span data-ttu-id="8cd97-113">使用網站管理工具</span><span class="sxs-lookup"><span data-stu-id="8cd97-113">Using the Web Site Administration Tool</span></span>

<span data-ttu-id="8cd97-114">在進行其他動作之前，我們應該先建立一些使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="8cd97-114">Before we do anything else, we should start by creating some users and roles.</span></span> <span data-ttu-id="8cd97-115">建立新使用者和角色最簡單的方式，就是利用 Visual Studio 2008 的網站管理工具。</span><span class="sxs-lookup"><span data-stu-id="8cd97-115">The easiest way to create new users and roles is to take advantage of the Visual Studio 2008 Web Site Administration Tool.</span></span> <span data-ttu-id="8cd97-116">您可以藉由選取 [專案]、[ **ASP.NET**設定] 功能表選項來啟動此工具。</span><span class="sxs-lookup"><span data-stu-id="8cd97-116">You can launch this tool by selecting the menu option **Project, ASP.NET Configuration**.</span></span> <span data-ttu-id="8cd97-117">或者，您也可以藉由按一下 hammer 的（有點令人驚訝的）圖示來啟動網站管理工具，這是出現在 [方案總管] 視窗頂端的世界（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="8cd97-117">Alternatively, you can launch the Web Site Administration Tool by clicking the (somewhat scary) icon of the hammer hitting the world that appears at the top of the Solution Explorer window (see Figure 1).</span></span>

<span data-ttu-id="8cd97-118">**圖1–啟動網站管理工具**</span><span class="sxs-lookup"><span data-stu-id="8cd97-118">**Figure 1 – Launching the Web Site Administration Tool**</span></span>

![clip_image002 [4]](authenticating-users-with-forms-authentication-vb/_static/image1.jpg)

<span data-ttu-id="8cd97-120">在網站管理工具中，您可以藉由選取 [安全性] 索引標籤來建立新的使用者和角色。按一下 [**建立使用者**] 連結以建立名為 Stephen 的新使用者（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="8cd97-120">Within the Web Site Administration Tool, you create new users and roles by selecting the Security tab. Click the **Create user** link to create a new user named Stephen (see Figure 2).</span></span> <span data-ttu-id="8cd97-121">為 Stephen 使用者提供您想要的任何密碼（例如，*秘密*）。</span><span class="sxs-lookup"><span data-stu-id="8cd97-121">Provide the Stephen user with any password that you want (for example, *secret*).</span></span>

<span data-ttu-id="8cd97-122">**圖2–建立新的使用者**</span><span class="sxs-lookup"><span data-stu-id="8cd97-122">**Figure 2 – Creating a new user**</span></span>

![clip_image004 [4]](authenticating-users-with-forms-authentication-vb/_static/image2.jpg)

<span data-ttu-id="8cd97-124">您可以藉由先啟用角色並定義一或多個角色來建立新的角色。</span><span class="sxs-lookup"><span data-stu-id="8cd97-124">You create new roles by first enabling roles and defining one or more roles.</span></span> <span data-ttu-id="8cd97-125">按一下 [**啟用角色**] 連結來啟用角色。</span><span class="sxs-lookup"><span data-stu-id="8cd97-125">Enable roles by clicking the **Enable roles** link.</span></span> <span data-ttu-id="8cd97-126">接下來，按一下 [**建立或管理角色**] 連結來建立名為 [系統*管理員*] 的角色（請參閱 [圖 3]）。</span><span class="sxs-lookup"><span data-stu-id="8cd97-126">Next, create a role named *Administrators* by clicking the **Create or Manage roles** link (see Figure 3).</span></span>

<span data-ttu-id="8cd97-127">**圖3–建立新的角色**</span><span class="sxs-lookup"><span data-stu-id="8cd97-127">**Figure 3 – Creating a new role**</span></span>

![clip_image006 [4]](authenticating-users-with-forms-authentication-vb/_static/image3.jpg)

<span data-ttu-id="8cd97-129">最後，建立名為 Sally 的新使用者，並在建立 Sally 時，按一下 [建立使用者] 連結並選取 [系統管理員]，將 Sally 與系統管理員角色建立關聯（請參閱 [圖 4]）。</span><span class="sxs-lookup"><span data-stu-id="8cd97-129">Finally, create a new user named Sally and associate Sally with the Administrators role by clicking the Create User link and selecting Administrators when creating Sally (see Figure 4).</span></span>

<span data-ttu-id="8cd97-130">**圖4–將使用者新增至角色**</span><span class="sxs-lookup"><span data-stu-id="8cd97-130">**Figure 4 – Adding a user to a role**</span></span>

![clip_image008 [4]](authenticating-users-with-forms-authentication-vb/_static/image4.jpg)

<span data-ttu-id="8cd97-132">當所有動作都已完成，您應該有兩個名為 Stephen 和 Sally 的新使用者。</span><span class="sxs-lookup"><span data-stu-id="8cd97-132">When all is said and done, you should have two new users named Stephen and Sally.</span></span> <span data-ttu-id="8cd97-133">您也應該有一個名為 [系統管理員] 的新角色。</span><span class="sxs-lookup"><span data-stu-id="8cd97-133">You should also have a new role named Administrators.</span></span> <span data-ttu-id="8cd97-134">Sally 是 Administrators 角色的成員，而 Stephen 則不是。</span><span class="sxs-lookup"><span data-stu-id="8cd97-134">Sally is a member of the Administrators role and Stephen is not.</span></span>

#### <a name="requiring-authorization"></a><span data-ttu-id="8cd97-135">需要授權</span><span class="sxs-lookup"><span data-stu-id="8cd97-135">Requiring Authorization</span></span>

<span data-ttu-id="8cd97-136">您可以要求使用者在使用者叫用控制器動作之前進行驗證，方法是在動作中新增 [授權] 屬性。</span><span class="sxs-lookup"><span data-stu-id="8cd97-136">You can require a user to be authenticated before the user invokes a controller action by adding the [Authorize] attribute to the action.</span></span> <span data-ttu-id="8cd97-137">您可以將 [授權] 屬性套用至個別的控制器動作，也可以將此屬性套用至整個控制器類別。</span><span class="sxs-lookup"><span data-stu-id="8cd97-137">You can apply the [Authorize] attribute to an individual controller action or you can apply this attribute to an entire controller class.</span></span>

<span data-ttu-id="8cd97-138">例如，[清單 1] 中的控制器會公開名為 CompanySecrets （）的動作。</span><span class="sxs-lookup"><span data-stu-id="8cd97-138">For example, the controller in Listing 1 exposes an action named CompanySecrets().</span></span> <span data-ttu-id="8cd97-139">由於此動作是以 [授權] 屬性裝飾，因此除非使用者經過驗證，否則無法叫用此動作。</span><span class="sxs-lookup"><span data-stu-id="8cd97-139">Because this action is decorated with the [Authorize] attribute, this action cannot be invoked unless a user is authenticated.</span></span>

<span data-ttu-id="8cd97-140">**清單1– Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="8cd97-140">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample1.vb)]

<span data-ttu-id="8cd97-141">如果您藉由在瀏覽器的網址列中輸入 URL/Home/CompanySecrets 來叫用 CompanySecrets （）動作，而且您不是已驗證的使用者，則系統會自動將您重新導向至登入視圖（請參閱 [圖 5]）。</span><span class="sxs-lookup"><span data-stu-id="8cd97-141">If you invoke the CompanySecrets() action by entering the URL /Home/CompanySecrets in the address bar of your browser, and you are not an authenticated user, then you will be redirected to the Login view automatically (see Figure 5).</span></span>

<span data-ttu-id="8cd97-142">**[圖 5] –登入視圖**</span><span class="sxs-lookup"><span data-stu-id="8cd97-142">**Figure 5 – The Login view**</span></span>

![clip_image010 [4]](authenticating-users-with-forms-authentication-vb/_static/image5.jpg)

<span data-ttu-id="8cd97-144">您可以使用登入視圖來輸入您的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="8cd97-144">You can use the Login view to enter your user name and password.</span></span> <span data-ttu-id="8cd97-145">如果您不是已註冊的使用者，則可以按一下 [**註冊**] 連結以流覽至 [註冊] 視圖（請參閱 [圖 6]）。</span><span class="sxs-lookup"><span data-stu-id="8cd97-145">If you are not a registered user then you can click the **register** link to navigate to the Register view (see Figure 6).</span></span> <span data-ttu-id="8cd97-146">您可以使用 [註冊] 視圖來建立新的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="8cd97-146">You can use the Register view to create a new user account.</span></span>

<span data-ttu-id="8cd97-147">**圖6–註冊視圖**</span><span class="sxs-lookup"><span data-stu-id="8cd97-147">**Figure 6 – The Register view**</span></span>

![clip_image012](authenticating-users-with-forms-authentication-vb/_static/image6.jpg)

<span data-ttu-id="8cd97-149">成功登入之後，您可以看到 [CompanySecrets] 視圖（請參閱 [圖 7]）。</span><span class="sxs-lookup"><span data-stu-id="8cd97-149">After you successfully log in, you can see the CompanySecrets view (see Figure 7).</span></span> <span data-ttu-id="8cd97-150">根據預設，您會繼續登入，直到您關閉瀏覽器視窗為止。</span><span class="sxs-lookup"><span data-stu-id="8cd97-150">By default, you will continue to be logged in until you close your browser window.</span></span>

<span data-ttu-id="8cd97-151">**圖7– CompanySecrets 視圖**</span><span class="sxs-lookup"><span data-stu-id="8cd97-151">**Figure 7 – The CompanySecrets view**</span></span>

![clip_image014](authenticating-users-with-forms-authentication-vb/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a><span data-ttu-id="8cd97-153">依使用者名稱或使用者角色授權</span><span class="sxs-lookup"><span data-stu-id="8cd97-153">Authorizing by User Name or User Role</span></span>

<span data-ttu-id="8cd97-154">您可以使用 [授權] 屬性，將控制器動作的存取限制為一組特定的使用者或一組特定的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="8cd97-154">You can use the [Authorize] attribute to restrict access to a controller action to a particular set of users or a particular set of user roles.</span></span> <span data-ttu-id="8cd97-155">例如，[清單 2] 中修改後的主控制器包含兩個名為 StephenSecrets （）和 AdministratorSecrets （）的新動作。</span><span class="sxs-lookup"><span data-stu-id="8cd97-155">For example, the modified Home controller in Listing 2 contains two new actions named StephenSecrets() and AdministratorSecrets().</span></span>

<span data-ttu-id="8cd97-156">**清單2– Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="8cd97-156">**Listing 2 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample2.vb)]

<span data-ttu-id="8cd97-157">只有具有使用者名稱 Stephen 的使用者可以叫用 StephenSecrets （）動作。</span><span class="sxs-lookup"><span data-stu-id="8cd97-157">Only a user with the user name Stephen can invoke the StephenSecrets() action.</span></span> <span data-ttu-id="8cd97-158">所有其他使用者都會被重新導向至登入視圖。</span><span class="sxs-lookup"><span data-stu-id="8cd97-158">All other users get redirected to the Login view.</span></span> <span data-ttu-id="8cd97-159">Users 屬性會接受以逗號分隔的使用者帳戶名稱清單。</span><span class="sxs-lookup"><span data-stu-id="8cd97-159">The Users property accepts a comma separated list of user account names.</span></span>

<span data-ttu-id="8cd97-160">只有系統管理員（Administrators）角色中的使用者可以叫用 AdministratorSecrets （）動作。</span><span class="sxs-lookup"><span data-stu-id="8cd97-160">Only users in the Administrators role can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="8cd97-161">例如，因為 Sally 是 Administrators 群組的成員，所以她可以叫用 AdministratorSecrets （）動作。</span><span class="sxs-lookup"><span data-stu-id="8cd97-161">For example, because Sally is a member of the Administrators group, she can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="8cd97-162">所有其他使用者都會被重新導向至登入視圖。</span><span class="sxs-lookup"><span data-stu-id="8cd97-162">All other users get redirected to the Login view.</span></span> <span data-ttu-id="8cd97-163">[角色] 屬性會接受以逗號分隔的角色名稱清單。</span><span class="sxs-lookup"><span data-stu-id="8cd97-163">The Roles property accepts a comma separated list of role names.</span></span>

#### <a name="configuring-authentication"></a><span data-ttu-id="8cd97-164">設定驗證</span><span class="sxs-lookup"><span data-stu-id="8cd97-164">Configuring Authentication</span></span>

<span data-ttu-id="8cd97-165">此時，您可能會想知道使用者帳戶和角色資訊的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="8cd97-165">At this point, you might be wondering where the user account and role information is being stored.</span></span> <span data-ttu-id="8cd97-166">根據預設，資訊會儲存在位於 MVC 應用程式之應用程式\_Data 資料夾中名為 ASPNETDB.MDF 的（RANU） SQL Express 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="8cd97-166">By default, the information is stored in a (RANU) SQL Express database named ASPNETDB.mdf located in your MVC application's App\_Data folder.</span></span> <span data-ttu-id="8cd97-167">當您開始使用成員資格時，ASP.NET 架構會自動產生此資料庫。</span><span class="sxs-lookup"><span data-stu-id="8cd97-167">This database is generated by the ASP.NET framework automatically when you start using membership.</span></span>

<span data-ttu-id="8cd97-168">若要在 [方案總管] 視窗中看到 ASPNETDB.MDF .mdf 資料庫，您必須先選取 [功能表選項] [專案]、[顯示所有檔案]。</span><span class="sxs-lookup"><span data-stu-id="8cd97-168">In order to see the ASPNETDB.mdf database in the Solution Explorer window, you first need to select the menu option Project, Show All Files.</span></span>

<span data-ttu-id="8cd97-169">在開發應用程式時，使用預設的 SQL Express 資料庫是正常的。</span><span class="sxs-lookup"><span data-stu-id="8cd97-169">Using the default SQL Express database is fine when developing an application.</span></span> <span data-ttu-id="8cd97-170">不過，最有可能的情況是，您不會想要針對生產應用程式使用預設的 ASPNETDB.MDF .mdf 資料庫。</span><span class="sxs-lookup"><span data-stu-id="8cd97-170">Most likely, however, you won't want to use the default ASPNETDB.mdf database for a production application.</span></span> <span data-ttu-id="8cd97-171">在這種情況下，您可以藉由完成下列兩個步驟來變更儲存使用者帳戶資訊的位置：</span><span class="sxs-lookup"><span data-stu-id="8cd97-171">In that case, you can change where user account information is stored by completing the following two steps:</span></span>

1. <span data-ttu-id="8cd97-172">將應用程式服務資料庫物件新增至您的生產環境資料庫-變更應用程式連接字串以指向您的實際執行資料庫</span><span class="sxs-lookup"><span data-stu-id="8cd97-172">Add the Application Services database objects to your production database - Change your application connection string to point to your production database</span></span>

<span data-ttu-id="8cd97-173">第一個步驟是將所有必要的資料庫物件（資料表和預存程式）新增至您的生產環境資料庫。</span><span class="sxs-lookup"><span data-stu-id="8cd97-173">The first step is to add all of the necessary database objects (tables and stored procedures) to your production database.</span></span> <span data-ttu-id="8cd97-174">將這些物件新增至新資料庫的最簡單方式，就是利用 ASP.NET SQL Server 安裝程式 Wizard （請參閱 [圖 8]）。</span><span class="sxs-lookup"><span data-stu-id="8cd97-174">The easiest way to add these objects to a new database is to take advantage of the ASP.NET SQL Server Setup Wizard (see Figure 8).</span></span> <span data-ttu-id="8cd97-175">您可以從 Microsoft Visual Studio 2008 程式群組開啟 Visual Studio 2008 命令提示字元，並從命令提示字元執行下列命令，以啟動此工具：</span><span class="sxs-lookup"><span data-stu-id="8cd97-175">You can launch this tool by opening the Visual Studio 2008 Command Prompt from the Microsoft Visual Studio 2008 program group and executing the following command from the command prompt:</span></span>

<span data-ttu-id="8cd97-176">aspnet\_regsql</span><span class="sxs-lookup"><span data-stu-id="8cd97-176">aspnet\_regsql</span></span>

<span data-ttu-id="8cd97-177">**圖8– ASP.NET SQL Server 安裝程式 Wizard**</span><span class="sxs-lookup"><span data-stu-id="8cd97-177">**Figure 8 – The ASP.NET SQL Server Setup Wizard**</span></span>

![clip_image016](authenticating-users-with-forms-authentication-vb/_static/image8.jpg)

<span data-ttu-id="8cd97-179">[ASP.NET SQL Server 安裝程式] 會讓您選取網路上的 SQL Server 資料庫，並安裝 ASP.NET 應用程式服務所需的所有資料庫物件。</span><span class="sxs-lookup"><span data-stu-id="8cd97-179">The ASP.NET SQL Server Setup Wizard enables you to select a SQL Server database on your network and install all of the database objects required by the ASP.NET application services.</span></span> <span data-ttu-id="8cd97-180">資料庫伺服器不一定要位於您的本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="8cd97-180">The database server is not required to be located on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="8cd97-181">如果您不想使用 [ASP.NET SQL Server 安裝程式]，您可以在下列資料夾中找到用於新增應用程式服務資料庫物件的 SQL 腳本：</span><span class="sxs-lookup"><span data-stu-id="8cd97-181">If you don't want to use the ASP.NET SQL Server Setup Wizard, then you can find SQL scripts for adding the application services database objects in the following folder:</span></span>
> 
> 
> <span data-ttu-id="8cd97-182">C：\Windows\Microsoft.NET\Framework\v2.0.50727</span><span class="sxs-lookup"><span data-stu-id="8cd97-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span></span>

<span data-ttu-id="8cd97-183">建立必要的資料庫物件之後，您必須修改 MVC 應用程式所使用的資料庫連接。</span><span class="sxs-lookup"><span data-stu-id="8cd97-183">After you create the necessary database objects, you need to modify the database connection used by your MVC application.</span></span> <span data-ttu-id="8cd97-184">修改 web 設定（web.config）檔案中的 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 連接字串，使其指向實際執行的資料庫。</span><span class="sxs-lookup"><span data-stu-id="8cd97-184">Modify the ApplicationServices connection string in your web configuration (web.config) file so that it points to the production database.</span></span> <span data-ttu-id="8cd97-185">例如，清單3中的已修改連接會指向名為 MyProductionDB 的資料庫（原始 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 連接字串已標記為批註）。</span><span class="sxs-lookup"><span data-stu-id="8cd97-185">For example, the modified connection in Listing 3 points to a database named MyProductionDB (the original ApplicationServices connection string has been commented out).</span></span>

<span data-ttu-id="8cd97-186">**[清單 3] – web.config**</span><span class="sxs-lookup"><span data-stu-id="8cd97-186">**Listing 3 – Web.config**</span></span>

[!code-xml[Main](authenticating-users-with-forms-authentication-vb/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a><span data-ttu-id="8cd97-187">設定資料庫許可權</span><span class="sxs-lookup"><span data-stu-id="8cd97-187">Configuring Database Permissions</span></span>

<span data-ttu-id="8cd97-188">如果您使用整合式安全性來連接到您的資料庫，則必須將正確的 Windows 使用者帳戶新增為您資料庫的登入。</span><span class="sxs-lookup"><span data-stu-id="8cd97-188">If you use Integrated Security to connect to your database then you will need to add the correct Windows user account as a login to your database.</span></span> <span data-ttu-id="8cd97-189">正確的帳戶取決於您使用的是 ASP.NET 程式開發伺服器還是 Internet Information Services 作為 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8cd97-189">The correct account depends on whether you are using the ASP.NET Development Server or Internet Information Services as your web server.</span></span> <span data-ttu-id="8cd97-190">正確的使用者帳戶也取決於您的作業系統。</span><span class="sxs-lookup"><span data-stu-id="8cd97-190">The correct user account also depends on your operating system.</span></span>

<span data-ttu-id="8cd97-191">如果您使用 ASP.NET 程式開發伺服器（Visual Studio 所使用的預設 web 伺服器），則您的應用程式會在 Windows 使用者帳戶的內容中執行。</span><span class="sxs-lookup"><span data-stu-id="8cd97-191">If you are using the ASP.NET Development Server (the default web server used by Visual Studio) then your application executes within the context of your Windows user account.</span></span> <span data-ttu-id="8cd97-192">在此情況下，您必須將您的 Windows 使用者帳戶新增為資料庫伺服器登入。</span><span class="sxs-lookup"><span data-stu-id="8cd97-192">In that case, you need to add your Windows user account as a database server login.</span></span>

<span data-ttu-id="8cd97-193">或者，如果您使用 Internet Information Services，則必須將 ASPNET 帳戶或 NT 授權單位/網路服務帳戶新增為資料庫伺服器登入。</span><span class="sxs-lookup"><span data-stu-id="8cd97-193">Alternatively, if you are using Internet Information Services then you need to add either the ASPNET account or the NT AUTHORITY/NETWORK SERVICE account as a database server login.</span></span> <span data-ttu-id="8cd97-194">如果您使用的是 Windows XP，請將 ASPNET 帳戶新增為您資料庫的登入。</span><span class="sxs-lookup"><span data-stu-id="8cd97-194">If you are using Windows XP then add the ASPNET account as a login to your database.</span></span> <span data-ttu-id="8cd97-195">如果您使用的是較新的作業系統（例如 Windows Vista 或 Windows Server 2008），請新增 NT 授權單位/網路服務帳戶作為資料庫登入。</span><span class="sxs-lookup"><span data-stu-id="8cd97-195">If you are using a more recent operating system, such as Windows Vista or Windows Server 2008, then add the NT AUTHORITY/NETWORK SERVICE account as the database login.</span></span>

<span data-ttu-id="8cd97-196">您可以使用 Microsoft SQL Server Management Studio，將新的使用者帳戶新增至您的資料庫（請參閱 [圖 9]）。</span><span class="sxs-lookup"><span data-stu-id="8cd97-196">You can add a new user account to your database by using Microsoft SQL Server Management Studio (see Figure 9).</span></span>

<span data-ttu-id="8cd97-197">**圖9–建立新的 Microsoft SQL Server 登入**</span><span class="sxs-lookup"><span data-stu-id="8cd97-197">**Figure 9 – Creating a new Microsoft SQL Server login**</span></span>

![clip_image018](authenticating-users-with-forms-authentication-vb/_static/image9.jpg)

<span data-ttu-id="8cd97-199">建立必要的登入之後，您必須將登入對應至具有正確資料庫角色的資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="8cd97-199">After you create the required login, you need to map the login to a database user with the right database roles.</span></span> <span data-ttu-id="8cd97-200">按兩下登入，然後選取 [使用者對應] 索引標籤。選取一個或多個應用程式服務資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="8cd97-200">Double-click the login and select the User Mapping tab. Select one or more application services database roles.</span></span> <span data-ttu-id="8cd97-201">例如，為了驗證使用者，您必須啟用 aspnet\_成員資格\_BasicAccess 資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="8cd97-201">For example, in order to authenticate users, you need to enable the aspnet\_Membership\_BasicAccess database role.</span></span> <span data-ttu-id="8cd97-202">若要建立新的使用者，您必須啟用 aspnet\_成員資格\_FullAccess 資料庫角色（請參閱 [圖 10]）。</span><span class="sxs-lookup"><span data-stu-id="8cd97-202">In order to create new users, you need to enable the aspnet\_Membership\_FullAccess database role (see Figure 10).</span></span>

<span data-ttu-id="8cd97-203">**圖10–新增應用程式服務資料庫角色**</span><span class="sxs-lookup"><span data-stu-id="8cd97-203">**Figure 10 – Adding Application Services database roles**</span></span>

![clip_image020](authenticating-users-with-forms-authentication-vb/_static/image10.jpg)

#### <a name="summary"></a><span data-ttu-id="8cd97-205">總結</span><span class="sxs-lookup"><span data-stu-id="8cd97-205">Summary</span></span>

<span data-ttu-id="8cd97-206">在本教學課程中，您已瞭解如何在建立 ASP.NET MVC 應用程式時，使用表單驗證。</span><span class="sxs-lookup"><span data-stu-id="8cd97-206">In this tutorial, you learned how to use Forms authentication when building an ASP.NET MVC application.</span></span> <span data-ttu-id="8cd97-207">首先，您已瞭解如何利用網站管理工具來建立新的使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="8cd97-207">First, you learned how to create new users and roles by taking advantage of the Web Site Administration Tool.</span></span> <span data-ttu-id="8cd97-208">接下來，您已瞭解如何使用 [授權] 屬性來防止未經授權的使用者叫用控制器動作。</span><span class="sxs-lookup"><span data-stu-id="8cd97-208">Next, you learned how to use the [Authorize] attribute to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="8cd97-209">最後，您已瞭解如何設定 MVC 應用程式，以將使用者和角色資訊儲存在生產資料庫中。</span><span class="sxs-lookup"><span data-stu-id="8cd97-209">Finally, you learned how to configure your MVC application to store user and role information in a production database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8cd97-210">[上一頁](preventing-javascript-injection-attacks-cs.md)
> [下一頁](authenticating-users-with-windows-authentication-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8cd97-210">[Previous](preventing-javascript-injection-attacks-cs.md)
[Next](authenticating-users-with-windows-authentication-vb.md)</span></span>
