---
title: 開始使用 Razor 元件
author: guardrex
description: 了解如何開始使用 Razor 元件建立和修改 Razor 元件專案。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/03/2019
uid: razor-components/get-started
ms.openlocfilehash: a9ada603e5ed4e0e75c4aebc5105c331118666e6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036385"
---
# <a name="get-started-with-razor-components"></a><span data-ttu-id="55a92-103">開始使用 Razor 元件</span><span class="sxs-lookup"><span data-stu-id="55a92-103">Get started with Razor Components</span></span>

<span data-ttu-id="55a92-104">作者：[Daniel Roth](https://github.com/danroth27) 和 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="55a92-104">By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="55a92-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="55a92-105">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="55a92-106">必要條件：</span><span class="sxs-lookup"><span data-stu-id="55a92-106">Prerequisites:</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-vs-3.0.md)]

<span data-ttu-id="55a92-107">若要在 Visual Studio 中建立第一個 Razor 元件專案：</span><span class="sxs-lookup"><span data-stu-id="55a92-107">To create your first Razor Components project in Visual Studio:</span></span>

1. <span data-ttu-id="55a92-108">選取 **檔案** > **新專案** > **Web** > **ASP.NET Core Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="55a92-108">Select **File** > **New Project** > **Web** > **ASP.NET Core Web Application**.</span></span>
1. <span data-ttu-id="55a92-109">請確定 **.NET Core**並**ASP.NET Core 3.0**選取頂端。</span><span class="sxs-lookup"><span data-stu-id="55a92-109">Make sure **.NET Core** and **ASP.NET Core 3.0** are selected at the top.</span></span>
1. <span data-ttu-id="55a92-110">選擇**Razor 元件**範本，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="55a92-110">Choose the **Razor Components** template and select **OK**.</span></span>

   ![新的應用程式 對話方塊](https://msdnshared.blob.core.windows.net/media/2019/01/razor-components-template.png)

1. <span data-ttu-id="55a92-112">按下 **F5** 即可執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="55a92-112">Press **F5** to run the app.</span></span>

<span data-ttu-id="55a92-113">恭喜您！</span><span class="sxs-lookup"><span data-stu-id="55a92-113">Congratulations!</span></span> <span data-ttu-id="55a92-114">您剛剛執行第一個 Razor 元件應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="55a92-114">You just ran your first Razor Components app!</span></span>

<!--

# [Visual Studio Code](#tab/visual-studio-code)

Prerequisites:

[!INCLUDE[](~/includes/net-core-prereqs-vsc-3.0.md)]

To create your first Razor Components project in Visual Studio Code:

1. Execute the following command from a command shell:

   ```console
   dotnet new razorcomponents -o WebApplication1
   ```

1. Open the *WebApplication1* folder in Visual Studio Code.

1. Add a *.vscode* folder.

1. Add a *tasks.json* file to the *.vscode* folder with the following content:

   [!code-json[](get-started/samples_snapshot/3.x/tasks.json)]

1. Add a *launch.json* file to the *.vscode* folder with the following content:

   [!code-json[](get-started/samples_snapshot/3.x/launch.json)]

1. Execute the app using the Visual Studio Code debugger.

1. In a browser, navigate to `https://localhost:5001`.

Congratulations! You just ran your first Razor Components app!

# [Visual Studio for Mac](#tab/visual-studio-mac)

.NET Core 3.0 will be supported with Visual Studio for Mac version 8.0 or later. Visual Studio for Mac version 8.0 Preview isn't available at this time.

Use the [.NET Core CLI version of this topic](xref:razor-components/get-started?tabs=netcore-cli) on macOS.


[!INCLUDE[](~/includes/net-core-prereqs-mac-3.0.md)]

To create your first project Razor Components project in Visual Studio for Mac:

1. Select **File** > **New Solution** or **New Project**.
1. In the sidebar, select **.NET Core** > **App**.
1. Select **ASP.NET Core Razor Components** and select **Next**.
1. The **Target Framework** defaults to **.NET Core 3.0**. Select **Next**.
1. In the **Project Name** field, enter `WebApplication1`. Select **Create**.
1. Select **Run** > **Run Without Debugging** to run the app *without the debugger*. Running with the debugger isn't supported at this time.

Congratulations! You just ran your first Razor Components app!
-->

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="55a92-115">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="55a92-115">.NET Core CLI</span></span>](#tab/netcore-cli/)

<span data-ttu-id="55a92-116">必要條件：</span><span class="sxs-lookup"><span data-stu-id="55a92-116">Prerequisites:</span></span>

* [<span data-ttu-id="55a92-117">.NET core SDK 3.0 預覽</span><span class="sxs-lookup"><span data-stu-id="55a92-117">.NET Core SDK 3.0 Preview</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0)

1. <span data-ttu-id="55a92-118">若要從命令殼層中建立第一個 Razor 元件專案：</span><span class="sxs-lookup"><span data-stu-id="55a92-118">To create your first Razor Components project from a command shell:</span></span>

   ```console
   dotnet new razorcomponents -o WebApplication1
   cd WebApplication1
   dotnet run
   ```

1. <span data-ttu-id="55a92-119">在瀏覽器中，巡覽至 `https://localhost:5001`。</span><span class="sxs-lookup"><span data-stu-id="55a92-119">In a browser, navigate to `https://localhost:5001`.</span></span>

<span data-ttu-id="55a92-120">恭喜您！</span><span class="sxs-lookup"><span data-stu-id="55a92-120">Congratulations!</span></span> <span data-ttu-id="55a92-121">您剛剛執行第一個 Razor 元件應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="55a92-121">You just ran your first Razor Components app!</span></span>

---

## <a name="razor-components-project"></a><span data-ttu-id="55a92-122">Razor 元件專案</span><span class="sxs-lookup"><span data-stu-id="55a92-122">Razor Components project</span></span>

<span data-ttu-id="55a92-123">Razor 元件範本所建立的方案包含兩個專案：</span><span class="sxs-lookup"><span data-stu-id="55a92-123">The solution created by the Razor Components template contains two projects:</span></span>

* <span data-ttu-id="55a92-124">*WebApplication1.Server* &ndash;伺服器專案是設定裝載 Razor 元件應用程式的 ASP.NET Core 專案。</span><span class="sxs-lookup"><span data-stu-id="55a92-124">*WebApplication1.Server* &ndash; The server project is an ASP.NET Core project set up to host the Razor Components app.</span></span>
* <span data-ttu-id="55a92-125">*WebApplication1.App* &ndash;使用 Razor 元件在用戶端 web UI 專案。</span><span class="sxs-lookup"><span data-stu-id="55a92-125">*WebApplication1.App* &ndash; The client-side web UI project that uses Razor Components.</span></span>

<span data-ttu-id="55a92-126">中的 UI 邏輯*WebApplication1.App*專案分開基於 ASP.NET Core 3.0 Preview 2 的技術限制的應用程式的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="55a92-126">The UI logic in the *WebApplication1.App* project is separated from the rest of the app due to a technical limitation in ASP.NET Core 3.0 Preview 2.</span></span> <span data-ttu-id="55a92-127">Razor 檔案的副檔名 (*.cshtml*) 使用 Razor 元件也會使用 Razor Pages 和 MVC 的檢視。</span><span class="sxs-lookup"><span data-stu-id="55a92-127">The Razor file extension (*.cshtml*) used for Razor Components is also used for Razor Pages and MVC views.</span></span> <span data-ttu-id="55a92-128">目前，Razor 元件和 Razor 頁面/MVC 有不同的編譯模型，因此 Razor 元件 Razor 檔案會有所區隔。</span><span class="sxs-lookup"><span data-stu-id="55a92-128">Currently, Razor Components and Razor Pages/MVC have different compilation models, so the Razor Components Razor files are kept separate.</span></span> <span data-ttu-id="55a92-129">在未來的預覽版中，我們打算引進新的檔案副檔名 Razor 元件 (*.razor*)。</span><span class="sxs-lookup"><span data-stu-id="55a92-129">In a future preview, we plan to introduce a new file extension for Razor Components (*.razor*).</span></span> <span data-ttu-id="55a92-130">將裝載元件、 頁面和檢視*相同的專案中*。</span><span class="sxs-lookup"><span data-stu-id="55a92-130">Components, pages, and views will be hosted *in the same project*.</span></span>

<span data-ttu-id="55a92-131">執行應用程式時，多個頁面都是從資訊看板中的索引標籤：</span><span class="sxs-lookup"><span data-stu-id="55a92-131">When the app is run, multiple pages are available from tabs in the sidebar:</span></span>

* <span data-ttu-id="55a92-132">首頁</span><span class="sxs-lookup"><span data-stu-id="55a92-132">Home</span></span>
* <span data-ttu-id="55a92-133">計數器</span><span class="sxs-lookup"><span data-stu-id="55a92-133">Counter</span></span>
* <span data-ttu-id="55a92-134">擷取資料</span><span class="sxs-lookup"><span data-stu-id="55a92-134">Fetch data</span></span>

<span data-ttu-id="55a92-135">在 [計數器] 頁面上，選取 [按我] 按鈕以在不重新整理頁面的情況下讓計數器遞增。</span><span class="sxs-lookup"><span data-stu-id="55a92-135">On the Counter page, select the **Click me** button to increment the counter without a page refresh.</span></span> <span data-ttu-id="55a92-136">讓網頁中的計數器遞增通常需要撰寫 JavaScript，但 Razor 元件提供一個使用 C# 的更好方法。</span><span class="sxs-lookup"><span data-stu-id="55a92-136">Incrementing a counter in a webpage normally requires writing JavaScript, but Razor Components provides a better approach using C#.</span></span>

<span data-ttu-id="55a92-137">*WebApplication1.App/Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="55a92-137">*WebApplication1.App/Pages/Counter.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter1.cshtml)]

