---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 使用驗證和授權保護應用程式 |Microsoft Docs
author: microsoft
description: 步驟9顯示如何新增驗證和授權來保護我們的 NerdDinner 應用程式，讓使用者必須註冊並登入網站以建立 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8d509c5f15bb4d5014e53b8dc2a736454238e72c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600979"
---
# <a name="secure-applications-using-authentication-and-authorization"></a><span data-ttu-id="37dcf-103">保護使用驗證和授權的應用程式</span><span class="sxs-lookup"><span data-stu-id="37dcf-103">Secure Applications Using Authentication and Authorization</span></span>

<span data-ttu-id="37dcf-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="37dcf-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="37dcf-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="37dcf-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="37dcf-106">這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟9，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="37dcf-106">This is step 9 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="37dcf-107">步驟9顯示如何新增驗證和授權來保護我們的 NerdDinner 應用程式，讓使用者必須註冊並登入網站以建立新的 dinners，而且只有主控晚餐的使用者可以稍後再編輯。</span><span class="sxs-lookup"><span data-stu-id="37dcf-107">Step 9 shows how to add authentication and authorization to secure our NerdDinner application, so that users need to register and login to the site to create new dinners, and only the user who is hosting a dinner can edit it later.</span></span>
> 
> <span data-ttu-id="37dcf-108">如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="37dcf-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-9-authentication-and-authorization"></a><span data-ttu-id="37dcf-109">NerdDinner 步驟9：驗證和授權</span><span class="sxs-lookup"><span data-stu-id="37dcf-109">NerdDinner Step 9: Authentication and Authorization</span></span>

<span data-ttu-id="37dcf-110">我們的 NerdDinner 應用程式現在會授與網站建立和編輯任何晚餐之詳細資料的能力。</span><span class="sxs-lookup"><span data-stu-id="37dcf-110">Right now our NerdDinner application grants anyone visiting the site the ability to create and edit the details of any dinner.</span></span> <span data-ttu-id="37dcf-111">讓我們變更此動作，讓使用者必須註冊並登入網站以建立新的 dinners，並新增限制，如此一來，只有主控晚餐的使用者可以稍後再編輯。</span><span class="sxs-lookup"><span data-stu-id="37dcf-111">Let's change this so that users need to register and login to the site to create new dinners, and add a restriction so that only the user who is hosting a dinner can edit it later.</span></span>

<span data-ttu-id="37dcf-112">為此，我們將使用驗證和授權來保護應用程式。</span><span class="sxs-lookup"><span data-stu-id="37dcf-112">To enable this we'll use authentication and authorization to secure our application.</span></span>

### <a name="understanding-authentication-and-authorization"></a><span data-ttu-id="37dcf-113">瞭解驗證和授權</span><span class="sxs-lookup"><span data-stu-id="37dcf-113">Understanding Authentication and Authorization</span></span>

<span data-ttu-id="37dcf-114">*驗證*是識別和驗證存取應用程式之用戶端的身分識別的程式。</span><span class="sxs-lookup"><span data-stu-id="37dcf-114">*Authentication* is the process of identifying and validating the identity of a client accessing an application.</span></span> <span data-ttu-id="37dcf-115">更簡單的說，就是識別使用者流覽網站時的「使用者」。</span><span class="sxs-lookup"><span data-stu-id="37dcf-115">Put more simply, it is about identifying "who" the end-user is when they visit a website.</span></span> <span data-ttu-id="37dcf-116">ASP.NET 支援多種方式來驗證瀏覽器使用者。</span><span class="sxs-lookup"><span data-stu-id="37dcf-116">ASP.NET supports multiple ways to authenticate browser users.</span></span> <span data-ttu-id="37dcf-117">針對網際網路 web 應用程式，最常見的驗證方法稱為「表單驗證」。</span><span class="sxs-lookup"><span data-stu-id="37dcf-117">For Internet web applications, the most common authentication approach used is called "Forms Authentication".</span></span> <span data-ttu-id="37dcf-118">表單驗證可讓開發人員在其應用程式中撰寫 HTML 登入表單，然後驗證使用者針對資料庫或其他密碼認證存放區提交的使用者名稱/密碼。</span><span class="sxs-lookup"><span data-stu-id="37dcf-118">Forms Authentication enables a developer to author an HTML login form within their application, and then validate the username/password an end-user submits against a database or other password credential store.</span></span> <span data-ttu-id="37dcf-119">如果使用者名稱/密碼的組合正確，開發人員就可以要求 ASP.NET 發出加密的 HTTP cookie，以在未來的要求中識別使用者。</span><span class="sxs-lookup"><span data-stu-id="37dcf-119">If the username/password combination is correct, the developer can then ask ASP.NET to issue an encrypted HTTP cookie to identify the user across future requests.</span></span> <span data-ttu-id="37dcf-120">我們會使用表單驗證搭配我們的 NerdDinner 應用程式。</span><span class="sxs-lookup"><span data-stu-id="37dcf-120">We'll by using forms authentication with our NerdDinner application.</span></span>

