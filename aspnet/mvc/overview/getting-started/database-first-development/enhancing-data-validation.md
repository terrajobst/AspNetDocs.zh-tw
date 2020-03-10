---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 教學課程：使用 ASP.NET MVC 應用程式增強 EF Database First 的資料驗證
description: 本教學課程著重于將資料批註加入至資料模型，以指定驗證需求和顯示格式。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616274"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="d786c-103">教學課程：使用 ASP.NET MVC 應用程式增強 EF Database First 的資料驗證</span><span class="sxs-lookup"><span data-stu-id="d786c-103">Tutorial: Enhance data validation for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="d786c-104">使用 MVC、Entity Framework 和 ASP.NET 的樣板，您可以建立 web 應用程式，以提供介面給現有的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d786c-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="d786c-105">本教學課程系列會示範如何自動產生程式碼，讓使用者可以顯示、編輯、建立和刪除位於資料庫資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="d786c-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="d786c-106">產生的程式碼會對應至資料庫資料表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="d786c-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="d786c-107">本教學課程著重于將資料批註加入至資料模型，以指定驗證需求和顯示格式。</span><span class="sxs-lookup"><span data-stu-id="d786c-107">This tutorial focuses on adding data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="d786c-108">已根據意見區段中的使用者意見反應來改進。</span><span class="sxs-lookup"><span data-stu-id="d786c-108">It was improved based on feedback from users in the comments section.</span></span>

<span data-ttu-id="d786c-109">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="d786c-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d786c-110">加入資料批註</span><span class="sxs-lookup"><span data-stu-id="d786c-110">Add data annotations</span></span>
> * <span data-ttu-id="d786c-111">加入中繼資料類別</span><span class="sxs-lookup"><span data-stu-id="d786c-111">Add metadata classes</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d786c-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d786c-112">Prerequisites</span></span>

* [<span data-ttu-id="d786c-113">自訂視圖</span><span class="sxs-lookup"><span data-stu-id="d786c-113">Customize a view</span></span>](customizing-a-view.md)

## <a name="add-data-annotations"></a><span data-ttu-id="d786c-114">加入資料批註</span><span class="sxs-lookup"><span data-stu-id="d786c-114">Add data annotations</span></span>

<span data-ttu-id="d786c-115">如您在先前的主題中所見，部分資料驗證規則會自動套用至使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="d786c-115">As you saw in an earlier topic, some data validation rules are automatically applied to the user input.</span></span> <span data-ttu-id="d786c-116">例如，您只能為 [年級] 屬性提供一個數位。</span><span class="sxs-lookup"><span data-stu-id="d786c-116">For example, you can only provide a number for the Grade property.</span></span> <span data-ttu-id="d786c-117">若要指定更多資料驗證規則，您可以將資料批註加入至模型類別。</span><span class="sxs-lookup"><span data-stu-id="d786c-117">To specify more data validation rules, you can add data annotations to your model class.</span></span> <span data-ttu-id="d786c-118">在您的 web 應用程式中，會針對指定的屬性套用這些批註。</span><span class="sxs-lookup"><span data-stu-id="d786c-118">These annotations are applied throughout your web application for the specified property.</span></span> <span data-ttu-id="d786c-119">您也可以套用變更屬性顯示方式的格式化屬性;例如，變更文字標籤所使用的值。</span><span class="sxs-lookup"><span data-stu-id="d786c-119">You can also apply formatting attributes that change how the properties are displayed; such as, changing the value used for text labels.</span></span>

<span data-ttu-id="d786c-120">在本教學課程中，您將加入資料批註，以限制針對 FirstName、LastName 和 MiddleName 屬性所提供的值長度。</span><span class="sxs-lookup"><span data-stu-id="d786c-120">In this tutorial, you will add data annotations to restrict the length of the values provided for the FirstName, LastName, and MiddleName properties.</span></span> <span data-ttu-id="d786c-121">在資料庫中，這些值限制為50個字元;不過，在您的 web 應用程式中，目前不會強制字元限制。</span><span class="sxs-lookup"><span data-stu-id="d786c-121">In the database, these values are limited to 50 characters; however, in your web application that character limit is currently not enforced.</span></span> <span data-ttu-id="d786c-122">如果使用者為其中一個值提供超過50個字元，當嘗試將值儲存至資料庫時，頁面將會損毀。</span><span class="sxs-lookup"><span data-stu-id="d786c-122">If a user provides more than 50 characters for one of those values, the page will crash when attempting to save the value to the database.</span></span> <span data-ttu-id="d786c-123">您也會將等級限制為0到4之間的值。</span><span class="sxs-lookup"><span data-stu-id="d786c-123">You will also restrict Grade to values between 0 and 4.</span></span>

