---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: 成員資格 |Microsoft Docs
author: microsoft
description: ASP.NET 成員資格是以 ASP.NET 1.x 的表單驗證模型成功為基礎。 ASP.NET 表單驗證提供便利的方式來 incorp 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: da6fc205bd852a818d65425586cec38fdb08d310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642153"
---
# <a name="membership"></a><span data-ttu-id="ac811-104">成員資格</span><span class="sxs-lookup"><span data-stu-id="ac811-104">Membership</span></span>

<span data-ttu-id="ac811-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ac811-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="ac811-106">ASP.NET 成員資格是以 ASP.NET 1.x 的表單驗證模型成功為基礎。</span><span class="sxs-lookup"><span data-stu-id="ac811-106">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="ac811-107">ASP.NET 表單驗證提供便利的方法，將登入表單併入您的 ASP.NET 應用程式，並針對資料庫或其他資料存放區驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="ac811-107">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span>

<span data-ttu-id="ac811-108">ASP.NET 成員資格是以 ASP.NET 1.x 的表單驗證模型成功為基礎。</span><span class="sxs-lookup"><span data-stu-id="ac811-108">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="ac811-109">ASP.NET 表單驗證提供便利的方法，將登入表單併入您的 ASP.NET 應用程式，並針對資料庫或其他資料存放區驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="ac811-109">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span> <span data-ttu-id="ac811-110">FormsAuthentication 類別的成員可以處理 cookie 以進行驗證、檢查是否有有效的登入、將使用者登出等等。不過，在 ASP.NET 1.x 應用程式中執行表單驗證，可能需要相當多的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ac811-110">The members of the FormsAuthentication class make it possible to handle cookies for authentication, check for a valid login, log a user out etc. However, implementing Forms authentication in an ASP.NET 1.x application can require a fair amount of code.</span></span>

<span data-ttu-id="ac811-111">ASP.NET 2.0 中的成員資格只是使用表單驗證的主要進步。</span><span class="sxs-lookup"><span data-stu-id="ac811-111">Membership in ASP.NET 2.0 is a major advancement over using Forms authentication alone.</span></span> <span data-ttu-id="ac811-112">（與表單驗證結合時，成員資格最強大，但不需要使用表單驗證）。您很快就會看到，您可以使用 ASP.NET 成員資格和 ASP.NET 2.0 中的登入控制項來執行功能強大的成員資格系統，而不需要撰寫太多程式碼。</span><span class="sxs-lookup"><span data-stu-id="ac811-112">(Membership is most robust when coupled with Forms authentication, but using Forms authentication is not a requirement.) As you'll soon see, you can use ASP.NET Membership and the login controls in ASP.NET 2.0 to implement a powerful membership system without writing much code at all.</span></span>

## <a name="implementing-membership-in-aspnet-20"></a><span data-ttu-id="ac811-113">在 ASP.NET 2.0 中執行成員資格</span><span class="sxs-lookup"><span data-stu-id="ac811-113">Implementing Membership in ASP.NET 2.0</span></span>

<span data-ttu-id="ac811-114">成員資格是透過下列四個步驟來執行。</span><span class="sxs-lookup"><span data-stu-id="ac811-114">Membership is implemented by following four steps.</span></span> <span data-ttu-id="ac811-115">請記住，其中包含許多子步驟，以及可同時執行的選擇性設定。</span><span class="sxs-lookup"><span data-stu-id="ac811-115">Keep in mind that there are many sub-steps that are involved as well as optional configuration that can be implemented as well.</span></span> <span data-ttu-id="ac811-116">這些步驟的目的是要說明設定成員資格的重要概念。</span><span class="sxs-lookup"><span data-stu-id="ac811-116">These steps are meant to illustrate the big picture of configuring membership.</span></span>

1. <span data-ttu-id="ac811-117">建立您的成員資格資料庫（如果 SQL Server 做為成員資格存放區）。</span><span class="sxs-lookup"><span data-stu-id="ac811-117">Create your membership database (if SQL Server is used as the membership store.)</span></span>
2. <span data-ttu-id="ac811-118">在您的應用程式佈建檔中指定成員資格選項。</span><span class="sxs-lookup"><span data-stu-id="ac811-118">Specify the membership options in your applications configuration files.</span></span> <span data-ttu-id="ac811-119">（預設會啟用成員資格）。</span><span class="sxs-lookup"><span data-stu-id="ac811-119">(Membership is enabled by default.)</span></span>
3. <span data-ttu-id="ac811-120">決定您想要使用的成員資格存放區類型。</span><span class="sxs-lookup"><span data-stu-id="ac811-120">Determine the type of membership store you want to use.</span></span> <span data-ttu-id="ac811-121">選項包括：</span><span class="sxs-lookup"><span data-stu-id="ac811-121">Options are:</span></span> 

    - <span data-ttu-id="ac811-122">Microsoft SQL Server （版本7.0 或更新版本）</span><span class="sxs-lookup"><span data-stu-id="ac811-122">Microsoft SQL Server (version 7.0 or later)</span></span>
    - <span data-ttu-id="ac811-123">Active Directory 存放區</span><span class="sxs-lookup"><span data-stu-id="ac811-123">Active Directory Store</span></span>
    - <span data-ttu-id="ac811-124">自訂成員資格提供者</span><span class="sxs-lookup"><span data-stu-id="ac811-124">Custom membership provider</span></span>
4. <span data-ttu-id="ac811-125">設定應用程式以進行 ASP.NET 表單驗證。</span><span class="sxs-lookup"><span data-stu-id="ac811-125">Configure the application for ASP.NET Forms authentication.</span></span> <span data-ttu-id="ac811-126">同樣地，成員資格是設計來利用表單驗證，但不需要使用表單驗證。</span><span class="sxs-lookup"><span data-stu-id="ac811-126">Once again, Membership is designed to take advantage of Forms authentication, but using Forms authentication is not a requirement.</span></span>
5. <span data-ttu-id="ac811-127">定義成員資格的使用者帳戶，並視需要設定角色。</span><span class="sxs-lookup"><span data-stu-id="ac811-127">Define user accounts for membership and configure roles if desired.</span></span>

## <a name="creating-the-membership-database"></a><span data-ttu-id="ac811-128">建立成員資格資料庫</span><span class="sxs-lookup"><span data-stu-id="ac811-128">Creating the Membership Database</span></span>

<span data-ttu-id="ac811-129">如果您使用 SQL Server 7.0 或更新版本作為您的成員資格存放區，則可以使用 aspnet\_regsql 公用程式（可從 Visual Studio .NET 2005 命令提示字元中輕鬆取得）來設定您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac811-129">If you're using SQL Server 7.0 or later as your membership store, you can use the aspnet\_regsql utility (available most easily from the Visual Studio .NET 2005 Command Prompt) to configure your database.</span></span> <span data-ttu-id="ac811-130">Aspnet\_regsql 公用程式可用來做為命令提示字元工具或透過 GUI wizard。</span><span class="sxs-lookup"><span data-stu-id="ac811-130">The aspnet\_regsql utility can be used as a command prompt tool or via a GUI wizard.</span></span> <span data-ttu-id="ac811-131">Wizard 方法是設定資料庫最簡單的方式。</span><span class="sxs-lookup"><span data-stu-id="ac811-131">The wizard method is the easiest way to configure your database.</span></span> <span data-ttu-id="ac811-132">若要存取嚮導，只要執行下列命令即可：</span><span class="sxs-lookup"><span data-stu-id="ac811-132">To access the wizard, simply run the following command:</span></span>

