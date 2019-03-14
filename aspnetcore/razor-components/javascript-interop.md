---
title: Razor 元件 JavaScript interop
author: guardrex
description: 了解如何叫用 JavaScript 函式，從.NET 和.NET 從 JavaScript Blazor 和 Razor 元件的應用程式中的方法。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/javascript-interop
ms.openlocfilehash: 9f822fee8990b03ff15ffa9857a2ddd95328a6ce
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050365"
---
# <a name="razor-components-javascript-interop"></a><span data-ttu-id="890fc-103">Razor 元件 JavaScript interop</span><span class="sxs-lookup"><span data-stu-id="890fc-103">Razor Components JavaScript interop</span></span>

<span data-ttu-id="890fc-104">藉由[Javier Calvarro Nelson](https://github.com/javiercn)， [Daniel Roth](https://github.com/danroth27)，和[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="890fc-104">By [Javier Calvarro Nelson](https://github.com/javiercn), [Daniel Roth](https://github.com/danroth27), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="890fc-105">Razor 元件應用程式可以叫用 JavaScript 函式，從.NET 和.NET 中的 JavaScript 程式碼的方法。</span><span class="sxs-lookup"><span data-stu-id="890fc-105">A Razor Components app can invoke JavaScript functions from .NET and .NET methods from JavaScript code.</span></span>

## <a name="invoke-javascript-functions-from-net-methods"></a><span data-ttu-id="890fc-106">叫用.NET 方法的 JavaScript 函式</span><span class="sxs-lookup"><span data-stu-id="890fc-106">Invoke JavaScript functions from .NET methods</span></span>

<span data-ttu-id="890fc-107">有些.NET 程式碼時要呼叫的 JavaScript 函式需要的時候。</span><span class="sxs-lookup"><span data-stu-id="890fc-107">There are times when .NET code is required to call a JavaScript function.</span></span> <span data-ttu-id="890fc-108">例如，瀏覽器功能或從 JavaScript 程式庫應用程式的功能，可以公開 JavaScript 呼叫。</span><span class="sxs-lookup"><span data-stu-id="890fc-108">For example, a JavaScript call can expose browser capabilities or functionality from a JavaScript library to the app.</span></span>

<span data-ttu-id="890fc-109">若要從.NET 呼叫 JavaScript，使用`IJSRuntime`抽象概念。</span><span class="sxs-lookup"><span data-stu-id="890fc-109">To call into JavaScript from .NET, use the `IJSRuntime` abstraction.</span></span> <span data-ttu-id="890fc-110">`InvokeAsync<T>`方法`IJSRuntime`會為您想要搭配任意數目的 JSON 可序列化的引數叫用的 JavaScript 函式的識別項。</span><span class="sxs-lookup"><span data-stu-id="890fc-110">The `InvokeAsync<T>` method on `IJSRuntime` takes an identifier for the JavaScript function you wish to invoke along with any number of JSON-serializable arguments.</span></span> <span data-ttu-id="890fc-111">函式識別項是相對於全域範圍 (`window`)。</span><span class="sxs-lookup"><span data-stu-id="890fc-111">The function identifier is relative to the global scope (`window`).</span></span> <span data-ttu-id="890fc-112">如果您想要呼叫`window.someScope.someFunction`，此識別項是`someScope.someFunction`。</span><span class="sxs-lookup"><span data-stu-id="890fc-112">If you wish to call `window.someScope.someFunction`, the identifier is `someScope.someFunction`.</span></span> <span data-ttu-id="890fc-113">就不需要註冊函式，會在呼叫之前。</span><span class="sxs-lookup"><span data-stu-id="890fc-113">There's no need to register the function before it's called.</span></span> <span data-ttu-id="890fc-114">傳回的型別`T`也必須是 JSON 可序列化。</span><span class="sxs-lookup"><span data-stu-id="890fc-114">The return type `T` must also be JSON serializable.</span></span>

<span data-ttu-id="890fc-115">針對伺服器端 ASP.NET Core Razor 元件應用程式：</span><span class="sxs-lookup"><span data-stu-id="890fc-115">For server-side ASP.NET Core Razor Components apps:</span></span>

* <span data-ttu-id="890fc-116">伺服器端應用程式會處理多個使用者要求。</span><span class="sxs-lookup"><span data-stu-id="890fc-116">Multiple user requests are processed by the server-side app.</span></span> <span data-ttu-id="890fc-117">請不要呼叫`JSRuntime.Current`元件叫用 JavaScript 函式中。</span><span class="sxs-lookup"><span data-stu-id="890fc-117">Don't call `JSRuntime.Current` in a component to invoke JavaScript functions.</span></span>
* <span data-ttu-id="890fc-118">插入`IJSRuntime`抽象並用來發出 interop 的 JavaScript 呼叫插入的物件。</span><span class="sxs-lookup"><span data-stu-id="890fc-118">Inject the `IJSRuntime` abstraction and use the injected object to issue JavaScript interop calls.</span></span>

<span data-ttu-id="890fc-119">下列範例根據[TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder)，實驗性的 JavaScript 基礎解碼器。</span><span class="sxs-lookup"><span data-stu-id="890fc-119">The following example is based on [TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder), an experimental JavaScript-based decoder.</span></span> <span data-ttu-id="890fc-120">此範例示範如何叫用的 JavaScript 函式，從C#方法。</span><span class="sxs-lookup"><span data-stu-id="890fc-120">The example demonstrates how to invoke a JavaScript function from a C# method.</span></span> <span data-ttu-id="890fc-121">JavaScript 函式會接受位元組陣列，從C#方法，將陣列，並傳回元件用於顯示的文字。</span><span class="sxs-lookup"><span data-stu-id="890fc-121">The JavaScript function accepts a byte array from a C# method, decodes the array, and returns the text to the component for display.</span></span>

<span data-ttu-id="890fc-122">內部`<head>`項目*wwwroot/index.html*，提供使用的函式`TextDecoder`解碼傳入的陣列：</span><span class="sxs-lookup"><span data-stu-id="890fc-122">Inside the `<head>` element of *wwwroot/index.html*, provide a function that uses `TextDecoder` to decode a passed array:</span></span>

```html
<script>
  window.ConvertArray = (win1251Array) => {
    var win1251decoder = new TextDecoder('windows-1251');
    var bytes = new Uint8Array(win1251Array);
    var decodedArray = win1251decoder.decode(bytes);
    console.log(decodedArray);
    return decodedArray;
  };
</script>
```

<span data-ttu-id="890fc-123">JavaScript 程式碼，例如上述範例中，所示的程式碼也可以載入 JavaScript 檔案中的指令碼檔案的參考所*wwwroot/index.html*檔案。</span><span class="sxs-lookup"><span data-stu-id="890fc-123">JavaScript code, such as the code shown in the preceding example, can also be loaded by a JavaScript file with a reference to the script file in the *wwwroot/index.html* file.</span></span>

<span data-ttu-id="890fc-124">下列元件：</span><span class="sxs-lookup"><span data-stu-id="890fc-124">The following component:</span></span>

* <span data-ttu-id="890fc-125">叫用`ConvertArray`JavaScript 函式使用`JsRuntime`當元件 按鈕 (**轉換陣列**) 已選取。</span><span class="sxs-lookup"><span data-stu-id="890fc-125">Invokes the `ConvertArray` JavaScript function using `JsRuntime` when a component button (**Convert Array**) is selected.</span></span>
* <span data-ttu-id="890fc-126">JavaScript 函式呼叫之後，會傳遞的陣列轉換成字串。</span><span class="sxs-lookup"><span data-stu-id="890fc-126">After the JavaScript function is called, the passed array is converted into a string.</span></span> <span data-ttu-id="890fc-127">若要顯示的元件，會傳回字串。</span><span class="sxs-lookup"><span data-stu-id="890fc-127">The string is returned to the component for display.</span></span>

```cshtml
@page "/"
@using Microsoft.JSInterop;
@inject IJSRuntime JsRuntime;

<h1>Call JavaScript Function Example</h1>

<button type="button" class="btn btn-primary" onclick="@ConvertArray">
    Convert Array
</button>

<p class="mt-2" style="font-size:1.6em">
    <span class="badge badge-success">
        @ConvertedText
    </span>
</p>

@functions {
    // Quote (c)2005 Universal Pictures: Serenity
    // https://www.uphe.com/movies/serenity
    // David Krumholtz on IMDB: https://www.imdb.com/name/nm0472710/

    private MarkupString ConvertedText =
        new MarkupString("Select the <b>Convert Array</b> button.");

    private uint[] QuoteArray = new uint[]
        {
            60, 101, 109, 62, 67, 97, 110, 39, 116, 32, 115, 116, 111, 112, 32,
            116, 104, 101, 32, 115, 105, 103, 110, 97, 108, 44, 32, 77, 97,
            108, 46, 60, 47, 101, 109, 62, 32, 45, 32, 77, 114, 46, 32, 85, 110,
            105, 118, 101, 114, 115, 101, 10, 10,
        };

    async void ConvertArray()
    {
        var text =
            await JsRuntime.InvokeAsync<string>("ConvertArray", QuoteArray);

        ConvertedText = new MarkupString(text);

        StateHasChanged();
    }
}
```

<span data-ttu-id="890fc-128">用戶端 Blazor 應用程式，如`IJSRuntime`抽象層是從可存取`JSRuntime.Current`，這指的是目前使用者的要求。</span><span class="sxs-lookup"><span data-stu-id="890fc-128">For client-side Blazor apps, the `IJSRuntime` abstraction is accessible from `JSRuntime.Current`, which refers to the current user's request.</span></span> <span data-ttu-id="890fc-129">因為只有一位使用者的用戶端 Blazor 應用程式，使用`JSRuntime.Current`叫用 JavaScript 函式可正常運作。</span><span class="sxs-lookup"><span data-stu-id="890fc-129">Because there's only a single user of a client-side Blazor app, using `JSRuntime.Current` to invoke a JavaScript function works normally.</span></span> <span data-ttu-id="890fc-130">只使用`JSRuntime.Current`用戶端 Blazor 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="890fc-130">Only use `JSRuntime.Current` in client-side Blazor apps.</span></span>

<span data-ttu-id="890fc-131">本主題相關的用戶端範例應用程式，在兩個 JavaScript 函式可與接收使用者輸入並顯示歡迎訊息 DOM 互動的用戶端應用程式：</span><span class="sxs-lookup"><span data-stu-id="890fc-131">In the client-side sample app that accompanies this topic, two JavaScript functions are available to the client-side app that interact with the DOM to receive user input and display a welcome message:</span></span>

* <span data-ttu-id="890fc-132">`showPrompt` &ndash; 會產生接受使用者輸入 （使用者名稱） 的提示，並傳回給呼叫者的名稱。</span><span class="sxs-lookup"><span data-stu-id="890fc-132">`showPrompt` &ndash; Produces a prompt to accept user input (the user's name) and returns the name to the caller.</span></span>
* <span data-ttu-id="890fc-133">`displayWelcome` &ndash; 會從呼叫端的歡迎訊息指派至 DOM 物件，但`id`的`welcome`。</span><span class="sxs-lookup"><span data-stu-id="890fc-133">`displayWelcome` &ndash; Assigns a welcome message from the caller to a DOM object with an `id` of `welcome`.</span></span>

<span data-ttu-id="890fc-134">*wwwroot/exampleJsInterop.js*:</span><span class="sxs-lookup"><span data-stu-id="890fc-134">*wwwroot/exampleJsInterop.js*:</span></span>

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=2-7)]