<span data-ttu-id="37dcf-121">「授權」（ *Authorization* ）是判斷已驗證的使用者是否有權存取特定 URL/資源或執行某個動作的程式。</span><span class="sxs-lookup"><span data-stu-id="37dcf-121">*Authorization* is the process of determining whether an authenticated user has permission to access a particular URL/resource or to perform some action.</span></span> <span data-ttu-id="37dcf-122">例如，在我們的 NerdDinner 應用程式中，我們會想要授權只有登入的使用者可以存取 */Dinners/Create* URL，並建立新的 Dinners。</span><span class="sxs-lookup"><span data-stu-id="37dcf-122">For example, within our NerdDinner application we'll want to authorize that only users who are logged in can access the */Dinners/Create* URL and create new Dinners.</span></span> <span data-ttu-id="37dcf-123">我們也會想要新增授權邏輯，讓只有主控晚餐的使用者可以編輯它，並拒絕其他所有使用者的編輯存取。</span><span class="sxs-lookup"><span data-stu-id="37dcf-123">We'll also want to add authorization logic so that only the user who is hosting a dinner can edit it – and deny edit access to all other users.</span></span>

### <a name="forms-authentication-and-the-accountcontroller"></a><span data-ttu-id="37dcf-124">表單驗證和 AccountController</span><span class="sxs-lookup"><span data-stu-id="37dcf-124">Forms Authentication and the AccountController</span></span>

<span data-ttu-id="37dcf-125">ASP.NET MVC 的預設 Visual Studio 專案範本會在建立新的 ASP.NET MVC 應用程式時，自動啟用表單驗證。</span><span class="sxs-lookup"><span data-stu-id="37dcf-125">The default Visual Studio project template for ASP.NET MVC automatically enables forms authentication when new ASP.NET MVC applications are created.</span></span> <span data-ttu-id="37dcf-126">它也會自動將預先建立的帳戶登入頁面執行加入至專案中，這可讓您輕鬆地整合網站內的安全性。</span><span class="sxs-lookup"><span data-stu-id="37dcf-126">It also automatically adds a pre-built account login page implementation to the project – which makes it really easy to integrate security within a site.</span></span>

<span data-ttu-id="37dcf-127">[預設的網站] 主版頁面會在使用者存取時，于網站右上角顯示「登入」連結（未通過驗證）：</span><span class="sxs-lookup"><span data-stu-id="37dcf-127">The default Site.master master page displays a "Log On" link at the top-right of the site when the user accessing it is not authenticated:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

<span data-ttu-id="37dcf-128">按一下 [登入] 連結會將使用者帶到 */Account/LogOn* URL：</span><span class="sxs-lookup"><span data-stu-id="37dcf-128">Clicking the "Log On" link takes a user to the */Account/LogOn* URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

<span data-ttu-id="37dcf-129">尚未註冊的訪客可以按一下 [註冊] 連結來執行此動作，這會將其帶至 */Account/Register* URL，並允許他們輸入帳戶詳細資料：</span><span class="sxs-lookup"><span data-stu-id="37dcf-129">Visitors who haven't registered can do so by clicking the "Register" link – which will take them to the */Account/Register* URL and allow them to enter account details:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

<span data-ttu-id="37dcf-130">按一下 [註冊] 按鈕會在 ASP.NET 成員資格系統中建立新的使用者，並使用表單驗證在網站上驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="37dcf-130">Clicking the "Register" button will create a new user within the ASP.NET Membership system, and authenticate the user onto the site using forms authentication.</span></span>

