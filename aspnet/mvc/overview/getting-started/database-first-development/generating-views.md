---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: 教學課程：使用 ASP.NET MVC 應用程式產生 EF Database First 的視圖
description: 本教學課程著重于使用 ASP.NET 的架構來產生控制器和 views。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: e71e13e22d8a72e1699cfc70d4d93af603edba5b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616204"
---
# <a name="tutorial-generate-views-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="5d4ff-103">教學課程：使用 ASP.NET MVC 應用程式產生 EF Database First 的視圖</span><span class="sxs-lookup"><span data-stu-id="5d4ff-103">Tutorial: Generate views for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="5d4ff-104">使用 MVC、Entity Framework 和 ASP.NET 的樣板，您可以建立 web 應用程式，以提供介面給現有的資料庫。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="5d4ff-105">本教學課程系列會示範如何自動產生程式碼，讓使用者可以顯示、編輯、建立和刪除位於資料庫資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="5d4ff-106">產生的程式碼會對應至資料庫資料表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="5d4ff-107">本教學課程著重于使用 ASP.NET 的架構來產生控制器和 views。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-107">This tutorial focuses on using ASP.NET Scaffolding to generate the controllers and views.</span></span>

<span data-ttu-id="5d4ff-108">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="5d4ff-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5d4ff-109">新增 scaffold</span><span class="sxs-lookup"><span data-stu-id="5d4ff-109">Add scaffold</span></span>
> * <span data-ttu-id="5d4ff-110">將連結新增至新的視圖</span><span class="sxs-lookup"><span data-stu-id="5d4ff-110">Add links to new views</span></span>
> * <span data-ttu-id="5d4ff-111">顯示學生的視圖</span><span class="sxs-lookup"><span data-stu-id="5d4ff-111">Display student views</span></span>
> * <span data-ttu-id="5d4ff-112">顯示註冊視圖</span><span class="sxs-lookup"><span data-stu-id="5d4ff-112">Display enrollment views</span></span>

## <a name="prerequisite"></a><span data-ttu-id="5d4ff-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="5d4ff-113">Prerequisite</span></span>

* [<span data-ttu-id="5d4ff-114">建立 web 應用程式和資料模型</span><span class="sxs-lookup"><span data-stu-id="5d4ff-114">Create the web application and data models</span></span>](creating-the-web-application.md)

## <a name="add-scaffold"></a><span data-ttu-id="5d4ff-115">新增 scaffold</span><span class="sxs-lookup"><span data-stu-id="5d4ff-115">Add scaffold</span></span>

<span data-ttu-id="5d4ff-116">您已準備好產生可為模型類別提供標準資料作業的程式碼。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-116">You are ready to generate code that will provide standard data operations for the model classes.</span></span> <span data-ttu-id="5d4ff-117">您可以藉由新增 scaffold 專案來加入程式碼。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-117">You add the code by adding a scaffold item.</span></span> <span data-ttu-id="5d4ff-118">您可以新增的架構類型有許多選項;在本教學課程中，scaffold 會包含與您在上一節中建立的學生和註冊模型對應的控制器和 views。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-118">There are many options for the type of scaffolding you can add; in this tutorial, the scaffold will include a controller and views that correspond to the Student and Enrollment models you created in the previous section.</span></span>

