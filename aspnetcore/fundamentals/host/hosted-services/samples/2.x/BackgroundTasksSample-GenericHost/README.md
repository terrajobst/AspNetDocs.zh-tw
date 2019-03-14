---
ms.openlocfilehash: 6b2bc386ec179e786de205af0ca6dbd610e000d9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056485"
---
# <a name="aspnet-core-background-tasks-sample-generic-host"></a>ASP.NET Core 背景工作範例 (泛型主機)

此範例說明如何使用 [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice)。 這個範例會示範[在 ASP.NET Core 中使用託管服務的背景工作](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services)主題中所述的功能。

在 [Visual Studio Code](https://code.visualstudio.com/) 中執行範例時，請將 *.vscode/launch.json* 中主控台設定的 **console** 值設定成 `externalTerminal` 或 `integratedTerminal`。 使用 `internalConsole` 會不相容於應用程式用於將背景工作項目加入佇列的按鍵輸入。