<span data-ttu-id="37dcf-131">當使用者登入時，網站主要會變更頁面的右上方，以輸出「歡迎 [使用者名稱]！」</span><span class="sxs-lookup"><span data-stu-id="37dcf-131">When a user is logged-in, the Site.master changes the top-right of the page to output a "Welcome [username]!"</span></span> <span data-ttu-id="37dcf-132">訊息並呈現「登出」連結，而不是「登入」。</span><span class="sxs-lookup"><span data-stu-id="37dcf-132">message and renders a "Log Off" link instead of a "Log On" one.</span></span> <span data-ttu-id="37dcf-133">按一下 [登出] 連結會登出使用者：</span><span class="sxs-lookup"><span data-stu-id="37dcf-133">Clicking the "Log Off" link logs out the user:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

<span data-ttu-id="37dcf-134">上述登入、登出和註冊功能會在 AccountController 類別中實作為其建立專案時 Visual Studio 加入至專案中。</span><span class="sxs-lookup"><span data-stu-id="37dcf-134">The above login, logout, and registration functionality is implemented within the AccountController class that was added to our project by Visual Studio when it created the project.</span></span> <span data-ttu-id="37dcf-135">AccountController 的 UI 是使用 \Views\Account 目錄內的視圖範本來執行：</span><span class="sxs-lookup"><span data-stu-id="37dcf-135">The UI for the AccountController is implemented using view templates within the \Views\Account directory:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

<span data-ttu-id="37dcf-136">AccountController 類別會使用 ASP.NET 表單驗證系統來發出加密的驗證 cookie，以及用來儲存和驗證使用者名稱/密碼的 ASP.NET 成員資格 API。</span><span class="sxs-lookup"><span data-stu-id="37dcf-136">The AccountController class uses the ASP.NET Forms Authentication system to issue encrypted authentication cookies, and the ASP.NET Membership API to store and validate usernames/passwords.</span></span> <span data-ttu-id="37dcf-137">ASP.NET 成員資格 API 是可擴充的，可讓您使用任何密碼認證存放區。</span><span class="sxs-lookup"><span data-stu-id="37dcf-137">The ASP.NET Membership API is extensible and enables any password credential store to be used.</span></span> <span data-ttu-id="37dcf-138">ASP.NET 隨附內建的成員資格提供者，可將使用者名稱/密碼儲存在 SQL 資料庫中，或在 Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="37dcf-138">ASP.NET ships with built-in membership provider implementations that store username/passwords within a SQL database, or within Active Directory.</span></span>

<span data-ttu-id="37dcf-139">我們可以藉由開啟專案根目錄中的 "web.config" 檔案，並尋找其中的 &lt;成員資格&gt; 區段，設定我們的 NerdDinner 應用程式應使用的成員資格提供者。</span><span class="sxs-lookup"><span data-stu-id="37dcf-139">We can configure which membership provider our NerdDinner application should use by opening the "web.config" file at the root of the project and looking for the &lt;membership&gt; section within it.</span></span> <span data-ttu-id="37dcf-140">建立專案時新增的預設 web.config 會註冊 SQL 成員資格提供者，並將它設定為使用名為 "Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception" 的連接字串來指定資料庫位置。</span><span class="sxs-lookup"><span data-stu-id="37dcf-140">The default web.config added when the project was created registers the SQL membership provider, and configures it to use a connection-string named "ApplicationServices" to specify the database location.</span></span>

<span data-ttu-id="37dcf-141">預設的 "Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception" 連接字串（在 web.config 檔案的 &lt;connectionStrings&gt; 區段中指定）會設定為使用 SQL Express。</span><span class="sxs-lookup"><span data-stu-id="37dcf-141">The default "ApplicationServices" connection string (which is specified within the &lt;connectionStrings&gt; section of the web.config file) is configured to use SQL Express.</span></span> <span data-ttu-id="37dcf-142">它會指向名為 "ASPNETDB.MDF" 的 SQL Express 資料庫。應用程式的 "App\_Data" 目錄底下的 .MDF "。</span><span class="sxs-lookup"><span data-stu-id="37dcf-142">It points to a SQL Express database named "ASPNETDB.MDF" under the application's "App\_Data" directory.</span></span> <span data-ttu-id="37dcf-143">如果在應用程式中第一次使用成員資格 API 時，此資料庫不存在，則 ASP.NET 會自動建立資料庫，並在其中布建適當的成員資格資料庫架構：</span><span class="sxs-lookup"><span data-stu-id="37dcf-143">If this database doesn't exist the first time the Membership API is used within the application, ASP.NET will automatically create the database and provision the appropriate membership database schema within it:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

