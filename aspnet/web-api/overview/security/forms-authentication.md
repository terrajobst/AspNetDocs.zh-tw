---
uid: web-api/overview/security/forms-authentication
title: ASP.NET Web API 中的表單驗證 |Microsoft Docs
author: MikeWasson
description: 描述在 ASP.NET Web API 中使用表單驗證。
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 147bfab76e48497f35a72b28cd935f40ec4193bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598592"
---
# <a name="forms-authentication-in-aspnet-web-api"></a>ASP.NET Web API 中的表單驗證

由[Mike Wasson](https://github.com/MikeWasson)

表單驗證會使用 HTML 表單，將使用者的認證傳送給伺服器。 這不是網際網路標準。 表單驗證僅適用于從 web 應用程式呼叫的 web Api，讓使用者可以與 HTML 表單進行互動。

| 優點 | 缺點 |
| --- | --- |
| -易於執行：內建于 ASP.NET 中。 -使用 ASP.NET 成員資格提供者，這可讓您輕鬆地管理使用者帳戶。 | -不是標準 HTTP 驗證機制;會使用 HTTP cookie，而不是標準的授權標頭。 -需要瀏覽器用戶端。 -認證會以純文字傳送。 -容易遭受跨網站偽造要求（CSRF）;需要反 CSRF 量值。 -不容易從 nonbrowser 用戶端使用。 登入需要瀏覽器。 -使用者認證會在要求中傳送。 -某些使用者停用 cookie。 |

簡單地說，ASP.NET 中的表單驗證的運作方式如下所示：

1. 用戶端會要求需要驗證的資源。
2. 如果使用者未經過驗證，伺服器會傳回 HTTP 302 （找到）並重新導向至登入頁面。
3. 使用者輸入認證並提交表單。
4. 伺服器會傳回另一個 HTTP 302，以重新導向回原始 URI。 此回應包含驗證 cookie。
5. 用戶端再次要求資源。 此要求包含驗證 cookie，因此伺服器會授與要求。

![](forms-authentication/_static/image1.png)

如需詳細資訊，請參閱[表單驗證的總覽。](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)

## <a name="using-forms-authentication-with-web-api"></a>使用表單驗證搭配 Web API

若要建立使用表單驗證的應用程式，請在 MVC 4 專案嚮導中選取 [網際網路應用程式] 範本。 此範本會建立用於管理帳戶的 MVC 控制器。 您也可以使用 ASP.NET 秋季2012更新中所提供的「單一頁面應用程式」範本。

在 Web API 控制器中，您可以使用 `[Authorize]` 屬性來限制存取，如[使用 [授權] 屬性](authentication-and-authorization-in-aspnet-web-api.md#auth3)中所述。

表單驗證會使用會話 cookie 來驗證要求。 瀏覽器會自動將所有相關的 cookie 傳送至目的地網站。 這項功能讓表單驗證可能容易遭受跨網站偽造要求（CSRF）攻擊，請參閱[防止跨網站偽造要求（CSRF）攻擊](preventing-cross-site-request-forgery-csrf-attacks.md)。

表單驗證不會加密使用者的認證。 因此，除非搭配 SSL 使用，否則表單驗證並不安全。 請參閱[在 WEB API 中使用 SSL](working-with-ssl-in-web-api.md)。
