---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 授權伺服器 |Microsoft Docs
author: hongyes
description: 本教學課程將引導您瞭解如何使用 OWIN OAuth 中介軟體來執行 OAuth 2.0 授權伺服器。 這是只有 outlin 的先進教學課程 。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: 39c78ee57f791a94af7a5fb66c3ac42d7239760f
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000677"
---
# <a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="8e3b3-104">OWIN OAuth 2.0 授權伺服器</span><span class="sxs-lookup"><span data-stu-id="8e3b3-104">OWIN OAuth 2.0 Authorization Server</span></span>

<span data-ttu-id="8e3b3-105">[OAuth 2.0 架構](http://tools.ietf.org/html/rfc6749)可讓協力廠商應用程式取得對 HTTP 服務的有限存取權。</span><span class="sxs-lookup"><span data-stu-id="8e3b3-105">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="8e3b3-106">用戶端不會使用資源擁有者的認證來存取受保護的資源, 而是會取得存取權杖 (這是表示特定範圍、存留期和其他存取屬性的字串)。</span><span class="sxs-lookup"><span data-stu-id="8e3b3-106">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="8e3b3-107">授權伺服器會向協力廠商用戶端發出存取權杖, 並核准資源擁有者。</span><span class="sxs-lookup"><span data-stu-id="8e3b3-107">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="8e3b3-108">OWIN 會定義 .NET web 伺服器和 web 應用程式之間的標準介面。</span><span class="sxs-lookup"><span data-stu-id="8e3b3-108">OWIN defines a standard interface between .NET web servers and web applications.</span></span> <span data-ttu-id="8e3b3-109">OWIN 介面的目標是要將伺服器和應用程式分離, 鼓勵開發適用于 .NET 網頁程式開發的簡單模組, 並藉由成為開放式標準, 來促進 .NET 網頁程式開發工具的開放原始碼生態系統。</span><span class="sxs-lookup"><span data-stu-id="8e3b3-109">The goal of the OWIN interface is to decouple server and application, encourage the development of simple modules for .NET web development, and, by being an open standard, stimulate the open source ecosystem of .NET web development tools.</span></span>

<span data-ttu-id="8e3b3-110">如需詳細資訊, 請參閱[OWIN](http://owin.org/)</span><span class="sxs-lookup"><span data-stu-id="8e3b3-110">For more information, see [OWIN](http://owin.org/)</span></span>