<span data-ttu-id="37dcf-144">如果您想要使用完整的 SQL Server 實例（或連接到遠端資料庫）而不使用 SQL Express，我們只需要更新 web.config 檔案中的 "Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception" 連接字串，並確認適當的成員資格架構已新增至其指向的資料庫。</span><span class="sxs-lookup"><span data-stu-id="37dcf-144">If instead of using SQL Express we wanted to use a full SQL Server instance (or connect to a remote database), all we'd need to-do is to update the "ApplicationServices" connection string within the web.config file and make sure that the appropriate membership schema has been added to the database it points at.</span></span> <span data-ttu-id="37dcf-145">您可以在 \Windows\Microsoft.NET\Framework\v2.0.50727\ 目錄中執行 "aspnet\_regsql" 公用程式，將成員資格和其他 ASP.NET 應用程式服務的適當架構加入至資料庫。</span><span class="sxs-lookup"><span data-stu-id="37dcf-145">You can run the "aspnet\_regsql.exe" utility within the \Windows\Microsoft.NET\Framework\v2.0.50727\ directory to add the appropriate schema for membership and the other ASP.NET application services to a database.</span></span>

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a><span data-ttu-id="37dcf-146">使用 [授權] 篩選準則授權/Dinners/Create URL</span><span class="sxs-lookup"><span data-stu-id="37dcf-146">Authorizing the /Dinners/Create URL using the [Authorize] filter</span></span>

<span data-ttu-id="37dcf-147">我們不需要撰寫任何程式碼來啟用 NerdDinner 應用程式的安全驗證和帳戶管理。</span><span class="sxs-lookup"><span data-stu-id="37dcf-147">We didn't have to write any code to enable a secure authentication and account management implementation for the NerdDinner application.</span></span> <span data-ttu-id="37dcf-148">使用者可以向應用程式註冊新帳戶，以及登入/登出網站。</span><span class="sxs-lookup"><span data-stu-id="37dcf-148">Users can register new accounts with our application, and login/logout of the site.</span></span>

<span data-ttu-id="37dcf-149">現在，我們可以將授權邏輯新增至應用程式，並使用訪客的驗證狀態和使用者名稱來控制他們在網站內可以和不能執行的動作。</span><span class="sxs-lookup"><span data-stu-id="37dcf-149">Now we can add authorization logic to the application, and use the authentication status and username of visitors to control what they can and can't do within the site.</span></span> <span data-ttu-id="37dcf-150">讓我們從將授權邏輯新增至 DinnersController 類別的「建立」動作方法開始。</span><span class="sxs-lookup"><span data-stu-id="37dcf-150">Let's begin by adding authorization logic to the "Create" action methods of our DinnersController class.</span></span> <span data-ttu-id="37dcf-151">具體而言，我們會要求存取 */Dinners/Create* URL 的使用者必須登入。</span><span class="sxs-lookup"><span data-stu-id="37dcf-151">Specifically, we will require that users accessing the */Dinners/Create* URL must be logged in.</span></span> <span data-ttu-id="37dcf-152">如果未登入，我們會將它們重新導向至登入頁面，讓他們可以登入。</span><span class="sxs-lookup"><span data-stu-id="37dcf-152">If they aren't logged in we'll redirect them to the login page so that they can sign-in.</span></span>

<span data-ttu-id="37dcf-153">執行此邏輯相當簡單。</span><span class="sxs-lookup"><span data-stu-id="37dcf-153">Implementing this logic is pretty easy.</span></span> <span data-ttu-id="37dcf-154">我們只需要將 [授權] 篩選屬性新增至我們的 Create 動作方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="37dcf-154">All we need to-do is to add an [Authorize] filter attribute to our Create action methods like so:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

