---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: 教學課程：使用 MVC 5 開始使用 Entity Framework 6 Code First |Microsoft Docs
description: 在這一系列的教學課程中，您將瞭解如何建立 ASP.NET MVC 5 應用程式，以使用 Entity Framework 6 來進行資料存取。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: a00a5a3aa295c2584b90abbf931c258c9e1b58ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616127"
---
# <a name="tutorial-get-started-with-entity-framework-6-code-first-using-mvc-5"></a><span data-ttu-id="9db9e-103">教學課程：使用 MVC 5 開始使用 Entity Framework 6 Code First</span><span class="sxs-lookup"><span data-stu-id="9db9e-103">Tutorial: Get Started with Entity Framework 6 Code First using MVC 5</span></span>

> [!NOTE]
> <span data-ttu-id="9db9e-104">針對新的開發，建議[ASP.NET Core Razor Pages](/aspnet/core/razor-pages) ASP.NET MVC 控制器和 views。</span><span class="sxs-lookup"><span data-stu-id="9db9e-104">For new development, we recommend [ASP.NET Core Razor Pages](/aspnet/core/razor-pages) over ASP.NET MVC controllers and views.</span></span> <span data-ttu-id="9db9e-105">如需與使用 Razor Pages 類似的教學課程系列，請參閱[教學課程：開始使用 ASP.NET Core 中的 Razor Pages](/aspnet/core/tutorials/razor-pages/razor-pages-start)。</span><span class="sxs-lookup"><span data-stu-id="9db9e-105">For a tutorial series similar to this one using Razor Pages, see [Tutorial: Get started with Razor Pages in ASP.NET Core](/aspnet/core/tutorials/razor-pages/razor-pages-start).</span></span> <span data-ttu-id="9db9e-106">新的教學課程：</span><span class="sxs-lookup"><span data-stu-id="9db9e-106">The new tutorial:</span></span>
> * <span data-ttu-id="9db9e-107">比較容易學習。</span><span class="sxs-lookup"><span data-stu-id="9db9e-107">Is easier to follow.</span></span>
> * <span data-ttu-id="9db9e-108">提供更多 EF Core 最佳做法。</span><span class="sxs-lookup"><span data-stu-id="9db9e-108">Provides more EF Core best practices.</span></span>
> * <span data-ttu-id="9db9e-109">使用更有效率的查詢。</span><span class="sxs-lookup"><span data-stu-id="9db9e-109">Uses more efficient queries.</span></span>
> * <span data-ttu-id="9db9e-110">具有最新的 API。</span><span class="sxs-lookup"><span data-stu-id="9db9e-110">Is more current with the latest API.</span></span>
> * <span data-ttu-id="9db9e-111">涵蓋更多功能。</span><span class="sxs-lookup"><span data-stu-id="9db9e-111">Covers more features.</span></span>
> * <span data-ttu-id="9db9e-112">是新應用程式開發的建議方法。</span><span class="sxs-lookup"><span data-stu-id="9db9e-112">Is the preferred approach for new application development.</span></span>

<span data-ttu-id="9db9e-113">在這一系列的教學課程中，您將瞭解如何建立 ASP.NET MVC 5 應用程式，以使用 Entity Framework 6 來進行資料存取。</span><span class="sxs-lookup"><span data-stu-id="9db9e-113">In this series of tutorials, you learn how to build an ASP.NET MVC 5 application that uses Entity Framework 6 for data access.</span></span> <span data-ttu-id="9db9e-114">本教學課程使用 Code First 工作流程。</span><span class="sxs-lookup"><span data-stu-id="9db9e-114">This tutorial uses the Code First workflow.</span></span> <span data-ttu-id="9db9e-115">如需如何在 Code First、Database First 和 Model First 之間進行選擇的詳細資訊，請參閱[建立模型](/ef/ef6/modeling/)。</span><span class="sxs-lookup"><span data-stu-id="9db9e-115">For information about how to choose between Code First, Database First, and Model First, see [Create a model](/ef/ef6/modeling/).</span></span>

