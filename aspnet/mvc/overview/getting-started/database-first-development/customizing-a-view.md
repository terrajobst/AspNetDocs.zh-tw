---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 教學課程：使用 ASP.NET MVC 應用程式自訂 EF Database First 的 view
description: 本教學課程著重于變更自動產生的視圖，以增強簡報。
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583591"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="31147-103">教學課程：使用 ASP.NET MVC 應用程式自訂 EF Database First 的 view</span><span class="sxs-lookup"><span data-stu-id="31147-103">Tutorial: Customize view for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="31147-104">使用 MVC、Entity Framework 和 ASP.NET 的樣板，您可以建立 web 應用程式，以提供介面給現有的資料庫。</span><span class="sxs-lookup"><span data-stu-id="31147-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="31147-105">本教學課程系列會示範如何自動產生程式碼，讓使用者可以顯示、編輯、建立和刪除位於資料庫資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="31147-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="31147-106">產生的程式碼會對應至資料庫資料表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="31147-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="31147-107">本教學課程著重于變更自動產生的視圖，以增強簡報。</span><span class="sxs-lookup"><span data-stu-id="31147-107">This tutorial focuses on changing the automatically-generated views to enhance the presentation.</span></span>

<span data-ttu-id="31147-108">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="31147-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="31147-109">將課程新增至學生詳細資料頁面</span><span class="sxs-lookup"><span data-stu-id="31147-109">Add courses to the student detail page</span></span>
> * <span data-ttu-id="31147-110">確認課程已新增至頁面</span><span class="sxs-lookup"><span data-stu-id="31147-110">Confirm that the courses are added to the page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31147-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="31147-111">Prerequisites</span></span>

* [<span data-ttu-id="31147-112">變更資料庫</span><span class="sxs-lookup"><span data-stu-id="31147-112">Change the database</span></span>](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a><span data-ttu-id="31147-113">新增課程到學生的詳細資料</span><span class="sxs-lookup"><span data-stu-id="31147-113">Add courses to student detail</span></span>

<span data-ttu-id="31147-114">產生的程式碼會為您的應用程式提供良好的起點，但不一定要提供應用程式中所需的所有功能。</span><span class="sxs-lookup"><span data-stu-id="31147-114">The generated code provides a good starting point for your application but it does not necessarily provide all of the functionality that you need in your application.</span></span> <span data-ttu-id="31147-115">您可以自訂程式碼，以符合應用程式的特定需求。</span><span class="sxs-lookup"><span data-stu-id="31147-115">You can customize the code to meet the particular requirements of your application.</span></span> <span data-ttu-id="31147-116">目前，您的應用程式不會顯示所選學生的已註冊課程。</span><span class="sxs-lookup"><span data-stu-id="31147-116">Currently, your application does not display the enrolled courses for the selected student.</span></span> <span data-ttu-id="31147-117">在本節中，您會將每個學生註冊的課程新增至學生的**詳細資料**視圖。</span><span class="sxs-lookup"><span data-stu-id="31147-117">In this section, you will add the enrolled courses for each student to the **Details** view for the student.</span></span>

<span data-ttu-id="31147-118"> > **學生** > *詳細資料中*開啟**Views** 。 cshtml。</span><span class="sxs-lookup"><span data-stu-id="31147-118">Open **Views** > **Students** > *Details.cshtml*.</span></span> <span data-ttu-id="31147-119">在最後一個 &lt;/dl&gt; 標記，但在關閉 &lt;/div&gt; 標記之前，新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="31147-119">Below the last &lt;/dl&gt; tag, but before the closing &lt;/div&gt; tag, add the following code.</span></span>

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

<span data-ttu-id="31147-120">這段程式碼會建立一個資料表，針對所選學生在註冊資料表中的每筆記錄，顯示一個資料列。</span><span class="sxs-lookup"><span data-stu-id="31147-120">This code creates a table that displays a row for each record in the Enrollment table for the selected student.</span></span> <span data-ttu-id="31147-121">**顯示**方法會針對表示運算式的物件（modelItem）呈現 HTML。</span><span class="sxs-lookup"><span data-stu-id="31147-121">The **Display** method renders HTML for the object (modelItem) that represents the expression.</span></span> <span data-ttu-id="31147-122">您可以使用顯示方法（而不只是在程式碼中內嵌屬性值），以確定該值的格式是否正確，取決於其型別和該型別的範本。</span><span class="sxs-lookup"><span data-stu-id="31147-122">You use the Display method (rather than simply embedding the property value in the code) to make sure the value is formatted correctly based on its type and the template for that type.</span></span> <span data-ttu-id="31147-123">在此範例中，每個運算式會從迴圈中的目前記錄傳回單一屬性，而這些值是轉譯成文字的基本類型。</span><span class="sxs-lookup"><span data-stu-id="31147-123">In this example, each expression returns a single property from the current record in the loop, and the values are primitive types which are rendered as text.</span></span>

## <a name="confirm-courses-are-added"></a><span data-ttu-id="31147-124">確認課程已新增</span><span class="sxs-lookup"><span data-stu-id="31147-124">Confirm courses are added</span></span>

<span data-ttu-id="31147-125">執行方案。</span><span class="sxs-lookup"><span data-stu-id="31147-125">Run the solution.</span></span> <span data-ttu-id="31147-126">按一下 [**學生清單**]，然後選取其中一個學生的 [**詳細資料**]。</span><span class="sxs-lookup"><span data-stu-id="31147-126">Click **List of students** and select **Details** for one of the students.</span></span> <span data-ttu-id="31147-127">您會看到已註冊的課程已包含在此視圖中。</span><span class="sxs-lookup"><span data-stu-id="31147-127">You will see the enrolled courses have been included in the view.</span></span>

![註冊的學生](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a><span data-ttu-id="31147-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="31147-129">Next steps</span></span>
<span data-ttu-id="31147-130">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="31147-130">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="31147-131">將課程新增至學生詳細資料頁面</span><span class="sxs-lookup"><span data-stu-id="31147-131">Added courses to the student detail page</span></span>
> * <span data-ttu-id="31147-132">確認課程已新增至頁面</span><span class="sxs-lookup"><span data-stu-id="31147-132">Confirmed that the courses are added to the page</span></span>

<span data-ttu-id="31147-133">請前進到下一個教學課程，以瞭解如何新增資料批註來指定驗證需求和顯示格式。</span><span class="sxs-lookup"><span data-stu-id="31147-133">Advance to the next tutorial to learn how to add data annotations to specify validation requirements and display formatting.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="31147-134">增強資料驗證</span><span class="sxs-lookup"><span data-stu-id="31147-134">Enhance data validation</span></span>](enhancing-data-validation.md)