<span data-ttu-id="37dcf-155">ASP.NET MVC 支援建立「動作篩選準則」的功能，可用來執行可透過宣告方式套用至動作方法的重複使用邏輯。</span><span class="sxs-lookup"><span data-stu-id="37dcf-155">ASP.NET MVC supports the ability to create "action filters" that can be used to implement re-usable logic that can be declaratively applied to action methods.</span></span> <span data-ttu-id="37dcf-156">[授權] 篩選是 ASP.NET MVC 提供的其中一個內建動作篩選準則，可讓開發人員以宣告方式將授權規則套用至動作方法和控制器類別。</span><span class="sxs-lookup"><span data-stu-id="37dcf-156">The [Authorize] filter is one of the built-in action filters provided by ASP.NET MVC, and it enables a developer to declaratively apply authorization rules to action methods and controller classes.</span></span>

<span data-ttu-id="37dcf-157">套用時，如果沒有任何參數（如上面所示），[授權] 篩選準則會強制執行動作方法要求的使用者必須登入，而且如果不是，則會自動將瀏覽器重新導向至登入 URL。</span><span class="sxs-lookup"><span data-stu-id="37dcf-157">When applied without any parameters (like above) the [Authorize] filter enforces that the user making the action method request must be logged in – and it will automatically redirect the browser to the login URL if they aren't.</span></span> <span data-ttu-id="37dcf-158">執行此重新導向時，原先要求的 URL 會當做 querystring 引數傳遞（例如：/Account/LogOn？ReturnUrl =% 2fDinners% 2fCreate）。</span><span class="sxs-lookup"><span data-stu-id="37dcf-158">When doing this redirect the originally requested URL is passed as a querystring argument (for example: /Account/LogOn?ReturnUrl=%2fDinners%2fCreate).</span></span> <span data-ttu-id="37dcf-159">然後，AccountController 會在使用者登入後，將其重新導向回到原始要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="37dcf-159">The AccountController will then redirect the user back to the originally requested URL once they login.</span></span>

<span data-ttu-id="37dcf-160">[授權] 篩選準則可選擇性地支援指定「使用者」或「角色」內容的能力，此屬性可用來要求使用者必須登入，並在允許的使用者清單中，或是允許的安全性角色的成員。</span><span class="sxs-lookup"><span data-stu-id="37dcf-160">The [Authorize] filter optionally supports the ability to specify a "Users" or "Roles" property that can be used to require that the user is both logged in and within a list of allowed users or a member of an allowed security role.</span></span> <span data-ttu-id="37dcf-161">例如，下列程式碼只允許兩個特定的使用者 "scottgu" 和 "billg" 存取/Dinners/Create URL：</span><span class="sxs-lookup"><span data-stu-id="37dcf-161">For example, the code below only allows two specific users, "scottgu" and "billg", to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

<span data-ttu-id="37dcf-162">不過，在程式碼中內嵌特定的使用者名稱，通常是相當不容易維護的。</span><span class="sxs-lookup"><span data-stu-id="37dcf-162">Embedding specific user names within code tends to be pretty un-maintainable though.</span></span> <span data-ttu-id="37dcf-163">較好的方法是定義程式碼所檢查的較高層級「角色」，然後使用資料庫或 active directory 系統（讓實際的使用者對應清單從程式碼外部儲存），將使用者對應至角色。</span><span class="sxs-lookup"><span data-stu-id="37dcf-163">A better approach is to define higher-level "roles" that the code checks against, and then to map users into the role using either a database or active directory system (enabling the actual user mapping list to be stored externally from the code).</span></span> <span data-ttu-id="37dcf-164">ASP.NET 包含內建角色管理 API，以及一組內建的角色提供者（包括適用于 SQL 和 Active Directory），可協助執行此使用者/角色對應。</span><span class="sxs-lookup"><span data-stu-id="37dcf-164">ASP.NET includes a built-in role management API as well as a built-in set of role providers (including ones for SQL and Active Directory) that can help perform this user/role mapping.</span></span> <span data-ttu-id="37dcf-165">然後，我們可以更新程式碼，只允許特定「系統管理員」角色內的使用者存取/Dinners/Create URL：</span><span class="sxs-lookup"><span data-stu-id="37dcf-165">We could then update the code to only allow users within a specific "admin" role to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a><span data-ttu-id="37dcf-166">建立 Dinners 時使用 User.Identity.Name 屬性</span><span class="sxs-lookup"><span data-stu-id="37dcf-166">Using the User.Identity.Name property when Creating Dinners</span></span>

