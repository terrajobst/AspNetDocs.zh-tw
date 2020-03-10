---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: 使用 Razor 和不顯眼的 JavaScript 建立 MVC 3 應用程式 |Microsoft Docs
author: microsoft
description: 使用者清單範例 web 應用程式示範使用 Razor view 引擎建立 ASP.NET MVC 3 應用程式有多麼簡單。 範例應用程式 。
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: fb63493ff22c9261fc5746a998a32f2511141f87
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540982"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="c8364-104">使用 Razor 和低調的 JavaScript 建立 MVC 3 應用程式</span><span class="sxs-lookup"><span data-stu-id="c8364-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="c8364-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c8364-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c8364-106">使用者清單範例 web 應用程式示範使用 Razor view 引擎建立 ASP.NET MVC 3 應用程式有多麼簡單。</span><span class="sxs-lookup"><span data-stu-id="c8364-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="c8364-107">範例應用程式示範如何使用新的 Razor view 引擎搭配 ASP.NET MVC 第3版和 Visual Studio 2010 來建立虛構的使用者清單網站，其中包含建立、顯示、編輯和刪除使用者等功能。</span><span class="sxs-lookup"><span data-stu-id="c8364-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="c8364-108">本教學課程說明建立 MVC 3 應用程式的使用者清單範例時，所採取的步驟。</span><span class="sxs-lookup"><span data-stu-id="c8364-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="c8364-109">本主題提供具有C#和 VB 原始程式碼的 Visual Studio 專案：[下載](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)。</span><span class="sxs-lookup"><span data-stu-id="c8364-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="c8364-110">如果您對本教學課程有任何疑問，請將其張貼至[MVC 論壇](https://forums.asp.net/1146.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c8364-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="c8364-111">概觀</span><span class="sxs-lookup"><span data-stu-id="c8364-111">Overview</span></span>

<span data-ttu-id="c8364-112">您將建立的應用程式是簡單的使用者清單網站。</span><span class="sxs-lookup"><span data-stu-id="c8364-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="c8364-113">使用者可以輸入、查看及更新使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="c8364-113">Users can enter, view, and update user information.</span></span>

![範例網站](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="c8364-115">您可以在[這裡](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)下載 VB C#和已完成的專案。</span><span class="sxs-lookup"><span data-stu-id="c8364-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="c8364-116">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c8364-116">Creating the Web Application</span></span>

<span data-ttu-id="c8364-117">若要開始本教學課程，請開啟 Visual Studio 2010，並使用*ASP.NET MVC 3 Web 應用程式*範本建立新的專案。</span><span class="sxs-lookup"><span data-stu-id="c8364-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="c8364-118">將應用程式命名為 &quot;Mvc3Razor&quot;。</span><span class="sxs-lookup"><span data-stu-id="c8364-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="c8364-119">[![新的 MVC 3 專案](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="c8364-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="c8364-120">在 [**新增 ASP.NET MVC 3 專案**] 對話方塊中，選取 [**網際網路應用程式**]，選取 [Razor 視圖引擎]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="c8364-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![[新增 ASP.NET MVC 3 專案] 對話方塊](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="c8364-122">在本教學課程中，您將不會使用 ASP.NET 成員資格提供者，因此您可以刪除與登入和成員資格相關聯的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="c8364-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="c8364-123">在**方案總管**中，移除下列檔案和目錄：</span><span class="sxs-lookup"><span data-stu-id="c8364-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="c8364-124">*Controllers\AccountController*</span><span class="sxs-lookup"><span data-stu-id="c8364-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="c8364-125">*Models\AccountModels*</span><span class="sxs-lookup"><span data-stu-id="c8364-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="c8364-126">*Views\Shared\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="c8364-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="c8364-127">*Views\Account* （以及此目錄中的所有檔案）</span><span class="sxs-lookup"><span data-stu-id="c8364-127">*Views\Account* (and all the files in this directory)</span></span>

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="c8364-129">編輯\_的配置<em>cshtml</em>檔案，並將名為 `logindisplay` 的 `<div>` 元素內的標記取代為停用&quot;的 [登入] <em>&quot;</em>訊息。</span><span class="sxs-lookup"><span data-stu-id="c8364-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="c8364-130">下列範例會顯示新的標記：</span><span class="sxs-lookup"><span data-stu-id="c8364-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="c8364-131">加入模型</span><span class="sxs-lookup"><span data-stu-id="c8364-131">Adding the Model</span></span>

<span data-ttu-id="c8364-132">在**方案總管**中，以滑鼠右鍵按一下 [*模型*] 資料夾，選取 [**新增**]，然後按一下 [**類別**]。</span><span class="sxs-lookup"><span data-stu-id="c8364-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![新增使用者 Mdl 類別](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="c8364-134">將類別命名為 `UserModel`。</span><span class="sxs-lookup"><span data-stu-id="c8364-134">Name the class `UserModel`.</span></span> <span data-ttu-id="c8364-135">使用下列程式碼取代*UserModel*檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="c8364-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="c8364-136">`UserModel` 類別代表使用者。</span><span class="sxs-lookup"><span data-stu-id="c8364-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="c8364-137">類別的每個成員都會使用[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間中的[必要](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)屬性來標注。</span><span class="sxs-lookup"><span data-stu-id="c8364-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="c8364-138">[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間中的屬性會為 web 應用程式提供自動用戶端和伺服器端驗證。</span><span class="sxs-lookup"><span data-stu-id="c8364-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="c8364-139">開啟 `HomeController` 類別並加入 `using` 指示詞，讓您可以存取 `UserModel` 和 `Users` 類別：</span><span class="sxs-lookup"><span data-stu-id="c8364-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="c8364-140">在 `HomeController` 宣告之後，將下列批註和參考新增至 `Users` 類別：</span><span class="sxs-lookup"><span data-stu-id="c8364-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="c8364-141">`Users` 類別是簡化的記憶體內部資料存放區，您將在本教學課程中使用。</span><span class="sxs-lookup"><span data-stu-id="c8364-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="c8364-142">在實際的應用程式中，您會使用資料庫來儲存使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="c8364-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="c8364-143">在下列範例中，會顯示 `HomeController` 檔案的前幾行：</span><span class="sxs-lookup"><span data-stu-id="c8364-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="c8364-144">建立應用程式，以便在下一個步驟中將使用者模型提供給 [樣板]。</span><span class="sxs-lookup"><span data-stu-id="c8364-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="c8364-145">建立預設的視圖</span><span class="sxs-lookup"><span data-stu-id="c8364-145">Creating the Default View</span></span>

<span data-ttu-id="c8364-146">下一個步驟是新增動作方法和 view 來顯示使用者。</span><span class="sxs-lookup"><span data-stu-id="c8364-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="c8364-147">刪除現有的*Views\Home\Index*檔案。</span><span class="sxs-lookup"><span data-stu-id="c8364-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="c8364-148">您將建立新的*索引*檔案來顯示使用者。</span><span class="sxs-lookup"><span data-stu-id="c8364-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="c8364-149">在 `HomeController` 類別中，將 `Index` 方法的內容取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="c8364-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="c8364-150">在 `Index` 方法內按一下滑鼠右鍵，然後按一下 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="c8364-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![加入視圖](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="c8364-152">選取 [**建立強型別視圖**] 選項。</span><span class="sxs-lookup"><span data-stu-id="c8364-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="c8364-153">針對**View data class**，選取**Mvc3Razor UserModel**。</span><span class="sxs-lookup"><span data-stu-id="c8364-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="c8364-154">（如果您在 [ **View data class** ] 方塊中看不到 [ **Mvc3Razor** ]，則必須建立專案）。請確定 [view engine] 已設定為 [ **Razor**]。</span><span class="sxs-lookup"><span data-stu-id="c8364-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="c8364-155">將 [**視圖內容**] 設定為 [**清單**]，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="c8364-155">Set **View content** to **List** and then click **Add**.</span></span>

![新增索引視圖](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="c8364-157">新的視圖會自動 scaffold 傳遞至 `Index` 視圖的使用者資料。</span><span class="sxs-lookup"><span data-stu-id="c8364-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="c8364-158">檢查新產生的*Views\Home\Index*檔案。</span><span class="sxs-lookup"><span data-stu-id="c8364-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="c8364-159">[**建立新**的]、[**編輯**]、[**詳細資料**] 和 [**刪除**] 連結無法運作，但頁面的其餘部分則會正常運作。</span><span class="sxs-lookup"><span data-stu-id="c8364-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="c8364-160">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="c8364-160">Run the page.</span></span> <span data-ttu-id="c8364-161">您會看到使用者清單。</span><span class="sxs-lookup"><span data-stu-id="c8364-161">You see a list of users.</span></span>

![[索引] 頁面](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="c8364-163">開啟*Index. cshtml*檔案，並以下列程式碼取代 **[編輯**]、[**詳細資料**] 和 [**刪除**] 的 `ActionLink` 標記：</span><span class="sxs-lookup"><span data-stu-id="c8364-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="c8364-164">使用者名稱會用來作為識別碼，以在 [**編輯**]、[**詳細資料**] 和 [**刪除**] 連結中尋找選取的記錄。</span><span class="sxs-lookup"><span data-stu-id="c8364-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="c8364-165">建立詳細資料檢視</span><span class="sxs-lookup"><span data-stu-id="c8364-165">Creating the Details View</span></span>

<span data-ttu-id="c8364-166">下一個步驟是新增 `Details` 動作方法和 view，以便顯示使用者詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c8364-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![詳細資料](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="c8364-168">將下列 `Details` 方法加入至主控制器：</span><span class="sxs-lookup"><span data-stu-id="c8364-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="c8364-169">在 `Details` 方法內按一下滑鼠右鍵，然後選取 [<strong>新增視圖</strong>]。</span><span class="sxs-lookup"><span data-stu-id="c8364-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="c8364-170">確認 [ <strong>View data class</strong> ] 方塊包含<strong>Mvc3Razor。 UserModel</strong><em>。</em></span><span class="sxs-lookup"><span data-stu-id="c8364-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="c8364-171">將 [<strong>查看內容</strong>] 設定為<strong>詳細資料</strong>，然後按一下 [<strong>新增</strong>]。</span><span class="sxs-lookup"><span data-stu-id="c8364-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![新增詳細資料檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="c8364-173">執行應用程式並選取 [詳細資料] 連結。</span><span class="sxs-lookup"><span data-stu-id="c8364-173">Run the application and select a details link.</span></span> <span data-ttu-id="c8364-174">自動的範例會顯示模型中的每個屬性。</span><span class="sxs-lookup"><span data-stu-id="c8364-174">The automatic scaffolding shows each property in the model.</span></span>

![詳細資料](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="c8364-176">建立編輯檢視</span><span class="sxs-lookup"><span data-stu-id="c8364-176">Creating the Edit View</span></span>

<span data-ttu-id="c8364-177">將下列 `Edit` 方法新增至 home 控制器。</span><span class="sxs-lookup"><span data-stu-id="c8364-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="c8364-178">如先前的步驟所示新增視圖，但將 [ **view content** ] 設定為 [**編輯**]。</span><span class="sxs-lookup"><span data-stu-id="c8364-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![新增編輯檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="c8364-180">執行應用程式，並編輯其中一個使用者的姓氏和名字。</span><span class="sxs-lookup"><span data-stu-id="c8364-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="c8364-181">如果您違反任何已套用至 `UserModel` 類別的 `DataAnnotation` 條件約束，當您提交表單時，您會看到伺服器程式碼所產生的驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="c8364-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="c8364-182">例如，如果您將第一個名稱 &quot;王&quot; 以 &quot;&quot;，則在提交表單時，表單上會顯示下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="c8364-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="c8364-183">在本教學課程中，您會將使用者名稱視為主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="c8364-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="c8364-184">因此，無法變更 [使用者名稱] 屬性。</span><span class="sxs-lookup"><span data-stu-id="c8364-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="c8364-185">在*編輯的 cshtml*檔案中，緊接在 `Html.BeginForm` 語句之後，將使用者名稱設定為隱藏欄位。</span><span class="sxs-lookup"><span data-stu-id="c8364-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="c8364-186">這會導致屬性在模型中傳遞。</span><span class="sxs-lookup"><span data-stu-id="c8364-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="c8364-187">下列程式碼片段顯示 `Hidden` 語句的位置：</span><span class="sxs-lookup"><span data-stu-id="c8364-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="c8364-188">使用 `DisplayFor` 呼叫來取代使用者名稱的 `TextBoxFor` 和 `ValidationMessageFor` 標記。</span><span class="sxs-lookup"><span data-stu-id="c8364-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="c8364-189">`DisplayFor` 方法會將屬性顯示為唯讀元素。</span><span class="sxs-lookup"><span data-stu-id="c8364-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="c8364-190">下列範例顯示完整的標記。</span><span class="sxs-lookup"><span data-stu-id="c8364-190">The following example shows the completed markup.</span></span> <span data-ttu-id="c8364-191">原始的 `TextBoxFor` 和 `ValidationMessageFor` 呼叫會使用 Razor 開始-批註和結束批註字元（`@* *@`）進行批註化</span><span class="sxs-lookup"><span data-stu-id="c8364-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="c8364-192">啟用用戶端驗證</span><span class="sxs-lookup"><span data-stu-id="c8364-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="c8364-193">若要在 ASP.NET MVC 3 中啟用用戶端驗證，您必須設定兩個旗標，而且必須包含三個 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="c8364-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="c8364-194">開啟應用程式的*web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="c8364-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="c8364-195">確認 應用程式設定 中的 `that ClientValidationEnabled` 和 `UnobtrusiveJavaScriptEnabled` 設定為 true。</span><span class="sxs-lookup"><span data-stu-id="c8364-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="c8364-196">根*web.config*檔案中的下列片段會顯示正確的設定：</span><span class="sxs-lookup"><span data-stu-id="c8364-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="c8364-197">將 `UnobtrusiveJavaScriptEnabled` 設定為 true 可啟用不顯眼的 Ajax 和不顯眼的用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="c8364-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="c8364-198">當您使用不顯眼的驗證時，驗證規則會變成 HTML5 屬性。</span><span class="sxs-lookup"><span data-stu-id="c8364-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="c8364-199">HTML5 屬性名稱只能包含小寫字母、數位和虛線。</span><span class="sxs-lookup"><span data-stu-id="c8364-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="c8364-200">將 `ClientValidationEnabled` 設定為 true 會啟用用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="c8364-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="c8364-201">藉由*在應用程式的 web.config 檔案*中設定這些索引鍵，您可以針對整個應用程式啟用用戶端驗證和不顯眼的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="c8364-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="c8364-202">您也可以使用下列程式碼，在個別的 views 或控制器方法中啟用或停用這些設定：</span><span class="sxs-lookup"><span data-stu-id="c8364-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="c8364-203">您也需要在呈現的視圖中包含數個 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="c8364-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="c8364-204">在所有視圖中包含 JavaScript 的簡單方法，就是將它們新增至*Views\Shared\\_Layout. cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="c8364-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="c8364-205">以下列程式碼取代 *\_Layout*檔案的 `<head>` 元素：</span><span class="sxs-lookup"><span data-stu-id="c8364-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="c8364-206">前兩個 jQuery 腳本是由 Microsoft Ajax 內容傳遞網路（CDN）所主控。</span><span class="sxs-lookup"><span data-stu-id="c8364-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="c8364-207">藉由利用 Microsoft Ajax CDN，您可以大幅提升應用程式的第一次點擊效能。</span><span class="sxs-lookup"><span data-stu-id="c8364-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="c8364-208">執行應用程式，然後按一下 [編輯] 連結。</span><span class="sxs-lookup"><span data-stu-id="c8364-208">Run the application and click an edit link.</span></span> <span data-ttu-id="c8364-209">在瀏覽器中查看頁面的來源。</span><span class="sxs-lookup"><span data-stu-id="c8364-209">View the page's source in the browser.</span></span> <span data-ttu-id="c8364-210">瀏覽器來源會顯示多個表單 `data-val` 的屬性（用於資料驗證）。</span><span class="sxs-lookup"><span data-stu-id="c8364-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="c8364-211">當啟用用戶端驗證和不顯眼的 JavaScript 時，具有用戶端驗證規則的輸入欄位會包含 `data-val="true"` 屬性，以觸發不顯眼的用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="c8364-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="c8364-212">例如，模型中的 [`City`] 欄位是以[必要](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)的屬性裝飾，這會導致 HTML 顯示在下列範例中：</span><span class="sxs-lookup"><span data-stu-id="c8364-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="c8364-213">針對每個用戶端驗證規則，會加入具有 `data-val-rulename="message"`格式的屬性。</span><span class="sxs-lookup"><span data-stu-id="c8364-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="c8364-214">使用稍早所示的 `City` 欄位範例時，必要的用戶端驗證規則會產生 `data-val-required` 屬性和訊息 &quot;[City] 欄位必須&quot;。</span><span class="sxs-lookup"><span data-stu-id="c8364-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="c8364-215">執行應用程式、編輯其中一個使用者，然後清除 [`City`] 欄位。</span><span class="sxs-lookup"><span data-stu-id="c8364-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="c8364-216">當您按 tab 鍵移出欄位時，您會看到用戶端驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="c8364-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![需要城市](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="c8364-218">同樣地，針對用戶端驗證規則中的每個參數，會加入具有 `data-val-rulename-paramname=paramvalue`格式的屬性。</span><span class="sxs-lookup"><span data-stu-id="c8364-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="c8364-219">例如，`FirstName` 屬性會加上[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)屬性的批註，並指定最小長度3，最大長度為8。</span><span class="sxs-lookup"><span data-stu-id="c8364-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="c8364-220">名為 `length` 的資料驗證規則具有參數名稱 `max` 和參數值8。</span><span class="sxs-lookup"><span data-stu-id="c8364-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="c8364-221">以下顯示當您編輯其中一個使用者時，為 [`FirstName`] 欄位產生的 HTML：</span><span class="sxs-lookup"><span data-stu-id="c8364-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="c8364-222">如需不顯眼的用戶端驗證的詳細資訊，請參閱 Brad Wilson 的 blog 中的 ASP.NET MVC 3 中的「不[顯眼的用戶端驗證](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)」專案。</span><span class="sxs-lookup"><span data-stu-id="c8364-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="c8364-223">在 ASP.NET MVC 3 Beta 中，您有時需要提交表單，才能啟動用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="c8364-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="c8364-224">這可能會在最終版本中變更。</span><span class="sxs-lookup"><span data-stu-id="c8364-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="c8364-225">建立建立視圖</span><span class="sxs-lookup"><span data-stu-id="c8364-225">Creating the Create View</span></span>

<span data-ttu-id="c8364-226">下一個步驟是新增 `Create` 動作方法和 view，讓使用者能夠建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="c8364-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="c8364-227">將下列 `Create` 方法加入至主控制器：</span><span class="sxs-lookup"><span data-stu-id="c8364-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="c8364-228">如先前的步驟所示新增視圖，但將**view content**設定為 **[建立]。**</span><span class="sxs-lookup"><span data-stu-id="c8364-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![建立檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="c8364-230">執行應用程式，選取 [**建立**] 連結，然後新增新的使用者。</span><span class="sxs-lookup"><span data-stu-id="c8364-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="c8364-231">`Create` 方法會自動利用用戶端和伺服器端驗證。</span><span class="sxs-lookup"><span data-stu-id="c8364-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="c8364-232">請嘗試輸入包含空白字元的使用者名稱，例如 &quot;Ben X&quot;。</span><span class="sxs-lookup"><span data-stu-id="c8364-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="c8364-233">當您使用 tab 鍵移出 [使用者名稱] 欄位時，就會顯示用戶端驗證錯誤（`White space is not allowed`）。</span><span class="sxs-lookup"><span data-stu-id="c8364-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="c8364-234">新增 Delete 方法</span><span class="sxs-lookup"><span data-stu-id="c8364-234">Add the Delete method</span></span>

<span data-ttu-id="c8364-235">若要完成本教學課程，請將下列 `Delete` 方法加入至主控制器：</span><span class="sxs-lookup"><span data-stu-id="c8364-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="c8364-236">新增 [`Delete`] 視圖，如同先前的步驟，將 [ **view content** ] 設定為 [**刪除**]。</span><span class="sxs-lookup"><span data-stu-id="c8364-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![刪除檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="c8364-238">您現在有一個簡單但功能完整的 ASP.NET MVC 3 應用程式，具有驗證。</span><span class="sxs-lookup"><span data-stu-id="c8364-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
