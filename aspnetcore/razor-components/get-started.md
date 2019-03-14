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
# <a name="get-started-with-razor-components"></a>開始使用 Razor 元件

作者：[Daniel Roth](https://github.com/danroth27) 和 [Luke Latham](https://github.com/guardrex)

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

必要條件：

[!INCLUDE[](~/includes/net-core-prereqs-vs-3.0.md)]

若要在 Visual Studio 中建立第一個 Razor 元件專案：

1. 選取 **檔案** > **新專案** > **Web** > **ASP.NET Core Web 應用程式**。
1. 請確定 **.NET Core**並**ASP.NET Core 3.0**選取頂端。
1. 選擇**Razor 元件**範本，然後選取**確定**。

   ![新的應用程式 對話方塊](https://msdnshared.blob.core.windows.net/media/2019/01/razor-components-template.png)

1. 按下 **F5** 即可執行應用程式。

恭喜您！ 您剛剛執行第一個 Razor 元件應用程式 ！

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

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli/)

必要條件：

* [.NET core SDK 3.0 預覽](https://dotnet.microsoft.com/download/dotnet-core/3.0)

1. 若要從命令殼層中建立第一個 Razor 元件專案：

   ```console
   dotnet new razorcomponents -o WebApplication1
   cd WebApplication1
   dotnet run
   ```

1. 在瀏覽器中，巡覽至 `https://localhost:5001`。

恭喜您！ 您剛剛執行第一個 Razor 元件應用程式 ！

---

## <a name="razor-components-project"></a>Razor 元件專案

Razor 元件範本所建立的方案包含兩個專案：

* *WebApplication1.Server* &ndash;伺服器專案是設定裝載 Razor 元件應用程式的 ASP.NET Core 專案。
* *WebApplication1.App* &ndash;使用 Razor 元件在用戶端 web UI 專案。

中的 UI 邏輯*WebApplication1.App*專案分開基於 ASP.NET Core 3.0 Preview 2 的技術限制的應用程式的其餘部分。 Razor 檔案的副檔名 (*.cshtml*) 使用 Razor 元件也會使用 Razor Pages 和 MVC 的檢視。 目前，Razor 元件和 Razor 頁面/MVC 有不同的編譯模型，因此 Razor 元件 Razor 檔案會有所區隔。 在未來的預覽版中，我們打算引進新的檔案副檔名 Razor 元件 (*.razor*)。 將裝載元件、 頁面和檢視*相同的專案中*。

執行應用程式時，多個頁面都是從資訊看板中的索引標籤：

* 首頁
* 計數器
* 擷取資料

在 [計數器] 頁面上，選取 [按我] 按鈕以在不重新整理頁面的情況下讓計數器遞增。 讓網頁中的計數器遞增通常需要撰寫 JavaScript，但 Razor 元件提供一個使用 C# 的更好方法。

*WebApplication1.App/Pages/Counter.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter1.cshtml)]

申請`/counter`在瀏覽器中所指定`@page`指示詞，在頂端，導致計數器元件來呈現其內容。 元件會轉譯成接著可用來更新 UI 富彈性又有效率的方式呈現樹狀結構的記憶體中表示法。

每次**Click me**按鈕已選取：

* `onclick`引發事件。
* 已呼叫 `IncrementCount` 方法。
* `currentCount`會遞增。
* 元件會轉譯一次。

執行階段會比較新的內容來將舊內容，並只會套用已變更的內容與文件物件模型 (DOM)。

您可以將元件加入另一個元件使用 HTML 的類似語法。 元件參數會指定使用屬性或子內容。 比方說，將計數器元件可以加入至應用程式的首頁加`<Counter />`索引元件的項目。

*WebApplication1.App/Pages/Index.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Index1.cshtml?highlight=7)]

執行應用程式。 在首頁上都有它自己的計數器。

若要將參數加入至計數器的元件，更新 元件的`@functions`區塊：

* 新增的屬性`IncrementAmount`附有`[Parameter]`屬性。
* 將 `IncrementCount` 方法變更為在增加 `currentCount`的值時使用 `IncrementAmount`。

*WebApplication1.App/Pages/Counter.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter2.cshtml?highlight=4,8)]

使用屬性在「首頁」元件的 `<Counter>` 元素中指定 `IncrementAmount` 參數。

*WebApplication1.App/Pages/Index.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Index2.cshtml)]

執行應用程式。 在首頁上有它自己的十個在每次增加的計數器**Click me**按鈕已選取。

## <a name="next-steps"></a>後續步驟

<xref:tutorials/first-razor-components-app>