<span data-ttu-id="d786c-124">選取 [ > **ContosoModel**的**模型**] > **ContosoModel.tt** ，然後開啟*Student.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="d786c-124">Select **Models** > **ContosoModel.edmx** > **ContosoModel.tt** and open the *Student.cs* file.</span></span> <span data-ttu-id="d786c-125">將下列反白顯示的程式碼新增至類別。</span><span class="sxs-lookup"><span data-stu-id="d786c-125">Add the following highlighted code to the class.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

<span data-ttu-id="d786c-126">開啟*Enrollment.cs* ，並新增下列反白顯示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d786c-126">Open *Enrollment.cs* and add the following highlighted code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

<span data-ttu-id="d786c-127">建置方案。</span><span class="sxs-lookup"><span data-stu-id="d786c-127">Build the solution.</span></span>

<span data-ttu-id="d786c-128">按一下 [**學生清單**]，然後選取 [**編輯**]。</span><span class="sxs-lookup"><span data-stu-id="d786c-128">Click **List of students** and select **Edit**.</span></span> <span data-ttu-id="d786c-129">如果您嘗試輸入超過50個字元，就會顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d786c-129">If you attempt to enter more than 50 characters, an error message is displayed.</span></span>

![顯示錯誤訊息](enhancing-data-validation/_static/image1.png)

<span data-ttu-id="d786c-131">回到首頁。</span><span class="sxs-lookup"><span data-stu-id="d786c-131">Go back to the home page.</span></span> <span data-ttu-id="d786c-132">按一下 [**註冊清單**]，然後選取 [**編輯**]。</span><span class="sxs-lookup"><span data-stu-id="d786c-132">Click **List of enrollments** and select **Edit**.</span></span> <span data-ttu-id="d786c-133">嘗試提供高於4的等級。</span><span class="sxs-lookup"><span data-stu-id="d786c-133">Attempt to provide a grade above 4.</span></span> <span data-ttu-id="d786c-134">您會收到此錯誤：*欄位等級必須介於0到4之間。*</span><span class="sxs-lookup"><span data-stu-id="d786c-134">You will receive this error: *The field Grade must be between 0 and 4.*</span></span>

## <a name="add-metadata-classes"></a><span data-ttu-id="d786c-135">加入中繼資料類別</span><span class="sxs-lookup"><span data-stu-id="d786c-135">Add metadata classes</span></span>

<span data-ttu-id="d786c-136">當您不希望資料庫變更時，直接將驗證屬性加入至模型類別會運作。不過，如果您的資料庫變更，而您需要重新產生模型類別，您將會遺失已套用至模型類別的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="d786c-136">Adding the validation attributes directly to the model class works when you do not expect the database to change; however, if your database changes and you need to regenerate the model class, you will lose all of the attributes you had applied to the model class.</span></span> <span data-ttu-id="d786c-137">這種方法可能非常沒有效率，而且容易遺失重要的驗證規則。</span><span class="sxs-lookup"><span data-stu-id="d786c-137">This approach can be very inefficient and prone to losing important validation rules.</span></span>

<span data-ttu-id="d786c-138">若要避免這個問題，您可以新增包含屬性的中繼資料類別。</span><span class="sxs-lookup"><span data-stu-id="d786c-138">To avoid this problem, you can add a metadata class that contains the attributes.</span></span> <span data-ttu-id="d786c-139">當您將模型類別關聯至中繼資料類別時，這些屬性會套用至模型。</span><span class="sxs-lookup"><span data-stu-id="d786c-139">When you associate the model class to the metadata class, those attributes are applied to the model.</span></span> <span data-ttu-id="d786c-140">在此方法中，您可以重新產生模型類別，而不會遺失已套用至中繼資料類別的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="d786c-140">In this approach, the model class can be regenerated without losing all of the attributes that have been applied to the metadata class.</span></span>