`aspnet_regsql W`

<span data-ttu-id="ac811-133">執行該命令後，您會看到 ASP.NET SQL Server 安裝程式嚮導，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ac811-133">Once you run that command, you will be presented with the ASP.NET SQL Server Setup Wizard as shown below.</span></span>

![](membership/_static/image1.jpg)

<span data-ttu-id="ac811-134">**圖 1**</span><span class="sxs-lookup"><span data-stu-id="ac811-134">**Figure 1**</span></span>

<span data-ttu-id="ac811-135">[ASP.NET SQL Server 安裝程式] 會在您于 Wizard 中指定的實例中建立網站。</span><span class="sxs-lookup"><span data-stu-id="ac811-135">The ASP.NET SQL Server Setup Wizard creates the Web site in the instance you specify in the wizard.</span></span> <span data-ttu-id="ac811-136">不過，ASP.NET 會使用 machine.config 檔案中的連接字串來連接到您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac811-136">However, ASP.NET will use the connection string in the machine.config file to connect to your database.</span></span> <span data-ttu-id="ac811-137">根據預設，這個連接字串會指向 SQL Server 2005 實例，因此，如果您使用 SQL Server 2000 或 SQL Server 7.0 實例，就必須修改 machine.config 檔案中的連接字串。</span><span class="sxs-lookup"><span data-stu-id="ac811-137">By default, this connection string will point to a SQL Server 2005 instance, so if you are using a SQL Server 2000 or SQL Server 7.0 instance, you will need to modify the connection string in the machine.config file.</span></span> <span data-ttu-id="ac811-138">該連接字串可以在這裡找到：</span><span class="sxs-lookup"><span data-stu-id="ac811-138">That connection string can be located here:</span></span>

[!code-xml[Main](membership/samples/sample1.xml)]

<span data-ttu-id="ac811-139">可惜的是，如果您不修改連接字串，ASP.NET 就不會提供描述性錯誤。</span><span class="sxs-lookup"><span data-stu-id="ac811-139">Unfortunately, if you don't modify the connection string, ASP.NET will not give you a descriptive error.</span></span> <span data-ttu-id="ac811-140">它只會繼續抱怨，指出您尚未建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac811-140">It will just continue to complain saying that you haven't created the database.</span></span> <span data-ttu-id="ac811-141">在上述案例中，我已修改連接字串，以指向我的本機 SQL Server 2000 實例。</span><span class="sxs-lookup"><span data-stu-id="ac811-141">In the case above, I have modified the connection string to point to my local SQL Server 2000 instance.</span></span>

## <a name="specifying-configuration-and-adding-users-and-roles"></a><span data-ttu-id="ac811-142">指定設定及新增使用者和角色</span><span class="sxs-lookup"><span data-stu-id="ac811-142">Specifying Configuration and Adding Users and Roles</span></span>

<span data-ttu-id="ac811-143">設定成員資格的下一個步驟是將必要的資訊新增至應用程式的 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="ac811-143">The next step in configuring Membership is to add the necessary information to the web.config file of the application.</span></span> <span data-ttu-id="ac811-144">在 ASP.NET 1.x 中，修改 web.config 檔案有時候很棘手，因為使用的是 lowerCamelCase，而缺乏 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="ac811-144">In ASP.NET 1.x, modifying the web.config file was sometimes difficult because of the use of lowerCamelCase and the lack of Intellisense.</span></span> <span data-ttu-id="ac811-145">Visual Studio .NET 2005 可讓您更輕鬆地使用 Intellisense 來處理設定檔，但 ASP.NET 2.0 會藉由提供 Web 介面來編輯設定檔，而更進一步。</span><span class="sxs-lookup"><span data-stu-id="ac811-145">Visual Studio .NET 2005 makes the task much easier with Intellisense for configuration files, but ASP.NET 2.0 goes one step further by providing a Web interface for editing configuration files.</span></span>

<span data-ttu-id="ac811-146">若要啟動 Web 介面，您可以按一下 [方案總管] 工具列上的 [ASP.NET 設定] 按鈕，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ac811-146">You can launch the Web interface by clicking the ASP.NET Configuration button on the Solution Explorer toolbar as shown below.</span></span> <span data-ttu-id="ac811-147">您也可以透過在插入登入控制項時顯示的快顯視窗，啟動 Web 介面。</span><span class="sxs-lookup"><span data-stu-id="ac811-147">You can also launch the Web interface via pop-ups that are displayed when Login controls are inserted.</span></span>

![](membership/_static/image2.jpg)

<span data-ttu-id="ac811-148">**圖 2**</span><span class="sxs-lookup"><span data-stu-id="ac811-148">**Figure 2**</span></span>

<span data-ttu-id="ac811-149">這會啟動 ASP.NET 的網站管理工具，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ac811-149">This launches the ASP.NET Web Site Administration Tool shown below.</span></span> <span data-ttu-id="ac811-150">ASP.NET 網站管理是一個四個索引標籤的介面，可讓您輕鬆地管理應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="ac811-150">The ASP.NET Web Site Administration is a four-tab interface that makes it easy to manage application settings.</span></span> <span data-ttu-id="ac811-151">下列索引標籤可供使用：</span><span class="sxs-lookup"><span data-stu-id="ac811-151">The following tabs are available:</span></span>

- <span data-ttu-id="ac811-152">**Home**</span><span class="sxs-lookup"><span data-stu-id="ac811-152">**Home**</span></span>
- <span data-ttu-id="ac811-153">**安全性**設定使用者、角色和存取權。</span><span class="sxs-lookup"><span data-stu-id="ac811-153">**Security** Configure users, roles, and access.</span></span>
- <span data-ttu-id="ac811-154">**應用程式**設定應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="ac811-154">**Application** Configure application settings.</span></span>
- <span data-ttu-id="ac811-155">**提供者**設定並測試您的應用程式成員資格提供者。</span><span class="sxs-lookup"><span data-stu-id="ac811-155">**Provider** Configure and test your applications membership provider.</span></span>

<span data-ttu-id="ac811-156">網站管理工具可讓您輕鬆地建立新的使用者、建立新的角色，以及管理使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="ac811-156">The Web Site Administration Tool allows you to easily create new users, create new roles, and to manage users and roles.</span></span> <span data-ttu-id="ac811-157">Windows 介面不提供這項功能。</span><span class="sxs-lookup"><span data-stu-id="ac811-157">This ability is not available in the Windows interface.</span></span> <span data-ttu-id="ac811-158">Windows 介面可讓您輕鬆定義授權設定，以及加入、刪除及管理提供者、不在網站管理工具中的功能。</span><span class="sxs-lookup"><span data-stu-id="ac811-158">The Windows interface allows you to easily define authorization settings and to add, delete, and manage providers, capabilities that are not in the Web Site Administration Tool.</span></span>