<span data-ttu-id="55a92-138">申請`/counter`在瀏覽器中所指定`@page`指示詞，在頂端，導致計數器元件來呈現其內容。</span><span class="sxs-lookup"><span data-stu-id="55a92-138">A request for `/counter` in the browser, as specified by the `@page` directive at the top, causes the Counter component to render its content.</span></span> <span data-ttu-id="55a92-139">元件會轉譯成接著可用來更新 UI 富彈性又有效率的方式呈現樹狀結構的記憶體中表示法。</span><span class="sxs-lookup"><span data-stu-id="55a92-139">Components render into an in-memory representation of the render tree that can then be used to update the UI in a flexible and efficient way.</span></span>

<span data-ttu-id="55a92-140">每次**Click me**按鈕已選取：</span><span class="sxs-lookup"><span data-stu-id="55a92-140">Each time the **Click me** button is selected:</span></span>

* <span data-ttu-id="55a92-141">`onclick`引發事件。</span><span class="sxs-lookup"><span data-stu-id="55a92-141">The `onclick` event is fired.</span></span>
* <span data-ttu-id="55a92-142">已呼叫 `IncrementCount` 方法。</span><span class="sxs-lookup"><span data-stu-id="55a92-142">The `IncrementCount` method is called.</span></span>
* <span data-ttu-id="55a92-143">`currentCount`會遞增。</span><span class="sxs-lookup"><span data-stu-id="55a92-143">The `currentCount` is incremented.</span></span>
* <span data-ttu-id="55a92-144">元件會轉譯一次。</span><span class="sxs-lookup"><span data-stu-id="55a92-144">The component is rendered again.</span></span>