<span data-ttu-id="d786c-141">在 [**模型**] 資料夾中，新增名為*Metadata.cs*的類別。</span><span class="sxs-lookup"><span data-stu-id="d786c-141">In the **Models** folder, add a class named *Metadata.cs*.</span></span>

<span data-ttu-id="d786c-142">將*Metadata.cs*中的程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="d786c-142">Replace the code in *Metadata.cs* with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

<span data-ttu-id="d786c-143">這些中繼資料類別包含您先前套用至模型類別的所有驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="d786c-143">These metadata classes contain all of the validation attributes that you had previously applied to the model classes.</span></span> <span data-ttu-id="d786c-144">**顯示**屬性是用來變更文字標籤所使用的值。</span><span class="sxs-lookup"><span data-stu-id="d786c-144">The **Display** attribute is used to change the value used for text labels.</span></span>

<span data-ttu-id="d786c-145">現在，您必須將模型類別關聯至中繼資料類別。</span><span class="sxs-lookup"><span data-stu-id="d786c-145">Now, you must associate the model classes with the metadata classes.</span></span>

<span data-ttu-id="d786c-146">在 [**模型**] 資料夾中，新增名為*PartialClasses.cs*的類別。</span><span class="sxs-lookup"><span data-stu-id="d786c-146">In the **Models** folder, add a class named *PartialClasses.cs*.</span></span>

<span data-ttu-id="d786c-147">以下列程式碼取代檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="d786c-147">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

<span data-ttu-id="d786c-148">請注意，每個類別都標示為 `partial` 類別，而且每個類別都符合名稱和命名空間，做為自動產生的類別。</span><span class="sxs-lookup"><span data-stu-id="d786c-148">Notice that each class is marked as a `partial` class, and each matches the name and namespace as the class that is automatically generated.</span></span> <span data-ttu-id="d786c-149">藉由將中繼資料屬性套用至部分類別，您可以確保資料驗證屬性會套用至自動產生的類別。</span><span class="sxs-lookup"><span data-stu-id="d786c-149">By applying the metadata attribute to the partial class, you ensure that the data validation attributes will be applied to the automatically-generated class.</span></span> <span data-ttu-id="d786c-150">當您重新產生模型類別時，這些屬性將不會遺失，因為中繼資料屬性會套用到不會重新產生的部分類別中。</span><span class="sxs-lookup"><span data-stu-id="d786c-150">These attributes will not be lost when you regenerate the model classes because the metadata attribute is applied in partial classes that are not regenerated.</span></span>

<span data-ttu-id="d786c-151">若要重新產生自動產生的類別，請開啟*ContosoModel .edmx*檔案。</span><span class="sxs-lookup"><span data-stu-id="d786c-151">To regenerate the automatically-generated classes, open the *ContosoModel.edmx* file.</span></span> <span data-ttu-id="d786c-152">同樣地，以滑鼠右鍵按一下設計介面，然後選取 [**從資料庫更新模型**]。</span><span class="sxs-lookup"><span data-stu-id="d786c-152">Once again, right-click on the design surface and select **Update Model from Database**.</span></span> <span data-ttu-id="d786c-153">即使您尚未變更資料庫，此程式還是會重新產生類別。</span><span class="sxs-lookup"><span data-stu-id="d786c-153">Even though you have not changed the database, this process will regenerate the classes.</span></span> <span data-ttu-id="d786c-154">在 [**重新**整理] 索引標籤中，選取 [**資料表**] 並**完成**。</span><span class="sxs-lookup"><span data-stu-id="d786c-154">In the **Refresh** tab, select **Tables** and **Finish**.</span></span>

<span data-ttu-id="d786c-155">儲存*ContosoModel .edmx*檔案以套用變更。</span><span class="sxs-lookup"><span data-stu-id="d786c-155">Save the *ContosoModel.edmx* file to apply the changes.</span></span>

