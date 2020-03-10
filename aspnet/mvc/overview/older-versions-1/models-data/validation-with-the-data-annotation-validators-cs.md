---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
title: 使用資料注釋驗證程式（C#）進行驗證 |Microsoft Docs
author: microsoft
description: 利用資料批註模型系結器，在 ASP.NET MVC 應用程式中執行驗證。 瞭解如何使用不同類型的驗證程式 。
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 7ca8013e-9dfc-4e33-8336-cdccfd5f9414
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
msc.type: authoredcontent
ms.openlocfilehash: e154384c08adf0c14920afff85e983a67b41707c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542130"
---
# <a name="validation-with-the-data-annotation-validators-c"></a><span data-ttu-id="4b998-104">驗證與資料註解驗證器 (C#)</span><span class="sxs-lookup"><span data-stu-id="4b998-104">Validation with the Data Annotation Validators (C#)</span></span>

<span data-ttu-id="4b998-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4b998-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="4b998-106">利用資料批註模型系結器，在 ASP.NET MVC 應用程式中執行驗證。</span><span class="sxs-lookup"><span data-stu-id="4b998-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="4b998-107">瞭解如何使用不同類型的驗證程式屬性，並在 Microsoft Entity Framework 中使用它們。</span><span class="sxs-lookup"><span data-stu-id="4b998-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>

<span data-ttu-id="4b998-108">在本教學課程中，您將瞭解如何使用資料批註驗證程式，在 ASP.NET MVC 應用程式中執行驗證。</span><span class="sxs-lookup"><span data-stu-id="4b998-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="4b998-109">使用資料批註驗證器的優點是，它們可讓您藉由將一或多個屬性（例如 Required 或 StringLength 屬性）新增至類別屬性來執行驗證。</span><span class="sxs-lookup"><span data-stu-id="4b998-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="4b998-110">在您可以使用資料批註驗證程式之前，您必須先下載資料批註模型系結器。</span><span class="sxs-lookup"><span data-stu-id="4b998-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="4b998-111">您可以按一下[這裡](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)，從 CodePlex 網站下載資料批註模型系結器範例。</span><span class="sxs-lookup"><span data-stu-id="4b998-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>

<span data-ttu-id="4b998-112">請務必瞭解資料批註模型系結器不是 Microsoft ASP.NET MVC 架構的官方部分。</span><span class="sxs-lookup"><span data-stu-id="4b998-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="4b998-113">雖然資料批註模型系結器是由 Microsoft ASP.NET MVC 小組所建立，但 Microsoft 不會針對本教學課程中所述和使用的資料批註模型系結器提供正式的產品支援。</span><span class="sxs-lookup"><span data-stu-id="4b998-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>

## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="4b998-114">使用資料注釋模型系結器</span><span class="sxs-lookup"><span data-stu-id="4b998-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="4b998-115">若要在 ASP.NET 的 MVC 應用程式中使用資料批註模型系結器，您必須先加入 DataAnnotations 的參考和 System.workflow.componentmodel.activity. DataAnnotations .dll 元件中。</span><span class="sxs-lookup"><span data-stu-id="4b998-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="4b998-116">選取功能表選項 [**專案]、[加入參考**]。</span><span class="sxs-lookup"><span data-stu-id="4b998-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="4b998-117">接著，按一下 [**流覽**] 索引標籤，並流覽至您下載（和解壓縮）資料批註模型系結器範例的位置（請參閱 [**圖 1**]）。</span><span class="sxs-lookup"><span data-stu-id="4b998-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image2.png)](validation-with-the-data-annotation-validators-cs/_static/image1.png)

<span data-ttu-id="4b998-118">**圖 1**：加入資料批註模型系結器的參考（[按一下以查看完整大小的影像](validation-with-the-data-annotation-validators-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="4b998-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-cs/_static/image3.png))</span></span>

<span data-ttu-id="4b998-119">選取 DataAnnotations 元件和 System.workflow.componentmodel.activity. DataAnnotations .dll 元件，然後按一下 **確定**按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b998-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>

<span data-ttu-id="4b998-120">您無法使用 .NET Framework Service Pack 1 隨附的 DataAnnotations 和資料批註模型系結器。</span><span class="sxs-lookup"><span data-stu-id="4b998-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="4b998-121">您必須使用包含在資料批註模型系結器範例下載中的 System.workflow.componentmodel.activity. DataAnnotations .dll 元件版本。</span><span class="sxs-lookup"><span data-stu-id="4b998-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>

<span data-ttu-id="4b998-122">最後，您必須在 global.asax 檔案中註冊 DataAnnotations 模型系結器。</span><span class="sxs-lookup"><span data-stu-id="4b998-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="4b998-123">將下列程式程式碼新增至應用程式\_Start （）事件處理常式，讓應用程式\_Start （）方法看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="4b998-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample1.cs)]