<span data-ttu-id="37dcf-167">我們可以使用控制器基類上公開的 User.Identity.Name 屬性，來抓取要求目前登入使用者的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="37dcf-167">We can retrieve the username of the currently logged-in user of a request using the User.Identity.Name property exposed on the Controller base class.</span></span>

<span data-ttu-id="37dcf-168">先前當我們實作為 Create （）動作方法的 HTTP POST 版本時，我們已將晚餐的 "HostedBy" 屬性硬式編碼為靜態字串。</span><span class="sxs-lookup"><span data-stu-id="37dcf-168">Earlier when we implemented the HTTP-POST version of our Create() action method we had hardcoded the "HostedBy" property of the Dinner to a static string.</span></span> <span data-ttu-id="37dcf-169">我們現在可以更新此程式碼，改為使用 User.Identity.Name 屬性，並為建立晚餐的主機自動新增一個 RSVP：</span><span class="sxs-lookup"><span data-stu-id="37dcf-169">We can now update this code to instead use the User.Identity.Name property, as well as automatically add an RSVP for the host creating the Dinner:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

<span data-ttu-id="37dcf-170">因為我們已將 [授權] 屬性新增至 Create （）方法，所以 ASP.NET MVC 會確保只有在流覽/Dinners/Create URL 的使用者登入網站時，才會執行動作方法。</span><span class="sxs-lookup"><span data-stu-id="37dcf-170">Because we have added an [Authorize] attribute to the Create() method, ASP.NET MVC ensures that the action method only executes if the user visiting the /Dinners/Create URL is logged in on the site.</span></span> <span data-ttu-id="37dcf-171">因此，User.Identity.Name 屬性值一律會包含有效的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="37dcf-171">As such, the User.Identity.Name property value will always contain a valid username.</span></span>

### <a name="using-the-useridentityname-property-when-editing-dinners"></a><span data-ttu-id="37dcf-172">編輯 Dinners 時使用 User.Identity.Name 屬性</span><span class="sxs-lookup"><span data-stu-id="37dcf-172">Using the User.Identity.Name property when Editing Dinners</span></span>

<span data-ttu-id="37dcf-173">現在讓我們新增一些授權邏輯，以限制使用者只能編輯其本身所裝載之 dinners 的屬性。</span><span class="sxs-lookup"><span data-stu-id="37dcf-173">Let's now add some authorization logic that restricts users so that they can only edit the properties of dinners they themselves are hosting.</span></span>

<span data-ttu-id="37dcf-174">為協助解決此情況，我們會先將「IsHostedBy （使用者名稱）」 helper 方法新增至晚餐物件（在我們稍早建立的 Dinner.cs 部分類別中）。</span><span class="sxs-lookup"><span data-stu-id="37dcf-174">To help with this, we'll first add an "IsHostedBy(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="37dcf-175">根據提供的使用者名稱是否與晚餐 HostedBy 屬性相符，此 helper 方法會傳回 true 或 false，並封裝對其執行不區分大小寫字串比較所需的邏輯：</span><span class="sxs-lookup"><span data-stu-id="37dcf-175">This helper method returns true or false depending on whether a supplied username matches the Dinner HostedBy property, and encapsulates the logic necessary to perform a case-insensitive string comparison of them:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

<span data-ttu-id="37dcf-176">然後，我們會在 DinnersController 類別內的 Edit （）動作方法中新增 [授權] 屬性。</span><span class="sxs-lookup"><span data-stu-id="37dcf-176">We'll then add an [Authorize] attribute to the Edit() action methods within our DinnersController class.</span></span> <span data-ttu-id="37dcf-177">這可確保使用者必須登入，才能要求 */Dinners/Edit/[id]* URL。</span><span class="sxs-lookup"><span data-stu-id="37dcf-177">This will ensure that users must be logged in to request a */Dinners/Edit/[id]* URL.</span></span>

<span data-ttu-id="37dcf-178">然後，我們可以將程式碼新增至我們的編輯方法，以使用 IsHostedBy （使用者名稱） helper 方法來確認登入的使用者是否符合晚餐主機。</span><span class="sxs-lookup"><span data-stu-id="37dcf-178">We can then add code to our Edit methods that uses the Dinner.IsHostedBy(username) helper method to verify that the logged-in user matches the Dinner host.</span></span> <span data-ttu-id="37dcf-179">如果使用者不是主機，我們會顯示「InvalidOwner」視圖並結束要求。</span><span class="sxs-lookup"><span data-stu-id="37dcf-179">If the user is not the host, we'll display an "InvalidOwner" view and terminate the request.</span></span> <span data-ttu-id="37dcf-180">執行此動作的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="37dcf-180">The code to do this looks like below:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