<span data-ttu-id="ac811-159">若要啟動 Windows 介面，請開啟 [Internet Information Services] 嵌入式管理單元，以滑鼠右鍵按一下您的應用程式，然後選擇 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="ac811-159">To launch the Windows interface, open the Internet Information Services snap-in, right-click on your application, and choose Properties.</span></span> <span data-ttu-id="ac811-160">按一下 [ASP.NET] 索引標籤，然後按一下 [編輯設定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ac811-160">Click the ASP.NET tab and then click the Edit Configuration button.</span></span> <span data-ttu-id="ac811-161">（應用程式必須在 ASP.NET 2.0 下執行，才能啟用 [編輯設定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ac811-161">(The application must be running under ASP.NET 2.0 for the Edit Configuration button to be enabled.</span></span> <span data-ttu-id="ac811-162">您也可以在 [ASP.NET] 對話方塊中設定 ASP.NET 版本）。[ASP.NET 設定設定] 對話方塊隨即顯示，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ac811-162">You can configure the ASP.NET version in the ASP.NET dialog as well.) The ASP.NET Configuration Settings dialog is displayed as shown below.</span></span>

![](membership/_static/image3.jpg)

<span data-ttu-id="ac811-163">**圖 3**</span><span class="sxs-lookup"><span data-stu-id="ac811-163">**Figure 3**</span></span>

<span data-ttu-id="ac811-164">[一般] 索引標籤上會列出 [連接字串] 和 [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="ac811-164">On the General tab, connection strings and application settings are listed.</span></span> <span data-ttu-id="ac811-165">斜體中的任何設定都定義于父設定檔中（machine.config 或較高層級的 web.config），而不是斜體的設定則來自應用程式佈建檔。</span><span class="sxs-lookup"><span data-stu-id="ac811-165">Any settings in italics are defined in a parent configuration file (either the machine.config or a web.config at a higher level) and settings not in italics are from the applications configuration file.</span></span> <span data-ttu-id="ac811-166">如果在應用層級新增、移除或編輯設定，ASP.NET 會在應用層級 web.config 新增、移除或修改設定，而不是從繼承它的設定檔中移除設定。</span><span class="sxs-lookup"><span data-stu-id="ac811-166">If a setting is added, removed, or edited at the application level, ASP.NET will add, remove, or modify the setting at the application levels web.config instead of removing the setting from the configuration file from which it is inherited.</span></span>

<span data-ttu-id="ac811-167">[驗證] 索引標籤如下所示。</span><span class="sxs-lookup"><span data-stu-id="ac811-167">The Authentication tab is shown below.</span></span> <span data-ttu-id="ac811-168">這是您將設定成員資格設定的位置。</span><span class="sxs-lookup"><span data-stu-id="ac811-168">This is where you will configure your membership settings.</span></span> <span data-ttu-id="ac811-169">您可以在這裡設定表單驗證設定、成員資格提供者和角色提供者。</span><span class="sxs-lookup"><span data-stu-id="ac811-169">Forms authentication settings, membership providers, and role providers can be configured here.</span></span>

![](membership/_static/image4.jpg)

<span data-ttu-id="ac811-170">**圖 4**</span><span class="sxs-lookup"><span data-stu-id="ac811-170">**Figure 4**</span></span>

## <a name="implementing-membership-in-your-application"></a><span data-ttu-id="ac811-171">在您的應用程式中執行成員資格</span><span class="sxs-lookup"><span data-stu-id="ac811-171">Implementing Membership in Your Application</span></span>

<span data-ttu-id="ac811-172">在您的應用程式中執行 ASP.NET 2.0 成員資格的最簡單方式，就是使用提供的登入控制項。</span><span class="sxs-lookup"><span data-stu-id="ac811-172">The easiest way to implement ASP.NET 2.0 membership in your application is to use the provided Logon controls.</span></span> <span data-ttu-id="ac811-173">這個方法可讓您在不需撰寫任何程式碼的情況下，執行 ASP.NET 2.0 成員資格的基本概念。</span><span class="sxs-lookup"><span data-stu-id="ac811-173">This method allows you to implement the basics of ASP.NET 2.0 membership without writing any code at all.</span></span>

<span data-ttu-id="ac811-174">ASP.NET 2.0 提供下列登入控制：</span><span class="sxs-lookup"><span data-stu-id="ac811-174">The following Logon controls are available in ASP.NET 2.0:</span></span>

## <a name="login-control"></a><span data-ttu-id="ac811-175">Login 控制項</span><span class="sxs-lookup"><span data-stu-id="ac811-175">Login Control</span></span>

<span data-ttu-id="ac811-176">登入控制項會提供介面，讓使用者登入您的成員資格系統。</span><span class="sxs-lookup"><span data-stu-id="ac811-176">The Login control provides an interface for someone to log into your membership system.</span></span> <span data-ttu-id="ac811-177">它會為您提供 [使用者名稱] 和 [密碼] 文字方塊和 [登入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ac811-177">It provides you with a username and password textbox and a login button.</span></span> <span data-ttu-id="ac811-178">還有許多其他常見的功能，例如註冊尚未完成的人員的連結、可讓使用者在後續造訪時自動登入的核取方塊、密碼提醒的連結等等。您可以透過控制項的屬性自訂登入控制項的所有功能。</span><span class="sxs-lookup"><span data-stu-id="ac811-178">Many other common features such as a link to register for people who have not yet done so, a checkbox that allows the user to automatically login on subsequent visits, a link for a password reminder, etc. All features of the Login control are customizable via the properties of the control.</span></span>

<span data-ttu-id="ac811-179">在 ASP.NET 1.x 中，開發人員在使用表單驗證時，必須撰寫相當大量的程式碼來進行查閱。</span><span class="sxs-lookup"><span data-stu-id="ac811-179">In ASP.NET 1.x, developers had to write a fair amount of code to do a lookup when using Forms authentication.</span></span> <span data-ttu-id="ac811-180">有了 ASP.NET 2.0 成員資格，您就可以驗證使用者，而不需要撰寫任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="ac811-180">With ASP.NET 2.0 membership, you can validate users without writing any code at all.</span></span> <span data-ttu-id="ac811-181">ASP.NET 會自動為您執行使用者查閱。</span><span class="sxs-lookup"><span data-stu-id="ac811-181">ASP.NET will automatically do the look-up of the user for you.</span></span> <span data-ttu-id="ac811-182">（如果您使用登入控制項，而不使用 ASP.NET 成員資格，則可以使用**OnAuthenticate**方法來驗證使用者）。</span><span class="sxs-lookup"><span data-stu-id="ac811-182">(If you are using the Login control without using ASP.NET membership, you can use the **OnAuthenticate** method to validate the user.)</span></span>

## <a name="loginview-control"></a><span data-ttu-id="ac811-183">LoginView 控制項</span><span class="sxs-lookup"><span data-stu-id="ac811-183">LoginView Control</span></span>

<span data-ttu-id="ac811-184">LoginView 控制項是樣板化控制項，預設會提供兩個範本;AnonymousTemplate 和 LoggedInTemplate。</span><span class="sxs-lookup"><span data-stu-id="ac811-184">The LoginView control is a templated control that provides two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="ac811-185">所顯示的範本取決於使用者是否登入您的成員資格系統。</span><span class="sxs-lookup"><span data-stu-id="ac811-185">The template that is displayed is determined by whether or not the user is logged into your membership system.</span></span> <span data-ttu-id="ac811-186">此控制項通常用來在使用者尚未登入時顯示登入控制項，以及在使用者已登入時，使用 LoginStatus 控制項和（或）其他登入控制項。</span><span class="sxs-lookup"><span data-stu-id="ac811-186">This control is typically used to display a Login control when a user has not yet logged in and a LoginStatus control and/or other login controls when the user has logged in.</span></span> <span data-ttu-id="ac811-187">如果您在 ASP.NET 應用程式中使用角色管理，LoginView 控制項可以根據使用者角色來顯示特定的範本。</span><span class="sxs-lookup"><span data-stu-id="ac811-187">If you are using role management in your ASP.NET application, the LoginView control can display a specific template based upon the users role.</span></span> <span data-ttu-id="ac811-188">（稍後會涵蓋 ASP.NET 角色管理的詳細資訊。）</span><span class="sxs-lookup"><span data-stu-id="ac811-188">(More on ASP.NET role management will be covered later.)</span></span>

## <a name="passwordrecovery-control"></a><span data-ttu-id="ac811-189">PasswordRecovery 控制項</span><span class="sxs-lookup"><span data-stu-id="ac811-189">PasswordRecovery Control</span></span>

<span data-ttu-id="ac811-190">PasswordRecovery 控制項可讓使用者使用其目前的密碼來接收電子郵件，或重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="ac811-190">The PasswordRecovery control allows users to receive an email with his or her current password or reset his or her password.</span></span> <span data-ttu-id="ac811-191">純文字和加密密碼可以復原，並以電子郵件傳送給使用者。</span><span class="sxs-lookup"><span data-stu-id="ac811-191">Clear text and encrypted passwords can be recovered and emailed to users.</span></span> <span data-ttu-id="ac811-192">如果密碼已雜湊，則無法復原。</span><span class="sxs-lookup"><span data-stu-id="ac811-192">If the password is hashed, it cannot be recovered.</span></span> <span data-ttu-id="ac811-193">相反地，使用者將需要執行密碼重設。</span><span class="sxs-lookup"><span data-stu-id="ac811-193">Instead the user will be required to perform a password reset.</span></span>

## <a name="loginstatus-control"></a><span data-ttu-id="ac811-194">LoginStatus 控制項</span><span class="sxs-lookup"><span data-stu-id="ac811-194">LoginStatus Control</span></span>

<span data-ttu-id="ac811-195">LoginStatus 控制項是用來對未登入的使用者，以及目前登入的使用者顯示登出指示器。</span><span class="sxs-lookup"><span data-stu-id="ac811-195">The LoginStatus control is used to display a login indicator to users who are not logged in and a logout indicator to users who are currently logged in.</span></span> <span data-ttu-id="ac811-196">IsAuthenticated 屬性是用來決定要顯示的指標。</span><span class="sxs-lookup"><span data-stu-id="ac811-196">The Request.IsAuthenticated property is used to determine which indicator to display.</span></span> <span data-ttu-id="ac811-197">LoginStatus 控制項所顯示的指標可以是文字（透過**LoginText**和**LogoutText**屬性實作為）或影像（透過**LoginImageUrl**和**LogoutImageUrl**屬性實作為實）。</span><span class="sxs-lookup"><span data-stu-id="ac811-197">The indicator displayed by the LoginStatus control can be text (implemented via the **LoginText** and **LogoutText** properties) or images (implemented via the **LoginImageUrl** and **LogoutImageUrl** properties.)</span></span>

<span data-ttu-id="ac811-198">當使用者透過 LoginStatus 控制項登出時，會將他或她重新導向至**LogoutPageUrl**屬性所指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="ac811-198">When a user logs out via the LoginStatus control, he or she is redirected to the URL specified by the **LogoutPageUrl** property.</span></span> <span data-ttu-id="ac811-199">如果未設定該屬性，則會重新整理目前的頁面。</span><span class="sxs-lookup"><span data-stu-id="ac811-199">If that property is not set, the current page is refreshed.</span></span> <span data-ttu-id="ac811-200">由於網站可能受到表單驗證的保護，因此目前頁面的重新整理會將使用者重新導向至網站的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="ac811-200">Since the site is likely protected by Forms authentication, the refresh of the current page will redirect the user to the login page for the site.</span></span>

## <a name="loginname-control"></a><span data-ttu-id="ac811-201">LoginName 控制項</span><span class="sxs-lookup"><span data-stu-id="ac811-201">LoginName Control</span></span>

<span data-ttu-id="ac811-202">LoginName 控制項會顯示目前登入網站的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="ac811-202">The LoginName control displays the username of the user currently logged into the site.</span></span>

## <a name="createuserwizard-control"></a><span data-ttu-id="ac811-203">CreateUserWizard 控制項</span><span class="sxs-lookup"><span data-stu-id="ac811-203">CreateUserWizard Control</span></span>

<span data-ttu-id="ac811-204">CreateUserWizard 控制項提供使用者一個便利的方式來註冊您的成員資格系統。</span><span class="sxs-lookup"><span data-stu-id="ac811-204">The CreateUserWizard control provides users with a convenient way to register for your membership system.</span></span> <span data-ttu-id="ac811-205">您可以透過如下所示的介面，新增步驟（實作為 WizardSteps 的集合）。</span><span class="sxs-lookup"><span data-stu-id="ac811-205">You can add steps (implemented as a collection of WizardSteps) via the interface shown below.</span></span>

![](membership/_static/image5.jpg)

<span data-ttu-id="ac811-206">**圖5**</span><span class="sxs-lookup"><span data-stu-id="ac811-206">**Figure 5**</span></span>

<span data-ttu-id="ac811-207">CreateUserWizard 是衍生自 Wizard 類別的樣板化控制項，並提供下列範本：</span><span class="sxs-lookup"><span data-stu-id="ac811-207">The CreateUserWizard is a templated control that derives from the Wizard class and provides the following templates:</span></span>

- <span data-ttu-id="ac811-208">**System.windows.controls.headereditemscontrol.headertemplate**此範本控制 wizard 標頭的外觀。</span><span class="sxs-lookup"><span data-stu-id="ac811-208">**HeaderTemplate** This template controls the appearance of the header of the wizard.</span></span>
- <span data-ttu-id="ac811-209">**SidebarTemplate**此範本控制 wizard 提要欄位的外觀。</span><span class="sxs-lookup"><span data-stu-id="ac811-209">**SidebarTemplate** This template controls the appearance of the sidebar of the wizard.</span></span>
- <span data-ttu-id="ac811-210">**StartNavigationTemplate**此範本會在開始步驟中控制流覽的外觀。</span><span class="sxs-lookup"><span data-stu-id="ac811-210">**StartNavigationTemplate** This template controls the appearance of the navigation are of the wizard at the start step.</span></span>
- <span data-ttu-id="ac811-211">**StepNavigationTemplate**此範本控制流覽區域的外觀，而不是在 [開始] 或 [完成] 步驟中。</span><span class="sxs-lookup"><span data-stu-id="ac811-211">**StepNavigationTemplate** This template controls the appearance of the navigation area when not in the start or finish step.</span></span>
- <span data-ttu-id="ac811-212">**FinishNavigationTemplate**此範本會在完成步驟時控制流覽區域的外觀。</span><span class="sxs-lookup"><span data-stu-id="ac811-212">**FinishNavigationTemplate** This template controls the appearance of the navigation area when on the finish step.</span></span>

<span data-ttu-id="ac811-213">此外，針對您新增至 Wizard 的每個步驟，ASP.NET 都會建立一個自訂範本，其中同時包含該步驟的 ContentTemplate 和 CustomNavigationTemplate。</span><span class="sxs-lookup"><span data-stu-id="ac811-213">Additionally, for each step that you add to the Wizard, ASP.NET will create a custom template that contains both a ContentTemplate and a CustomNavigationTemplate for that step.</span></span> <span data-ttu-id="ac811-214">如需自訂 CreateUserWizard 的完整詳細資料，請參閱 VS.NET 2005 檔：</span><span class="sxs-lookup"><span data-stu-id="ac811-214">For full details on customizing the CreateUserWizard, see the VS.NET 2005 documentation:</span></span>

## <a name="changepassword-control"></a><span data-ttu-id="ac811-215">ChangePassword 控制項</span><span class="sxs-lookup"><span data-stu-id="ac811-215">ChangePassword Control</span></span>

<span data-ttu-id="ac811-216">ChangePassword 控制項可讓使用者變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="ac811-216">The ChangePassword control allows users to change his or her password.</span></span> <span data-ttu-id="ac811-217">如果 DisplayUserName 屬性為 true （預設為 false），則使用者可以在未登入時變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="ac811-217">If the DisplayUserName property is true (it is false by default), the user can change his or her password when they are not logged in.</span></span> <span data-ttu-id="ac811-218">如果使用者已經登入，而且 DisplayUserName 屬性為 true，*使用者就能夠*變更另一位未登入使用者的密碼，讓他們知道該使用者的使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="ac811-218">If the user *is* already logged in and the DisplayUserName property is true, the user will be able to change the password of another user that is not logged in providing they know the user ID of that user.</span></span>

<span data-ttu-id="ac811-219">請記住，如果您想要讓使用者能夠在不登入的情況下變更密碼，您必須確定顯示 ChangePassword 控制項的頁面允許匿名存取。</span><span class="sxs-lookup"><span data-stu-id="ac811-219">Keep in mind that if you want users to be able to change passwords without having to log in, you will need to ensure that the page on which the ChangePassword control is displayed allows anonymous access.</span></span> <span data-ttu-id="ac811-220">很明顯地，使用者必須提供其舊密碼，才能變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="ac811-220">Obviously, users will have to provide their old password in order to change their password.</span></span>

## <a name="role-management"></a><span data-ttu-id="ac811-221">角色管理</span><span class="sxs-lookup"><span data-stu-id="ac811-221">Role Management</span></span>

<span data-ttu-id="ac811-222">角色管理可讓您將使用者指派給特定角色，然後根據該角色來限制對特定檔案或資料夾的存取權。</span><span class="sxs-lookup"><span data-stu-id="ac811-222">Role management allows you to assign users to a particular role and then restrict access to certain file or folders based on that role.</span></span> <span data-ttu-id="ac811-223">角色管理也會提供 API，讓您以程式設計方式判斷更輕鬆地角色，或判斷特定角色中的所有使用者，並據以回應。</span><span class="sxs-lookup"><span data-stu-id="ac811-223">Role management also provides an API so that you can programmatically determine someones role or determine all users in a particular role and respond accordingly.</span></span>

<span data-ttu-id="ac811-224">角色管理不是 ASP.NET 成員資格的需求，也不需要成員資格就能使用角色管理。</span><span class="sxs-lookup"><span data-stu-id="ac811-224">Role management is not a requirement in ASP.NET membership, nor is membership a requirement in order to use role management.</span></span> <span data-ttu-id="ac811-225">不過，這兩個補充程式都很好，而開發人員可能會將它們彼此搭配使用。</span><span class="sxs-lookup"><span data-stu-id="ac811-225">However, the two supplement each other nicely and it is likely that developers will use them in conjunction with each other.</span></span>

<span data-ttu-id="ac811-226">若要在您的應用程式中啟用角色管理，請在 web.config 檔案中進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="ac811-226">To enable role management in your application, make the following change in your web.config file:</span></span>

[!code-xml[Main](membership/samples/sample2.xml)]

<span data-ttu-id="ac811-227">當**cacheRolesInCookie**屬性設定為 true 時，ASP.NET 會在用戶端上的 cookie 中快取使用者角色成員資格。</span><span class="sxs-lookup"><span data-stu-id="ac811-227">When the **cacheRolesInCookie** attribute is set to true, ASP.NET caches a users role membership in a cookie on the client.</span></span> <span data-ttu-id="ac811-228">這可讓角色查閱進行，而不需要呼叫 RoleProvider。</span><span class="sxs-lookup"><span data-stu-id="ac811-228">This allows role lookups to occur without calls into the RoleProvider.</span></span> <span data-ttu-id="ac811-229">使用此屬性時，建議開發人員確保**cookieProtection**屬性設定為 All。</span><span class="sxs-lookup"><span data-stu-id="ac811-229">When using this attribute, developers are encouraged to ensure that the **cookieProtection** attribute is set to All.</span></span> <span data-ttu-id="ac811-230">（這是預設設定）。這可確保 cookie 資料經過加密，並協助確保 cookie 內容尚未改變。</span><span class="sxs-lookup"><span data-stu-id="ac811-230">(This is the default setting.) This ensures that the cookie data are encrypted and helps to ensure that the cookies contents haven't been altered.</span></span> <span data-ttu-id="ac811-231">您可以使用 [網站管理工具] 來新增角色。</span><span class="sxs-lookup"><span data-stu-id="ac811-231">Roles can be added using the Web Site Administration Tool.</span></span> <span data-ttu-id="ac811-232">它可讓您輕鬆地定義角色、根據這些角色設定網站元件的存取權，以及將使用者指派給角色。</span><span class="sxs-lookup"><span data-stu-id="ac811-232">It allows you to easily define roles, configure access to parts of the site based on those roles, and assign users to roles.</span></span>

![](membership/_static/image6.jpg)

<span data-ttu-id="ac811-233">**圖6**</span><span class="sxs-lookup"><span data-stu-id="ac811-233">**Figure 6**</span></span>

<span data-ttu-id="ac811-234">如上所示，只要輸入角色的名稱，然後按一下 [新增角色]，即可新增角色。</span><span class="sxs-lookup"><span data-stu-id="ac811-234">As shown above, new roles can be added by simply entering the name of the role and then clicking Add Role.</span></span> <span data-ttu-id="ac811-235">按一下現有角色清單中的適當連結，即可管理或刪除現有的角色。</span><span class="sxs-lookup"><span data-stu-id="ac811-235">Existing roles can be managed or deleted by clicking the appropriate link in the list of existing roles.</span></span>

<span data-ttu-id="ac811-236">當您管理角色時，您可以新增或移除使用者，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ac811-236">When you manage a role, you can add or remove users as shown below.</span></span>

![](membership/_static/image7.jpg)

<span data-ttu-id="ac811-237">**圖7**</span><span class="sxs-lookup"><span data-stu-id="ac811-237">**Figure 7**</span></span>

<span data-ttu-id="ac811-238">藉由勾選 [使用者為角色] 核取方塊，您可以輕鬆地將使用者新增至特定角色。</span><span class="sxs-lookup"><span data-stu-id="ac811-238">By checking the User Is In Role checkbox, you can easily add a user to a specific role.</span></span> <span data-ttu-id="ac811-239">ASP.NET 會自動以適當的專案更新您的成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac811-239">ASP.NET will automatically update your membership database with the appropriate entries.</span></span> <span data-ttu-id="ac811-240">您也會想要設定應用程式的存取規則。</span><span class="sxs-lookup"><span data-stu-id="ac811-240">You will also want to configure access rules for your application.</span></span> <span data-ttu-id="ac811-241">ASP.NET 1.x 開發人員很熟悉如何透過 web.config 檔案中的 &lt;authorization&gt; 元素進行這項作業，而且 ASP.NET 2.0 中仍提供該選項。</span><span class="sxs-lookup"><span data-stu-id="ac811-241">ASP.NET 1.x developers are familiar with doing this via the &lt;authorization&gt; element in the web.config file, and that option is still available in ASP.NET 2.0.</span></span> <span data-ttu-id="ac811-242">不過，使用網站管理工具來管理存取規則的方式較簡單，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ac811-242">However, its easier to manage access rules using the Web Site Administration Tool as shown below.</span></span>

![](membership/_static/image8.jpg)

<span data-ttu-id="ac811-243">**圖8**</span><span class="sxs-lookup"><span data-stu-id="ac811-243">**Figure 8**</span></span>

<span data-ttu-id="ac811-244">在此情況下，系統管理資料夾會反白顯示（很難以看出，因為工具會以淺灰色醒目提示），而且系統管理員角色已被授與存取權。</span><span class="sxs-lookup"><span data-stu-id="ac811-244">In this case, the Administration folder is highlighted (its difficult to see because the tool highlights it in light gray) and the Administrators role has been granted access.</span></span> <span data-ttu-id="ac811-245">所有其他使用者都會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="ac811-245">All other users are denied.</span></span> <span data-ttu-id="ac811-246">您可以按一下 head 圖示來選取規則，然後使用 [上移] 和 [下移] 按鈕來排列規則。</span><span class="sxs-lookup"><span data-stu-id="ac811-246">You can click on the head icon to select a rule and then use the Move Up and Move Down buttons to arrange the rules.</span></span> <span data-ttu-id="ac811-247">如同 ASP.NET &lt;授權&gt; 元素，規則會依照其出現的順序進行處理。</span><span class="sxs-lookup"><span data-stu-id="ac811-247">As with the ASP.NET &lt;authorization&gt; element, rules are processed in the order in which they appear.</span></span> <span data-ttu-id="ac811-248">換句話說，如果上述的程式中的規則順序已反轉，則沒有人可以存取 [系統管理] 資料夾，因為 ASP.NET 會遇到的第一個規則是拒絕每個使用者加入該資料夾的規則。</span><span class="sxs-lookup"><span data-stu-id="ac811-248">In other words, if the order of rules in the shot above were reversed, no one would have access to the Administration folder because the first rule that ASP.NET would encounter would be the rule that denies everyone to the folder.</span></span>

<span data-ttu-id="ac811-249">ASP.NET 2.0 會將 web.config 檔案新增至您要為其指定存取規則的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ac811-249">ASP.NET 2.0 adds a web.config file to the folder for which you are specifying an access rule.</span></span> <span data-ttu-id="ac811-250">您可以透過設定檔或透過網站管理工具來編輯存取規則。</span><span class="sxs-lookup"><span data-stu-id="ac811-250">Access rules can be edited via the configuration file or via the Web Site Administration Tool.</span></span> <span data-ttu-id="ac811-251">換句話說，網站管理工具只是一個介面，可以在使用者易記的環境中編輯設定檔。</span><span class="sxs-lookup"><span data-stu-id="ac811-251">In other words, the Web Site Administration Tool is simply an interface through which the configuration file can be edited in a user-friendly environment.</span></span>

## <a name="using-roles-in-code"></a><span data-ttu-id="ac811-252">在程式碼中使用角色</span><span class="sxs-lookup"><span data-stu-id="ac811-252">Using Roles in Code</span></span>

<span data-ttu-id="ac811-253">自1.x 版起，角色管理的 API 尚未變更。</span><span class="sxs-lookup"><span data-stu-id="ac811-253">The API for role management has not changed since version 1.x.</span></span> <span data-ttu-id="ac811-254">**IsInRole**方法是用來判斷使用者是否為特定角色。</span><span class="sxs-lookup"><span data-stu-id="ac811-254">The **IsInRole** method is used to determine if a user is in a particular role.</span></span>

[!code-csharp[Main](membership/samples/sample3.cs)]

<span data-ttu-id="ac811-255">ASP.NET 也會建立 RolePrincipal 實例，做為目前內容的成員。</span><span class="sxs-lookup"><span data-stu-id="ac811-255">ASP.NET also creates a RolePrincipal instance as a member of the current context.</span></span> <span data-ttu-id="ac811-256">RolePrincipal 物件可以用來取得使用者所屬的所有角色，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ac811-256">The RolePrincipal object can be used to obtain all of the roles to which the user belongs as follows:</span></span>

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a><span data-ttu-id="ac811-257">使用 Rolegroup 搭配 LoginView 控制項</span><span class="sxs-lookup"><span data-stu-id="ac811-257">Using RoleGroups with the LoginView Control</span></span>

<span data-ttu-id="ac811-258">既然您已經瞭解角色管理和成員資格，讓我們來簡單地討論 LoginView 控制項如何利用 ASP.NET 2.0 中的這項功能。</span><span class="sxs-lookup"><span data-stu-id="ac811-258">Now that you have an understanding of role management and membership, lets discuss briefly how the LoginView control takes advantage of this capability in ASP.NET 2.0.</span></span> <span data-ttu-id="ac811-259">如先前所討論，LoginView 控制項是一個樣板化控制項，其中預設包含兩個範本;AnonymousTemplate 和 LoggedInTemplate。</span><span class="sxs-lookup"><span data-stu-id="ac811-259">As previously discussed, the LoginView control is a templated control that contains two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="ac811-260">在 [LoginView 工作] 對話方塊中，是一個連結（如下所示），可讓您編輯 Rolegroup。</span><span class="sxs-lookup"><span data-stu-id="ac811-260">Within the LoginView Tasks dialog is a link (shown below) that allows you to edit RoleGroups.</span></span>

![](membership/_static/image9.jpg)

<span data-ttu-id="ac811-261">**圖9**</span><span class="sxs-lookup"><span data-stu-id="ac811-261">**Figure 9**</span></span>

<span data-ttu-id="ac811-262">每個 RoleGroup 物件都包含一個字串陣列，用以定義 RoleGroup 適用的角色。</span><span class="sxs-lookup"><span data-stu-id="ac811-262">Each RoleGroup object contains an array of strings that defines which roles that RoleGroup applies to.</span></span> <span data-ttu-id="ac811-263">若要將新的 RoleGroup 加入至 LoginView 控制項，請按一下 [編輯 Rolegroup] 連結。</span><span class="sxs-lookup"><span data-stu-id="ac811-263">To add a new RoleGroup to the LoginView control, click the Edit RoleGroups link.</span></span> <span data-ttu-id="ac811-264">在上圖中，您可以看到我已為系統管理員加入新的 RoleGroup。</span><span class="sxs-lookup"><span data-stu-id="ac811-264">In the image above, you can see that I have added a new RoleGroup for Administrators.</span></span> <span data-ttu-id="ac811-265">藉由從 [Views] 下拉式清單中選取該 RoleGroup （RoleGroup [0]），我可以設定只會向系統管理員角色成員顯示的範本。</span><span class="sxs-lookup"><span data-stu-id="ac811-265">By selecting that RoleGroup (RoleGroup[0]) from the Views dropdown, I can configure a template that will only be displayed to members of the Administrators role.</span></span> <span data-ttu-id="ac811-266">在下圖中，我加入了新的 RoleGroup，它會套用至 Sales 角色的成員和散發角色。</span><span class="sxs-lookup"><span data-stu-id="ac811-266">In the image below, I have added a new RoleGroup that applies to members of the Sales role and the Distribution role.</span></span> <span data-ttu-id="ac811-267">這會將第二個 RoleGroup 新增至 [LoginView 工作] 對話方塊中的 [Views] 下拉式清單，而任何加入該範本的專案將會由 [銷售] 或 [散發] 角色中的任何使用者顯示。</span><span class="sxs-lookup"><span data-stu-id="ac811-267">This adds a second RoleGroup to the Views dropdown in the LoginView Tasks dialog and anything added to that template will be visible by any user in either the Sales or Distribution role.</span></span>

![](membership/_static/image10.jpg)

<span data-ttu-id="ac811-268">**圖10**</span><span class="sxs-lookup"><span data-stu-id="ac811-268">**Figure 10**</span></span>

## <a name="overriding-the-existing-membership-provider"></a><span data-ttu-id="ac811-269">覆寫現有的成員資格提供者</span><span class="sxs-lookup"><span data-stu-id="ac811-269">Overriding the Existing Membership Provider</span></span>

<span data-ttu-id="ac811-270">有幾種方式可讓您擴充 ASP.NET 成員資格的功能。</span><span class="sxs-lookup"><span data-stu-id="ac811-270">There are a couple of ways that you can extend the functionality of ASP.NET membership.</span></span> <span data-ttu-id="ac811-271">首先，您可以很明顯地變更 SqlMembershipProvider 類別的現有功能，方法是從它繼承並覆寫其方法。</span><span class="sxs-lookup"><span data-stu-id="ac811-271">First of all, you can obviously change the existing functionality of the SqlMembershipProvider class by inheriting from it and overriding its methods.</span></span> <span data-ttu-id="ac811-272">例如，如果您想要在建立使用者時執行自己的功能，您可以建立繼承自 SqlMembershipProvider 的自訂類別，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ac811-272">For example, if you want to implement your own functionality when users are created, you can create your own class that inherits from SqlMembershipProvider as follows:</span></span>

[!code-csharp[Main](membership/samples/sample5.cs)]

<span data-ttu-id="ac811-273">另一方面，如果您想要建立自己的提供者（例如，將您的成員資格資訊儲存在 Access 資料庫中），您可以建立自己的提供者。</span><span class="sxs-lookup"><span data-stu-id="ac811-273">If, on the other hand, you want to create your own provider (to store your membership information in an Access database, for example), you can create your own provider.</span></span>

## <a name="creating-your-own-membership-provider"></a><span data-ttu-id="ac811-274">建立您自己的成員資格提供者</span><span class="sxs-lookup"><span data-stu-id="ac811-274">Creating Your Own Membership Provider</span></span>

<span data-ttu-id="ac811-275">若要建立您自己的成員資格提供者，首先您必須建立繼承自 MembershipProvider 類別的類別。</span><span class="sxs-lookup"><span data-stu-id="ac811-275">To create your own membership provider, you will first need to create a class that inherits from the MembershipProvider class.</span></span> <span data-ttu-id="ac811-276">如果您使用 VB.NET，Visual Studio 2005 將會為您需要覆寫的所有方法新增存根。</span><span class="sxs-lookup"><span data-stu-id="ac811-276">If you are using VB.NET, Visual Studio 2005 will add the stubs for all of the methods that you need to override.</span></span> <span data-ttu-id="ac811-277">如果您使用C#的是，您可以在其中加入 stub。</span><span class="sxs-lookup"><span data-stu-id="ac811-277">If you are using C#, its up to you to add the stubs.</span></span>

<span data-ttu-id="ac811-278">您將需要覆寫下列各項：</span><span class="sxs-lookup"><span data-stu-id="ac811-278">You will need to override the following:</span></span>

- <span data-ttu-id="ac811-279">ApplicationName 屬性</span><span class="sxs-lookup"><span data-stu-id="ac811-279">ApplicationName property</span></span>
- <span data-ttu-id="ac811-280">ChangePassword 函數</span><span class="sxs-lookup"><span data-stu-id="ac811-280">ChangePassword function</span></span>
- <span data-ttu-id="ac811-281">ChangePasswordQuestionAndAnswer 函式</span><span class="sxs-lookup"><span data-stu-id="ac811-281">ChangePasswordQuestionAndAnswer function</span></span>
- <span data-ttu-id="ac811-282">CreateUser 函式</span><span class="sxs-lookup"><span data-stu-id="ac811-282">CreateUser function</span></span>
- <span data-ttu-id="ac811-283">DeleteUser 函式</span><span class="sxs-lookup"><span data-stu-id="ac811-283">DeleteUser function</span></span>
- <span data-ttu-id="ac811-284">EnablePasswordReset 屬性</span><span class="sxs-lookup"><span data-stu-id="ac811-284">EnablePasswordReset property</span></span>
- <span data-ttu-id="ac811-285">EnablePasswordRetrieval 屬性</span><span class="sxs-lookup"><span data-stu-id="ac811-285">EnablePasswordRetrieval property</span></span>
- <span data-ttu-id="ac811-286">FindUsersByEmail 函式</span><span class="sxs-lookup"><span data-stu-id="ac811-286">FindUsersByEmail function</span></span>
- <span data-ttu-id="ac811-287">FindUsersByName 函式</span><span class="sxs-lookup"><span data-stu-id="ac811-287">FindUsersByName function</span></span>
- <span data-ttu-id="ac811-288">GetAllUsers 函式</span><span class="sxs-lookup"><span data-stu-id="ac811-288">GetAllUsers function</span></span>
- <span data-ttu-id="ac811-289">GetNumberOfUsersOnline 函式</span><span class="sxs-lookup"><span data-stu-id="ac811-289">GetNumberOfUsersOnline function</span></span>
- <span data-ttu-id="ac811-290">GetPassword 函式</span><span class="sxs-lookup"><span data-stu-id="ac811-290">GetPassword function</span></span>
- <span data-ttu-id="ac811-291">GetUser 函式</span><span class="sxs-lookup"><span data-stu-id="ac811-291">GetUser function</span></span>
- <span data-ttu-id="ac811-292">GetUserNameByEmail 函式</span><span class="sxs-lookup"><span data-stu-id="ac811-292">GetUserNameByEmail function</span></span>
- <span data-ttu-id="ac811-293">MaxInvalidPasswordAttempts 屬性</span><span class="sxs-lookup"><span data-stu-id="ac811-293">MaxInvalidPasswordAttempts property</span></span>
- <span data-ttu-id="ac811-294">MinRequiredNonAlphanumericCharacters 屬性</span><span class="sxs-lookup"><span data-stu-id="ac811-294">MinRequiredNonAlphanumericCharacters property</span></span>
- <span data-ttu-id="ac811-295">MinRequiredPasswordLength 屬性</span><span class="sxs-lookup"><span data-stu-id="ac811-295">MinRequiredPasswordLength property</span></span>
- <span data-ttu-id="ac811-296">PasswordAttemptWindow 屬性</span><span class="sxs-lookup"><span data-stu-id="ac811-296">PasswordAttemptWindow property</span></span>
- <span data-ttu-id="ac811-297">PasswordFormat 屬性</span><span class="sxs-lookup"><span data-stu-id="ac811-297">PasswordFormat property</span></span>
- <span data-ttu-id="ac811-298">PasswordStrengthRegularExpression 屬性</span><span class="sxs-lookup"><span data-stu-id="ac811-298">PasswordStrengthRegularExpression property</span></span>
- <span data-ttu-id="ac811-299">RequiresQuestionAndAnswer 屬性</span><span class="sxs-lookup"><span data-stu-id="ac811-299">RequiresQuestionAndAnswer property</span></span>
- <span data-ttu-id="ac811-300">RequiresUniqueEmail 屬性</span><span class="sxs-lookup"><span data-stu-id="ac811-300">RequiresUniqueEmail property</span></span>
- <span data-ttu-id="ac811-301">ResetPassword 函式</span><span class="sxs-lookup"><span data-stu-id="ac811-301">ResetPassword function</span></span>
- <span data-ttu-id="ac811-302">解除鎖定使用者函式</span><span class="sxs-lookup"><span data-stu-id="ac811-302">Unlock user function</span></span>
- <span data-ttu-id="ac811-303">UpdateUser 函式</span><span class="sxs-lookup"><span data-stu-id="ac811-303">UpdateUser function</span></span>
- <span data-ttu-id="ac811-304">ValidateUser 函式</span><span class="sxs-lookup"><span data-stu-id="ac811-304">ValidateUser function</span></span>

<span data-ttu-id="ac811-305">這是一份以C#開發人員的身分來執行的清單。</span><span class="sxs-lookup"><span data-stu-id="ac811-305">Thats quite a list to implement as a C# developer.</span></span> <span data-ttu-id="ac811-306">您可能會發現，在 VB.NET 中建立類別，而不需要任何執行，然後使用 .NET 反映程式或類似的工具，將C#程式碼轉換為。</span><span class="sxs-lookup"><span data-stu-id="ac811-306">You may find it easier to create the class in VB.NET without any implementation and then use .NET Reflector or a similar tool to convert the code to C#.</span></span>

<span data-ttu-id="ac811-307">連接字串和其他屬性應設定為 Initialize 方法中的預設值。</span><span class="sxs-lookup"><span data-stu-id="ac811-307">The connection string and other properties should be set to their defaults in the Initialize method.</span></span> <span data-ttu-id="ac811-308">（在執行時間載入提供者時，會引發 Initialize 方法）。Initialize 方法的第二個參數是 NameValueCollection 類型，而且是與 web.config 檔案中自訂提供者相關聯之 &lt;加入&gt; 元素的參考。</span><span class="sxs-lookup"><span data-stu-id="ac811-308">(The Initialize method is fired when the provider is loaded at runtime.) The second parameter to the Initialize method is of type System.Collections.Specialized.NameValueCollection and is a reference to the &lt;add&gt; element that is associated with your custom provider in the web.config file.</span></span> <span data-ttu-id="ac811-309">該專案看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="ac811-309">That entry looks like the following:</span></span>

[!code-xml[Main](membership/samples/sample6.xml)]

<span data-ttu-id="ac811-310">以下是 Initialize 方法的範例。</span><span class="sxs-lookup"><span data-stu-id="ac811-310">Here is an example of the Initialize method.</span></span>

[!code-csharp[Main](membership/samples/sample7.cs)]

<span data-ttu-id="ac811-311">若要在提交登入表單時驗證使用者，您將需要使用 ValidateUser 方法。</span><span class="sxs-lookup"><span data-stu-id="ac811-311">In order to validate the user when they submit your login form, you will need to use the ValidateUser method.</span></span> <span data-ttu-id="ac811-312">這個方法會在使用者按一下登入控制項中的 [登入] 按鈕時引發。</span><span class="sxs-lookup"><span data-stu-id="ac811-312">This method fires when the user clicks the login button in the Login control.</span></span> <span data-ttu-id="ac811-313">您將會在此方法中放置執行使用者查閱的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ac811-313">You will place your code that does the user lookup in this method.</span></span>

<span data-ttu-id="ac811-314">如您所見，撰寫自己的成員資格提供者並不容易，而且可讓您擴充 ASP.NET 2.0 的這項強大功能。</span><span class="sxs-lookup"><span data-stu-id="ac811-314">As you can see, writing your own membership provider is not difficult and allows you to extend this powerful functionality of ASP.NET 2.0.</span></span>