<span data-ttu-id="890fc-135">地方`<script>`參考中的 JavaScript 檔案的標記*wwwroot/index.html*檔案：</span><span class="sxs-lookup"><span data-stu-id="890fc-135">Place the `<script>` tag that references the JavaScript file in the *wwwroot/index.html* file:</span></span>

[!code-html[](./common/samples/3.x/BlazorSample/wwwroot/index.html?highlight=16)]

<span data-ttu-id="890fc-136">不將指令碼標記放在元件檔，因為無法以動態方式更新指令碼標記。</span><span class="sxs-lookup"><span data-stu-id="890fc-136">Don't place a script tag in a component file because the script tag can't be updated dynamically.</span></span>

<span data-ttu-id="890fc-137">使用 JavaScript 函式，藉由呼叫.NET 方法 interop`InvokeAsync<T>`方法`IJSRuntime`。</span><span class="sxs-lookup"><span data-stu-id="890fc-137">.NET methods interop with the JavaScript functions by calling `InvokeAsync<T>` method on `IJSRuntime`.</span></span>

<span data-ttu-id="890fc-138">範例應用程式會使用一組C#方法，`Prompt`並`Display`，以叫用`showPrompt`並`displayWelcome`JavaScript 函式：</span><span class="sxs-lookup"><span data-stu-id="890fc-138">The sample app uses a pair of C# methods, `Prompt` and `Display`, to invoke the `showPrompt` and `displayWelcome` JavaScript functions:</span></span>