<span data-ttu-id="4b998-124">這一行程式碼會將 ataAnnotationsModelBinder 註冊為整個 ASP.NET MVC 應用程式的預設模型系結器。</span><span class="sxs-lookup"><span data-stu-id="4b998-124">This line of code registers the ataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="4b998-125">使用資料批註驗證程式屬性</span><span class="sxs-lookup"><span data-stu-id="4b998-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="4b998-126">當您使用資料批註模型系結器時，您會使用驗證程式屬性來執行驗證。</span><span class="sxs-lookup"><span data-stu-id="4b998-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="4b998-127">System.workflow.componentmodel.activity. DataAnnotations 命名空間包含下列驗證程式屬性：</span><span class="sxs-lookup"><span data-stu-id="4b998-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="4b998-128">範圍–可讓您驗證屬性的值是否落在指定的值範圍之間。</span><span class="sxs-lookup"><span data-stu-id="4b998-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="4b998-129">RegularExpression –可讓您驗證屬性的值是否符合指定的正則運算式模式。</span><span class="sxs-lookup"><span data-stu-id="4b998-129">RegularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="4b998-130">必要–可讓您將屬性標示為必要。</span><span class="sxs-lookup"><span data-stu-id="4b998-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="4b998-131">StringLength –可讓您指定字串屬性的最大長度。</span><span class="sxs-lookup"><span data-stu-id="4b998-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="4b998-132">驗證–所有驗證程式屬性的基類。</span><span class="sxs-lookup"><span data-stu-id="4b998-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="4b998-133">如果任何標準驗證程式都不符合您的驗證需求，則您一律可以選擇從基底驗證屬性繼承新的驗證程式屬性，以建立自訂的驗證程式屬性。</span><span class="sxs-lookup"><span data-stu-id="4b998-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>

<span data-ttu-id="4b998-134">[**清單 1** ] 中的 [Product] 類別說明如何使用這些驗證程式屬性。</span><span class="sxs-lookup"><span data-stu-id="4b998-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="4b998-135">[名稱]、[描述] 和 [單價] 屬性會標示為必要。</span><span class="sxs-lookup"><span data-stu-id="4b998-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="4b998-136">Name 屬性的字串長度必須小於10個字元。</span><span class="sxs-lookup"><span data-stu-id="4b998-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="4b998-137">最後，[單價] 屬性必須符合代表貨幣金額的正則運算式模式。</span><span class="sxs-lookup"><span data-stu-id="4b998-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample2.cs)]

<span data-ttu-id="4b998-138">**清單 1**： Models\Product.cs</span><span class="sxs-lookup"><span data-stu-id="4b998-138">**Listing 1**: Models\Product.cs</span></span>

<span data-ttu-id="4b998-139">Product 類別說明如何使用一個額外的屬性： DisplayName 屬性。</span><span class="sxs-lookup"><span data-stu-id="4b998-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="4b998-140">當屬性顯示在錯誤訊息中時，DisplayName 屬性可讓您修改屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="4b998-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="4b998-141">您可以顯示錯誤訊息「需要價格欄位」，而不是顯示錯誤訊息「需要單價欄位」。</span><span class="sxs-lookup"><span data-stu-id="4b998-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="4b998-142">如果您想要完全自訂驗證程式所顯示的錯誤訊息，您可以將自訂錯誤訊息指派給驗證器的 ErrorMessage 屬性，如下所示： `<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="4b998-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>

<span data-ttu-id="4b998-143">您可以使用 [**清單 1** ] 中的 [Product] 類別搭配 [**清單 2**] 中的 Create （）控制器動作。</span><span class="sxs-lookup"><span data-stu-id="4b998-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="4b998-144">當模型狀態包含任何錯誤時，此控制器動作會重新顯示 [建立] 視圖。</span><span class="sxs-lookup"><span data-stu-id="4b998-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample3.cs)]

