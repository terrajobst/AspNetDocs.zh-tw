---
ms.openlocfilehash: b6f39dd0dedb38961eb021cde355f7ec83283195
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024865"
---
# <a name="aspnet-core-web-api-controller-sample"></a>ASP.NET Core Web API 控制器範例

此範例應用程式包含下列專案：

- **WebApiSample.Api.22*:ASP.NET Core 2.2 專案，目標為.NET Core 2.2。
- **WebApiSample.Api.21**:ASP.NET Core 2.1 的專案，目標為.NET Core 2.1。
- **WebApiSample.Api.Pre21**:以.NET Core 2.0 為目標的 ASP.NET Core 2.0 專案。
- **WebApiSample.DataAccess**:.NET Standard 2.0 類別庫做為資料存取層的 2 個 Web API 專案。

本範例說明建立 Web API 控制器的各種方式：

- [來自 ControllerBase 的衍生類別](https://docs.microsoft.com/aspnet/core/web-api#derive-class-from-controllerbase)
- [以 ApiControllerAttribute 標註類別](https://docs.microsoft.com/aspnet/core/web-api#annotate-class-with-apicontrollerattribute)