<span data-ttu-id="890fc-139">*JsInteropClasses/ExampleJsInterop.cs*:</span><span class="sxs-lookup"><span data-stu-id="890fc-139">*JsInteropClasses/ExampleJsInterop.cs*:</span></span>

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=6-8,14-16)]

<span data-ttu-id="890fc-140">`IJSRuntime`抽象層是以非同步方式來提供伺服器端案例。</span><span class="sxs-lookup"><span data-stu-id="890fc-140">The `IJSRuntime` abstraction is asynchronous to allow for server-side scenarios.</span></span> <span data-ttu-id="890fc-141">如果應用程式執行用戶端，而且您想要以同步方式叫用的 JavaScript 函式來向下轉型`IJSInProcessRuntime`並呼叫`Invoke<T>`改。</span><span class="sxs-lookup"><span data-stu-id="890fc-141">If the app runs client-side and you want to invoke a JavaScript function synchronously, downcast to `IJSInProcessRuntime` and call `Invoke<T>` instead.</span></span> <span data-ttu-id="890fc-142">建議的大部分 JavaScript interop 程式庫使用非同步 Api，以確保程式庫適用於所有案例中，用戶端或伺服器端。</span><span class="sxs-lookup"><span data-stu-id="890fc-142">We recommend that most JavaScript interop libraries use the async APIs to ensure the libraries are available in all scenarios, client-side or server-side.</span></span>

