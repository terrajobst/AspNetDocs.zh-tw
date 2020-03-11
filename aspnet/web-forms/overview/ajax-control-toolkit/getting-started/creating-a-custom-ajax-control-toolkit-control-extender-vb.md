---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: 建立自訂 AJAX 控制項工具組控制項擴充項（VB） |Microsoft Docs
author: microsoft
description: 自訂延伸可讓您自訂和擴充 ASP.NET 控制項的功能，而不需要建立新的類別。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 0849fa6c13679e0cd01bb20a4067a097acbce298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578159"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a><span data-ttu-id="4911a-103">建立自訂的 AJAX Control Toolkit 控制項擴充項 (VB)</span><span class="sxs-lookup"><span data-stu-id="4911a-103">Creating a Custom AJAX Control Toolkit Control Extender (VB)</span></span>

<span data-ttu-id="4911a-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4911a-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="4911a-105">自訂延伸可讓您自訂和擴充 ASP.NET 控制項的功能，而不需要建立新的類別。</span><span class="sxs-lookup"><span data-stu-id="4911a-105">Custom Extenders enable you to customize and extend the capabilities of ASP.NET controls without having to create new classes.</span></span>

<span data-ttu-id="4911a-106">在本教學課程中，您將瞭解如何建立自訂的 AJAX 控制項工具組控制項擴充項。</span><span class="sxs-lookup"><span data-stu-id="4911a-106">In this tutorial, you learn how to create a custom AJAX Control Toolkit control extender.</span></span> <span data-ttu-id="4911a-107">我們建立了一個簡單但實用的新擴充項，當您在 TextBox 中輸入文字時，會將按鈕的狀態從停用變更為啟用。</span><span class="sxs-lookup"><span data-stu-id="4911a-107">We create a simple, but useful, new extender that changes the state of a Button from disabled to enabled when you type text into a TextBox.</span></span> <span data-ttu-id="4911a-108">閱讀本教學課程之後，您將能夠使用自己的控制項擴充項來延伸 ASP.NET AJAX 工具組。</span><span class="sxs-lookup"><span data-stu-id="4911a-108">After reading this tutorial, you will be able to extend the ASP.NET AJAX Toolkit with your own control extenders.</span></span>

<span data-ttu-id="4911a-109">您可以使用 Visual Studio 或 Visual Web Developer 來建立自訂控制項擴充項（請確定您擁有最新版本的 Visual Web Developer）。</span><span class="sxs-lookup"><span data-stu-id="4911a-109">You can create custom control extenders using either Visual Studio or Visual Web Developer (make sure that you have the latest version of Visual Web Developer).</span></span>

## <a name="overview-of-the-disabledbutton-extender"></a><span data-ttu-id="4911a-110">DisabledButton 擴充項的總覽</span><span class="sxs-lookup"><span data-stu-id="4911a-110">Overview of the DisabledButton Extender</span></span>

<span data-ttu-id="4911a-111">我們的新控制項擴充項名為 DisabledButton 擴充項。</span><span class="sxs-lookup"><span data-stu-id="4911a-111">Our new control extender is named the DisabledButton extender.</span></span> <span data-ttu-id="4911a-112">這個擴充項會有三個屬性：</span><span class="sxs-lookup"><span data-stu-id="4911a-112">This extender will have three properties:</span></span>

- <span data-ttu-id="4911a-113">TargetControlID-控制項擴充的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="4911a-113">TargetControlID - The TextBox that the control extends.</span></span>
- <span data-ttu-id="4911a-114">TargetButtonIID-已停用或啟用的按鈕。</span><span class="sxs-lookup"><span data-stu-id="4911a-114">TargetButtonIID - The Button that is disabled or enabled.</span></span>
- <span data-ttu-id="4911a-115">DisabledText-一開始顯示在按鈕中的文字。</span><span class="sxs-lookup"><span data-stu-id="4911a-115">DisabledText - The text that is initially displayed in the Button.</span></span> <span data-ttu-id="4911a-116">當您開始輸入時，按鈕會顯示 [按鈕文字] 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="4911a-116">When you start typing, the Button displays the value of the Button Text property.</span></span>

<span data-ttu-id="4911a-117">您會將 DisabledButton 擴充項與 TextBox 和 Button 控制項連結。</span><span class="sxs-lookup"><span data-stu-id="4911a-117">You hook the DisabledButton extender to a TextBox and Button control.</span></span> <span data-ttu-id="4911a-118">在您輸入任何文字之前，按鈕會停用，而且 TextBox 和按鈕看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="4911a-118">Before you type any text, the Button is disabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

<span data-ttu-id="4911a-119">（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="4911a-119">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))</span></span>