<span data-ttu-id="37dcf-181">然後，我們可以在 \Views\Dinners 目錄上按一下滑鼠右鍵，然後選擇 [加入&gt;View] 功能表命令，以建立新的 "InvalidOwner" 視圖。</span><span class="sxs-lookup"><span data-stu-id="37dcf-181">We can then right-click on the \Views\Dinners directory and choose the Add-&gt;View menu command to create a new "InvalidOwner" view.</span></span> <span data-ttu-id="37dcf-182">我們會在其中填入下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="37dcf-182">We'll populate it with the below error message:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

<span data-ttu-id="37dcf-183">現在當使用者嘗試編輯他們不擁有的晚餐時，他們會收到錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="37dcf-183">And now when a user attempts to edit a dinner they don't own, they'll get an error message:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

<span data-ttu-id="37dcf-184">我們可以對控制器內的 Delete （）動作方法重複相同的步驟，以鎖定刪除 Dinners 的許可權，並確保只有晚餐的主機可以將其刪除。</span><span class="sxs-lookup"><span data-stu-id="37dcf-184">We can repeat the same steps for the Delete() action methods within our controller to lock down permission to delete Dinners as well, and ensure that only the host of a Dinner can delete it.</span></span>

### <a name="showinghiding-edit-and-delete-links"></a><span data-ttu-id="37dcf-185">顯示/隱藏編輯和刪除連結</span><span class="sxs-lookup"><span data-stu-id="37dcf-185">Showing/Hiding Edit and Delete Links</span></span>

<span data-ttu-id="37dcf-186">我們會從詳細資料 URL 連結到 DinnersController 類別的 [編輯] 和 [刪除] 動作方法：</span><span class="sxs-lookup"><span data-stu-id="37dcf-186">We are linking to the Edit and Delete action method of our DinnersController class from our Details URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

<span data-ttu-id="37dcf-187">目前，我們會顯示 [編輯] 和 [刪除] 動作連結，而不論詳細資料 URL 的訪客是否為晚餐的主機。</span><span class="sxs-lookup"><span data-stu-id="37dcf-187">Currently we are showing the Edit and Delete action links regardless of whether the visitor to the details URL is the host of the dinner.</span></span> <span data-ttu-id="37dcf-188">讓我們變更此項，如此一來，只有在造訪的使用者是晚餐的擁有者時，才會顯示連結。</span><span class="sxs-lookup"><span data-stu-id="37dcf-188">Let's change this so that the links are only displayed if the visiting user is the owner of the dinner.</span></span>

<span data-ttu-id="37dcf-189">DinnersController 內的 Details （）動作方法會抓取晚餐物件，然後將它當做模型物件傳遞至我們的 view 範本：</span><span class="sxs-lookup"><span data-stu-id="37dcf-189">The Details() action method within our DinnersController retrieves a Dinner object and then passes it as the model object to our view template:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

<span data-ttu-id="37dcf-190">我們可以使用 IsHostedBy （）協助程式方法來更新我們的 view 範本，以有條件地顯示/隱藏編輯和刪除連結，如下所示：</span><span class="sxs-lookup"><span data-stu-id="37dcf-190">We can update our view template to conditionally show/hide the Edit and Delete links by using the Dinner.IsHostedBy() helper method like below:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a><span data-ttu-id="37dcf-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37dcf-191">Next Steps</span></span>

<span data-ttu-id="37dcf-192">現在我們來看一下如何讓已驗證的使用者使用 AJAX 來進行 dinners。</span><span class="sxs-lookup"><span data-stu-id="37dcf-192">Let's now look at how we can enable authenticated users to RSVP for dinners using AJAX.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="37dcf-193">[上一頁](implement-efficient-data-paging.md)
> [下一頁](use-ajax-to-deliver-dynamic-updates.md)</span><span class="sxs-lookup"><span data-stu-id="37dcf-193">[Previous](implement-efficient-data-paging.md)
[Next](use-ajax-to-deliver-dynamic-updates.md)</span></span>