<span data-ttu-id="890fc-143">範例應用程式包含元件，可示範 JS interop。</span><span class="sxs-lookup"><span data-stu-id="890fc-143">The sample app includes a component to demonstrate JS interop.</span></span> <span data-ttu-id="890fc-144">元件：</span><span class="sxs-lookup"><span data-stu-id="890fc-144">The component:</span></span>

* <span data-ttu-id="890fc-145">接收透過 JS 提示使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="890fc-145">Receives user input via a JS prompt.</span></span>
* <span data-ttu-id="890fc-146">要處理的元件傳回的文字。</span><span class="sxs-lookup"><span data-stu-id="890fc-146">Returns the text to the component for processing.</span></span>
* <span data-ttu-id="890fc-147">呼叫第二個的 JS 函式與顯示歡迎訊息 DOM 互動。</span><span class="sxs-lookup"><span data-stu-id="890fc-147">Calls a second JS function that interacts with the DOM to display a welcome message.</span></span>

<span data-ttu-id="890fc-148">*Pages/JSInterop.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="890fc-148">*Pages/JSInterop.cshtml*:</span></span>

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=1&end=21&highlight=2-3,9-11,13,16-20)]

1. <span data-ttu-id="890fc-149">當`TriggerJsPrompt`執行選取的元件**觸發程序 JavaScript 提示** 按鈕，`ExampleJsInterop.Prompt`方法中的C#呼叫程式碼。</span><span class="sxs-lookup"><span data-stu-id="890fc-149">When `TriggerJsPrompt` is executed by selecting the component's **Trigger JavaScript Prompt** button, the `ExampleJsInterop.Prompt` method in C# code is called.</span></span>
1. <span data-ttu-id="890fc-150">`Prompt`方法會執行 JavaScript`showPrompt`中所提供的函式*wwwroot/exampleJsInterop.js*檔案。</span><span class="sxs-lookup"><span data-stu-id="890fc-150">The `Prompt` method executes the JavaScript `showPrompt` function provided in the *wwwroot/exampleJsInterop.js* file.</span></span>
1. <span data-ttu-id="890fc-151">`showPrompt`函式會接受使用者輸入 （使用者的名稱），也就是 HTML 編碼，並傳回至`Prompt`方法最後回到元件。</span><span class="sxs-lookup"><span data-stu-id="890fc-151">The `showPrompt` function accepts user input (the user's name), which is HTML-encoded and returned to the `Prompt` method and ultimately back to the component.</span></span> <span data-ttu-id="890fc-152">該元件會將使用者的名稱儲存在本機變數中， `name`。</span><span class="sxs-lookup"><span data-stu-id="890fc-152">The component stores the user's name in a local variable, `name`.</span></span>
1. <span data-ttu-id="890fc-153">將字串儲存在`name`會納入歡迎訊息，傳遞至第二個C#方法中， `ExampleJsInterop.Display`。</span><span class="sxs-lookup"><span data-stu-id="890fc-153">The string stored in `name` is incorporated into a welcome message, which is passed to a second C# method, `ExampleJsInterop.Display`.</span></span>
1. <span data-ttu-id="890fc-154">`Display` 呼叫的 JavaScript 函式， `displayWelcome`，會呈現標題標記的歡迎訊息。</span><span class="sxs-lookup"><span data-stu-id="890fc-154">`Display` calls a JavaScript function, `displayWelcome`, which renders the welcome message into a heading tag.</span></span>

## <a name="capture-references-to-elements"></a><span data-ttu-id="890fc-155">擷取的項目參考</span><span class="sxs-lookup"><span data-stu-id="890fc-155">Capture references to elements</span></span>

<span data-ttu-id="890fc-156">有些[JavaScript interop](xref:razor-components/javascript-interop)案例需要 HTML 項目的參考。</span><span class="sxs-lookup"><span data-stu-id="890fc-156">Some [JavaScript interop](xref:razor-components/javascript-interop) scenarios require references to HTML elements.</span></span> <span data-ttu-id="890fc-157">比方說，UI 程式庫可能需要的項目參考進行初始化，或者您可能需要類似命令的 Api 呼叫項目，例如`focus`或`play`。</span><span class="sxs-lookup"><span data-stu-id="890fc-157">For example, a UI library may require an element reference for initialization, or you might need to call command-like APIs on an element, such as `focus` or `play`.</span></span>

<span data-ttu-id="890fc-158">您可以擷取在元件中的 HTML 項目的參考，加上`ref`屬性的 HTML 項目，然後定義類型的欄位`ElementRef`名稱的值相符`ref`屬性。</span><span class="sxs-lookup"><span data-stu-id="890fc-158">You can capture references to HTML elements in a component by adding a `ref` attribute to the HTML element and then defining a field of type `ElementRef` whose name matches the value of the `ref` attribute.</span></span>

<span data-ttu-id="890fc-159">下列範例會示範擷取使用者名稱輸入項目的參考：</span><span class="sxs-lookup"><span data-stu-id="890fc-159">The following example shows capturing a reference to the username input element:</span></span>

```csharp
<input ref="username" ... />

@functions {
    ElementRef username;
}
```

> [!NOTE]
> <span data-ttu-id="890fc-160">請勿**不**這種方式填入 DOM 中使用擷取的項目參考</span><span class="sxs-lookup"><span data-stu-id="890fc-160">Do **not** use captured element references as a way of populating the DOM.</span></span> <span data-ttu-id="890fc-161">如此一來，可能會干擾宣告式轉譯模型。</span><span class="sxs-lookup"><span data-stu-id="890fc-161">Doing so may interfere with the declarative rendering model.</span></span>

<span data-ttu-id="890fc-162">.NET 程式碼是而言，`ElementRef`是不透明的控制代碼。</span><span class="sxs-lookup"><span data-stu-id="890fc-162">As far as .NET code is concerned, an `ElementRef` is an opaque handle.</span></span> <span data-ttu-id="890fc-163">*只*您可以使用它做一件事是將其傳遞至 JavaScript 程式碼，透過 JavaScript interop。</span><span class="sxs-lookup"><span data-stu-id="890fc-163">The *only* thing you can do with it is pass it through to JavaScript code via JavaScript interop.</span></span> <span data-ttu-id="890fc-164">當您這樣做時，JavaScript 後端程式碼會接收`HTMLElement`執行個體，它可以使用一般的 DOM Api。</span><span class="sxs-lookup"><span data-stu-id="890fc-164">When you do so, the JavaScript-side code receives an `HTMLElement` instance, which it can use with normal DOM APIs.</span></span>

<span data-ttu-id="890fc-165">比方說，下列程式碼會定義.NET 延伸模組方法，以允許將焦點設定在項目：</span><span class="sxs-lookup"><span data-stu-id="890fc-165">For example, the following code defines a .NET extension method that enables setting the focus on an element:</span></span>

<span data-ttu-id="890fc-166">*mylib.js*:</span><span class="sxs-lookup"><span data-stu-id="890fc-166">*mylib.js*:</span></span>

```javascript
window.myLib = {
  focusElement : function (element) {
    element.focus();
  }
}
```

<span data-ttu-id="890fc-167">*ElementRefExtensions.cs*:</span><span class="sxs-lookup"><span data-stu-id="890fc-167">*ElementRefExtensions.cs*:</span></span>

```csharp
using Microsoft.AspNetCore.Blazor;
using Microsoft.JSInterop;
using System.Threading.Tasks;

namespace MyLib
{
    public static class MyLibElementRefExtensions
    {
        public static Task Focus(this ElementRef elementRef)
        {
            return JSRuntime.Current.InvokeAsync<object>("myLib.focusElement", elementRef);
        }
    }
}
```

<span data-ttu-id="890fc-168">接下來是輸入在您的元件之一：</span><span class="sxs-lookup"><span data-stu-id="890fc-168">Now you can focus inputs in any of your components:</span></span>

```cshtml
@using MyLib

<input ref="username" />
<button onclick="@SetFocus">Set focus</button>

@functions {
    ElementRef username;

    void SetFocus()
    {
        username.Focus();
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="890fc-169">`username`元件呈現，並包含其輸出之後，才會填入變數`<input>`項目。</span><span class="sxs-lookup"><span data-stu-id="890fc-169">The `username` variable is only populated after the component renders and its output includes the `<input>` element.</span></span> <span data-ttu-id="890fc-170">如果您嘗試將傳遞擴展`ElementRef`JavaScript 程式碼中，JavaScript 程式碼會接收`null`。</span><span class="sxs-lookup"><span data-stu-id="890fc-170">If you try to pass an unpopulated `ElementRef` to JavaScript code, the JavaScript code receives `null`.</span></span> <span data-ttu-id="890fc-171">若要操作項目參考，該元件已經完成呈現 （若要設定初始焦點的項目上） 的使用之後`OnAfterRenderAsync`或是`OnAfterRender`[元件的生命週期方法](xref:razor-components/components#lifecycle-methods)。</span><span class="sxs-lookup"><span data-stu-id="890fc-171">To manipulate element references after the component has finished rendering (to set the initial focus on an element) use the `OnAfterRenderAsync` or `OnAfterRender` [component lifecycle methods](xref:razor-components/components#lifecycle-methods).</span></span>

## <a name="invoke-net-methods-from-javascript-functions"></a><span data-ttu-id="890fc-172">叫用.NET 方法，從 JavaScript 函式</span><span class="sxs-lookup"><span data-stu-id="890fc-172">Invoke .NET methods from JavaScript functions</span></span>

### <a name="static-net-method-call"></a><span data-ttu-id="890fc-173">靜態的.NET 方法呼叫</span><span class="sxs-lookup"><span data-stu-id="890fc-173">Static .NET method call</span></span>

<span data-ttu-id="890fc-174">若要叫用靜態的.NET 方法，從 JavaScript，請使用`DotNet.invokeMethod`或`DotNet.invokeMethodAsync`函式。</span><span class="sxs-lookup"><span data-stu-id="890fc-174">To invoke a static .NET method from JavaScript, use the `DotNet.invokeMethod` or `DotNet.invokeMethodAsync` functions.</span></span> <span data-ttu-id="890fc-175">在您想要呼叫時，包含函式，以及任何引數的組件名稱的靜態方法的識別碼中傳遞。</span><span class="sxs-lookup"><span data-stu-id="890fc-175">Pass in the identifier of the static method you wish to call, the name of the assembly containing the function, and any arguments.</span></span> <span data-ttu-id="890fc-176">同樣地，非同步版本是以支援伺服器端案例的慣用物件。</span><span class="sxs-lookup"><span data-stu-id="890fc-176">Again, the async version is preferred to support server-side scenarios.</span></span> <span data-ttu-id="890fc-177">若要可叫用 javascript，.NET 方法必須是公用、 靜態的以及與裝飾`[JSInvokable]`。</span><span class="sxs-lookup"><span data-stu-id="890fc-177">To be invokable from JavaScript, the .NET method must be public, static, and decorated with `[JSInvokable]`.</span></span> <span data-ttu-id="890fc-178">根據預設，方法識別項是方法名稱，但您可以指定不同的識別項使用`JSInvokableAttribute`建構函式。</span><span class="sxs-lookup"><span data-stu-id="890fc-178">By default, the method identifier is the method name, but you can specify a different identifier using the `JSInvokableAttribute` constructor.</span></span> <span data-ttu-id="890fc-179">呼叫開放式泛型方法目前不支援。</span><span class="sxs-lookup"><span data-stu-id="890fc-179">Calling open generic methods isn't currently supported.</span></span>

<span data-ttu-id="890fc-180">範例應用程式包含C#方法傳回的陣列`int`s。</span><span class="sxs-lookup"><span data-stu-id="890fc-180">The sample app includes a C# method to return an array of `int`s.</span></span> <span data-ttu-id="890fc-181">方法以裝飾`JSInvokable`屬性。</span><span class="sxs-lookup"><span data-stu-id="890fc-181">The method is decorated with the `JSInvokable` attribute.</span></span>

<span data-ttu-id="890fc-182">*Pages/JsInterop.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="890fc-182">*Pages/JsInterop.cshtml*:</span></span>

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=47&end=58&highlight=7-11)]

<span data-ttu-id="890fc-183">提供給用戶端 JavaScript 叫用C#.NET 方法。</span><span class="sxs-lookup"><span data-stu-id="890fc-183">JavaScript served to the client invokes the C# .NET method.</span></span>

<span data-ttu-id="890fc-184">*wwwroot/exampleJsInterop.js*:</span><span class="sxs-lookup"><span data-stu-id="890fc-184">*wwwroot/exampleJsInterop.js*:</span></span>

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=8-12)]

<span data-ttu-id="890fc-185">當**觸發程序.NET 靜態方法 ReturnArrayAsync**選取按鈕時，檢查在瀏覽器的 web 開發人員工具主控台輸出：</span><span class="sxs-lookup"><span data-stu-id="890fc-185">When the **Trigger .NET static method ReturnArrayAsync** button is selected, examine the console output in the browser's web developer tools:</span></span>

```console
Array(4) [ 1, 2, 3, 4 ]
```

<span data-ttu-id="890fc-186">第四個陣列值推入至的陣列 (`data.push(4);`) 所傳回`ReturnArrayAsync`。</span><span class="sxs-lookup"><span data-stu-id="890fc-186">The fourth array value is pushed to the array (`data.push(4);`) returned by `ReturnArrayAsync`.</span></span>

### <a name="instance-method-call"></a><span data-ttu-id="890fc-187">執行個體方法呼叫</span><span class="sxs-lookup"><span data-stu-id="890fc-187">Instance method call</span></span>

<span data-ttu-id="890fc-188">您也可以從 JavaScript 呼叫.NET 執行個體方法。</span><span class="sxs-lookup"><span data-stu-id="890fc-188">You can also call .NET instance methods from JavaScript.</span></span> <span data-ttu-id="890fc-189">要叫用的.NET 執行個體方法，從 JavaScript，第一次.NET 執行個體傳遞給 JavaScript 藉由包裝在`DotNetObjectRef`執行個體。</span><span class="sxs-lookup"><span data-stu-id="890fc-189">To invoke a .NET instance method from JavaScript, first pass the .NET instance to JavaScript by wrapping it in a `DotNetObjectRef` instance.</span></span> <span data-ttu-id="890fc-190">.NET 執行個體由參考傳遞至 JavaScript，以及您可以叫用執行個體使用的.NET 執行個體方法`invokeMethod`或`invokeMethodAsync`函式。</span><span class="sxs-lookup"><span data-stu-id="890fc-190">The .NET instance is passed by reference to JavaScript, and you can invoke .NET instance methods on the instance using the `invokeMethod` or `invokeMethodAsync` functions.</span></span> <span data-ttu-id="890fc-191">您也可以將.NET 執行個體傳遞做為引數，當叫用 JavaScript 從其他.NET 方法。</span><span class="sxs-lookup"><span data-stu-id="890fc-191">The .NET instance can also be passed as an argument when invoking other .NET methods from JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="890fc-192">範例應用程式會將訊息記錄到用戶端主控台。</span><span class="sxs-lookup"><span data-stu-id="890fc-192">The sample app logs messages to the client-side console.</span></span> <span data-ttu-id="890fc-193">下列範例中所示範的範例應用程式，請檢查瀏覽器的開發人員工具中的瀏覽器的主控台輸出。</span><span class="sxs-lookup"><span data-stu-id="890fc-193">For the following examples demonstrated by the sample app, examine the browser's console output in the browser's developer tools.</span></span>

<span data-ttu-id="890fc-194">當**觸發程序的.NET 執行個體方法 HelloHelper.SayHello**選取按鈕時，`ExampleJsInterop.CallHelloHelperSayHello`呼叫，並將名稱中，傳遞`Blazor`，方法。</span><span class="sxs-lookup"><span data-stu-id="890fc-194">When the **Trigger .NET instance method HelloHelper.SayHello** button is selected, `ExampleJsInterop.CallHelloHelperSayHello` is called and passes a name, `Blazor`, to the method.</span></span>

<span data-ttu-id="890fc-195">*Pages/JsInterop.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="890fc-195">*Pages/JsInterop.cshtml*:</span></span>

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=60&end=69&highlight=8)]

<span data-ttu-id="890fc-196">`CallHelloHelperSayHello` JavaScript 函式會叫用`sayHello`的新執行個體與`HelloHelper`。</span><span class="sxs-lookup"><span data-stu-id="890fc-196">`CallHelloHelperSayHello` invokes the JavaScript function `sayHello` with a new instance of `HelloHelper`.</span></span>

<span data-ttu-id="890fc-197">*JsInteropClasses/ExampleJsInterop.cs*:</span><span class="sxs-lookup"><span data-stu-id="890fc-197">*JsInteropClasses/ExampleJsInterop.cs*:</span></span>

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=19-25)]

<span data-ttu-id="890fc-198">*wwwroot/exampleJsInterop.js*:</span><span class="sxs-lookup"><span data-stu-id="890fc-198">*wwwroot/exampleJsInterop.js*:</span></span>

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=15-17)]

<span data-ttu-id="890fc-199">將名稱傳遞給`HelloHelper`的建構函式，它會設定`HelloHelper.Name`屬性。</span><span class="sxs-lookup"><span data-stu-id="890fc-199">The name is passed to `HelloHelper`'s constructor, which sets the `HelloHelper.Name` property.</span></span> <span data-ttu-id="890fc-200">當 JavaScript 函式`sayHello`執行時，`HelloHelper.SayHello`傳回`Hello, {Name}!`訊息，由 JavaScript 函式寫入至主控台。</span><span class="sxs-lookup"><span data-stu-id="890fc-200">When the JavaScript function `sayHello` is executed, `HelloHelper.SayHello` returns the `Hello, {Name}!` message, which is written to the console by the JavaScript function.</span></span>

<span data-ttu-id="890fc-201">*JsInteropClasses/HelloHelper.cs*:</span><span class="sxs-lookup"><span data-stu-id="890fc-201">*JsInteropClasses/HelloHelper.cs*:</span></span>

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/HelloHelper.cs?name=snippet1&highlight=5,10-11)]

<span data-ttu-id="890fc-202">在瀏覽器的 web 開發人員工具中輸出的主控台：</span><span class="sxs-lookup"><span data-stu-id="890fc-202">Console output in the browser's web developer tools:</span></span>

```console
Hello, Blazor!
```

## <a name="share-interop-code-in-a-razor-component-class-library"></a><span data-ttu-id="890fc-203">共用元件 Razor 類別庫中的 interop 程式碼</span><span class="sxs-lookup"><span data-stu-id="890fc-203">Share interop code in a Razor Component class library</span></span>

<span data-ttu-id="890fc-204">JavaScript interop 程式碼可以包含在 Razor 元件類別庫 (`dotnet new blazorlib`)，這可讓您共用的 NuGet 套件中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="890fc-204">JavaScript interop code can be included in a Razor Component class library (`dotnet new blazorlib`), which allows you to share the code in a NuGet package.</span></span>

<span data-ttu-id="890fc-205">Razor 元件類別程式庫會處理已建置的組件中內嵌的 JavaScript 資源。</span><span class="sxs-lookup"><span data-stu-id="890fc-205">The Razor Component class library handles embedding JavaScript resources in the built assembly.</span></span> <span data-ttu-id="890fc-206">JavaScript 檔案會放置於*wwwroot*資料夾，然後工具會負責建置程式庫時，內嵌資源。</span><span class="sxs-lookup"><span data-stu-id="890fc-206">The JavaScript files are placed in the *wwwroot* folder, and the tooling takes care of embedding the resources when the library is built.</span></span>

<span data-ttu-id="890fc-207">應用程式的專案檔中參考的內建的 NuGet 套件，就像任何標準的 NuGet 套件參考。</span><span class="sxs-lookup"><span data-stu-id="890fc-207">The built NuGet package is referenced in the project file of the app just as any normal NuGet package is referenced.</span></span> <span data-ttu-id="890fc-208">還原應用程式之後，應用程式程式碼可以呼叫 JavaScript，就好像C#。</span><span class="sxs-lookup"><span data-stu-id="890fc-208">After the app has been restored, app code can call into JavaScript as if it were C#.</span></span>