<span data-ttu-id="4b998-145">**清單 2**： Controllers\ProductController.vb</span><span class="sxs-lookup"><span data-stu-id="4b998-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="4b998-146">最後，您可以用滑鼠右鍵按一下 [建立] （）動作，然後選取功能表選項 [**加入視圖**]，在 [**清單 3** ] 中建立此視圖。</span><span class="sxs-lookup"><span data-stu-id="4b998-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="4b998-147">建立具有 Product 類別的強型別視圖做為模型類別。</span><span class="sxs-lookup"><span data-stu-id="4b998-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="4b998-148">從 [視圖內容] 下拉式清單中選取 [**建立**] （請參閱 [**圖 2**]）。</span><span class="sxs-lookup"><span data-stu-id="4b998-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image5.png)](validation-with-the-data-annotation-validators-cs/_static/image4.png)

<span data-ttu-id="4b998-149">**圖 2**：新增 Create View</span><span class="sxs-lookup"><span data-stu-id="4b998-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-cs/samples/sample4.aspx)]

<span data-ttu-id="4b998-150">**清單 3**： Views\Product\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="4b998-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="4b998-151">從 [**加入視圖**] 功能表選項所產生的 [建立] 表單中移除 [識別碼] 欄位。</span><span class="sxs-lookup"><span data-stu-id="4b998-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="4b998-152">因為識別碼欄位對應到識別欄位，所以您不會想要允許使用者輸入此欄位的值。</span><span class="sxs-lookup"><span data-stu-id="4b998-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>

<span data-ttu-id="4b998-153">如果您提交表單以建立產品，但未在必要欄位中輸入值，則會顯示 [**圖 3** ] 中的驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="4b998-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image7.png)](validation-with-the-data-annotation-validators-cs/_static/image6.png)

<span data-ttu-id="4b998-154">**圖 3**：遺漏必要欄位</span><span class="sxs-lookup"><span data-stu-id="4b998-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="4b998-155">如果您輸入不正確貨幣金額，則會顯示 [**圖 4** ] 中的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="4b998-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image9.png)](validation-with-the-data-annotation-validators-cs/_static/image8.png)

<span data-ttu-id="4b998-156">**圖 4**：不正確貨幣金額</span><span class="sxs-lookup"><span data-stu-id="4b998-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="4b998-157">搭配 Entity Framework 使用資料批註驗證程式</span><span class="sxs-lookup"><span data-stu-id="4b998-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="4b998-158">如果您使用 Microsoft Entity Framework 來產生資料模型類別，則無法直接將驗證程式屬性套用至您的類別。</span><span class="sxs-lookup"><span data-stu-id="4b998-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="4b998-159">因為 Entity Framework Designer 會產生模型類別，所以您對模型類別所做的任何變更將會在下一次於設計工具中進行任何變更時遭到覆寫。</span><span class="sxs-lookup"><span data-stu-id="4b998-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="4b998-160">如果您想要將驗證程式與 Entity Framework 產生的類別搭配使用，則需要建立中繼資料類別。</span><span class="sxs-lookup"><span data-stu-id="4b998-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="4b998-161">您可以將驗證程式套用至中繼資料類別，而不是將驗證程式套用至實際的類別。</span><span class="sxs-lookup"><span data-stu-id="4b998-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="4b998-162">例如，假設您已使用 Entity Framework 建立電影類別（請參閱 [**圖 5**]）。</span><span class="sxs-lookup"><span data-stu-id="4b998-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="4b998-163">想像一下，您想要讓電影標題和主管屬性都需要屬性。</span><span class="sxs-lookup"><span data-stu-id="4b998-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="4b998-164">在這種情況下，您可以在 [**清單 4**] 中建立部分類別和中繼資料類別。</span><span class="sxs-lookup"><span data-stu-id="4b998-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image11.png)](validation-with-the-data-annotation-validators-cs/_static/image10.png)

<span data-ttu-id="4b998-165">**圖 5**： Entity Framework 產生的 Movie 類別</span><span class="sxs-lookup"><span data-stu-id="4b998-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample5.cs)]

