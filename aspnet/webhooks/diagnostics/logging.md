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
# <a name="aspnet-webhooks-logging"></a><span data-ttu-id="1b93b-103">ASP.NET Webhook 記錄</span><span class="sxs-lookup"><span data-stu-id="1b93b-103">ASP.NET WebHooks logging</span></span>

<span data-ttu-id="1b93b-104">Microsoft ASP.NET Webhook 會使用記錄來報告問題和問題。</span><span class="sxs-lookup"><span data-stu-id="1b93b-104">Microsoft ASP.NET WebHooks uses logging as a way of reporting issues and problems.</span></span> <span data-ttu-id="1b93b-105">根據預設，系統會使用[追蹤](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx)接聽[程式](https://msdn.microsoft.com/library/system.diagnostics.trace)（如任何其他記錄資料流程）來受控記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1b93b-105">By default logs are written using [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) where they can be manged using [Trace Listeners](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) like any other log stream.</span></span>

<span data-ttu-id="1b93b-106">將您的 Web 應用程式部署為 Azure Web 應用程式時，系統會自動挑選記錄，並可與任何其他的[診斷](https://msdn.microsoft.com/library/system.diagnostics.trace)記錄一起管理。</span><span class="sxs-lookup"><span data-stu-id="1b93b-106">When deploying your Web Application as an Azure Web App, the logs are automatically picked up and can be managed together with any other [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) logging.</span></span> <span data-ttu-id="1b93b-107">如需詳細資訊，請參閱[在 Azure App Service 中啟用 web 應用程式的診斷記錄功能](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span><span class="sxs-lookup"><span data-stu-id="1b93b-107">For details, please see [Enable diagnostics logging for web apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span></span>

<span data-ttu-id="1b93b-108">此外，您可以直接從 Visual Studio 中取得記錄，如[使用 Visual Studio 針對 Azure App Service 中的 web 應用程式進行疑難排解](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)中所述。</span><span class="sxs-lookup"><span data-stu-id="1b93b-108">In addition, logs can be obtained straight from inside Visual Studio as described in [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="redirecting-logs"></a><span data-ttu-id="1b93b-109">重新導向記錄</span><span class="sxs-lookup"><span data-stu-id="1b93b-109">Redirecting Logs</span></span>

<span data-ttu-id="1b93b-110">您不需要將記錄[寫入至 system.servicemodel](https://msdn.microsoft.com/library/system.diagnostics.trace)，而是可以提供替代的記錄執行，以便直接登入記錄管理員，例如[Log4Net](http://logging.apache.org/log4net/)和[NLog](http://nlog-project.org/)。</span><span class="sxs-lookup"><span data-stu-id="1b93b-110">Instead of writing logs to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace), it is possible to provide an alternate logging implementation that can log directly to a log manager such as [Log4Net](http://logging.apache.org/log4net/) and [NLog](http://nlog-project.org/).</span></span> <span data-ttu-id="1b93b-111">只要提供[ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs)的執行，並向您選擇的相依性插入引擎註冊，就會由 Microsoft ASP.NET webhook 來挑選它。</span><span class="sxs-lookup"><span data-stu-id="1b93b-111">Simply provide an implementation of [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) and register it with a dependency injection engine of your choice and it will get picked up by Microsoft ASP.NET WebHooks.</span></span> <span data-ttu-id="1b93b-112">如需詳細資訊，請參閱[ASP.NET Web API 2 中](https://www.asp.net/web-api/overview/advanced/dependency-injection)的相依性插入。</span><span class="sxs-lookup"><span data-stu-id="1b93b-112">Please see [Dependency Injection in ASP.NET Web API 2](https://www.asp.net/web-api/overview/advanced/dependency-injection) for details.</span></span>
