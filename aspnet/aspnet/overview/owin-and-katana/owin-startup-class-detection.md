---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: OWIN 啟動類別偵測 |Microsoft Docs
author: Praburaj
description: 本教學課程說明如何設定要載入的 OWIN startup 類別。 如需 OWIN 的詳細資訊，請參閱專案 Katana 的總覽。 本教學課程是 。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: e1670c32049ec33dd4d1941a091a429d3929c452
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617044"
---
# <a name="owin-startup-class-detection"></a><span data-ttu-id="50873-105">OWIN 啟動類別偵測</span><span class="sxs-lookup"><span data-stu-id="50873-105">OWIN Startup Class Detection</span></span>

> <span data-ttu-id="50873-106">本教學課程說明如何設定要載入的 OWIN startup 類別。</span><span class="sxs-lookup"><span data-stu-id="50873-106">This tutorial shows how to configure which OWIN startup class is loaded.</span></span> <span data-ttu-id="50873-107">如需 OWIN 的詳細資訊，請參閱[專案 Katana 的總覽](an-overview-of-project-katana.md)。</span><span class="sxs-lookup"><span data-stu-id="50873-107">For more information on OWIN, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="50873-108">本教學課程是由 Rick Anderson （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）、Praburaj Thiagarajan 和 Howard Dierking （ [@howard\_Dierking](https://twitter.com/howard_dierking) ）撰寫。</span><span class="sxs-lookup"><span data-stu-id="50873-108">This tutorial was written by Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan, and Howard Dierking ( [@howard\_dierking](https://twitter.com/howard_dierking) ).</span></span>
>
> ## <a name="prerequisites"></a><span data-ttu-id="50873-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="50873-109">Prerequisites</span></span>
>
> [<span data-ttu-id="50873-110">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="50873-110">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="owin-startup-class-detection"></a><span data-ttu-id="50873-111">OWIN 啟動類別偵測</span><span class="sxs-lookup"><span data-stu-id="50873-111">OWIN Startup Class Detection</span></span>

 <span data-ttu-id="50873-112">每個 OWIN 應用程式都有一個啟動類別，您可以在其中指定應用程式管線的元件。</span><span class="sxs-lookup"><span data-stu-id="50873-112">Every OWIN Application has a startup class where you specify components for the application pipeline.</span></span> <span data-ttu-id="50873-113">有不同的方式可讓您連接啟動類別與執行時間，視您選擇的裝載模型而定（OwinHost、IIS 和 IIS Express）。</span><span class="sxs-lookup"><span data-stu-id="50873-113">There are different ways you can connect your startup class with the runtime, depending on the hosting model you choose (OwinHost, IIS, and IIS-Express).</span></span> <span data-ttu-id="50873-114">本教學課程中所顯示的 startup 類別可以在每個裝載應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="50873-114">The startup class shown in this tutorial can be used in every hosting application.</span></span> <span data-ttu-id="50873-115">您可以使用下列其中一種方法，將啟動類別與主控執行時間連接：</span><span class="sxs-lookup"><span data-stu-id="50873-115">You connect the startup class with the hosting runtime using one of the these approaches:</span></span>

1. <span data-ttu-id="50873-116">**命名慣例**： Katana 會在符合元件名稱或全域命名空間的命名空間中，尋找名為 `Startup` 的類別。</span><span class="sxs-lookup"><span data-stu-id="50873-116">**Naming Convention**: Katana looks for a class named `Startup` in namespace matching the assembly name or the global namespace.</span></span>
2. <span data-ttu-id="50873-117">**OwinStartup 屬性**：這是大部分開發人員用來指定啟動類別的方法。</span><span class="sxs-lookup"><span data-stu-id="50873-117">**OwinStartup Attribute**: This is the approach most developers will take to specify the startup class.</span></span> <span data-ttu-id="50873-118">下列屬性會將 startup 類別設定為 `StartupDemo` 命名空間中的 `TestStartup` 類別。</span><span class="sxs-lookup"><span data-stu-id="50873-118">The following attribute will set the startup class to the `TestStartup` class in the `StartupDemo` namespace.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   <span data-ttu-id="50873-119">`OwinStartup` 屬性會覆寫命名慣例。</span><span class="sxs-lookup"><span data-stu-id="50873-119">The `OwinStartup` attribute overrides the naming convention.</span></span> <span data-ttu-id="50873-120">您也可以指定具有此屬性的易記名稱，不過，使用易記名稱時，您也必須使用設定檔中的 `appSetting` 元素。</span><span class="sxs-lookup"><span data-stu-id="50873-120">You can also specify a friendly name with this attribute, however, using a friendly name requires you to also use the `appSetting` element in the configuration file.</span></span>
3. <span data-ttu-id="50873-121">**設定檔中的 appSetting 元素**： `appSetting` 元素會覆寫 `OwinStartup` 屬性和命名慣例。</span><span class="sxs-lookup"><span data-stu-id="50873-121">**The appSetting element in the Configuration file**: The `appSetting` element overrides the `OwinStartup` attribute and naming convention.</span></span> <span data-ttu-id="50873-122">您可以有多個啟動類別（每個都使用 `OwinStartup` 屬性），並使用類似下列的標記來設定要在設定檔案中載入的啟動類別：</span><span class="sxs-lookup"><span data-stu-id="50873-122">You can have multiple startup classes (each using an `OwinStartup` attribute) and configure which startup class will be loaded in a configuration file using markup similar to the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   <span data-ttu-id="50873-123">您也可以使用下列索引鍵，明確指定啟動類別和元件：</span><span class="sxs-lookup"><span data-stu-id="50873-123">The following key, which explicitly specifies the startup class and assembly can also be used:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   <span data-ttu-id="50873-124">設定檔中的下列 XML 會指定 `ProductionConfiguration`的易記啟動類別名稱。</span><span class="sxs-lookup"><span data-stu-id="50873-124">The following XML in the configuration file specifies a friendly startup class name of `ProductionConfiguration`.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   <span data-ttu-id="50873-125">上述標記必須與下列 `OwinStartup` 屬性搭配使用，以指定易記名稱並導致 `ProductionStartup2` 類別執行。</span><span class="sxs-lookup"><span data-stu-id="50873-125">The above markup must be used with the following `OwinStartup` attribute which specifies a friendly name and causes the `ProductionStartup2` class to run.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. <span data-ttu-id="50873-126">若要停用 OWIN 啟動探索，請在 web.config 檔案中新增具有 `"false"` 值的 `appSetting owin:AutomaticAppStartup`。</span><span class="sxs-lookup"><span data-stu-id="50873-126">To disable OWIN startup discovery add the `appSetting owin:AutomaticAppStartup` with a value of `"false"` in the web.config file.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a><span data-ttu-id="50873-127">使用 OWIN 啟動建立 ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="50873-127">Create an ASP.NET Web App using OWIN Startup</span></span>

1. <span data-ttu-id="50873-128">建立空的 Asp.Net web 應用程式，並將其命名為**StartupDemo**。</span><span class="sxs-lookup"><span data-stu-id="50873-128">Create an empty Asp.Net web application and name it **StartupDemo**.</span></span> <span data-ttu-id="50873-129">-使用 NuGet 套件管理員安裝 `Microsoft.Owin.Host.SystemWeb`。</span><span class="sxs-lookup"><span data-stu-id="50873-129">- Install `Microsoft.Owin.Host.SystemWeb` using the NuGet package manager.</span></span> <span data-ttu-id="50873-130">從 [**工具**] 功能表中，依序選取 [ **NuGet 套件管理員**] 和 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="50873-130">From the **Tools** menu, select **NuGet Package Manager**, and then **Package Manager Console**.</span></span> <span data-ttu-id="50873-131">輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="50873-131">Enter the following command:</span></span>

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. <span data-ttu-id="50873-132">新增 OWIN startup 類別。</span><span class="sxs-lookup"><span data-stu-id="50873-132">Add an OWIN startup class.</span></span> <span data-ttu-id="50873-133">在 Visual Studio 2017 中以滑鼠右鍵按一下專案，然後選取 [新增**類別**]。在 [**加入新專案**] 對話方塊的 [搜尋] 欄位中輸入*OWIN* ，並將名稱變更為 Startup.cs，然後選取 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="50873-133">In Visual Studio 2017 right-click the project and select **Add Class**.- In the **Add New Item** dialog box, enter *OWIN* in the search field, and change the name to Startup.cs, and then select **Add**.</span></span>

     ![](owin-startup-class-detection/_static/image1.png)

   <span data-ttu-id="50873-134">下次您想要新增*Owin 啟動類別*時，它會出現在 [**新增**] 功能表中。</span><span class="sxs-lookup"><span data-stu-id="50873-134">The next time you want to add an *Owin Startup class*, it will be in available from the **Add** menu.</span></span>

     ![](owin-startup-class-detection/_static/image2.png)

   <span data-ttu-id="50873-135">或者，您也可以用滑鼠右鍵按一下專案，然後依**序選取 [** 新增] 和 [**新專案**]，然後選取 [ **Owin] 啟動類別**。</span><span class="sxs-lookup"><span data-stu-id="50873-135">Alternatively, you can right-click the project and select **Add**, then select **New Item**, and then select the **Owin Startup class**.</span></span>

     ![](owin-startup-class-detection/_static/image3.png)

- <span data-ttu-id="50873-136">將*Startup.cs*檔案中產生的程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="50873-136">Replace the generated code in the *Startup.cs* file with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  <span data-ttu-id="50873-137">`app.Use` lambda 運算式是用來將指定的中介軟體元件註冊至 OWIN 管線。</span><span class="sxs-lookup"><span data-stu-id="50873-137">The `app.Use` lambda expression is used to register the specified middleware component to the OWIN pipeline.</span></span> <span data-ttu-id="50873-138">在此情況下，我們會先設定傳入要求的記錄，再回應傳入的要求。</span><span class="sxs-lookup"><span data-stu-id="50873-138">In this case we are setting up logging of incoming requests before responding to the incoming request.</span></span> <span data-ttu-id="50873-139">`next` 參數是管線中下一個元件的委派（ [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) [&lt; 工作](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx)&gt;）。</span><span class="sxs-lookup"><span data-stu-id="50873-139">The `next` parameter is the delegate ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt; ) to the next component in the pipeline.</span></span> <span data-ttu-id="50873-140">`app.Run` lambda 運算式會將管線連結到傳入的要求，並提供回應機制。</span><span class="sxs-lookup"><span data-stu-id="50873-140">The `app.Run` lambda expression hooks up the pipeline to incoming requests and provides the response mechanism.</span></span>
     > [!NOTE]
     > <span data-ttu-id="50873-141">在上述程式碼中，我們已將 `OwinStartup` 屬性標記為批註，而我們將依賴執行名為 `Startup` 的類別。-按***F5***執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="50873-141">In the code above we have commented out the `OwinStartup` attribute and we're relying on the convention of running the class named `Startup` .- Press ***F5*** to run the application.</span></span> <span data-ttu-id="50873-142">按幾次 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="50873-142">Hit refresh a few times.</span></span>

    <span data-ttu-id="50873-143">![](owin-startup-class-detection/_static/image4.png) 注意：本教學課程中的影像所顯示的數位不會符合您看到的數位。</span><span class="sxs-lookup"><span data-stu-id="50873-143">![](owin-startup-class-detection/_static/image4.png) Note: The number shown in the images in this tutorial will not match the number you see.</span></span> <span data-ttu-id="50873-144">當您重新整理頁面時，會使用毫秒字串來顯示新的回應。</span><span class="sxs-lookup"><span data-stu-id="50873-144">The millisecond string is used to show a new response when you refresh the page.</span></span>
  <span data-ttu-id="50873-145">您可以在 [**輸出**] 視窗中看到追蹤資訊。</span><span class="sxs-lookup"><span data-stu-id="50873-145">You can see the trace information in the **Output** window.</span></span>

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a><span data-ttu-id="50873-146">新增更多啟動類別</span><span class="sxs-lookup"><span data-stu-id="50873-146">Add More Startup Classes</span></span>

<span data-ttu-id="50873-147">在本節中，我們將新增另一個 Startup 類別。</span><span class="sxs-lookup"><span data-stu-id="50873-147">In this section we'll add another Startup class.</span></span> <span data-ttu-id="50873-148">您可以將多個 OWIN 啟動類別新增至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="50873-148">You can add multiple OWIN startup class to your application.</span></span> <span data-ttu-id="50873-149">例如，您可能會想要建立用於開發、測試和生產環境的啟動類別。</span><span class="sxs-lookup"><span data-stu-id="50873-149">For example, you might want to create startup classes for development, testing and production.</span></span>

1. <span data-ttu-id="50873-150">建立新的 OWIN 啟動類別，並將其命名為 `ProductionStartup`。</span><span class="sxs-lookup"><span data-stu-id="50873-150">Create a new OWIN Startup class and name it `ProductionStartup`.</span></span>
2. <span data-ttu-id="50873-151">使用下列程式碼取代產生的程式碼：</span><span class="sxs-lookup"><span data-stu-id="50873-151">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. <span data-ttu-id="50873-152">按下 Control F5 以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="50873-152">Press Control F5 to run the app.</span></span> <span data-ttu-id="50873-153">`OwinStartup` 屬性會指定執行生產啟動類別。</span><span class="sxs-lookup"><span data-stu-id="50873-153">The `OwinStartup` attribute specifies the production startup class is run.</span></span>

    ![](owin-startup-class-detection/_static/image6.png)
4. <span data-ttu-id="50873-154">建立另一個 OWIN 啟動類別，並將其命名為 `TestStartup`。</span><span class="sxs-lookup"><span data-stu-id="50873-154">Create another OWIN Startup class and name it `TestStartup`.</span></span>
5. <span data-ttu-id="50873-155">使用下列程式碼取代產生的程式碼：</span><span class="sxs-lookup"><span data-stu-id="50873-155">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   <span data-ttu-id="50873-156">上述 `OwinStartup` 屬性多載會將 `TestingConfiguration` 指定為啟動類別的*易記*名稱。</span><span class="sxs-lookup"><span data-stu-id="50873-156">The `OwinStartup` attribute overload above specifies `TestingConfiguration` as the *friendly* name of the Startup class.</span></span>
6. <span data-ttu-id="50873-157">開啟*web.config*檔案，並新增 OWIN 應用程式啟動金鑰，它會指定啟動類別的易記名稱：</span><span class="sxs-lookup"><span data-stu-id="50873-157">Open the *web.config* file and add the OWIN App startup key which specifies the friendly name of the Startup class:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. <span data-ttu-id="50873-158">按下 Control F5 以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="50873-158">Press Control F5 to run the app.</span></span> <span data-ttu-id="50873-159">應用程式設定元素會採用上述專案，並執行測試設定。</span><span class="sxs-lookup"><span data-stu-id="50873-159">The app settings element takes precedent, and the test configuration is run.</span></span>

    ![](owin-startup-class-detection/_static/image7.png)
8. <span data-ttu-id="50873-160">從 `TestStartup` 類別中的 `OwinStartup` 屬性移除*易記*名稱。</span><span class="sxs-lookup"><span data-stu-id="50873-160">Remove the *friendly* name from the `OwinStartup` attribute in the `TestStartup` class.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. <span data-ttu-id="50873-161">以下列內容取代*web.config*檔案中的 OWIN 應用程式啟動金鑰：</span><span class="sxs-lookup"><span data-stu-id="50873-161">Replace the OWIN App startup key in the *web.config* file with the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. <span data-ttu-id="50873-162">將每個類別中的 `OwinStartup` 屬性還原為 Visual Studio 所產生的預設屬性代碼：</span><span class="sxs-lookup"><span data-stu-id="50873-162">Revert the `OwinStartup` attribute in each class to the default attribute code generated by Visual Studio:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    <span data-ttu-id="50873-163">下列每個 OWIN 應用程式啟動金鑰都會導致生產環境類別執行。</span><span class="sxs-lookup"><span data-stu-id="50873-163">Each of the OWIN App startup keys below will cause the production class to run.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    <span data-ttu-id="50873-164">最後一個啟動金鑰會指定啟動設定方法。</span><span class="sxs-lookup"><span data-stu-id="50873-164">The last startup key specifies the startup configuration method.</span></span> <span data-ttu-id="50873-165">下列 OWIN 應用程式啟動金鑰可讓您將 configuration 類別的名稱變更為 `MyConfiguration`。</span><span class="sxs-lookup"><span data-stu-id="50873-165">The following OWIN App startup key allows you to change the name of the configuration class to `MyConfiguration` .</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a><span data-ttu-id="50873-166">使用 Owinhost</span><span class="sxs-lookup"><span data-stu-id="50873-166">Using Owinhost.exe</span></span>

1. <span data-ttu-id="50873-167">以下列標記取代 Web.config 檔案：</span><span class="sxs-lookup"><span data-stu-id="50873-167">Replace the Web.config file with the following markup:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   <span data-ttu-id="50873-168">最後一個索引鍵是，因此在此情況下會指定 `TestStartup`。</span><span class="sxs-lookup"><span data-stu-id="50873-168">The last key wins, so in this case `TestStartup` is specified.</span></span>
2. <span data-ttu-id="50873-169">從 PMC 安裝 Owinhost：</span><span class="sxs-lookup"><span data-stu-id="50873-169">Install Owinhost from the PMC:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. <span data-ttu-id="50873-170">流覽至應用程式資料夾（*包含 web.config 檔案*的資料夾），然後在命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="50873-170">Navigate to the application folder (the folder containing the *Web.config* file) and in a command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   <span data-ttu-id="50873-171">命令視窗會顯示：</span><span class="sxs-lookup"><span data-stu-id="50873-171">The command window will show:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. <span data-ttu-id="50873-172">以 `http://localhost:5000/`的 URL 啟動瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="50873-172">Launch a browser with the URL `http://localhost:5000/`.</span></span>

    ![](owin-startup-class-detection/_static/image8.png)

   <span data-ttu-id="50873-173">OwinHost 遵守上述的啟動慣例。</span><span class="sxs-lookup"><span data-stu-id="50873-173">OwinHost honored the startup conventions listed above.</span></span>
5. <span data-ttu-id="50873-174">在命令視窗中，按 Enter 鍵結束 OwinHost。</span><span class="sxs-lookup"><span data-stu-id="50873-174">In the command window, press Enter to exit OwinHost.</span></span>
6. <span data-ttu-id="50873-175">在 `ProductionStartup` 類別中，新增下列 OwinStartup 屬性，以指定易記名稱*ProductionConfiguration*。</span><span class="sxs-lookup"><span data-stu-id="50873-175">In the `ProductionStartup` class, add the following OwinStartup attribute which specifies a friendly name of *ProductionConfiguration*.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. <span data-ttu-id="50873-176">在命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="50873-176">In the command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   <span data-ttu-id="50873-177">已載入生產啟動類別。</span><span class="sxs-lookup"><span data-stu-id="50873-177">The Production startup class is loaded.</span></span>
    ![](owin-startup-class-detection/_static/image9.png)

   <span data-ttu-id="50873-178">我們的應用程式有多個啟動類別，在此範例中，我們已延後要載入的啟動類別，直到執行時間為止。</span><span class="sxs-lookup"><span data-stu-id="50873-178">Our application has multiple startup classes, and in this example we have deferred which startup class to load until runtime.</span></span>
8. <span data-ttu-id="50873-179">測試下列執行時間啟動選項：</span><span class="sxs-lookup"><span data-stu-id="50873-179">Test the following runtime startup options:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]