<span data-ttu-id="4b998-166">**清單 4**： Models\Movie.cs</span><span class="sxs-lookup"><span data-stu-id="4b998-166">**Listing 4**: Models\Movie.cs</span></span>

<span data-ttu-id="4b998-167">[**清單 4** ] 中的檔案包含兩個名為 Movie 和 MovieMetaData 的類別。</span><span class="sxs-lookup"><span data-stu-id="4b998-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="4b998-168">Movie 類別是部分類別。</span><span class="sxs-lookup"><span data-stu-id="4b998-168">The Movie class is a partial class.</span></span> <span data-ttu-id="4b998-169">它會對應到 DataModel 所產生的部分類別，這些是由包含在 .vb 檔案中的 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="4b998-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="4b998-170">目前，.NET framework 不支援部分屬性。</span><span class="sxs-lookup"><span data-stu-id="4b998-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="4b998-171">因此，您無法將驗證程式屬性套用至 DataModel 中定義的 Movie 類別屬性，方法是將驗證程式屬性套用至**清單 4**中所定義之 movie 類別的屬性。</span><span class="sxs-lookup"><span data-stu-id="4b998-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="4b998-172">請注意，Movie 部分類別會以指向 MovieMetaData 類別的 MetadataType 屬性裝飾。</span><span class="sxs-lookup"><span data-stu-id="4b998-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="4b998-173">MovieMetaData 類別包含 Movie 類別屬性的 proxy 屬性。</span><span class="sxs-lookup"><span data-stu-id="4b998-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="4b998-174">驗證程式屬性會套用至 MovieMetaData 類別的屬性。</span><span class="sxs-lookup"><span data-stu-id="4b998-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="4b998-175">Title、Director 和 DateReleased 屬性都會標示為必要屬性。</span><span class="sxs-lookup"><span data-stu-id="4b998-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="4b998-176">必須指派包含少於5個字元的字串給 Director 屬性。</span><span class="sxs-lookup"><span data-stu-id="4b998-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="4b998-177">最後，DisplayName 屬性會套用至 DateReleased 屬性，以顯示錯誤訊息，例如「需要發行日期欄位」。</span><span class="sxs-lookup"><span data-stu-id="4b998-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="4b998-178">而不是「需要 DateReleased 欄位」錯誤。</span><span class="sxs-lookup"><span data-stu-id="4b998-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="4b998-179">請注意，MovieMetaData 類別中的 proxy 屬性不需要表示與 Movie 類別中的對應屬性相同的類型。</span><span class="sxs-lookup"><span data-stu-id="4b998-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="4b998-180">例如，Director 屬性是 Movie 類別中的字串屬性和 MovieMetaData 類別中的物件屬性。</span><span class="sxs-lookup"><span data-stu-id="4b998-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>

<span data-ttu-id="4b998-181">[**圖 6** ] 中的頁面說明當您為電影內容輸入不正確值時，所傳回的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="4b998-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image13.png)](validation-with-the-data-annotation-validators-cs/_static/image12.png)

<span data-ttu-id="4b998-182">**圖 6**：搭配 Entity Framework 使用驗證程式（[按一下以觀看完整大小的影像](validation-with-the-data-annotation-validators-cs/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="4b998-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-cs/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="4b998-183">總結</span><span class="sxs-lookup"><span data-stu-id="4b998-183">Summary</span></span>

<span data-ttu-id="4b998-184">在本教學課程中，您已瞭解如何利用資料批註模型系結器，在 ASP.NET MVC 應用程式中執行驗證。</span><span class="sxs-lookup"><span data-stu-id="4b998-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="4b998-185">您已瞭解如何使用不同類型的驗證程式屬性，例如 Required 和 StringLength 屬性。</span><span class="sxs-lookup"><span data-stu-id="4b998-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="4b998-186">您也已瞭解如何在使用 Microsoft Entity Framework 時使用這些屬性。</span><span class="sxs-lookup"><span data-stu-id="4b998-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4b998-187">[上一頁](validating-with-a-service-layer-cs.md)
> [下一頁](creating-model-classes-with-the-entity-framework-vb.md)</span><span class="sxs-lookup"><span data-stu-id="4b998-187">[Previous](validating-with-a-service-layer-cs.md)
[Next](creating-model-classes-with-the-entity-framework-vb.md)</span></span>
