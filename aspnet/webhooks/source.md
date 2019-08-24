---
uid: webhooks/source
title: ASP.NET Webhook 原始程式碼和 NuGet 套件 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 原始程式碼和 NuGet 套件的連結
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: 8d07848754d9efda9c893b8ba54ac6d0c0214a53
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000707"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET Webhook 原始程式碼和 NuGet 套件

Microsoft ASP.NET Webhook 是 Microsoft ASP.NET 系列模組的一部分, 並裝載為[GitHub 上的開放原始碼專案](https://github.com/aspnet/WebHooks)。 這表示我們接受貢獻, 但在提交提取要求之前, 請先查看[貢獻方針](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)。

您目前閱讀的線上檔也會以[開放原始碼的形式裝載在 GitHub 上](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide), 也會接受貢獻。

## <a name="nuget-packages"></a>NuGet 套件

[NuGet 套件](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)分為三個部分:

* [常見](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common):在寄件者和接收者之間共用的通用封裝。

* [寄件者](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom):一組支援將您自己的 Webhook 傳送給其他人的封裝。 傳送[webhook](sending/senders.md)中會更詳細地說明傳送 webhook 的功能。

* [接收者](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers):一組支援接收其他人 Webhook 的套件。 接收 Webhook 的功能會在[接收 webhook](receiving/index.md)中有更詳細的說明。