<span data-ttu-id="4911a-120">當您開始輸入文字之後，按鈕就會啟用，而且 TextBox 和按鈕看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="4911a-120">After you start typing text, the Button is enabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

<span data-ttu-id="4911a-121">（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="4911a-121">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))</span></span>

<span data-ttu-id="4911a-122">若要建立控制項擴充項，我們需要建立下列三個檔案：</span><span class="sxs-lookup"><span data-stu-id="4911a-122">To create our control extender, we need to create the following three files:</span></span>

- <span data-ttu-id="4911a-123">DisabledButtonExtender：此檔案是伺服器端控制項類別，會管理建立擴充項，並可讓您在設計階段設定屬性。</span><span class="sxs-lookup"><span data-stu-id="4911a-123">DisabledButtonExtender.vb - This file is the server-side control class that will manage creating your extender and allow you to set the properties at design-time.</span></span> <span data-ttu-id="4911a-124">它也會定義可在您的擴充項上設定的屬性。</span><span class="sxs-lookup"><span data-stu-id="4911a-124">It also defines the properties that can be set on your extender.</span></span> <span data-ttu-id="4911a-125">這些屬性可以透過程式碼和在設計階段存取，並符合 DisableButtonBehavior 中定義的屬性。</span><span class="sxs-lookup"><span data-stu-id="4911a-125">These properties are accessible via code and at design time and match properties defined in the DisableButtonBehavior.js file.</span></span>
- <span data-ttu-id="4911a-126">DisabledButtonBehavior--此檔案是您將新增所有用戶端腳本邏輯的位置。</span><span class="sxs-lookup"><span data-stu-id="4911a-126">DisabledButtonBehavior.js -- This file is where you will add all of your client script logic.</span></span>
- <span data-ttu-id="4911a-127">DisabledButtonDesigner .vb-這個類別會啟用設計階段功能。</span><span class="sxs-lookup"><span data-stu-id="4911a-127">DisabledButtonDesigner.vb - This class enables design-time functionality.</span></span> <span data-ttu-id="4911a-128">如果您想要讓控制項擴充項與 Visual Studio/Visual Web Developer Designer 正常搭配運作，您需要此類別。</span><span class="sxs-lookup"><span data-stu-id="4911a-128">You need this class if you want the control extender to work correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="4911a-129">因此，控制項擴充項包含伺服器端控制項、用戶端行為和伺服器端設計工具類別。</span><span class="sxs-lookup"><span data-stu-id="4911a-129">So a control extender consists of a server-side control, a client-side behavior, and a server-side designer class.</span></span> <span data-ttu-id="4911a-130">在下列各節中，您將瞭解如何建立這三個檔案。</span><span class="sxs-lookup"><span data-stu-id="4911a-130">You learn how to create all three of these files in the following sections.</span></span>

## <a name="creating-the-custom-extender-website-and-project"></a><span data-ttu-id="4911a-131">建立自訂擴充項網站和專案</span><span class="sxs-lookup"><span data-stu-id="4911a-131">Creating the Custom Extender Website and Project</span></span>

<span data-ttu-id="4911a-132">第一個步驟是在 Visual Studio/Visual Web Developer 中建立類別庫專案和網站。</span><span class="sxs-lookup"><span data-stu-id="4911a-132">The first step is to create a class library project and website in Visual Studio/Visual Web Developer.</span></span> <span data-ttu-id="4911a-133">我們會在類別庫專案中建立自訂擴充項，並在網站中測試自訂擴充項。</span><span class="sxs-lookup"><span data-stu-id="4911a-133">We�ll create the custom extender in the class library project and test the custom extender in the website.</span></span>

<span data-ttu-id="4911a-134">讓我們從網站開始。</span><span class="sxs-lookup"><span data-stu-id="4911a-134">Let�s start with the website.</span></span> <span data-ttu-id="4911a-135">請遵循下列步驟來建立網站：</span><span class="sxs-lookup"><span data-stu-id="4911a-135">Follow these steps to create the website:</span></span>

1. <span data-ttu-id="4911a-136">選取功能表選項 [檔案] **、[新增網站**]。</span><span class="sxs-lookup"><span data-stu-id="4911a-136">Select the menu option **File, New Web Site**.</span></span>
2. <span data-ttu-id="4911a-137">選取 [ **ASP.NET 網站**] 範本。</span><span class="sxs-lookup"><span data-stu-id="4911a-137">Select the **ASP.NET Web Site** template.</span></span>
3. <span data-ttu-id="4911a-138">將新網站命名為*Website1*。</span><span class="sxs-lookup"><span data-stu-id="4911a-138">Name the new website *Website1*.</span></span>
4. <span data-ttu-id="4911a-139">按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4911a-139">Click the **OK** button.</span></span>

