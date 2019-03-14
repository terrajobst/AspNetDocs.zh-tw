---
ms.openlocfilehash: eb2f83504129ae2b19ff5d85a2bc7d90293b43d6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043395"
---
* Startup.cs:[啟動類別](xref:fundamentals/startup)-類別會設定要求管線來處理對應用程式的所有要求。
* Program.cs:[程式類別](xref:fundamentals/index)，其中包含應用程式的主要進入點。
* firstapp.csproj :[專案檔](/dotnet/articles/core/preview3/tools/csproj)ASP.NET Core 應用程式的 MSBuild 專案檔案格式。 包含專案對專案參考 NuGet 參考和其他專案相關的項目。
* appsettings.json / appsettings。Development.json:環境基底的應用程式設定設定檔。 [請參閱組態](xref:fundamentals/configuration/index)。
* bower.json:Bower 套件專案的相依性。
* .bowerrc:Bower 組態檔會定義當 Bower 下載資產時，安裝元件的位置。
* bundleconfig.json： 統合及縮小前端 JavaScript 和 CSS 的資產的組態檔。
* 檢視：包含 Razor 檢視。 檢視是顯示應用程式使用者介面 (UI) 的元件。 一般而言，此 UI 會顯示模型資料。
* 控制站：一開始包含 MVC 控制器*HomeController.cs*。 控制器是處理瀏覽器要求的類別。
* wwwroot:Web 應用程式根資料夾。

如需詳細資訊，請參閱[MVC 模式](xref:mvc/overview)。