<span data-ttu-id="9db9e-116">本教學課程系列會說明如何建立 Contoso 大學範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="9db9e-116">This tutorial series explains how to build the Contoso University sample application.</span></span> <span data-ttu-id="9db9e-117">範例應用程式是簡單的大學網站。</span><span class="sxs-lookup"><span data-stu-id="9db9e-117">The sample application is a simple university website.</span></span> <span data-ttu-id="9db9e-118">有了它，您就可以查看和更新學生、課程和講師資訊。</span><span class="sxs-lookup"><span data-stu-id="9db9e-118">With it, you can view and update student, course, and instructor information.</span></span> <span data-ttu-id="9db9e-119">以下是您所建立的兩個畫面：</span><span class="sxs-lookup"><span data-stu-id="9db9e-119">Here are two of the screens you create:</span></span>

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![編輯學生](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="9db9e-122">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="9db9e-122">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9db9e-123">建立 MVC web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9db9e-123">Create an MVC web app</span></span>
> * <span data-ttu-id="9db9e-124">設定網站樣式</span><span class="sxs-lookup"><span data-stu-id="9db9e-124">Set up the site style</span></span>
> * <span data-ttu-id="9db9e-125">安裝 Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="9db9e-125">Install Entity Framework 6</span></span>
> * <span data-ttu-id="9db9e-126">建立資料模型</span><span class="sxs-lookup"><span data-stu-id="9db9e-126">Create the data model</span></span>
> * <span data-ttu-id="9db9e-127">建立資料庫內容</span><span class="sxs-lookup"><span data-stu-id="9db9e-127">Create the database context</span></span>
> * <span data-ttu-id="9db9e-128">使用測試資料將 DB 初始化</span><span class="sxs-lookup"><span data-stu-id="9db9e-128">Initialize DB with test data</span></span>
> * <span data-ttu-id="9db9e-129">設定 EF 6 使用 LocalDB</span><span class="sxs-lookup"><span data-stu-id="9db9e-129">Set up EF 6 to use LocalDB</span></span>
> * <span data-ttu-id="9db9e-130">建立控制器和檢視</span><span class="sxs-lookup"><span data-stu-id="9db9e-130">Create controller and views</span></span>
> * <span data-ttu-id="9db9e-131">檢視資料庫</span><span class="sxs-lookup"><span data-stu-id="9db9e-131">View the database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9db9e-132">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9db9e-132">Prerequisites</span></span>

* [<span data-ttu-id="9db9e-133">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9db9e-133">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

## <a name="create-an-mvc-web-app"></a><span data-ttu-id="9db9e-134">建立 MVC web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9db9e-134">Create an MVC web app</span></span>

1. <span data-ttu-id="9db9e-135">開啟 Visual Studio，並使用C# **ASP.NET web 應用程式（.NET Framework）** 範本建立 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="9db9e-135">Open Visual Studio and create a C# web project using the **ASP.NET Web Application (.NET Framework)** template.</span></span> <span data-ttu-id="9db9e-136">將專案命名為*ContosoUniversity* ，然後選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9db9e-136">Name the project *ContosoUniversity* and select **OK**.</span></span>

   ![Visual Studio 中的 [新增專案] 對話方塊](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-project-dialog.png)

1. <span data-ttu-id="9db9e-138">在 [**新增 ASP.NET Web 應用程式-ContosoUniversity**] 中，選取 [ **MVC**]。</span><span class="sxs-lookup"><span data-stu-id="9db9e-138">In **New ASP.NET Web Application - ContosoUniversity**, select **MVC**.</span></span>

   ![Visual Studio 中的 [新增 web 應用程式] 對話方塊](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-web-app-dialog.png)

    > [!NOTE]
    > <span data-ttu-id="9db9e-140">根據預設，**驗證**選項會設定為 [**不需要驗證**]。</span><span class="sxs-lookup"><span data-stu-id="9db9e-140">By default, the **Authentication** option is set to **No Authentication**.</span></span> <span data-ttu-id="9db9e-141">在本教學課程中，web 應用程式不需要使用者登入。</span><span class="sxs-lookup"><span data-stu-id="9db9e-141">For this tutorial, the web app doesn't require users to sign in.</span></span> <span data-ttu-id="9db9e-142">此外，它也不會根據登入的使用者來限制存取權。</span><span class="sxs-lookup"><span data-stu-id="9db9e-142">Also, it doesn't restrict access based on who's signed in.</span></span>

1. <span data-ttu-id="9db9e-143">選取 [確定] 建立專案。</span><span class="sxs-lookup"><span data-stu-id="9db9e-143">Select **OK** to create the project.</span></span>

## <a name="set-up-the-site-style"></a><span data-ttu-id="9db9e-144">設定網站樣式</span><span class="sxs-lookup"><span data-stu-id="9db9e-144">Set up the site style</span></span>

<span data-ttu-id="9db9e-145">一些簡單的變更會設定網站的功能表、配置和首頁。</span><span class="sxs-lookup"><span data-stu-id="9db9e-145">A few simple changes will set up the site menu, layout, and home page.</span></span>

1. <span data-ttu-id="9db9e-146">開啟*Views\Shared\\_Layout*，並進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="9db9e-146">Open *Views\Shared\\_Layout.cshtml*, and make the following changes:</span></span>

   - <span data-ttu-id="9db9e-147">將每個出現的「我的 ASP.NET 應用程式」和「應用程式名稱」變更為「Contoso 大學」。</span><span class="sxs-lookup"><span data-stu-id="9db9e-147">Change each occurrence of "My ASP.NET Application" and "Application name" to "Contoso University".</span></span>
   - <span data-ttu-id="9db9e-148">新增學生、課程、講師和部門的功能表項目，並刪除連絡人項目。</span><span class="sxs-lookup"><span data-stu-id="9db9e-148">Add menu entries for Students, Courses, Instructors, and Departments, and delete the Contact entry.</span></span>

   <span data-ttu-id="9db9e-149">這些變更會反白顯示在下列程式碼片段中：</span><span class="sxs-lookup"><span data-stu-id="9db9e-149">The changes are highlighted in the following code snippet:</span></span>

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

2. <span data-ttu-id="9db9e-150">在*Views\Home\Index.cshtml*中，將檔案的內容取代為下列程式碼，以將 ASP.NET 和 MVC 的文字取代為此應用程式的文字：</span><span class="sxs-lookup"><span data-stu-id="9db9e-150">In *Views\Home\Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this application:</span></span>

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

3. <span data-ttu-id="9db9e-151">按 Ctrl + F5 執行網站。</span><span class="sxs-lookup"><span data-stu-id="9db9e-151">Press Ctrl+F5 to run the web site.</span></span> <span data-ttu-id="9db9e-152">您會在首頁上看到主功能表。</span><span class="sxs-lookup"><span data-stu-id="9db9e-152">You see the home page with the main menu.</span></span>

## <a name="install-entity-framework-6"></a><span data-ttu-id="9db9e-153">安裝 Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="9db9e-153">Install Entity Framework 6</span></span>

1. <span data-ttu-id="9db9e-154">從 [**工具**] 功能表中，選擇 [ **NuGet 套件管理員**]，然後選擇 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="9db9e-154">From the **Tools** menu, choose **NuGet Package Manager**, and then choose **Package Manager Console**.</span></span>

2. <span data-ttu-id="9db9e-155">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="9db9e-155">In the **Package Manager Console** window, enter the following command:</span></span>

   ```text
   Install-Package EntityFramework
   ```

<span data-ttu-id="9db9e-156">此步驟是本教學課程的幾個步驟中的其中一個，但這可能是由 ASP.NET MVC 樣板功能自動完成的。</span><span class="sxs-lookup"><span data-stu-id="9db9e-156">This step is one of a few steps that this tutorial has you do manually, but that could have been done automatically by the ASP.NET MVC scaffolding feature.</span></span> <span data-ttu-id="9db9e-157">您要手動執行這些動作，讓您可以看到使用 Entity Framework （EF）所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="9db9e-157">You're doing them manually so that you can see the steps required to use Entity Framework (EF).</span></span> <span data-ttu-id="9db9e-158">您稍後會使用此架構來建立 MVC 控制器和 views。</span><span class="sxs-lookup"><span data-stu-id="9db9e-158">You'll use scaffolding later to create the MVC controller and views.</span></span> <span data-ttu-id="9db9e-159">替代方式是讓 [架構] 自動安裝 EF NuGet 封裝、建立資料庫內容類別，並建立連接字串。</span><span class="sxs-lookup"><span data-stu-id="9db9e-159">An alternative is to let scaffolding automatically install the EF NuGet package, create the database context class, and create the connection string.</span></span> <span data-ttu-id="9db9e-160">當您準備好這樣做時，您只需要略過這些步驟，並在建立實體類別之後 scaffold 您的 MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="9db9e-160">When you're ready to do it that way, all you have to do is skip those steps and scaffold your MVC controller after you create your entity classes.</span></span>

## <a name="create-the-data-model"></a><span data-ttu-id="9db9e-161">建立資料模型</span><span class="sxs-lookup"><span data-stu-id="9db9e-161">Create the data model</span></span>

<span data-ttu-id="9db9e-162">接下來您會為 Contoso 大學應用程式建立實體類別。</span><span class="sxs-lookup"><span data-stu-id="9db9e-162">Next you'll create entity classes for the Contoso University application.</span></span> <span data-ttu-id="9db9e-163">您將從下列三個實體開始：</span><span class="sxs-lookup"><span data-stu-id="9db9e-163">You'll start with the following three entities:</span></span>

<span data-ttu-id="9db9e-164">**課程** <-> **註冊** <-> **Student**</span><span class="sxs-lookup"><span data-stu-id="9db9e-164">**Course** <-> **Enrollment** <-> **Student**</span></span>

| <span data-ttu-id="9db9e-165">實體</span><span class="sxs-lookup"><span data-stu-id="9db9e-165">Entities</span></span> | <span data-ttu-id="9db9e-166">Relationship</span><span class="sxs-lookup"><span data-stu-id="9db9e-166">Relationship</span></span> |
| -------- | ------------ |
| <span data-ttu-id="9db9e-167">註冊課程</span><span class="sxs-lookup"><span data-stu-id="9db9e-167">Course to Enrollment</span></span> | <span data-ttu-id="9db9e-168">一對多</span><span class="sxs-lookup"><span data-stu-id="9db9e-168">One-to-many</span></span> |
| <span data-ttu-id="9db9e-169">要註冊的學生</span><span class="sxs-lookup"><span data-stu-id="9db9e-169">Student to Enrollment</span></span> | <span data-ttu-id="9db9e-170">一對多</span><span class="sxs-lookup"><span data-stu-id="9db9e-170">One-to-many</span></span> |

<span data-ttu-id="9db9e-171">在 `Student` 和 `Enrollment` 實體之間存在一對多關聯性，`Course` 與 `Enrollment` 實體之間也存在一對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="9db9e-171">There's a one-to-many relationship between `Student` and `Enrollment` entities, and there's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="9db9e-172">換句話說，一位學生可以註冊並參加任何數目的課程，而一個課程也可以有任何數目的學生註冊。</span><span class="sxs-lookup"><span data-stu-id="9db9e-172">In other words, a student can be enrolled in any number of courses, and a course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="9db9e-173">在下列各節中，您將為每個實體建立一個類別。</span><span class="sxs-lookup"><span data-stu-id="9db9e-173">In the following sections, you'll create a class for each one of these entities.</span></span>

> [!NOTE]
> <span data-ttu-id="9db9e-174">如果您在完成所有這些實體類別的建立之前嘗試編譯專案，您會收到編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="9db9e-174">If you try to compile the project before you finish creating all of these entity classes, you'll get compiler errors.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="9db9e-175">Student 實體</span><span class="sxs-lookup"><span data-stu-id="9db9e-175">The Student entity</span></span>

- <span data-ttu-id="9db9e-176">在 [*模型*] 資料夾中，建立名為*Student.cs*的類別檔案，方法是以滑鼠右鍵按一下**方案總管**中的資料夾，然後選擇 [**加入** > **類別**]。</span><span class="sxs-lookup"><span data-stu-id="9db9e-176">In the *Models* folder, create a class file named *Student.cs* by right-clicking on the folder in **Solution Explorer** and choosing **Add** > **Class**.</span></span> <span data-ttu-id="9db9e-177">使用下列程式碼取代範本程式碼：</span><span class="sxs-lookup"><span data-stu-id="9db9e-177">Replace the template code with the following code:</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="9db9e-178">`ID` 屬性會成為資料庫資料表中的主索引鍵資料行，並對應至這個類別。</span><span class="sxs-lookup"><span data-stu-id="9db9e-178">The `ID` property will become the primary key column of the database table that corresponds to this class.</span></span> <span data-ttu-id="9db9e-179">根據預設，Entity Framework 會將名為 `ID` 或*classname* `ID` 的屬性解讀為主要索引鍵。</span><span class="sxs-lookup"><span data-stu-id="9db9e-179">By default, Entity Framework interprets a property that's named `ID` or *classname* `ID` as the primary key.</span></span>

<span data-ttu-id="9db9e-180">`Enrollments` 屬性為*導覽屬性*。</span><span class="sxs-lookup"><span data-stu-id="9db9e-180">The `Enrollments` property is a *navigation property*.</span></span> <span data-ttu-id="9db9e-181">導覽屬性會保留與此實體相關的其他實體。</span><span class="sxs-lookup"><span data-stu-id="9db9e-181">Navigation properties hold other entities that are related to this entity.</span></span> <span data-ttu-id="9db9e-182">在此情況下，`Student` 實體的 `Enrollments` 屬性會保存與該 `Student` 實體相關的所有 `Enrollment` 實體。</span><span class="sxs-lookup"><span data-stu-id="9db9e-182">In this case, the `Enrollments` property of a `Student` entity will hold all of the `Enrollment` entities that are related to that `Student` entity.</span></span> <span data-ttu-id="9db9e-183">換句話說，如果資料庫中給定的 `Student` 資料列有兩個相關的 `Enrollment` 列（在其 `StudentID` 外鍵資料行中包含該學生的主鍵值的資料列），該 `Student` 實體的 `Enrollments` 導覽屬性會包含這兩個 `Enrollment` 的實體。</span><span class="sxs-lookup"><span data-stu-id="9db9e-183">In other words, if a given `Student` row in the database has two related `Enrollment` rows (rows that contain that student's primary key value in their `StudentID` foreign key column), that `Student` entity's `Enrollments` navigation property will contain those two `Enrollment` entities.</span></span>

<span data-ttu-id="9db9e-184">導覽屬性通常會定義為 `virtual`，讓它們可以利用某些 Entity Framework 的功能，例如消極式*載入*。</span><span class="sxs-lookup"><span data-stu-id="9db9e-184">Navigation properties are typically defined as `virtual` so that they can take advantage of certain Entity Framework functionality such as *lazy loading*.</span></span> <span data-ttu-id="9db9e-185">（稍後將在本系列稍後的[讀取相關資料](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)教學課程中說明消極式載入）。</span><span class="sxs-lookup"><span data-stu-id="9db9e-185">(Lazy loading will be explained later, in the [Reading Related Data](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial later in this series.)</span></span>

<span data-ttu-id="9db9e-186">若導覽屬性可保有多個實體 (例如在多對多或一對多關聯性中的情況)，其類型必須為一個清單，使得實體可以在該清單中新增、刪除或更新，例如 `ICollection`。</span><span class="sxs-lookup"><span data-stu-id="9db9e-186">If a navigation property can hold multiple entities (as in many-to-many or one-to-many relationships), its type must be a list in which entries can be added, deleted, and updated, such as `ICollection`.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="9db9e-187">Enrollment 實體</span><span class="sxs-lookup"><span data-stu-id="9db9e-187">The Enrollment entity</span></span>

- <span data-ttu-id="9db9e-188">在 *Models* 資料夾中，建立 *Enrollment.cs*，然後使用下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="9db9e-188">In the *Models* folder, create *Enrollment.cs* and replace the existing code with the following code:</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="9db9e-189">`EnrollmentID` 屬性將會是主要金鑰;這個實體會使用*classname* `ID` 模式，而不是由您在 `Student` 實體中看到的本身 `ID`。</span><span class="sxs-lookup"><span data-stu-id="9db9e-189">The `EnrollmentID` property will be the primary key; this entity uses the *classname* `ID` pattern instead of `ID` by itself as you saw in the `Student` entity.</span></span> <span data-ttu-id="9db9e-190">通常您會選擇一個模式，然後在您整個資料模型中使用此模式。</span><span class="sxs-lookup"><span data-stu-id="9db9e-190">Ordinarily you would choose one pattern and use it throughout your data model.</span></span> <span data-ttu-id="9db9e-191">在這裡，此變化僅作為向您展示使用不同模式之用。</span><span class="sxs-lookup"><span data-stu-id="9db9e-191">Here, the variation illustrates that you can use either pattern.</span></span> <span data-ttu-id="9db9e-192">在稍後的教學課程中，您將瞭解如何使用 `ID` 而不 `classname`，讓您更輕鬆地在資料模型中執行繼承。</span><span class="sxs-lookup"><span data-stu-id="9db9e-192">In a later tutorial, you'll see how using `ID` without `classname` makes it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="9db9e-193">`Grade` 屬性是[列舉](/ef/ef6/modeling/code-first/data-types/enums)。</span><span class="sxs-lookup"><span data-stu-id="9db9e-193">The `Grade` property is an [enum](/ef/ef6/modeling/code-first/data-types/enums).</span></span> <span data-ttu-id="9db9e-194">`Grade` 型別宣告後方的問號表示 `Grade` 屬性[可為 Null](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)。</span><span class="sxs-lookup"><span data-stu-id="9db9e-194">The question mark after the `Grade` type declaration indicates that the `Grade` property is [nullable](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types).</span></span> <span data-ttu-id="9db9e-195">Null 的等級與零的等級不同-null 表示不知道等級或尚未指派。</span><span class="sxs-lookup"><span data-stu-id="9db9e-195">A grade that's null is different from a zero grade — null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="9db9e-196">`StudentID` 屬性是外部索引鍵，對應的導覽屬性是 `Student`。</span><span class="sxs-lookup"><span data-stu-id="9db9e-196">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="9db9e-197">`Enrollment` 實體與一個 `Student` 實體關聯，因此屬性僅能保有單一 `Student` 實體 (不像您先前看到的 `Student.Enrollments` 導覽屬性可保有多個 `Enrollment` 實體)。</span><span class="sxs-lookup"><span data-stu-id="9db9e-197">An `Enrollment` entity is associated with one `Student` entity, so the property can only hold a single `Student` entity (unlike the `Student.Enrollments` navigation property you saw earlier, which can hold multiple `Enrollment` entities).</span></span>

<span data-ttu-id="9db9e-198">`CourseID` 屬性是外部索引鍵，對應的導覽屬性是 `Course`。</span><span class="sxs-lookup"><span data-stu-id="9db9e-198">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="9db9e-199">一個 `Enrollment` 實體與一個 `Course` 實體建立關聯。</span><span class="sxs-lookup"><span data-stu-id="9db9e-199">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="9db9e-200">Entity Framework 將屬性（property）&lt;導覽屬性名稱命名為「外鍵屬性」， *&gt;&lt;主鍵屬性名稱&gt;* （例如 `StudentID` `Student` 實體的主要索引鍵 `Student` 後，`ID`導覽屬性的）。</span><span class="sxs-lookup"><span data-stu-id="9db9e-200">Entity Framework interprets a property as a foreign key property if it's named *&lt;navigation property name&gt;&lt;primary key property name&gt;* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="9db9e-201">外鍵屬性也可以命名為相同 *&lt;主鍵屬性名稱&gt;* （例如 `CourseID`，因為 `Course` 實體的主要索引鍵是 `CourseID`）。</span><span class="sxs-lookup"><span data-stu-id="9db9e-201">Foreign key properties can also be named the same simply *&lt;primary key property name&gt;* (for example, `CourseID` since the `Course` entity's primary key is `CourseID`).</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="9db9e-202">Course 實體</span><span class="sxs-lookup"><span data-stu-id="9db9e-202">The Course entity</span></span>

- <span data-ttu-id="9db9e-203">在 [*模型*] 資料夾中，建立*Course.cs*，將範本程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="9db9e-203">In the *Models* folder, create *Course.cs*, replacing the template code with the following code:</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="9db9e-204">`Enrollments` 屬性為導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="9db9e-204">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="9db9e-205">`Course` 實體可以與任何數量的 `Enrollment` 實體相關。</span><span class="sxs-lookup"><span data-stu-id="9db9e-205">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="9db9e-206">我們將在本系列稍後的教學課程中，進一步瞭解 <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute> 屬性。</span><span class="sxs-lookup"><span data-stu-id="9db9e-206">We'll say more about the <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute> attribute in a later tutorial in this series.</span></span> <span data-ttu-id="9db9e-207">基本上，此屬性可讓您為課程輸入主索引鍵，而非讓資料庫產生它。</span><span class="sxs-lookup"><span data-stu-id="9db9e-207">Basically, this attribute lets you enter the primary key for the course rather than having the database generate it.</span></span>

## <a name="create-the-database-context"></a><span data-ttu-id="9db9e-208">建立資料庫內容</span><span class="sxs-lookup"><span data-stu-id="9db9e-208">Create the database context</span></span>

<span data-ttu-id="9db9e-209">協調給定資料模型 Entity Framework 功能的主要類別是*資料庫內容*類。</span><span class="sxs-lookup"><span data-stu-id="9db9e-209">The main class that coordinates Entity Framework functionality for a given data model is the *database context* class.</span></span> <span data-ttu-id="9db9e-210">您可以藉由衍生自[DbCoNtext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.113).aspx)類別來建立此類別。</span><span class="sxs-lookup"><span data-stu-id="9db9e-210">You create this class by deriving from the [System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.113).aspx) class.</span></span> <span data-ttu-id="9db9e-211">在您的程式碼中，您可以指定要包含在資料模型中的實體。</span><span class="sxs-lookup"><span data-stu-id="9db9e-211">In your code, you specify which entities are included in the data model.</span></span> <span data-ttu-id="9db9e-212">您也可以自訂某些 Entity Framework 行為。</span><span class="sxs-lookup"><span data-stu-id="9db9e-212">You can also customize certain Entity Framework behavior.</span></span> <span data-ttu-id="9db9e-213">在此專案中，類別命名為 `SchoolContext`。</span><span class="sxs-lookup"><span data-stu-id="9db9e-213">In this project, the class is named `SchoolContext`.</span></span>

- <span data-ttu-id="9db9e-214">若要在 ContosoUniversity 專案中建立資料夾，請以滑鼠右鍵按一下**方案總管**中的專案，然後按一下 [**加入**]，再按一下 [**新增資料夾**]。</span><span class="sxs-lookup"><span data-stu-id="9db9e-214">To create a folder in the ContosoUniversity project, right-click the project in **Solution Explorer** and click **Add**, and then click **New Folder**.</span></span> <span data-ttu-id="9db9e-215">將新資料夾命名為*DAL* （適用于資料存取層）。</span><span class="sxs-lookup"><span data-stu-id="9db9e-215">Name the new folder *DAL* (for Data Access Layer).</span></span> <span data-ttu-id="9db9e-216">在該資料夾中，建立名為*SchoolCoNtext.cs*的新類別檔案，並以下列程式碼取代範本程式碼：</span><span class="sxs-lookup"><span data-stu-id="9db9e-216">In that folder, create a new class file named *SchoolContext.cs*, and replace the template code with the following code:</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specify-entity-sets"></a><span data-ttu-id="9db9e-217">指定實體集</span><span class="sxs-lookup"><span data-stu-id="9db9e-217">Specify entity sets</span></span>

<span data-ttu-id="9db9e-218">此程式碼會為每個實體集建立[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.113).aspx)屬性。</span><span class="sxs-lookup"><span data-stu-id="9db9e-218">This code creates a [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.113).aspx) property for each entity set.</span></span> <span data-ttu-id="9db9e-219">在 Entity Framework 術語中，*實體集*通常會對應至資料庫資料表，而*實體*會對應到資料表中的資料列。</span><span class="sxs-lookup"><span data-stu-id="9db9e-219">In Entity Framework terminology, an *entity set* typically corresponds to a database table, and an *entity* corresponds to a row in the table.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9db9e-220">您可以省略 `DbSet<Enrollment>` 和 `DbSet<Course>` 語句，它的作用相同。</span><span class="sxs-lookup"><span data-stu-id="9db9e-220">You can omit the `DbSet<Enrollment>` and `DbSet<Course>` statements and it would work the same.</span></span> <span data-ttu-id="9db9e-221">Entity Framework 會隱含地包含這些專案，因為 `Student` 實體會參考 `Enrollment` 實體，而 `Enrollment` 實體會參考 `Course` 實體。</span><span class="sxs-lookup"><span data-stu-id="9db9e-221">Entity Framework would include them implicitly because the `Student` entity references the `Enrollment` entity and the `Enrollment` entity references the `Course` entity.</span></span>

