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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617107"
---
# <a name="owin-oauth-20-authorization-server"></a>OWIN OAuth 2.0 授權伺服器

[OAuth 2.0 架構](http://tools.ietf.org/html/rfc6749)可讓協力廠商應用程式取得對 HTTP 服務的有限存取權。 用戶端不會使用資源擁有者的認證來存取受保護的資源，而是會取得存取權杖（這是表示特定範圍、存留期和其他存取屬性的字串）。 授權伺服器會向協力廠商用戶端發出存取權杖，並核准資源擁有者。

OWIN 會定義 .NET web 伺服器和 web 應用程式之間的標準介面。 OWIN 介面的目標是要將伺服器和應用程式分離，鼓勵開發適用于 .NET 網頁程式開發的簡單模組，並藉由成為開放式標準，來促進 .NET 網頁程式開發工具的開放原始碼生態系統。

如需詳細資訊，請參閱[OWIN](http://owin.org/)
