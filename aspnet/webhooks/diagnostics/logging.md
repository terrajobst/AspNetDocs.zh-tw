---
uid: webhooks/diagnostics/logging
title: ASP.NET Webhook 記錄 |Microsoft Docs
author: rick-anderson
description: 如何在 ASP.NET Webhook 中進行記錄。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: a05b32c4a8f9577bcf6170bd19a9e440b1aeb75b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547877"
---
# <a name="aspnet-webhooks-logging"></a>ASP.NET Webhook 記錄

Microsoft ASP.NET Webhook 會使用記錄來報告問題和問題。 根據預設，系統會使用[追蹤](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx)接聽[程式](https://msdn.microsoft.com/library/system.diagnostics.trace)（如任何其他記錄資料流程）來受控記錄檔。

將您的 Web 應用程式部署為 Azure Web 應用程式時，系統會自動挑選記錄，並可與任何其他的[診斷](https://msdn.microsoft.com/library/system.diagnostics.trace)記錄一起管理。 如需詳細資訊，請參閱[在 Azure App Service 中啟用 web 應用程式的診斷記錄功能](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)

此外，您可以直接從 Visual Studio 中取得記錄，如[使用 Visual Studio 針對 Azure App Service 中的 web 應用程式進行疑難排解](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)中所述。

## <a name="redirecting-logs"></a>重新導向記錄

您不需要將記錄[寫入至 system.servicemodel](https://msdn.microsoft.com/library/system.diagnostics.trace)，而是可以提供替代的記錄執行，以便直接登入記錄管理員，例如[Log4Net](http://logging.apache.org/log4net/)和[NLog](http://nlog-project.org/)。 只要提供[ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs)的執行，並向您選擇的相依性插入引擎註冊，就會由 Microsoft ASP.NET webhook 來挑選它。 如需詳細資訊，請參閱[ASP.NET Web API 2 中](https://www.asp.net/web-api/overview/advanced/dependency-injection)的相依性插入。