<span data-ttu-id="55a92-145">執行階段會比較新的內容來將舊內容，並只會套用已變更的內容與文件物件模型 (DOM)。</span><span class="sxs-lookup"><span data-stu-id="55a92-145">The runtime compares the new content to the previous content and only applies the changed content to the Document Object Model (DOM).</span></span>

<span data-ttu-id="55a92-146">您可以將元件加入另一個元件使用 HTML 的類似語法。</span><span class="sxs-lookup"><span data-stu-id="55a92-146">Add a component to another component using an HTML-like syntax.</span></span> <span data-ttu-id="55a92-147">元件參數會指定使用屬性或子內容。</span><span class="sxs-lookup"><span data-stu-id="55a92-147">Component parameters are specified using attributes or child content.</span></span> <span data-ttu-id="55a92-148">比方說，將計數器元件可以加入至應用程式的首頁加`<Counter />`索引元件的項目。</span><span class="sxs-lookup"><span data-stu-id="55a92-148">For example, a Counter component can be added to the app's homepage by adding a `<Counter />` element to the Index component.</span></span>

<span data-ttu-id="55a92-149">*WebApplication1.App/Pages/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="55a92-149">*WebApplication1.App/Pages/Index.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Index1.cshtml?highlight=7)]

<span data-ttu-id="55a92-150">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="55a92-150">Run the app.</span></span> <span data-ttu-id="55a92-151">在首頁上都有它自己的計數器。</span><span class="sxs-lookup"><span data-stu-id="55a92-151">The homepage has its own counter.</span></span>

<span data-ttu-id="55a92-152">若要將參數加入至計數器的元件，更新 元件的`@functions`區塊：</span><span class="sxs-lookup"><span data-stu-id="55a92-152">To add a parameter to the Counter component, update the component's `@functions` block:</span></span>

* <span data-ttu-id="55a92-153">新增的屬性`IncrementAmount`附有`[Parameter]`屬性。</span><span class="sxs-lookup"><span data-stu-id="55a92-153">Add a property for `IncrementAmount` decorated with the `[Parameter]` attribute.</span></span>
* <span data-ttu-id="55a92-154">將 `IncrementCount` 方法變更為在增加 `currentCount`的值時使用 `IncrementAmount`。</span><span class="sxs-lookup"><span data-stu-id="55a92-154">Change the `IncrementCount` method to use the `IncrementAmount` when increasing the value of `currentCount`.</span></span>

<span data-ttu-id="55a92-155">*WebApplication1.App/Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="55a92-155">*WebApplication1.App/Pages/Counter.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter2.cshtml?highlight=4,8)]

<span data-ttu-id="55a92-156">使用屬性在「首頁」元件的 `<Counter>` 元素中指定 `IncrementAmount` 參數。</span><span class="sxs-lookup"><span data-stu-id="55a92-156">Specify an `IncrementAmount` parameter in the Home component's `<Counter>` element using an attribute.</span></span>

<span data-ttu-id="55a92-157">*WebApplication1.App/Pages/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="55a92-157">*WebApplication1.App/Pages/Index.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Index2.cshtml)]

<span data-ttu-id="55a92-158">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="55a92-158">Run the app.</span></span> <span data-ttu-id="55a92-159">在首頁上有它自己的十個在每次增加的計數器**Click me**按鈕已選取。</span><span class="sxs-lookup"><span data-stu-id="55a92-159">The homepage has its own counter that increments by ten each time the **Click me** button is selected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55a92-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55a92-160">Next steps</span></span>

<xref:tutorials/first-razor-components-app>