<span data-ttu-id="d786c-156">開啟*Student.cs*檔案或*Enrollment.cs*檔案，並注意您稍早套用的資料驗證屬性已不再位於檔案中。</span><span class="sxs-lookup"><span data-stu-id="d786c-156">Open the *Student.cs* file or the *Enrollment.cs* file, and notice that the data validation attributes you applied earlier are no longer in the file.</span></span> <span data-ttu-id="d786c-157">不過，請執行應用程式，並請注意，當您輸入資料時，仍然會套用驗證規則。</span><span class="sxs-lookup"><span data-stu-id="d786c-157">However, run the application, and notice that the validation rules are still applied when you enter data.</span></span>

## <a name="conclusion"></a><span data-ttu-id="d786c-158">結論</span><span class="sxs-lookup"><span data-stu-id="d786c-158">Conclusion</span></span>

<span data-ttu-id="d786c-159">此系列提供了簡單的範例，說明如何從現有的資料庫產生程式碼，讓使用者可以編輯、更新、建立和刪除資料。</span><span class="sxs-lookup"><span data-stu-id="d786c-159">This series provided a simple example of how to generate code from an existing database that enables users to edit, update, create and delete data.</span></span> <span data-ttu-id="d786c-160">它使用 ASP.NET MVC 5、Entity Framework 和 ASP.NET 樣板來建立專案。</span><span class="sxs-lookup"><span data-stu-id="d786c-160">It used ASP.NET MVC 5, Entity Framework and ASP.NET Scaffolding to create the project.</span></span> 

<span data-ttu-id="d786c-161">如需 Code First 開發的簡介範例，請參閱[使用 ASP.NET MVC 5 消費者入門](../introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="d786c-161">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> 

<span data-ttu-id="d786c-162">如需更先進的範例，請參閱[建立 ASP.NET MVC 4 應用程式的 Entity Framework 資料模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="d786c-162">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="d786c-163">請注意，您用來處理 Database First 中資料的 DbCoNtext API，與您用來處理 Code First 中資料的 API 相同。</span><span class="sxs-lookup"><span data-stu-id="d786c-163">Note that the DbContext API that you use for working with data in Database First is the same as the API you use for working with data in Code First.</span></span> <span data-ttu-id="d786c-164">即使您想要使用 Database First，您也可以瞭解如何處理更複雜的案例，例如讀取和更新相關資料、處理並行衝突，以及從 Code First 教學課程。</span><span class="sxs-lookup"><span data-stu-id="d786c-164">Even if you intend to use Database First, you can learn how to handle more complex scenarios such as reading and updating related data, handling concurrency conflicts, and so forth from a Code First tutorial.</span></span> <span data-ttu-id="d786c-165">唯一的差異在於資料庫、內容類別和實體類別的建立方式。</span><span class="sxs-lookup"><span data-stu-id="d786c-165">The only difference is in how the database, context class, and entity classes are created.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d786c-166">其他資源</span><span class="sxs-lookup"><span data-stu-id="d786c-166">Additional resources</span></span>

<span data-ttu-id="d786c-167">如需資料驗證注釋的完整清單，您可以將它套用至屬性和類別，請參閱[system.workflow.componentmodel.activity. DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d786c-167">For a full list of data validation annotations you can apply to properties and classes, see [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d786c-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d786c-168">Next steps</span></span>

<span data-ttu-id="d786c-169">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="d786c-169">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d786c-170">新增的資料批註</span><span class="sxs-lookup"><span data-stu-id="d786c-170">Added data annotations</span></span>
> * <span data-ttu-id="d786c-171">已新增中繼資料類別</span><span class="sxs-lookup"><span data-stu-id="d786c-171">Added metadata classes</span></span>

<span data-ttu-id="d786c-172">若要瞭解如何將 web 應用程式和 SQL database 部署到 Azure App Service，請參閱此教學課程：</span><span class="sxs-lookup"><span data-stu-id="d786c-172">To learn how to deploy a web app and SQL database to Azure App Service, see this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d786c-173">將 .NET 應用程式部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d786c-173">Deploy a .NET app to Azure App Service</span></span>](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)