<span data-ttu-id="4911a-140">接下來，我們必須建立類別庫專案，其中將包含控制項擴充項的程式碼：</span><span class="sxs-lookup"><span data-stu-id="4911a-140">Next, we need to create the class library project that will contain the code for the control extender:</span></span>

1. <span data-ttu-id="4911a-141">選取功能表選項 [檔案] **、[加入]、[新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="4911a-141">Select the menu option **File, Add, New Project**.</span></span>
2. <span data-ttu-id="4911a-142">選取 [**類別庫**] 範本。</span><span class="sxs-lookup"><span data-stu-id="4911a-142">Select the **Class Library** template.</span></span>
3. <span data-ttu-id="4911a-143">以名稱**CustomExtenders**命名新的類別庫。</span><span class="sxs-lookup"><span data-stu-id="4911a-143">Name the new class library with the name **CustomExtenders**.</span></span>
4. <span data-ttu-id="4911a-144">按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4911a-144">Click the **OK** button.</span></span>

<span data-ttu-id="4911a-145">完成這些步驟之後，您的方案總管視窗看起來應該像 [圖 1] 所示。</span><span class="sxs-lookup"><span data-stu-id="4911a-145">After you complete these steps, your Solution Explorer window should look like Figure 1.</span></span>

<span data-ttu-id="4911a-146">[使用網站和類別庫專案 ![解決方案](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="4911a-146">[![Solution with website and class library project](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="4911a-147">**圖 01**：使用網站和類別庫專案的解決方案（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png)）</span><span class="sxs-lookup"><span data-stu-id="4911a-147">**Figure 01**: Solution with website and class library project([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))</span></span>

<span data-ttu-id="4911a-148">接下來，您必須將所有必要的元件參考加入至類別庫專案：</span><span class="sxs-lookup"><span data-stu-id="4911a-148">Next, you need to add all of the necessary assembly references to the class library project:</span></span>

1. <span data-ttu-id="4911a-149">以滑鼠右鍵按一下 CustomExtenders 專案，然後選取 [**新增參考**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="4911a-149">Right-click the CustomExtenders project and select the menu option **Add Reference**.</span></span>
2. <span data-ttu-id="4911a-150">選取 [.NET] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4911a-150">Select the .NET tab.</span></span>
3. <span data-ttu-id="4911a-151">加入下列組件的參考：</span><span class="sxs-lookup"><span data-stu-id="4911a-151">Add references to the following assemblies:</span></span>

    1. <span data-ttu-id="4911a-152">System.Web.dll</span><span class="sxs-lookup"><span data-stu-id="4911a-152">System.Web.dll</span></span>
    2. <span data-ttu-id="4911a-153">System.Web.Extensions.dll</span><span class="sxs-lookup"><span data-stu-id="4911a-153">System.Web.Extensions.dll</span></span>
    3. <span data-ttu-id="4911a-154">System.Design.dll</span><span class="sxs-lookup"><span data-stu-id="4911a-154">System.Design.dll</span></span>
    4. <span data-ttu-id="4911a-155">System.web. 副檔名 .dll</span><span class="sxs-lookup"><span data-stu-id="4911a-155">System.Web.Extensions.Design.dll</span></span>
4. <span data-ttu-id="4911a-156">選取 [流覽] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4911a-156">Select the Browse tab.</span></span>
5. <span data-ttu-id="4911a-157">加入 AjaxControlToolkit 元件的參考。</span><span class="sxs-lookup"><span data-stu-id="4911a-157">Add a reference to the AjaxControlToolkit.dll assembly.</span></span> <span data-ttu-id="4911a-158">這個元件位於您下載 AJAX 控制項工具組的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="4911a-158">This assembly is located in the folder where you downloaded the AJAX Control Toolkit.</span></span>

<span data-ttu-id="4911a-159">您可以用滑鼠右鍵按一下您的專案，選取 [屬性]，然後按一下 [參考] 索引標籤，來確認您已加入所有正確的參考（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="4911a-159">You can verify that you have added all of the right references by right-clicking your project, selecting Properties, and clicking the References tab (see Figure 2).</span></span>

<span data-ttu-id="4911a-160">[具有必要參考的 ![參考資料夾](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="4911a-160">[![References folder with required references](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)</span></span>

<span data-ttu-id="4911a-161">**圖 02**：具有必要參考的參考資料夾（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="4911a-161">**Figure 02**: References folder with required references([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png))</span></span>

## <a name="creating-the-custom-control-extender"></a><span data-ttu-id="4911a-162">建立自訂控制項擴充項</span><span class="sxs-lookup"><span data-stu-id="4911a-162">Creating the Custom Control Extender</span></span>

<span data-ttu-id="4911a-163">既然我們已經有了類別庫，我們就可以開始建立擴充性控制項。</span><span class="sxs-lookup"><span data-stu-id="4911a-163">Now that we have our class library, we can start building our extender control.</span></span> <span data-ttu-id="4911a-164">讓我們從自訂擴充項控制項類別的簡略骨骼開始（請參閱 [清單 1]）。</span><span class="sxs-lookup"><span data-stu-id="4911a-164">Let�s start with the bare bones of a custom extender control class (see Listing 1).</span></span>

<span data-ttu-id="4911a-165">**清單 1-MyCustomExtender .vb**</span><span class="sxs-lookup"><span data-stu-id="4911a-165">**Listing 1 - MyCustomExtender.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

<span data-ttu-id="4911a-166">在 [清單 1] 中，您會注意到控制項擴充項類別的幾件事。</span><span class="sxs-lookup"><span data-stu-id="4911a-166">There are several things that you notice about the control extender class in Listing 1.</span></span> <span data-ttu-id="4911a-167">首先，請注意類別是繼承自基底 ExtenderControlBase 類別。</span><span class="sxs-lookup"><span data-stu-id="4911a-167">First, notice that the class inherits from the base ExtenderControlBase class.</span></span> <span data-ttu-id="4911a-168">所有的 AJAX 控制項工具組擴充項控制項都是衍生自這個基類。</span><span class="sxs-lookup"><span data-stu-id="4911a-168">All AJAX Control Toolkit extender controls derive from this base class.</span></span> <span data-ttu-id="4911a-169">例如，基類包含 TargetID 屬性，這是每個控制項擴充項的必要屬性。</span><span class="sxs-lookup"><span data-stu-id="4911a-169">For example, the base class includes the TargetID property that is a required property of every control extender.</span></span>

<span data-ttu-id="4911a-170">接下來，請注意類別包含下列兩個與用戶端腳本相關的屬性：</span><span class="sxs-lookup"><span data-stu-id="4911a-170">Next, notice that the class includes the following two attributes related to client script:</span></span>

- <span data-ttu-id="4911a-171">WebResource-導致檔案以內嵌資源的形式包含在元件中。</span><span class="sxs-lookup"><span data-stu-id="4911a-171">WebResource - Causes a file to be included as an embedded resource in an assembly.</span></span>
- <span data-ttu-id="4911a-172">ClientScriptResource-導致從元件抓取腳本資源。</span><span class="sxs-lookup"><span data-stu-id="4911a-172">ClientScriptResource - Causes a script resource to be retrieved from an assembly.</span></span>

<span data-ttu-id="4911a-173">WebResource 屬性是用來在編譯自訂擴充項時，將 MyControlBehavior JavaScript 檔案內嵌至元件中。</span><span class="sxs-lookup"><span data-stu-id="4911a-173">The WebResource attribute is used to embed the MyControlBehavior.js JavaScript file into the assembly when the custom extender is compiled.</span></span> <span data-ttu-id="4911a-174">ClientScriptResource 屬性是用來在網頁中使用自訂擴充項時，從元件中取出 MyControlBehavior 腳本。</span><span class="sxs-lookup"><span data-stu-id="4911a-174">The ClientScriptResource attribute is used to retrieve the MyControlBehavior.js script from the assembly when the custom extender is used in a web page.</span></span>

<span data-ttu-id="4911a-175">為了讓 WebResource 和 ClientScriptResource 屬性能夠正常執行，您必須將 JavaScript 檔案編譯為內嵌資源。</span><span class="sxs-lookup"><span data-stu-id="4911a-175">In order for the WebResource and ClientScriptResource attributes to work, you must compile the JavaScript file as an embedded resource.</span></span> <span data-ttu-id="4911a-176">在 [方案總管] 視窗中選取檔案，開啟屬性工作表，並將 [*內嵌的資源*] 值指派給 [**組建動作**] 屬性。</span><span class="sxs-lookup"><span data-stu-id="4911a-176">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property.</span></span>

<span data-ttu-id="4911a-177">請注意，控制項擴充項也包含 TargetControlType 屬性。</span><span class="sxs-lookup"><span data-stu-id="4911a-177">Notice that the control extender also includes a TargetControlType attribute.</span></span> <span data-ttu-id="4911a-178">這個屬性是用來指定控制項擴充項所延伸的控制項類型。</span><span class="sxs-lookup"><span data-stu-id="4911a-178">This attribute is used to specify the type of control that is extended by the control extender.</span></span> <span data-ttu-id="4911a-179">在 [清單 1] 的案例中，控制項擴充項是用來延伸文字方塊。</span><span class="sxs-lookup"><span data-stu-id="4911a-179">In the case of Listing 1, the control extender is used to extend a TextBox.</span></span>

<span data-ttu-id="4911a-180">最後，請注意，自訂擴充項包含名為 MyProperty 的屬性。</span><span class="sxs-lookup"><span data-stu-id="4911a-180">Finally, notice that the custom extender includes a property named MyProperty.</span></span> <span data-ttu-id="4911a-181">屬性會以 ExtenderControlProperty 屬性標記。</span><span class="sxs-lookup"><span data-stu-id="4911a-181">The property is marked with the ExtenderControlProperty attribute.</span></span> <span data-ttu-id="4911a-182">GetPropertyValue （）和 SetPropertyValue （）方法是用來將伺服器端控制擴充項的屬性值傳遞至用戶端行為。</span><span class="sxs-lookup"><span data-stu-id="4911a-182">The GetPropertyValue() and SetPropertyValue() methods are used to pass the property value from the server-side control extender to the client-side behavior.</span></span>

<span data-ttu-id="4911a-183">讓我們繼續執行 DisabledButton 擴充項的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4911a-183">Let�s go ahead and implement the code for our DisabledButton extender.</span></span> <span data-ttu-id="4911a-184">此擴充項的程式碼可在 [清單 2] 中找到。</span><span class="sxs-lookup"><span data-stu-id="4911a-184">The code for this extender can be found in Listing 2.</span></span>

<span data-ttu-id="4911a-185">**清單 2-DisabledButtonExtender .vb**</span><span class="sxs-lookup"><span data-stu-id="4911a-185">**Listing 2 - DisabledButtonExtender.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

<span data-ttu-id="4911a-186">[清單 2] 中的 DisabledButton 擴充項有兩個名為 TargetButtonID 和 DisabledText 的屬性。</span><span class="sxs-lookup"><span data-stu-id="4911a-186">The DisabledButton extender in Listing 2 has two properties named TargetButtonID and DisabledText.</span></span> <span data-ttu-id="4911a-187">套用至 TargetButtonID 屬性的 IDReferenceProperty 可防止您將 Button 控制項識別碼以外的任何專案指派給這個屬性。</span><span class="sxs-lookup"><span data-stu-id="4911a-187">The IDReferenceProperty applied to the TargetButtonID property prevents you from assigning anything other than the ID of a Button control to this property.</span></span>

<span data-ttu-id="4911a-188">WebResource 和 ClientScriptResource 屬性會將位於名為 DisabledButtonBehavior 之檔案中的用戶端行為與此擴充項產生關聯。</span><span class="sxs-lookup"><span data-stu-id="4911a-188">The WebResource and ClientScriptResource attributes associate a client-side behavior located in a file named DisabledButtonBehavior.js with this extender.</span></span> <span data-ttu-id="4911a-189">我們將在下一節討論此 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="4911a-189">We discuss this JavaScript file in the next section.</span></span>

## <a name="creating-the-custom-extender-behavior"></a><span data-ttu-id="4911a-190">建立自訂擴充項行為</span><span class="sxs-lookup"><span data-stu-id="4911a-190">Creating the Custom Extender Behavior</span></span>

<span data-ttu-id="4911a-191">控制項擴充項的用戶端元件稱為「行為」（behavior）。</span><span class="sxs-lookup"><span data-stu-id="4911a-191">The client-side component of a control extender is called a behavior.</span></span> <span data-ttu-id="4911a-192">停用和啟用按鈕的實際邏輯包含在 DisabledButton 行為中。</span><span class="sxs-lookup"><span data-stu-id="4911a-192">The actual logic for disabling and enabling the Button is contained in the DisabledButton behavior.</span></span> <span data-ttu-id="4911a-193">行為的 JavaScript 程式碼包含在 [清單 3] 中。</span><span class="sxs-lookup"><span data-stu-id="4911a-193">The JavaScript code for the behavior is included in Listing 3.</span></span>

<span data-ttu-id="4911a-194">**清單 3-DisabledButton .js**</span><span class="sxs-lookup"><span data-stu-id="4911a-194">**Listing 3 - DisabledButton.js**</span></span>

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

<span data-ttu-id="4911a-195">[清單 3] 中的 JavaScript 檔案包含名為 DisabledButtonBehavior 的用戶端類別。</span><span class="sxs-lookup"><span data-stu-id="4911a-195">The JavaScript file in Listing 3 contains a client-side class named DisabledButtonBehavior.</span></span> <span data-ttu-id="4911a-196">這個類別（如其伺服器端對應項）包含兩個名為 TargetButtonID 和 DisabledText 的屬性，您可以使用 get\_TargetButtonID/set\_TargetButtonID，並取得\_DisabledText/set\_DisabledText 來進行存取。</span><span class="sxs-lookup"><span data-stu-id="4911a-196">This class, like its server-side twin, includes two properties named TargetButtonID and DisabledText which you can access using get\_TargetButtonID/set\_TargetButtonID and get\_DisabledText/set\_DisabledText.</span></span>

<span data-ttu-id="4911a-197">Initialize （）方法會將 keyup 事件處理常式與行為的目標元素產生關聯。</span><span class="sxs-lookup"><span data-stu-id="4911a-197">The initialize() method associates a keyup event handler with the target element for the behavior.</span></span> <span data-ttu-id="4911a-198">每次您在與此行為相關聯的文字方塊中輸入字母時，就會執行 keyup 處理常式。</span><span class="sxs-lookup"><span data-stu-id="4911a-198">Each time you type a letter into the TextBox associated with this behavior, the keyup handler executes.</span></span> <span data-ttu-id="4911a-199">Keyup 處理常式會根據與行為關聯的 TextBox 是否包含任何文字，來啟用或停用按鈕。</span><span class="sxs-lookup"><span data-stu-id="4911a-199">The keyup handler either enables or disables the Button depending on whether the TextBox associated with the behavior contains any text.</span></span>

<span data-ttu-id="4911a-200">請記住，您必須將清單3中的 JavaScript 檔案編譯為內嵌資源。</span><span class="sxs-lookup"><span data-stu-id="4911a-200">Remember that you must compile the JavaScript file in Listing 3 as an embedded resource.</span></span> <span data-ttu-id="4911a-201">在 [方案總管] 視窗中選取檔案，開啟屬性工作表，並將 [*內嵌的資源*] 值指派給 [**組建動作**] 屬性（請參閱 [圖 3]）。</span><span class="sxs-lookup"><span data-stu-id="4911a-201">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property (see Figure 3).</span></span> <span data-ttu-id="4911a-202">Visual Studio 和 Visual Web Developer 都提供此選項。</span><span class="sxs-lookup"><span data-stu-id="4911a-202">This option is available in both Visual Studio and Visual Web Developer.</span></span>

<span data-ttu-id="4911a-203">[![新增 JavaScript 檔案做為內嵌資源](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="4911a-203">[![Adding a JavaScript file as an embedded resource](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)</span></span>

<span data-ttu-id="4911a-204">**圖 03**：將 JavaScript 檔案新增為內嵌資源（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png)）</span><span class="sxs-lookup"><span data-stu-id="4911a-204">**Figure 03**: Adding a JavaScript file as an embedded resource([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))</span></span>

## <a name="creating-the-custom-extender-designer"></a><span data-ttu-id="4911a-205">建立自訂的擴充項設計工具</span><span class="sxs-lookup"><span data-stu-id="4911a-205">Creating the Custom Extender Designer</span></span>

<span data-ttu-id="4911a-206">有一個我們需要建立的最後一個類別，才能完成我們的擴充項。</span><span class="sxs-lookup"><span data-stu-id="4911a-206">There is one last class that we need to create to complete our extender.</span></span> <span data-ttu-id="4911a-207">我們需要在 [清單 4] 中建立設計工具類別。</span><span class="sxs-lookup"><span data-stu-id="4911a-207">We need to create the designer class in Listing 4.</span></span> <span data-ttu-id="4911a-208">必須要有這個類別，才能讓擴充項與 Visual Studio/Visual Web Developer Designer 正確地運作。</span><span class="sxs-lookup"><span data-stu-id="4911a-208">This class is required to make the extender behave correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="4911a-209">**清單 4-DisabledButtonDesigner .vb**</span><span class="sxs-lookup"><span data-stu-id="4911a-209">**Listing 4 - DisabledButtonDesigner.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

<span data-ttu-id="4911a-210">您可以使用設計工具屬性，將 [清單 4] 中的設計工具與 DisabledButton 擴充項產生關聯。您需要將設計工具屬性套用至 DisabledButtonExtender 類別，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4911a-210">You associate the designer in Listing 4 with the DisabledButton extender with the Designer attribute.You need to apply the Designer attribute to the DisabledButtonExtender class like this:</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a><span data-ttu-id="4911a-211">使用自訂擴充項</span><span class="sxs-lookup"><span data-stu-id="4911a-211">Using the Custom Extender</span></span>

<span data-ttu-id="4911a-212">既然我們已完成建立 DisabledButton 控制項擴充項，現在可以在我們的 ASP.NET 網站中使用它。</span><span class="sxs-lookup"><span data-stu-id="4911a-212">Now that we have finished creating the DisabledButton control extender, it is time to use it in our ASP.NET website.</span></span> <span data-ttu-id="4911a-213">首先，我們需要將自訂擴充項加入 [工具箱] 中。</span><span class="sxs-lookup"><span data-stu-id="4911a-213">First, we need to add the custom extender to the toolbox.</span></span> <span data-ttu-id="4911a-214">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4911a-214">Follow these steps:</span></span>

1. <span data-ttu-id="4911a-215">按兩下 [方案總管] 視窗中的頁面，即可開啟 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="4911a-215">Open an ASP.NET page by double-clicking the page in the Solution Explorer window.</span></span>
2. <span data-ttu-id="4911a-216">以滑鼠右鍵按一下 [工具箱]，然後選取功能表選項 **[選擇專案**]。</span><span class="sxs-lookup"><span data-stu-id="4911a-216">Right-click the toolbox and select the menu option **Choose Items**.</span></span>
3. <span data-ttu-id="4911a-217">在 [選擇工具箱專案] 對話方塊中，流覽至 [CustomExtenders] 元件。</span><span class="sxs-lookup"><span data-stu-id="4911a-217">In the Choose Toolbox Items dialog, browse to the CustomExtenders.dll assembly.</span></span>
4. <span data-ttu-id="4911a-218">按一下 [**確定**] 按鈕以關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4911a-218">Click the **OK** button to close the dialog.</span></span>

<span data-ttu-id="4911a-219">完成這些步驟之後，[DisabledButton] 控制項擴充項應該會出現在 [工具箱] 中（請參閱 [圖 4]）。</span><span class="sxs-lookup"><span data-stu-id="4911a-219">After you complete these steps, the DisabledButton control extender should appear in the toolbox (see Figure 4).</span></span>

<span data-ttu-id="4911a-220">[在 [工具箱] 中 ![DisabledButton](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="4911a-220">[![DisabledButton in the toolbox](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)</span></span>

<span data-ttu-id="4911a-221">**圖 04**： [工具箱] 中的 DisabledButton （[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png)）</span><span class="sxs-lookup"><span data-stu-id="4911a-221">**Figure 04**: DisabledButton in the toolbox([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png))</span></span>

<span data-ttu-id="4911a-222">接下來，我們需要建立新的 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="4911a-222">Next, we need to create a new ASP.NET page.</span></span> <span data-ttu-id="4911a-223">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4911a-223">Follow these steps:</span></span>

1. <span data-ttu-id="4911a-224">建立名為 ShowDisabledButton 的新 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="4911a-224">Create a new ASP.NET page named ShowDisabledButton.aspx.</span></span>
2. <span data-ttu-id="4911a-225">將 ScriptManager 拖曳至頁面上。</span><span class="sxs-lookup"><span data-stu-id="4911a-225">Drag a ScriptManager onto the page.</span></span>
3. <span data-ttu-id="4911a-226">將 TextBox 控制項拖曳至頁面上。</span><span class="sxs-lookup"><span data-stu-id="4911a-226">Drag a TextBox control onto the page.</span></span>
4. <span data-ttu-id="4911a-227">將 [按鈕] 控制項拖曳至頁面上。</span><span class="sxs-lookup"><span data-stu-id="4911a-227">Drag a Button control onto the page.</span></span>
5. <span data-ttu-id="4911a-228">在屬性視窗中，將 [按鈕識別碼] 屬性變更為 [值<em>btnSave</em> ]，並將 [Text] 屬性變更為 [*儲存\** ] 值。</span><span class="sxs-lookup"><span data-stu-id="4911a-228">In the Properties window, change the Button ID property to the value <em>btnSave</em> and the Text property to the value *Save\**.</span></span>

<span data-ttu-id="4911a-229">我們建立了具有標準 ASP.NET TextBox 和 Button 控制項的頁面。</span><span class="sxs-lookup"><span data-stu-id="4911a-229">We created a page with a standard ASP.NET TextBox and Button control.</span></span>

<span data-ttu-id="4911a-230">接下來，我們需要使用 DisabledButton 擴充項來延伸 TextBox 控制項：</span><span class="sxs-lookup"><span data-stu-id="4911a-230">Next, we need to extend the TextBox control with the DisabledButton extender:</span></span>

1. <span data-ttu-id="4911a-231">選取 [**加入**擴充項工作] 選項，以開啟 [擴充性檢查程式] 對話方塊（請參閱 [圖 5]）。</span><span class="sxs-lookup"><span data-stu-id="4911a-231">Select the **Add Extender** task option to open the Extender Wizard dialog (see Figure 5).</span></span> <span data-ttu-id="4911a-232">請注意，此對話方塊包含我們的自訂 DisabledButton 擴充項。</span><span class="sxs-lookup"><span data-stu-id="4911a-232">Notice that the dialog includes our custom DisabledButton extender.</span></span>
2. <span data-ttu-id="4911a-233">選取 DisabledButton 擴充項，然後按一下 [**確定]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4911a-233">Select the DisabledButton extender and click the **OK** button.</span></span>

<span data-ttu-id="4911a-234">[![[擴充項嚮導] 對話方塊](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="4911a-234">[![The Extender Wizard dialog](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)</span></span>

<span data-ttu-id="4911a-235">**圖 05**： [擴充項嚮導] 對話方塊（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png)）</span><span class="sxs-lookup"><span data-stu-id="4911a-235">**Figure 05**: The Extender Wizard dialog([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))</span></span>

<span data-ttu-id="4911a-236">最後，我們可以設定 DisabledButton 擴充項的屬性。</span><span class="sxs-lookup"><span data-stu-id="4911a-236">Finally, we can set the properties of the DisabledButton extender.</span></span> <span data-ttu-id="4911a-237">藉由修改 TextBox 控制項的屬性，您可以修改 DisabledButton 擴充項的屬性：</span><span class="sxs-lookup"><span data-stu-id="4911a-237">You can modify the properties of the DisabledButton extender by modifying the properties of the TextBox control:</span></span>

1. <span data-ttu-id="4911a-238">在設計工具中選取文字方塊。</span><span class="sxs-lookup"><span data-stu-id="4911a-238">Select the TextBox in the Designer.</span></span>
2. <span data-ttu-id="4911a-239">在 屬性視窗中，展開 擴充項 節點（請參閱 圖 6）。</span><span class="sxs-lookup"><span data-stu-id="4911a-239">In the Properties window, expand the Extenders node (see Figure 6).</span></span>
3. <span data-ttu-id="4911a-240">將*儲存*的值指派給 DisabledText 屬性，並將*btnSave*值指定為 TargetButtonID 屬性。</span><span class="sxs-lookup"><span data-stu-id="4911a-240">Assign the value *Save* to the DisabledText property and the value *btnSave* to the TargetButtonID property.</span></span>

<span data-ttu-id="4911a-241">[![設定擴充項屬性](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="4911a-241">[![Setting extender properties](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)</span></span>

<span data-ttu-id="4911a-242">**圖 06**：設定擴充項屬性（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png)）</span><span class="sxs-lookup"><span data-stu-id="4911a-242">**Figure 06**: Setting extender properties([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))</span></span>

<span data-ttu-id="4911a-243">當您執行頁面（藉由按 F5）時，按鈕控制項一開始就會停用。</span><span class="sxs-lookup"><span data-stu-id="4911a-243">When you run the page (by hitting F5), the Button control is initially disabled.</span></span> <span data-ttu-id="4911a-244">一旦您開始在文字方塊中輸入文字，就會啟用按鈕控制項（請參閱 [圖 7]）。</span><span class="sxs-lookup"><span data-stu-id="4911a-244">As soon as you start entering text into the TextBox, the Button control is enabled (see Figure 7).</span></span>

<span data-ttu-id="4911a-245">[![DisabledButton 擴充項的作用中](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="4911a-245">[![The DisabledButton extender in action](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)</span></span>

<span data-ttu-id="4911a-246">**圖 07**：作用中的 DisabledButton 擴充項（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png)）</span><span class="sxs-lookup"><span data-stu-id="4911a-246">**Figure 07**: The DisabledButton extender in action([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))</span></span>

## <a name="summary"></a><span data-ttu-id="4911a-247">總結</span><span class="sxs-lookup"><span data-stu-id="4911a-247">Summary</span></span>

<span data-ttu-id="4911a-248">本教學課程的目的是要說明如何使用自訂的擴充項控制項來延伸 AJAX 控制項工具組。</span><span class="sxs-lookup"><span data-stu-id="4911a-248">The goal of this tutorial was to explain how you can extend the AJAX Control Toolkit with custom extender controls.</span></span> <span data-ttu-id="4911a-249">在本教學課程中，我們建立了一個簡單的 DisabledButton 控制項擴充項。</span><span class="sxs-lookup"><span data-stu-id="4911a-249">In this tutorial, we created a simple DisabledButton control extender.</span></span> <span data-ttu-id="4911a-250">我們藉由建立 DisabledButtonExtender 類別、DisabledButtonBehavior JavaScript 行為和 DisabledButtonDesigner 類別來實作為擴充項。</span><span class="sxs-lookup"><span data-stu-id="4911a-250">We implemented this extender by creating a DisabledButtonExtender class, a DisabledButtonBehavior JavaScript behavior, and a DisabledButtonDesigner class.</span></span> <span data-ttu-id="4911a-251">當您建立自訂控制項擴充項時，您會遵循一組類似的步驟。</span><span class="sxs-lookup"><span data-stu-id="4911a-251">You follow a similar set of steps whenever you create a custom control extender.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4911a-252">上一篇</span><span class="sxs-lookup"><span data-stu-id="4911a-252">Previous</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
