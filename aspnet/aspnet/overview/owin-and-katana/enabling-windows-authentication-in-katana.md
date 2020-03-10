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
# <a name="enabling-windows-authentication-in-katana"></a>在 Katana 中啟用 Windows 驗證

由[Mike Wasson](https://github.com/MikeWasson)

> 本文說明如何在 Katana 中啟用 Windows 驗證。 其中涵蓋兩個案例：使用 IIS 來裝載 Katana，以及在自訂進程中使用 HttpListener 來自我裝載 Katana。 感謝 Barry Dorrans、David Matson 和 Chris Ross 來審查這篇文章。

Katana 是 Microsoft 的[OWIN](http://owin.org/)，這是適用于 .Net 的開放式 Web 介面。 您可以在[這裡](an-overview-of-project-katana.md)閱讀 OWIN 和 Katana 的簡介。 OWIN 架構有數個層級：

- Host：管理 OWIN 管線執行所在的進程。
- 伺服器：開啟網路通訊端並接聽要求。
- 中介軟體：處理 HTTP 要求和回應。

Katana 目前提供兩部伺服器，兩者都支援 Windows 整合式驗證：

- **Owin. SystemWeb**。 使用 IIS 搭配 ASP.NET 管線。
- **Owin. HttpListener**。 使用[系統 HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)。 此伺服器目前是自我裝載 Katana 時的預設選項。

> [!NOTE]
> Katana 目前未提供適用于 Windows 驗證的 OWIN 中介軟體，因為伺服器中已提供這項功能。

## <a name="windows-authentication-in-iis"></a>IIS 中的 Windows 驗證

使用 SystemWeb 時，您可以直接在 IIS 中啟用 Windows 驗證。

讓我們從使用「ASP.NET Empty Web 應用程式」專案範本建立新的 ASP.NET 應用程式開始。

![](enabling-windows-authentication-in-katana/_static/image1.png)

接下來，新增 NuGet 套件。 從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。 在 [Package Manager Console] 視窗中，輸入下列命令：

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

現在，使用下列程式碼新增名為 `Startup` 的類別：

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

您只需要建立一個 OWIN 的 "Hello world" 應用程式，就可以在 IIS 上執行。 按 F5，進行應用程式偵錯。 您應該會看到「Hello World!」 在瀏覽器視窗中。

![](enabling-windows-authentication-in-katana/_static/image2.png)

接下來，我們將在 IIS Express 中啟用 Windows 驗證。 從 [ **View** ] 功能表中，選取 [**屬性**]。 按一下 方案總管中的專案名稱，以查看專案屬性。

在 [**屬性**] 視窗中，將 [**匿名驗證**]**設定為 [** **已停用**]，並將 [ **Windows 驗證**]

![](enabling-windows-authentication-in-katana/_static/image3.png)

當您從 Visual Studio 執行應用程式時，IIS Express 將需要使用者的 Windows 認證。 您可以使用[Fiddler](http://fiddler2.com/home)或另一個 HTTP 偵錯工具來查看這項工具。 以下是範例 HTTP 回應：

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

在此回應中，WWW 驗證標頭表示伺服器支援使用 Kerberos 或 NTLM 的[Negotiate](http://www.ietf.org/rfc/rfc4559.txt)通訊協定。

之後，當您將應用程式部署至伺服器時，請遵循下列[步驟](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)，在該伺服器上的 IIS 中啟用 Windows 驗證。

## <a name="windows-authentication-in-httplistener"></a>HttpListener 中的 Windows 驗證

如果您使用 HttpListener 來進行自我裝載 Katana，您可以直接在**HttpListener**實例上啟用 Windows 驗證。

首先，建立新的主控台應用程式。 接下來，新增 NuGet 套件。 從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。 在 [Package Manager Console] 視窗中，輸入下列命令：

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

現在，使用下列程式碼新增名為 `Startup` 的類別：

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

這個類別會從之前執行相同的 "Hello world" 範例，但它也會將 Windows 驗證設定為驗證配置。

在 `Main` 函式內，啟動 OWIN 管線：

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

您可以在 Fiddler 中傳送要求，以確認應用程式使用的是 Windows 驗證：

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a>相關主題

[Katana 專案概觀](an-overview-of-project-katana.md)

[System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[瞭解 MVC 5 中的 OWIN 表單驗證](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