### <a name="specify-the-connection-string"></a><span data-ttu-id="9db9e-222">指定連接字串</span><span class="sxs-lookup"><span data-stu-id="9db9e-222">Specify the connection string</span></span>

<span data-ttu-id="9db9e-223">連接字串的名稱（您稍後將會加入 web.config 檔案中）會傳遞至該函式。</span><span class="sxs-lookup"><span data-stu-id="9db9e-223">The name of the connection string (which you'll add to the Web.config file later) is passed in to the constructor.</span></span>

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

<span data-ttu-id="9db9e-224">您也可以傳入連接字串本身，而不是儲存在 web.config 檔案中的名稱。</span><span class="sxs-lookup"><span data-stu-id="9db9e-224">You could also pass in the connection string itself instead of the name of one that is stored in the Web.config file.</span></span> <span data-ttu-id="9db9e-225">如需指定要使用的資料庫之選項的詳細資訊，請參閱[連接字串和模型](/ef/ef6/fundamentals/configuring/connection-strings)。</span><span class="sxs-lookup"><span data-stu-id="9db9e-225">For more information about options for specifying the database to use, see [Connection strings and models](/ef/ef6/fundamentals/configuring/connection-strings).</span></span>

<span data-ttu-id="9db9e-226">如果您未明確指定連接字串或名稱，Entity Framework 會假設連接字串名稱與類別名稱相同。</span><span class="sxs-lookup"><span data-stu-id="9db9e-226">If you don't specify a connection string or the name of one explicitly, Entity Framework assumes that the connection string name is the same as the class name.</span></span> <span data-ttu-id="9db9e-227">此範例中的預設連接字串名稱會 `SchoolContext`，與您明確指定的相同。</span><span class="sxs-lookup"><span data-stu-id="9db9e-227">The default connection string name in this example would then be `SchoolContext`, the same as what you're specifying explicitly.</span></span>

### <a name="specify-singular-table-names"></a><span data-ttu-id="9db9e-228">指定單數資料表名稱</span><span class="sxs-lookup"><span data-stu-id="9db9e-228">Specify singular table names</span></span>

<span data-ttu-id="9db9e-229">[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法中的 `modelBuilder.Conventions.Remove` 語句會防止複數化資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="9db9e-229">The `modelBuilder.Conventions.Remove` statement in the [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) method prevents table names from being pluralized.</span></span> <span data-ttu-id="9db9e-230">如果您未這麼做，則資料庫中產生的資料表會命名為 `Students`、`Courses`和 `Enrollments`。</span><span class="sxs-lookup"><span data-stu-id="9db9e-230">If you didn't do this, the generated tables in the database would be named `Students`, `Courses`, and `Enrollments`.</span></span> <span data-ttu-id="9db9e-231">相反地，資料表名稱會是 `Student`、`Course`和 `Enrollment`。</span><span class="sxs-lookup"><span data-stu-id="9db9e-231">Instead, the table names will be `Student`, `Course`, and `Enrollment`.</span></span> <span data-ttu-id="9db9e-232">針對是否要複數化資料表名稱，開發人員並沒有共識。</span><span class="sxs-lookup"><span data-stu-id="9db9e-232">Developers disagree about whether table names should be pluralized or not.</span></span> <span data-ttu-id="9db9e-233">本教學課程使用單數形式，但重點在於，您可以藉由包含或省略這行程式碼來選取您偏好的任何格式。</span><span class="sxs-lookup"><span data-stu-id="9db9e-233">This tutorial uses the singular form, but the important point is that you can select whichever form you prefer by including or omitting this line of code.</span></span>

## <a name="initialize-db-with-test-data"></a><span data-ttu-id="9db9e-234">使用測試資料將 DB 初始化</span><span class="sxs-lookup"><span data-stu-id="9db9e-234">Initialize DB with test data</span></span>

<span data-ttu-id="9db9e-235">Entity Framework 可以在應用程式執行時，自動為您建立（或卸載並重新建立）資料庫。</span><span class="sxs-lookup"><span data-stu-id="9db9e-235">Entity Framework can automatically create (or drop and re-create) a database for you when the application runs.</span></span> <span data-ttu-id="9db9e-236">您可以指定每次執行應用程式時，或只有在模型與現有資料庫不同步時，才會執行此作業。</span><span class="sxs-lookup"><span data-stu-id="9db9e-236">You can specify that this should be done every time your application runs or only when the model is out of sync with the existing database.</span></span> <span data-ttu-id="9db9e-237">您也可以撰寫 `Seed` 方法，Entity Framework 在建立資料庫之後自動呼叫，以便將測試資料填入其中。</span><span class="sxs-lookup"><span data-stu-id="9db9e-237">You can also write a `Seed` method that Entity Framework automatically calls after creating the database in order to populate it with test data.</span></span>

<span data-ttu-id="9db9e-238">預設行為是只在資料庫不存在時才建立它（如果模型已變更且資料庫已經存在，則會擲回例外狀況）。</span><span class="sxs-lookup"><span data-stu-id="9db9e-238">The default behavior is to create a database only if it doesn't exist (and throw an exception if the model has changed and the database already exists).</span></span> <span data-ttu-id="9db9e-239">在本節中，您將指定每當模型變更時，應該卸載並重新建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="9db9e-239">In this section, you'll specify that the database should be dropped and re-created whenever the model changes.</span></span> <span data-ttu-id="9db9e-240">卸載資料庫會導致所有資料遺失。</span><span class="sxs-lookup"><span data-stu-id="9db9e-240">Dropping the database causes the loss of all your data.</span></span> <span data-ttu-id="9db9e-241">這在開發期間通常是正常的，因為當重新建立資料庫時，會執行 `Seed` 方法，並重新建立您的測試資料。</span><span class="sxs-lookup"><span data-stu-id="9db9e-241">This is generally okay during development, because the `Seed` method will run when the database is re-created and will re-create your test data.</span></span> <span data-ttu-id="9db9e-242">但是在生產環境中，您通常不會想要在每次需要變更資料庫架構時遺失所有資料。</span><span class="sxs-lookup"><span data-stu-id="9db9e-242">But in production you generally don't want to lose all your data every time you need to change the database schema.</span></span> <span data-ttu-id="9db9e-243">稍後您會看到如何使用 Code First 移轉變更資料庫架構，而不是卸載並重新建立資料庫，以處理模型變更。</span><span class="sxs-lookup"><span data-stu-id="9db9e-243">Later you'll see how to handle model changes by using Code First Migrations to change the database schema instead of dropping and re-creating the database.</span></span>

1. <span data-ttu-id="9db9e-244">在 DAL 資料夾中，建立名為*SchoolInitializer.cs*的新類別檔案，並將範本程式碼取代為下列程式碼，這會在需要時建立資料庫，並將測試資料載入至新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="9db9e-244">In the DAL folder, create a new class file named *SchoolInitializer.cs* and replace the template code with the following code, which causes a database to be created when needed and loads test data into the new database.</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

   <span data-ttu-id="9db9e-245">`Seed` 方法會將資料庫內容物件當做輸入參數，而方法中的程式碼會使用該物件將新的實體加入至資料庫。</span><span class="sxs-lookup"><span data-stu-id="9db9e-245">The `Seed` method takes the database context object as an input parameter, and the code in the method uses that object to add new entities to the database.</span></span> <span data-ttu-id="9db9e-246">針對每個實體類型，程式碼會建立新實體的集合，並將其加入適當的 `DbSet` 屬性，然後將變更儲存至資料庫。</span><span class="sxs-lookup"><span data-stu-id="9db9e-246">For each entity type, the code creates a collection of new  entities, adds them to the appropriate `DbSet` property, and then saves the changes to the database.</span></span> <span data-ttu-id="9db9e-247">在每個實體群組之後，都不需要呼叫 `SaveChanges` 方法，但在這裡完成這項作業，但如果程式碼寫入資料庫時發生例外狀況，就會協助您找出問題的來源。</span><span class="sxs-lookup"><span data-stu-id="9db9e-247">It isn't necessary to call the `SaveChanges` method after each group of entities, as is done here, but doing that helps you locate the source of a problem if an exception occurs while the code is writing to the database.</span></span>

2. <span data-ttu-id="9db9e-248">若要告知 Entity Framework 使用您的初始化運算式類別，請將專案新增至應用程式*web.config*檔案中的 `entityFramework` 元素（根專案資料夾中的），如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="9db9e-248">To tell Entity Framework to use your initializer class, add an element to the `entityFramework` element in the application *Web.config* file (the one in the root project folder), as shown in the following example:</span></span>

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

   <span data-ttu-id="9db9e-249">`context type` 會指定完整的內容類別名稱及其所在的元件，而 `databaseinitializer type` 會指定初始化運算式類別及其所在元件的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="9db9e-249">The `context type` specifies the fully qualified context class name and the assembly it's in, and the `databaseinitializer type` specifies the fully qualified name of the initializer class and the assembly it's in.</span></span> <span data-ttu-id="9db9e-250">（當您不想讓 EF 使用初始化運算式時，可以在 `context` 元素上設定屬性： `disableDatabaseInitialization="true"`）。如需詳細資訊，請參閱[設定檔案設定](/ef/ef6/fundamentals/configuring/config-file)。</span><span class="sxs-lookup"><span data-stu-id="9db9e-250">(When you don't want EF to use the initializer, you can set an attribute on the `context` element: `disableDatabaseInitialization="true"`.) For more information, see [Configuration File Settings](/ef/ef6/fundamentals/configuring/config-file).</span></span>

   <span data-ttu-id="9db9e-251">在*web.config*檔案中設定初始化運算式的替代方法是，藉由將 `Database.SetInitializer` 語句加入至*Global.asax.cs*檔案中的 `Application_Start` 方法，在程式碼中執行此動作。</span><span class="sxs-lookup"><span data-stu-id="9db9e-251">An alternative to setting the initializer in the *Web.config* file is to do it in code by adding a `Database.SetInitializer` statement to the `Application_Start` method in the *Global.asax.cs* file.</span></span> <span data-ttu-id="9db9e-252">如需詳細資訊，請參閱[瞭解 Entity Framework Code First 中的資料庫初始化運算式](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)。</span><span class="sxs-lookup"><span data-stu-id="9db9e-252">For more information, see [Understanding Database Initializers in Entity Framework Code First](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm).</span></span>

<span data-ttu-id="9db9e-253">應用程式現在已設定，因此當您第一次在指定的應用程式執行中存取資料庫時，Entity Framework 會將資料庫與模型（您的 `SchoolContext` 和實體類別）做比較。</span><span class="sxs-lookup"><span data-stu-id="9db9e-253">The application is now set up so that when you access the database for the first time in a given run of the application, Entity Framework compares the database to the model (your `SchoolContext` and entity classes).</span></span> <span data-ttu-id="9db9e-254">如果有差異，應用程式會卸載並重新建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="9db9e-254">If there's a difference, the application drops and re-creates the database.</span></span>

> [!NOTE]
> <span data-ttu-id="9db9e-255">當您將應用程式部署到生產 web 伺服器時，您必須移除或停用卸載並重新建立資料庫的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9db9e-255">When you deploy an application to a production web server, you must remove or disable code that drops and re-creates the database.</span></span> <span data-ttu-id="9db9e-256">您將在本系列稍後的教學課程中執行此動作。</span><span class="sxs-lookup"><span data-stu-id="9db9e-256">You'll do that in a later tutorial in this series.</span></span>

## <a name="set-up-ef-6-to-use-localdb"></a><span data-ttu-id="9db9e-257">設定 EF 6 使用 LocalDB</span><span class="sxs-lookup"><span data-stu-id="9db9e-257">Set up EF 6 to use LocalDB</span></span>

<span data-ttu-id="9db9e-258">[LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017)是輕量版的 SQL Server Express 資料庫引擎。</span><span class="sxs-lookup"><span data-stu-id="9db9e-258">[LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017) is a lightweight version of the SQL Server Express database engine.</span></span> <span data-ttu-id="9db9e-259">安裝和設定、視需要啟動，以及在使用者模式中執行，都很容易。</span><span class="sxs-lookup"><span data-stu-id="9db9e-259">It's easy to install and configure, starts on demand, and runs in user mode.</span></span> <span data-ttu-id="9db9e-260">LocalDB 會在 SQL Server Express 的特殊執行模式下執行，可讓您使用資料庫做為 *.mdf*檔案。</span><span class="sxs-lookup"><span data-stu-id="9db9e-260">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="9db9e-261">如果您想要能夠使用專案來複製資料庫，您可以將 LocalDB 資料庫檔案放在 Web 專案的*應用程式\_Data*資料夾中。</span><span class="sxs-lookup"><span data-stu-id="9db9e-261">You can put LocalDB database files in the *App\_Data* folder of a web project if you want to be able to copy the database with the project.</span></span> <span data-ttu-id="9db9e-262">SQL Server Express 中的使用者實例功能也可讓您使用 *.mdf*檔案，但是使用者實例功能已被取代;因此，建議使用 LocalDB 來處理 *.mdf*檔案。</span><span class="sxs-lookup"><span data-stu-id="9db9e-262">The user instance feature in SQL Server Express also enables you to work with *.mdf* files, but the user instance feature is deprecated; therefore, LocalDB is recommended for working with *.mdf* files.</span></span> <span data-ttu-id="9db9e-263">LocalDB 預設會隨 Visual Studio 安裝。</span><span class="sxs-lookup"><span data-stu-id="9db9e-263">LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="9db9e-264">通常，SQL Server Express 不會用於生產 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9db9e-264">Typically, SQL Server Express is not used for production web applications.</span></span> <span data-ttu-id="9db9e-265">不建議將 LocalDB 用於與 web 應用程式搭配使用的生產環境，因為它不是設計用於 IIS。</span><span class="sxs-lookup"><span data-stu-id="9db9e-265">LocalDB in particular is not recommended for production use with a web application because it's not designed to work with IIS.</span></span>

- <span data-ttu-id="9db9e-266">在本教學課程中，您將使用 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="9db9e-266">In this tutorial, you'll work with LocalDB.</span></span> <span data-ttu-id="9db9e-267">開啟*應用程式的 web.config 檔案*，然後在 `appSettings` 元素前面加入 `connectionStrings` 元素，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="9db9e-267">Open the application *Web.config* file and add a `connectionStrings` element preceding the `appSettings` element, as shown in the following example.</span></span> <span data-ttu-id="9db9e-268">（請務必更新根專案資料夾*中的 web.config 檔案。*</span><span class="sxs-lookup"><span data-stu-id="9db9e-268">(Make sure you update the *Web.config* file in the root project folder.</span></span> <span data-ttu-id="9db9e-269">*Views*子資料夾中也*有一個 web.config*檔案，您不需要更新此檔案）。</span><span class="sxs-lookup"><span data-stu-id="9db9e-269">There's also a *Web.config* file in the *Views* subfolder that you don't need to update.)</span></span>

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

<span data-ttu-id="9db9e-270">您已新增的連接字串會指定 Entity Framework 將使用名為*ContosoUniversity1*的 LocalDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9db9e-270">The connection string you've added specifies that Entity Framework will use a LocalDB database named *ContosoUniversity1.mdf*.</span></span> <span data-ttu-id="9db9e-271">（資料庫尚不存在，但 EF 會加以建立）。如果您想要在*應用程式\_Data*資料夾中建立資料庫，您可以將 `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` 新增至連接字串。</span><span class="sxs-lookup"><span data-stu-id="9db9e-271">(The database doesn't exist yet but EF will create it.) If you want to create the database in your *App\_Data* folder, you could add `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` to the connection string.</span></span> <span data-ttu-id="9db9e-272">如需連接字串的詳細資訊，請參閱[SQL Server ASP.NET Web 應用程式的連接字串](/previous-versions/aspnet/jj653752(v=vs.110))。</span><span class="sxs-lookup"><span data-stu-id="9db9e-272">For more information about connection strings, see [SQL Server Connection Strings for ASP.NET Web Applications](/previous-versions/aspnet/jj653752(v=vs.110)).</span></span>

<span data-ttu-id="9db9e-273">您實際上不需要*在 web.config 檔案*中使用連接字串。</span><span class="sxs-lookup"><span data-stu-id="9db9e-273">You don't actually need a connection string in the *Web.config* file.</span></span> <span data-ttu-id="9db9e-274">如果您未提供連接字串，Entity Framework 會根據您的內容類別來使用預設連接字串。</span><span class="sxs-lookup"><span data-stu-id="9db9e-274">If you don't supply a connection string, Entity Framework uses a default connection string based on your context class.</span></span> <span data-ttu-id="9db9e-275">如需詳細資訊，請參閱[Code First 至新的資料庫](/ef/ef6/modeling/code-first/workflows/new-database)。</span><span class="sxs-lookup"><span data-stu-id="9db9e-275">For more information, see [Code First to a New Database](/ef/ef6/modeling/code-first/workflows/new-database).</span></span>

## <a name="create-controller-and-views"></a><span data-ttu-id="9db9e-276">建立控制器和檢視</span><span class="sxs-lookup"><span data-stu-id="9db9e-276">Create controller and views</span></span>

<span data-ttu-id="9db9e-277">現在您將建立網頁來顯示資料。</span><span class="sxs-lookup"><span data-stu-id="9db9e-277">Now you'll create a web page to display data.</span></span> <span data-ttu-id="9db9e-278">要求資料的程式會自動觸發資料庫的建立。</span><span class="sxs-lookup"><span data-stu-id="9db9e-278">The process of requesting the data automatically triggers the creation of the database.</span></span> <span data-ttu-id="9db9e-279">首先您要建立新的控制器。</span><span class="sxs-lookup"><span data-stu-id="9db9e-279">You'll begin by creating a new controller.</span></span> <span data-ttu-id="9db9e-280">但是在執行此動作之前，請先建立專案，讓模型和內容類別別可用於 MVC 控制器的架構。</span><span class="sxs-lookup"><span data-stu-id="9db9e-280">But before you do that, build the project to make the model and context classes available to MVC controller scaffolding.</span></span>

1. <span data-ttu-id="9db9e-281">以滑鼠右鍵按一下**方案總管**中的 [**控制器**] 資料夾，選取 [**加入**]，然後按一下 [**新增 scaffold 專案**]。</span><span class="sxs-lookup"><span data-stu-id="9db9e-281">Right-click the **Controllers** folder in **Solution Explorer**, select **Add**, and then click **New Scaffolded Item**.</span></span>
2. <span data-ttu-id="9db9e-282">在 [**新增 Scaffold** ] 對話方塊中，使用 [Entity Framework] 選取 [**具有視圖的 MVC 5 控制器**]，然後選擇 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="9db9e-282">In the **Add Scaffold** dialog box, select **MVC 5 Controller with views, using Entity Framework**, and then choose **Add**.</span></span>

     ![Visual Studio 中的 [新增 Scaffold] 對話方塊](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/add-scaffold.png)

3. <span data-ttu-id="9db9e-284">在 [**新增控制器**] 對話方塊中，進行下列選擇，然後選擇 [**新增**]：</span><span class="sxs-lookup"><span data-stu-id="9db9e-284">In the **Add Controller** dialog box, make the following selections, and then choose **Add**:</span></span>

   - <span data-ttu-id="9db9e-285">模型類別： **Student （ContosoUniversity）** 。</span><span class="sxs-lookup"><span data-stu-id="9db9e-285">Model class: **Student (ContosoUniversity.Models)**.</span></span> <span data-ttu-id="9db9e-286">（如果您在下拉式清單中看不到這個選項，請建立專案，然後再試一次）。</span><span class="sxs-lookup"><span data-stu-id="9db9e-286">(If you don't see this option in the drop-down list, build the project and try again.)</span></span>
   - <span data-ttu-id="9db9e-287">資料內容類別： **SchoolCoNtext （ContosoUniversity）** 。</span><span class="sxs-lookup"><span data-stu-id="9db9e-287">Data context class: **SchoolContext (ContosoUniversity.DAL)**.</span></span>
   - <span data-ttu-id="9db9e-288">控制器名稱： **StudentController** （不是 studentscontroller.cs）。</span><span class="sxs-lookup"><span data-stu-id="9db9e-288">Controller name: **StudentController** (not StudentsController).</span></span>
   - <span data-ttu-id="9db9e-289">保留其他欄位的預設值。</span><span class="sxs-lookup"><span data-stu-id="9db9e-289">Leave the default values for the other fields.</span></span>

     <span data-ttu-id="9db9e-290">當您按一下 [**新增**] 時，scaffolder 會建立一個*StudentController.cs*檔，以及一組可與控制器搭配使用的視圖（ *. cshtml*檔案）。</span><span class="sxs-lookup"><span data-stu-id="9db9e-290">When you click **Add**, the scaffolder creates a *StudentController.cs* file and a set of views (*.cshtml* files) that work with the controller.</span></span> <span data-ttu-id="9db9e-291">在未來建立使用 Entity Framework 的專案時，您也可以利用 scaffolder 的一些額外功能：建立您的第一個模型類別、不要建立連接字串，然後在 [**新增控制器**] 方塊中選取 [**資料內容類別**] 旁邊的 [ **+** ] 按鈕，以指定**新的資料內容**。</span><span class="sxs-lookup"><span data-stu-id="9db9e-291">In the future when you create projects that use Entity Framework, you can also take advantage of some additional functionality of the scaffolder: create your first model class, don't create a connection string, and then in the **Add Controller** box specify **New data context** by selecting the **+** button next to **Data context class**.</span></span> <span data-ttu-id="9db9e-292">Scaffolder 會建立您的 `DbContext` 類別和您的連接字串，以及控制器和 views。</span><span class="sxs-lookup"><span data-stu-id="9db9e-292">The scaffolder will create your `DbContext` class and your connection string as well as the controller and views.</span></span>
4. <span data-ttu-id="9db9e-293">Visual Studio 會開啟*Controllers\StudentController.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="9db9e-293">Visual Studio opens the *Controllers\StudentController.cs* file.</span></span> <span data-ttu-id="9db9e-294">您會看到已建立可具現化資料庫內容物件的類別變數：</span><span class="sxs-lookup"><span data-stu-id="9db9e-294">You see that a class variable has been created that instantiates a database context object:</span></span>

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

     <span data-ttu-id="9db9e-295">`Index` 動作方法會藉由讀取資料庫內容實例的 `Students` 屬性，從*學生*實體集取得學生的清單：</span><span class="sxs-lookup"><span data-stu-id="9db9e-295">The `Index` action method gets a list of students from the *Students* entity set by reading the `Students` property of the database context instance:</span></span>

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

     <span data-ttu-id="9db9e-296">*Student\Index.cshtml* view 會在資料表中顯示此清單：</span><span class="sxs-lookup"><span data-stu-id="9db9e-296">The *Student\Index.cshtml* view displays this list in a table:</span></span>

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
5. <span data-ttu-id="9db9e-297">按 Ctrl+F5 執行專案。</span><span class="sxs-lookup"><span data-stu-id="9db9e-297">Press Ctrl+F5 to run the project.</span></span> <span data-ttu-id="9db9e-298">（如果您收到「無法建立陰影複製」錯誤，請關閉瀏覽器，然後再試一次）。</span><span class="sxs-lookup"><span data-stu-id="9db9e-298">(If you get a "Cannot create Shadow Copy" error, close the browser and try again.)</span></span>

     <span data-ttu-id="9db9e-299">按一下 [**學生**] 索引標籤，查看 `Seed` 方法所插入的測試資料。</span><span class="sxs-lookup"><span data-stu-id="9db9e-299">Click the **Students** tab to see the test data that the `Seed` method inserted.</span></span> <span data-ttu-id="9db9e-300">視瀏覽器視窗的範圍而定，您會在頂端的網址列中看到 [Student] 索引標籤連結，或者您必須按一下右上角才能看到連結。</span><span class="sxs-lookup"><span data-stu-id="9db9e-300">Depending on how narrow your browser window is, you'll see the Student tab link in the top address bar or you'll have to click the upper right corner to see the link.</span></span>

     ![功能表按鈕](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

## <a name="view-the-database"></a><span data-ttu-id="9db9e-302">檢視資料庫</span><span class="sxs-lookup"><span data-stu-id="9db9e-302">View the database</span></span>

<span data-ttu-id="9db9e-303">當您執行 [學生] 頁面，而應用程式嘗試存取資料庫時，EF 發現沒有資料庫，而且已建立一個。</span><span class="sxs-lookup"><span data-stu-id="9db9e-303">When you ran the Students page and the application tried to access the database, EF discovered that there was no database and created one.</span></span> <span data-ttu-id="9db9e-304">EF 接著會執行種子方法，將資料填入資料庫。</span><span class="sxs-lookup"><span data-stu-id="9db9e-304">EF then ran the seed method to populate the database with data.</span></span>

<span data-ttu-id="9db9e-305">您可以使用**伺服器總管**或**SQL Server 物件總管**（SSOX），在 Visual Studio 中查看資料庫。</span><span class="sxs-lookup"><span data-stu-id="9db9e-305">You can use either **Server Explorer** or **SQL Server Object Explorer** (SSOX) to view the database in Visual Studio.</span></span> <span data-ttu-id="9db9e-306">在本教學課程中，您將使用**伺服器總管**。</span><span class="sxs-lookup"><span data-stu-id="9db9e-306">For this tutorial, you'll use **Server Explorer**.</span></span>

1. <span data-ttu-id="9db9e-307">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="9db9e-307">Close the browser.</span></span>
2. <span data-ttu-id="9db9e-308">在**伺服器總管**中，展開 [**資料連線**] （您可能需要先選取 [重新整理] 按鈕）、展開 [ **School CoNtext （ContosoUniversity）** ]，然後展開 [**資料表]** ，以查看新資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="9db9e-308">In **Server Explorer**, expand **Data Connections** (you may need to select the refresh button first), expand **School Context (ContosoUniversity)**, and then expand **Tables** to see the tables in your new database.</span></span>

3. <span data-ttu-id="9db9e-309">以滑鼠右鍵按一下 [ **Student** ] 資料表，然後按一下 [**顯示資料表資料**]，以查看已建立的資料行以及已插入資料表中的資料列。</span><span class="sxs-lookup"><span data-stu-id="9db9e-309">Right-click the **Student** table and click **Show Table Data** to see the columns that were created and the rows that were inserted into the table.</span></span>

4. <span data-ttu-id="9db9e-310">關閉**伺服器總管**連接。</span><span class="sxs-lookup"><span data-stu-id="9db9e-310">Close the **Server Explorer** connection.</span></span>

<span data-ttu-id="9db9e-311">*ContosoUniversity1*是 *% USERPROFILE%* 資料夾中*的資料庫檔案。*</span><span class="sxs-lookup"><span data-stu-id="9db9e-311">The *ContosoUniversity1.mdf* and *.ldf* database files are in the *%USERPROFILE%* folder.</span></span>

<span data-ttu-id="9db9e-312">因為您使用的是 `DropCreateDatabaseIfModelChanges` 初始化運算式，所以您現在可以變更 `Student` 類別、再次執行應用程式，而且會自動重新建立資料庫以符合您的變更。</span><span class="sxs-lookup"><span data-stu-id="9db9e-312">Because you're using the `DropCreateDatabaseIfModelChanges` initializer, you could now make a change to the `Student` class, run the application again, and the database would automatically be re-created to match your change.</span></span> <span data-ttu-id="9db9e-313">例如，如果您將 `EmailAddress` 屬性加入 `Student` 類別，請再次執行 [學生] 頁面，然後再次查看資料表，您會看到新的 `EmailAddress` 資料行。</span><span class="sxs-lookup"><span data-stu-id="9db9e-313">For example, if you add an `EmailAddress` property to the `Student` class, run the Students page again, and then look at the table again, you'll see a new `EmailAddress` column.</span></span>

## <a name="conventions"></a><span data-ttu-id="9db9e-314">慣例</span><span class="sxs-lookup"><span data-stu-id="9db9e-314">Conventions</span></span>

<span data-ttu-id="9db9e-315">為了讓 Entity Framework 能夠為您建立完整資料庫，您必須撰寫的程式碼數量最少，因為*慣例*或 Entity Framework 所做的假設。</span><span class="sxs-lookup"><span data-stu-id="9db9e-315">The amount of code you had to write in order for Entity Framework to be able to create a complete database for you is minimal because of *conventions*, or assumptions that Entity Framework makes.</span></span> <span data-ttu-id="9db9e-316">其中有些是已記下或已使用，而不需要您知道它們：</span><span class="sxs-lookup"><span data-stu-id="9db9e-316">Some of them have already been noted or were used without your being aware of them:</span></span>

- <span data-ttu-id="9db9e-317">實體類別名稱的複數化形式會當做資料表名稱使用。</span><span class="sxs-lookup"><span data-stu-id="9db9e-317">The pluralized forms of entity class names are used as table names.</span></span>
- <span data-ttu-id="9db9e-318">實體屬性名稱會用於資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="9db9e-318">Entity property names are used for column names.</span></span>
- <span data-ttu-id="9db9e-319">名為 `ID` 或*classname* `ID` 的實體屬性會被辨識為主鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="9db9e-319">Entity properties that are named `ID` or *classname* `ID` are recognized as primary key properties.</span></span>
- <span data-ttu-id="9db9e-320">如果將屬性命名為 *&lt;導覽屬性名稱&gt;&lt;主鍵屬性名稱&gt;* （例如 `StudentID` `Student` 實體的主要索引鍵 `Student`），則會將其視為外鍵屬性。`ID`</span><span class="sxs-lookup"><span data-stu-id="9db9e-320">A property is interpreted as a foreign key property if it's named *&lt;navigation property name&gt;&lt;primary key property name&gt;* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="9db9e-321">外鍵屬性也可以命名為相同 &lt;主鍵屬性名稱&gt; （例如 `EnrollmentID`，因為 `Enrollment` 實體的主要索引鍵是 `EnrollmentID`）。</span><span class="sxs-lookup"><span data-stu-id="9db9e-321">Foreign key properties can also be named the same simply &lt;primary key property name&gt; (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="9db9e-322">您已瞭解可以覆寫慣例。</span><span class="sxs-lookup"><span data-stu-id="9db9e-322">You've seen that conventions can be overridden.</span></span> <span data-ttu-id="9db9e-323">例如，您指定不應複數化資料表名稱，稍後您會看到如何將屬性明確地標示為外鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="9db9e-323">For example, you specified that table names shouldn't be pluralized, and you'll see later how to explicitly mark a property as a foreign key property.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="9db9e-324">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="9db9e-324">Get the code</span></span>

[<span data-ttu-id="9db9e-325">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="9db9e-325">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="9db9e-326">其他資源</span><span class="sxs-lookup"><span data-stu-id="9db9e-326">Additional resources</span></span>

<span data-ttu-id="9db9e-327">如需 EF 6 的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="9db9e-327">For more about EF 6, see these articles:</span></span>

* [<span data-ttu-id="9db9e-328">ASP.NET 資料存取 - 建議資源</span><span class="sxs-lookup"><span data-stu-id="9db9e-328">ASP.NET Data Access - Recommended Resources</span></span>](../../../../whitepapers/aspnet-data-access-content-map.md)

* [<span data-ttu-id="9db9e-329">Code First 慣例</span><span class="sxs-lookup"><span data-stu-id="9db9e-329">Code First Conventions</span></span>](/ef/ef6/modeling/code-first/conventions/built-in)

* [<span data-ttu-id="9db9e-330">建立更複雜的資料模型</span><span class="sxs-lookup"><span data-stu-id="9db9e-330">Creating a More Complex Data Model</span></span>](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="next-steps"></a><span data-ttu-id="9db9e-331">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9db9e-331">Next steps</span></span>

<span data-ttu-id="9db9e-332">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="9db9e-332">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9db9e-333">建立 MVC web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9db9e-333">Created an MVC web app</span></span>
> * <span data-ttu-id="9db9e-334">設定網站樣式</span><span class="sxs-lookup"><span data-stu-id="9db9e-334">Set up the site style</span></span>
> * <span data-ttu-id="9db9e-335">已安裝 Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="9db9e-335">Installed Entity Framework 6</span></span>
> * <span data-ttu-id="9db9e-336">建立資料模型</span><span class="sxs-lookup"><span data-stu-id="9db9e-336">Created the data model</span></span>
> * <span data-ttu-id="9db9e-337">建立資料庫內容</span><span class="sxs-lookup"><span data-stu-id="9db9e-337">Created the database context</span></span>
> * <span data-ttu-id="9db9e-338">使用測試資料將 DB 初始化</span><span class="sxs-lookup"><span data-stu-id="9db9e-338">Initialized DB with test data</span></span>
> * <span data-ttu-id="9db9e-339">設定 EF 6 使用 LocalDB</span><span class="sxs-lookup"><span data-stu-id="9db9e-339">Set up EF 6 to use LocalDB</span></span>
> * <span data-ttu-id="9db9e-340">建立控制器和檢視</span><span class="sxs-lookup"><span data-stu-id="9db9e-340">Created controller and views</span></span>
> * <span data-ttu-id="9db9e-341">檢視資料庫</span><span class="sxs-lookup"><span data-stu-id="9db9e-341">Viewed the database</span></span>

<span data-ttu-id="9db9e-342">前往下一篇文章，以瞭解如何在您的控制器和 views 中檢查和自訂建立、讀取、更新、刪除（CRUD）程式碼。</span><span class="sxs-lookup"><span data-stu-id="9db9e-342">Advance to the next article to learn how to review and customize the create, read, update, delete (CRUD) code in your controllers and views.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9db9e-343">實作基本的 CRUD 功能</span><span class="sxs-lookup"><span data-stu-id="9db9e-343">Implement basic CRUD functionality</span></span>](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)