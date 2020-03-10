---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: 第7部分：成員資格和授權 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第7部分涵蓋成員資格和授權。
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a6a1a936e0ea29ea36721ba78f35845401f74c01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539197"
---
# <a name="part-7-membership-and-authorization"></a><span data-ttu-id="f9477-104">第7部分：成員資格和授權</span><span class="sxs-lookup"><span data-stu-id="f9477-104">Part 7: Membership and Authorization</span></span>

<span data-ttu-id="f9477-105">依[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="f9477-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="f9477-106">MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="f9477-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="f9477-107">MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。</span><span class="sxs-lookup"><span data-stu-id="f9477-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="f9477-108">本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="f9477-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="f9477-109">第7部分涵蓋成員資格和授權。</span><span class="sxs-lookup"><span data-stu-id="f9477-109">Part 7 covers Membership and Authorization.</span></span>

<span data-ttu-id="f9477-110">我們的商店經理控制器目前可供任何造訪我們網站的人存取。</span><span class="sxs-lookup"><span data-stu-id="f9477-110">Our Store Manager controller is currently accessible to anyone visiting our site.</span></span> <span data-ttu-id="f9477-111">讓我們將此變更為限制網站管理員的許可權。</span><span class="sxs-lookup"><span data-stu-id="f9477-111">Let's change this to restrict permission to site administrators.</span></span>

## <a name="adding-the-accountcontroller-and-views"></a><span data-ttu-id="f9477-112">新增 AccountController 和 Views</span><span class="sxs-lookup"><span data-stu-id="f9477-112">Adding the AccountController and Views</span></span>

<span data-ttu-id="f9477-113">[完整 ASP.NET MVC 3 Web 應用程式] 範本和 [ASP.NET MVC 3 空白 Web 應用程式] 範本之間有一個差異，就是空白範本不包含帳戶控制器。</span><span class="sxs-lookup"><span data-stu-id="f9477-113">One difference between the full ASP.NET MVC 3 Web Application template and the ASP.NET MVC 3 Empty Web Application template is that the empty template doesn't include an Account Controller.</span></span> <span data-ttu-id="f9477-114">我們會透過從完整的 ASP.NET MVC 3 Web 應用程式範本建立的新 ASP.NET MVC 應用程式複製一些檔案，以新增帳戶控制器。</span><span class="sxs-lookup"><span data-stu-id="f9477-114">We'll add an Account Controller by copying a few files from a new ASP.NET MVC application created from the full ASP.NET MVC 3 Web Application template.</span></span>

<span data-ttu-id="f9477-115">使用完整的 ASP.NET MVC 3 Web 應用程式範本建立新的 ASP.NET MVC 應用程式，並將下列檔案複製到專案中的相同目錄：</span><span class="sxs-lookup"><span data-stu-id="f9477-115">Create a new ASP.NET MVC application using the full ASP.NET MVC 3 Web Application template and copy the following files into the same directories in our project:</span></span>

1. <span data-ttu-id="f9477-116">複製控制器目錄中的 AccountController.cs</span><span class="sxs-lookup"><span data-stu-id="f9477-116">Copy AccountController.cs in the Controllers directory</span></span>
2. <span data-ttu-id="f9477-117">複製模型目錄中的 AccountModels</span><span class="sxs-lookup"><span data-stu-id="f9477-117">Copy AccountModels in the Models directory</span></span>
3. <span data-ttu-id="f9477-118">在 Views 目錄中建立帳戶目錄，並複製中的所有四個視圖</span><span class="sxs-lookup"><span data-stu-id="f9477-118">Create an Account directory inside the Views directory and copy all four views in</span></span>

<span data-ttu-id="f9477-119">變更控制器和模型類別的命名空間，使其開頭為 MvcMusicStore。</span><span class="sxs-lookup"><span data-stu-id="f9477-119">Change the namespace for the Controller and Model classes so they begin with MvcMusicStore.</span></span> <span data-ttu-id="f9477-120">AccountController 類別應該使用 MvcMusicStore 命名空間，而 AccountModels 類別應該使用 MvcMusicStore. 模型命名空間。</span><span class="sxs-lookup"><span data-stu-id="f9477-120">The AccountController class should use the MvcMusicStore.Controllers namespace, and the AccountModels class should use the MvcMusicStore.Models namespace.</span></span>

<span data-ttu-id="f9477-121">*注意：這些檔案也可從我們在本教學課程開頭複製網站設計檔案的 MvcMusicStore-Assets 下載中取得。成員資格檔案位於 Code 目錄中。*</span><span class="sxs-lookup"><span data-stu-id="f9477-121">*Note: These files are also available in the MvcMusicStore-Assets.zip download from which we copied our site design files at the beginning of the tutorial. The Membership files are located in the Code directory.*</span></span>

<span data-ttu-id="f9477-122">更新後的解決方案看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="f9477-122">The updated solution should look like the following:</span></span>

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a><span data-ttu-id="f9477-123">使用 ASP.NET 設定網站新增系統管理使用者</span><span class="sxs-lookup"><span data-stu-id="f9477-123">Adding an Administrative User with the ASP.NET Configuration site</span></span>

<span data-ttu-id="f9477-124">在我們的網站要求授權之前，我們必須先建立具有存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="f9477-124">Before we require Authorization in our website, we'll need to create a user with access.</span></span> <span data-ttu-id="f9477-125">建立使用者最簡單的方式是使用內建的 ASP.NET 設定網站。</span><span class="sxs-lookup"><span data-stu-id="f9477-125">The easiest way to create a user is to use the built-in ASP.NET Configuration website.</span></span>

<span data-ttu-id="f9477-126">按一下方案總管中的圖示，啟動 ASP.NET 設定網站。</span><span class="sxs-lookup"><span data-stu-id="f9477-126">Launch the ASP.NET Configuration website by clicking following the icon in the Solution Explorer.</span></span>

![](mvc-music-store-part-7/_static/image2.png)

<span data-ttu-id="f9477-127">這會啟動設定網站。</span><span class="sxs-lookup"><span data-stu-id="f9477-127">This launches a configuration website.</span></span> <span data-ttu-id="f9477-128">按一下 [首頁] 畫面上的 [安全性] 索引標籤，然後按一下畫面中央的 [啟用角色] 連結。</span><span class="sxs-lookup"><span data-stu-id="f9477-128">Click on the Security tab on the home screen, then click the "Enable roles" link in the center of the screen.</span></span>

![](mvc-music-store-part-7/_static/image3.png)

<span data-ttu-id="f9477-129">按一下 [建立或管理角色] 連結。</span><span class="sxs-lookup"><span data-stu-id="f9477-129">Click the "Create or Manage roles" link.</span></span>

![](mvc-music-store-part-7/_static/image4.png)

<span data-ttu-id="f9477-130">輸入 "Administrator" 作為角色名稱，然後按 [新增角色] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9477-130">Enter "Administrator" as the role name and press the Add Role button.</span></span>

![](mvc-music-store-part-7/_static/image5.png)

<span data-ttu-id="f9477-131">按一下 [上一步] 按鈕，然後按一下左側的 [建立使用者] 連結。</span><span class="sxs-lookup"><span data-stu-id="f9477-131">Click the Back button, then click on the Create user link on the left side.</span></span>

![](mvc-music-store-part-7/_static/image6.png)

<span data-ttu-id="f9477-132">使用下列資訊填寫左側的 [使用者資訊] 欄位：</span><span class="sxs-lookup"><span data-stu-id="f9477-132">Fill in the user information fields on the left using the following information:</span></span>

| <span data-ttu-id="f9477-133">**欄位**</span><span class="sxs-lookup"><span data-stu-id="f9477-133">**Field**</span></span> | <span data-ttu-id="f9477-134">**值**</span><span class="sxs-lookup"><span data-stu-id="f9477-134">**Value**</span></span> |
| --- | --- |
| <span data-ttu-id="f9477-135">**使用者名稱**</span><span class="sxs-lookup"><span data-stu-id="f9477-135">**User Name**</span></span> | <span data-ttu-id="f9477-136">系統管理員</span><span class="sxs-lookup"><span data-stu-id="f9477-136">Administrator</span></span> |
| <span data-ttu-id="f9477-137">**密碼**</span><span class="sxs-lookup"><span data-stu-id="f9477-137">**Password**</span></span> | <span data-ttu-id="f9477-138">password123!</span><span class="sxs-lookup"><span data-stu-id="f9477-138">password123!</span></span> |
| <span data-ttu-id="f9477-139">**確認密碼**</span><span class="sxs-lookup"><span data-stu-id="f9477-139">**Confirm Password**</span></span> | <span data-ttu-id="f9477-140">password123!</span><span class="sxs-lookup"><span data-stu-id="f9477-140">password123!</span></span> |
| <span data-ttu-id="f9477-141">**電子郵件**</span><span class="sxs-lookup"><span data-stu-id="f9477-141">**E-mail**</span></span> | <span data-ttu-id="f9477-142">（任何電子郵件地址都可使用）</span><span class="sxs-lookup"><span data-stu-id="f9477-142">(any email address will work)</span></span> |
| <span data-ttu-id="f9477-143">**安全性問題**</span><span class="sxs-lookup"><span data-stu-id="f9477-143">**Security Question**</span></span> | <span data-ttu-id="f9477-144">（任何您喜歡的）</span><span class="sxs-lookup"><span data-stu-id="f9477-144">(whatever you like)</span></span> |
| <span data-ttu-id="f9477-145">**安全性解答**</span><span class="sxs-lookup"><span data-stu-id="f9477-145">**Security Answer**</span></span> | <span data-ttu-id="f9477-146">（任何您喜歡的）</span><span class="sxs-lookup"><span data-stu-id="f9477-146">(whatever you like)</span></span> |

<span data-ttu-id="f9477-147">*注意：當然，您可以使用任何您想要的密碼。預設的密碼安全性設定需要7個字元長的密碼，且包含一個非英數位元。*</span><span class="sxs-lookup"><span data-stu-id="f9477-147">*Note: You can of course use any password you'd like. The default password security settings require a password that is 7 characters long and contains one non-alphanumeric character.*</span></span>

<span data-ttu-id="f9477-148">選取此使用者的系統管理員角色，然後按一下 [建立使用者] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9477-148">Select the Administrator role for this user, and click the Create User button.</span></span>

![](mvc-music-store-part-7/_static/image7.png)

<span data-ttu-id="f9477-149">此時，您應該會看到一則訊息，指出已成功建立使用者。</span><span class="sxs-lookup"><span data-stu-id="f9477-149">At this point, you should see a message indicating that the user was created successfully.</span></span>

![](mvc-music-store-part-7/_static/image8.png)

<span data-ttu-id="f9477-150">您現在可以關閉瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="f9477-150">You can now close the browser window.</span></span>

## <a name="role-based-authorization"></a><span data-ttu-id="f9477-151">以角色為基礎的授權</span><span class="sxs-lookup"><span data-stu-id="f9477-151">Role-based Authorization</span></span>

<span data-ttu-id="f9477-152">現在我們可以使用 [授權] 屬性來限制對 StoreManagerController 的存取，指定使用者必須是系統管理員角色，才能存取類別中的任何控制器動作。</span><span class="sxs-lookup"><span data-stu-id="f9477-152">Now we can restrict access to the StoreManagerController using the [Authorize] attribute, specifying that the user must be in the Administrator role to access any controller action in the class.</span></span>

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

<span data-ttu-id="f9477-153">*注意： [授權] 屬性可以放在特定動作方法以及控制器類別層級上。*</span><span class="sxs-lookup"><span data-stu-id="f9477-153">*Note: The [Authorize] attribute can be placed on specific action methods as well as at the Controller class level.*</span></span>

<span data-ttu-id="f9477-154">現在流覽至/StoreManager 會顯示 [登入] 對話方塊：</span><span class="sxs-lookup"><span data-stu-id="f9477-154">Now browsing to /StoreManager brings up a Log On dialog:</span></span>

![](mvc-music-store-part-7/_static/image9.png)

<span data-ttu-id="f9477-155">以新的系統管理員帳戶登入之後，我們就能夠如先前一樣前往專輯編輯畫面。</span><span class="sxs-lookup"><span data-stu-id="f9477-155">After logging on with our new Administrator account, we're able to go to the Album Edit screen as before.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f9477-156">[上一頁](mvc-music-store-part-6.md)
> [下一頁](mvc-music-store-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="f9477-156">[Previous](mvc-music-store-part-6.md)
[Next](mvc-music-store-part-8.md)</span></span>
