---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: 在 Katana 中啟用 Windows 驗證 |Microsoft Docs
author: MikeWasson
description: 本文說明如何在 Katana 中啟用 Windows 驗證。 其中涵蓋兩個案例：使用 IIS 來裝載 Katana，並使用 HttpListener 來進行自我裝載 Kat 。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 3d81e7e1bf13ab63417378fba0c5ab80213f404b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617177"
---
# <a name="enabling-windows-authentication-in-katana"></a><span data-ttu-id="1bda9-104">在 Katana 中啟用 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="1bda9-104">Enabling Windows Authentication in Katana</span></span>

<span data-ttu-id="1bda9-105">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1bda9-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="1bda9-106">本文說明如何在 Katana 中啟用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="1bda9-106">This article shows how to enable Windows Authentication in Katana.</span></span> <span data-ttu-id="1bda9-107">其中涵蓋兩個案例：使用 IIS 來裝載 Katana，以及在自訂進程中使用 HttpListener 來自我裝載 Katana。</span><span class="sxs-lookup"><span data-stu-id="1bda9-107">It covers two scenarios: Using IIS to host Katana, and using HttpListener to self-host Katana in a custom process.</span></span> <span data-ttu-id="1bda9-108">感謝 Barry Dorrans、David Matson 和 Chris Ross 來審查這篇文章。</span><span class="sxs-lookup"><span data-stu-id="1bda9-108">Thanks to Barry Dorrans, David Matson, and Chris Ross for reviewing this article.</span></span>