<span data-ttu-id="5d4ff-119">為了維持專案的一致性，您會將新的控制器新增至 [現有的**控制器**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-119">To maintain consistency in your project, you will add the new controller to the existing **Controllers** folder.</span></span> <span data-ttu-id="5d4ff-120">以滑鼠右鍵按一下 [**控制器**] 資料夾，**然後選取 [** 新增 > **新的 scaffold 專案**]。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-120">Right-click the **Controllers** folder, and select **Add** > **New Scaffolded Item**.</span></span>

<span data-ttu-id="5d4ff-121">使用 [ **Entity Framework] 選項，選取具有 views 的 MVC 5 控制器**。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-121">Select the **MVC 5 Controller with views, using Entity Framework** option.</span></span> <span data-ttu-id="5d4ff-122">此選項會產生控制器和視圖，以更新、刪除、建立和顯示模型中的資料。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-122">This option will generate the controller and views for updating, deleting, creating and displaying the data in your model.</span></span>

![新增 mvc 控制器](generating-views/_static/image2.png)

<span data-ttu-id="5d4ff-124">針對 [模型] 類別選取 [**學生（ContosoSite）** ]，然後選取內容類別的**ContosoUniversityDataEntities （ContosoSite）** 。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-124">Select **Student (ContosoSite.Models)** for the model class and select the **ContosoUniversityDataEntities (ContosoSite.Models)** for the context class.</span></span> <span data-ttu-id="5d4ff-125">將控制器名稱保留為**studentscontroller.cs**。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-125">Keep the controller name as **StudentsController**.</span></span>

<span data-ttu-id="5d4ff-126">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-126">Click **Add**.</span></span>

<span data-ttu-id="5d4ff-127">如果您收到錯誤，可能是因為您未在上一節中建立專案。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-127">If you receive an error, it may be because you did not build the project in the previous section.</span></span> <span data-ttu-id="5d4ff-128">若是如此，請嘗試建立專案，然後再次加入 scaffold 專案。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-128">If so, try building the project, and then add the scaffolded item again.</span></span>

<span data-ttu-id="5d4ff-129">程式碼產生程式完成之後，您會在專案的 [**控制器**和**views** ] > [**學生**] 資料夾中看到新的控制器和 views。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-129">After the code generation process is complete, you will see a new controller and views in your project's **Controllers** and **Views** > **Students** folders.</span></span>

<span data-ttu-id="5d4ff-130">再次執行相同的步驟，但新增**註冊**類別的 scaffold。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-130">Perform the same steps again, but add a scaffold for the **Enrollment** class.</span></span> <span data-ttu-id="5d4ff-131">完成時，您會有一個**EnrollmentsController.cs**檔案，以及**一個名為** **註冊** 的資料夾，其中包含 建立、刪除、詳細資料、編輯 和 索引</span><span class="sxs-lookup"><span data-stu-id="5d4ff-131">When finished, you have an **EnrollmentsController.cs** file, and a folder under **Views** named **Enrollments** with the Create, Delete, Details, Edit and Index views.</span></span>

## <a name="add-links-to-new-views"></a><span data-ttu-id="5d4ff-132">將連結新增至新的視圖</span><span class="sxs-lookup"><span data-stu-id="5d4ff-132">Add links to new views</span></span>

<span data-ttu-id="5d4ff-133">為了讓您更輕鬆地流覽至新的視圖，您可以將幾個超連結新增至學生和註冊的索引視圖。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-133">To make it easier for you to navigate to your new views, you can add a couple of hyperlinks to the Index views for students and enrollments.</span></span> <span data-ttu-id="5d4ff-134">在 > **Home** > 的**Views**資料夾中開啟檔案，這是您網站的*首頁。*</span><span class="sxs-lookup"><span data-stu-id="5d4ff-134">Open the file at **Views** > **Home** > *Index.cshtml*, which is the home page for your site.</span></span> <span data-ttu-id="5d4ff-135">在 jumbotron 下方新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-135">Add the following code below the jumbotron.</span></span>

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

<span data-ttu-id="5d4ff-136">對於 Html.actionlink 方法，第一個參數是要顯示在連結中的文字。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-136">For the ActionLink method, the first parameter is the text to display in the link.</span></span> <span data-ttu-id="5d4ff-137">第二個參數是動作，而第三個參數是控制器的名稱。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-137">The second parameter is the action and the third parameter is the name of the controller.</span></span> <span data-ttu-id="5d4ff-138">例如，第一個連結會指向 Studentscontroller.cs 中的索引動作。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-138">For example, the first link points to the Index action in StudentsController.</span></span> <span data-ttu-id="5d4ff-139">實際的超連結是由這些值所構成。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-139">The actual hyperlink is constructed from these values.</span></span> <span data-ttu-id="5d4ff-140">第一個連結最後會將使用者帶到**Views/** student 資料夾中的**Index. cshtml**檔案。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-140">The first link ultimately takes users to the **Index.cshtml** file within the **Views/Students** folder.</span></span>

## <a name="display-student-views"></a><span data-ttu-id="5d4ff-141">顯示學生的視圖</span><span class="sxs-lookup"><span data-stu-id="5d4ff-141">Display student views</span></span>

<span data-ttu-id="5d4ff-142">您會驗證新增至專案的程式碼是否正確地顯示學生清單，並可讓使用者編輯、建立或刪除資料庫中的學生記錄。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-142">You will verify that the code added to your project correctly displays a list of the students, and enables users to edit, create, or delete the student records in the database.</span></span>

<span data-ttu-id="5d4ff-143">以滑鼠右鍵按一下 > **Home** \* > 的\* **Views**檔案，然後選取 [**在瀏覽器中查看**]。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-143">Right-click the **Views** > **Home** > *Index.cshtml* file, and select **View in Browser**.</span></span> <span data-ttu-id="5d4ff-144">在應用程式首頁上，選取 [**學生清單**]。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-144">On the application home page, select **List of students**.</span></span>

![](generating-views/_static/image6.png)

<span data-ttu-id="5d4ff-145">在 [**索引**] 頁面上，請注意要修改此資料的學生和連結清單。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-145">On the **Index** page, notice the list of the students and links to modify this data.</span></span> <span data-ttu-id="5d4ff-146">選取 [**新建] 連結，並**為新的學生提供一些值。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-146">Select the **Create New** link and provide some values for a new student.</span></span> <span data-ttu-id="5d4ff-147">按一下 [**建立**]，並注意新的 student 已新增至您的清單。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-147">Click **Create**, and notice the new student is added to your list.</span></span>

<span data-ttu-id="5d4ff-148">回到 [**索引**] 頁面，選取 [**編輯**] 連結，然後變更學生的一些值。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-148">Back on the **Index** page, select the **Edit** link, and change some of the values for a student.</span></span> <span data-ttu-id="5d4ff-149">按一下 [**儲存**]，並注意學生記錄已經變更。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-149">Click **Save**, and notice the student record has been changed.</span></span>

<span data-ttu-id="5d4ff-150">最後，選取 [**刪除**] 連結，然後按一下 [**刪除**] 按鈕，確認您想要刪除記錄。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-150">Finally, select the **Delete** link and confirm that you want to delete the record by clicking the **Delete** button.</span></span>

<span data-ttu-id="5d4ff-151">在不撰寫任何程式碼的情況下，您已新增可對 Student 資料表中的資料執行一般作業的視圖。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-151">Without writing any code, you have added views that perform common operations on the data in the Student table.</span></span>

<span data-ttu-id="5d4ff-152">您可能已經注意到，欄位的文字標籤是以資料庫屬性為基礎（例如**LastName**），這不一定是您想要顯示在網頁上的內容。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-152">You may have noticed that the text label for a field is based on the database property (such as **LastName**) which is not necessarily what you want to display on the web page.</span></span> <span data-ttu-id="5d4ff-153">例如，您可能會偏好將標籤**命名為姓氏**。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-153">For example, you may prefer the label to be **Last Name**.</span></span> <span data-ttu-id="5d4ff-154">您稍後會在本教學課程中修正此顯示問題。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-154">You will fix this display issue later in the tutorial.</span></span>

## <a name="display-enrollment-views"></a><span data-ttu-id="5d4ff-155">顯示註冊視圖</span><span class="sxs-lookup"><span data-stu-id="5d4ff-155">Display enrollment views</span></span>

<span data-ttu-id="5d4ff-156">您的資料庫包含 Student 與註冊資料表之間的一對多關聯性，以及課程和註冊資料表之間的一對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-156">Your database includes a one-to-many relationship between the Student and Enrollment tables, and a one-to-many relationship between the Course and Enrollment tables.</span></span> <span data-ttu-id="5d4ff-157">註冊的視圖會正確地處理這些關聯性。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-157">The views for Enrollment correctly handle these relationships.</span></span> <span data-ttu-id="5d4ff-158">流覽至您網站的首頁，然後選取 [註冊] 連結**清單**，再選取 [**建立新**的] 連結。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-158">Navigate to the home page for your site and select the **List of enrollments** link and then the **Create New** link.</span></span>

<span data-ttu-id="5d4ff-159">此視圖會顯示一個表單，用來建立新的註冊記錄。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-159">The view displays a form for creating a new enrollment record.</span></span> <span data-ttu-id="5d4ff-160">特別要注意的是，表單包含 [ **CourseID** ] 下拉式清單和 [ **StudentID** ] 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-160">In particular, notice that the form contains a **CourseID** drop-down list and a **StudentID** drop-down list.</span></span> <span data-ttu-id="5d4ff-161">這兩者都會以相關資料表中的值填入。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-161">Both are populated with values from the related tables.</span></span>

<span data-ttu-id="5d4ff-162">此外，系統會根據欄位的資料類型，自動套用所提供值的驗證。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-162">Furthermore, validation of the provided values is automatically applied based on the data type of the field.</span></span> <span data-ttu-id="5d4ff-163">**等級**需要數位，因此如果您嘗試提供不相容的值，就會顯示錯誤訊息：*欄位等級必須是數位。*</span><span class="sxs-lookup"><span data-stu-id="5d4ff-163">**Grade** requires a number, so an error message is displayed if you try to provide an incompatible value: *The field Grade must be a number.*</span></span>

<span data-ttu-id="5d4ff-164">您已確認自動產生的視圖可讓使用者使用資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-164">You have verified that the automatically-generated views enable users to work with the data in the database.</span></span> <span data-ttu-id="5d4ff-165">在此系列的下一個教學課程中，您將會更新資料庫，並在 web 應用程式中進行對應的變更。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-165">In the next tutorial in this series, you will update the database and make the corresponding changes in the web application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d4ff-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d4ff-166">Next steps</span></span>

<span data-ttu-id="5d4ff-167">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="5d4ff-167">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5d4ff-168">已新增 scaffold</span><span class="sxs-lookup"><span data-stu-id="5d4ff-168">Added scaffold</span></span>
> * <span data-ttu-id="5d4ff-169">已將連結新增至新的視圖</span><span class="sxs-lookup"><span data-stu-id="5d4ff-169">Added links to new views</span></span>
> * <span data-ttu-id="5d4ff-170">顯示的學生視圖</span><span class="sxs-lookup"><span data-stu-id="5d4ff-170">Displayed student views</span></span>
> * <span data-ttu-id="5d4ff-171">顯示的註冊視圖</span><span class="sxs-lookup"><span data-stu-id="5d4ff-171">Displayed enrollment views</span></span>

<span data-ttu-id="5d4ff-172">請前進到下一個教學課程，以瞭解如何變更資料庫。</span><span class="sxs-lookup"><span data-stu-id="5d4ff-172">Advance to the next tutorial to learn how to change the database.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5d4ff-173">變更資料庫</span><span class="sxs-lookup"><span data-stu-id="5d4ff-173">Change the database</span></span>](changing-the-database.md)