<span data-ttu-id="1bda9-109">Katana 是 Microsoft 的[OWIN](http://owin.org/)，這是適用于 .Net 的開放式 Web 介面。</span><span class="sxs-lookup"><span data-stu-id="1bda9-109">Katana is Microsoft's implementation of [OWIN](http://owin.org/), the Open Web Interface for .NET.</span></span> <span data-ttu-id="1bda9-110">您可以在[這裡](an-overview-of-project-katana.md)閱讀 OWIN 和 Katana 的簡介。</span><span class="sxs-lookup"><span data-stu-id="1bda9-110">You can read an introduction to OWIN and Katana [here](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="1bda9-111">OWIN 架構有數個層級：</span><span class="sxs-lookup"><span data-stu-id="1bda9-111">The OWIN architecture has several layers:</span></span>

- <span data-ttu-id="1bda9-112">Host：管理 OWIN 管線執行所在的進程。</span><span class="sxs-lookup"><span data-stu-id="1bda9-112">Host: Manages the process in which the OWIN pipeline runs.</span></span>
- <span data-ttu-id="1bda9-113">伺服器：開啟網路通訊端並接聽要求。</span><span class="sxs-lookup"><span data-stu-id="1bda9-113">Server: Opens a network socket and listens for requests.</span></span>
- <span data-ttu-id="1bda9-114">中介軟體：處理 HTTP 要求和回應。</span><span class="sxs-lookup"><span data-stu-id="1bda9-114">Middleware: Processes the HTTP request and response.</span></span>

<span data-ttu-id="1bda9-115">Katana 目前提供兩部伺服器，兩者都支援 Windows 整合式驗證：</span><span class="sxs-lookup"><span data-stu-id="1bda9-115">Katana currently provides two servers, both of which support Windows Integrated Authentication:</span></span>

- <span data-ttu-id="1bda9-116">**Owin. SystemWeb**。</span><span class="sxs-lookup"><span data-stu-id="1bda9-116">**Microsoft.Owin.Host.SystemWeb**.</span></span> <span data-ttu-id="1bda9-117">使用 IIS 搭配 ASP.NET 管線。</span><span class="sxs-lookup"><span data-stu-id="1bda9-117">Uses IIS with the ASP.NET pipeline.</span></span>
- <span data-ttu-id="1bda9-118">**Owin. HttpListener**。</span><span class="sxs-lookup"><span data-stu-id="1bda9-118">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="1bda9-119">使用[系統 HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1bda9-119">Uses [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx).</span></span> <span data-ttu-id="1bda9-120">此伺服器目前是自我裝載 Katana 時的預設選項。</span><span class="sxs-lookup"><span data-stu-id="1bda9-120">This server is currently the default option when self-hosting Katana.</span></span>

> [!NOTE]
> <span data-ttu-id="1bda9-121">Katana 目前未提供適用于 Windows 驗證的 OWIN 中介軟體，因為伺服器中已提供這項功能。</span><span class="sxs-lookup"><span data-stu-id="1bda9-121">Katana does not currently provide OWIN middleware for Windows Authentication, because this functionality is already available in the servers.</span></span>

## <a name="windows-authentication-in-iis"></a><span data-ttu-id="1bda9-122">IIS 中的 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="1bda9-122">Windows Authentication in IIS</span></span>

<span data-ttu-id="1bda9-123">使用 SystemWeb 時，您可以直接在 IIS 中啟用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="1bda9-123">Using Microsoft.Owin.Host.SystemWeb, you can simply enable Windows Authentication in IIS.</span></span>

<span data-ttu-id="1bda9-124">讓我們從使用「ASP.NET Empty Web 應用程式」專案範本建立新的 ASP.NET 應用程式開始。</span><span class="sxs-lookup"><span data-stu-id="1bda9-124">Let's start by creating a new ASP.NET application, using the "ASP.NET Empty Web Application" project template.</span></span>

![](enabling-windows-authentication-in-katana/_static/image1.png)

<span data-ttu-id="1bda9-125">接下來，新增 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="1bda9-125">Next, add NuGet packages.</span></span> <span data-ttu-id="1bda9-126">從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="1bda9-126">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="1bda9-127">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="1bda9-127">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

<span data-ttu-id="1bda9-128">現在，使用下列程式碼新增名為 `Startup` 的類別：</span><span class="sxs-lookup"><span data-stu-id="1bda9-128">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

<span data-ttu-id="1bda9-129">您只需要建立一個 OWIN 的 "Hello world" 應用程式，就可以在 IIS 上執行。</span><span class="sxs-lookup"><span data-stu-id="1bda9-129">That's all you need to create a "Hello world" application for OWIN, running on IIS.</span></span> <span data-ttu-id="1bda9-130">按 F5，進行應用程式偵錯。</span><span class="sxs-lookup"><span data-stu-id="1bda9-130">Press F5 to debug the application.</span></span> <span data-ttu-id="1bda9-131">您應該會看到「Hello World!」</span><span class="sxs-lookup"><span data-stu-id="1bda9-131">You should see "Hello World!"</span></span> <span data-ttu-id="1bda9-132">在瀏覽器視窗中。</span><span class="sxs-lookup"><span data-stu-id="1bda9-132">in the browser window.</span></span>

![](enabling-windows-authentication-in-katana/_static/image2.png)

<span data-ttu-id="1bda9-133">接下來，我們將在 IIS Express 中啟用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="1bda9-133">Next, we'll enable Windows Authentication in IIS Express.</span></span> <span data-ttu-id="1bda9-134">從 [ **View** ] 功能表中，選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="1bda9-134">From the **View** menu, select **Properties**.</span></span> <span data-ttu-id="1bda9-135">按一下 方案總管中的專案名稱，以查看專案屬性。</span><span class="sxs-lookup"><span data-stu-id="1bda9-135">Click on the project name in Solution Explorer to view the project properties.</span></span>

<span data-ttu-id="1bda9-136">在 [**屬性**] 視窗中，將 [**匿名驗證**]**設定為 [** **已停用**]，並將 [ **Windows 驗證**]</span><span class="sxs-lookup"><span data-stu-id="1bda9-136">In the **Properties** window, set **Anonymous Authentication** to **Disabled** and set **Windows Authentication** to **Enabled**.</span></span>

![](enabling-windows-authentication-in-katana/_static/image3.png)

<span data-ttu-id="1bda9-137">當您從 Visual Studio 執行應用程式時，IIS Express 將需要使用者的 Windows 認證。</span><span class="sxs-lookup"><span data-stu-id="1bda9-137">When you run the application from Visual Studio, IIS Express will require the user's Windows credentials.</span></span> <span data-ttu-id="1bda9-138">您可以使用[Fiddler](http://fiddler2.com/home)或另一個 HTTP 偵錯工具來查看這項工具。</span><span class="sxs-lookup"><span data-stu-id="1bda9-138">You can see this by using [Fiddler](http://fiddler2.com/home) or another HTTP debugging tool.</span></span> <span data-ttu-id="1bda9-139">以下是範例 HTTP 回應：</span><span class="sxs-lookup"><span data-stu-id="1bda9-139">Here is an example HTTP response:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

<span data-ttu-id="1bda9-140">在此回應中，WWW 驗證標頭表示伺服器支援使用 Kerberos 或 NTLM 的[Negotiate](http://www.ietf.org/rfc/rfc4559.txt)通訊協定。</span><span class="sxs-lookup"><span data-stu-id="1bda9-140">The WWW-Authenticate headers in this response indicate that the server supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) protocol, which uses either Kerberos or NTLM.</span></span>

<span data-ttu-id="1bda9-141">之後，當您將應用程式部署至伺服器時，請遵循下列[步驟](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)，在該伺服器上的 IIS 中啟用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="1bda9-141">Later, when you deploy the application to a server, follow [these steps](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) to enable Windows Authentication in IIS on that server.</span></span>

## <a name="windows-authentication-in-httplistener"></a><span data-ttu-id="1bda9-142">HttpListener 中的 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="1bda9-142">Windows Authentication in HttpListener</span></span>

<span data-ttu-id="1bda9-143">如果您使用 HttpListener 來進行自我裝載 Katana，您可以直接在**HttpListener**實例上啟用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="1bda9-143">If you are using Microsoft.Owin.Host.HttpListener to self-host Katana, you can enable Windows Authentication directly on the **HttpListener** instance.</span></span>

<span data-ttu-id="1bda9-144">首先，建立新的主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1bda9-144">First, create a new console application.</span></span> <span data-ttu-id="1bda9-145">接下來，新增 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="1bda9-145">Next, add NuGet packages.</span></span> <span data-ttu-id="1bda9-146">從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="1bda9-146">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="1bda9-147">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="1bda9-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

<span data-ttu-id="1bda9-148">現在，使用下列程式碼新增名為 `Startup` 的類別：</span><span class="sxs-lookup"><span data-stu-id="1bda9-148">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

<span data-ttu-id="1bda9-149">這個類別會從之前執行相同的 "Hello world" 範例，但它也會將 Windows 驗證設定為驗證配置。</span><span class="sxs-lookup"><span data-stu-id="1bda9-149">This class implements the same "Hello world" example from before, but it also sets Windows Authentication as the authentication scheme.</span></span>

<span data-ttu-id="1bda9-150">在 `Main` 函式內，啟動 OWIN 管線：</span><span class="sxs-lookup"><span data-stu-id="1bda9-150">Inside the `Main` function, start the OWIN pipeline:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

<span data-ttu-id="1bda9-151">您可以在 Fiddler 中傳送要求，以確認應用程式使用的是 Windows 驗證：</span><span class="sxs-lookup"><span data-stu-id="1bda9-151">You can send a request in Fiddler to confirm that the application is using Windows Authentication:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a><span data-ttu-id="1bda9-152">相關主題</span><span class="sxs-lookup"><span data-stu-id="1bda9-152">Related Topics</span></span>

[<span data-ttu-id="1bda9-153">Katana 專案概觀</span><span class="sxs-lookup"><span data-stu-id="1bda9-153">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)

[<span data-ttu-id="1bda9-154">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="1bda9-154">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[<span data-ttu-id="1bda9-155">瞭解 MVC 5 中的 OWIN 表單驗證</span><span class="sxs-lookup"><span data-stu-id="1bda9-155">Understanding OWIN Forms Authentication in MVC 5</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
