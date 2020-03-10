---
uid: web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
title: '[How Do I：]根據自訂資訊控制 ASP.NET 網頁的快取 |Microsoft Docs'
author: rick-anderson
description: 在這段影片中，Chris Pels 示範如何根據自訂資訊來控制快取 ASP.NET 網頁的準則。 隨即建立範例頁面，然後將 [O ...]
ms.author: riande
ms.date: 02/19/2009
ms.assetid: f230c316-1313-4b8f-967c-62f9684fe378
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
msc.type: video
ms.openlocfilehash: 676bc8f234a6e517104d07fd58a0ff14aec73e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624730"
---
# <a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a>[How Do I：]根據自訂資訊控制 ASP.NET 網頁的快取

依[Chris Pels](https://twitter.com/chrispels)

在這段影片中，Chris Pels 示範如何根據自訂資訊來控制快取 ASP.NET 網頁的準則。 隨即建立範例頁面，然後使用 OutputCache 指示詞搭配包含自訂值的 VaryByCustom 屬性。 接下來，在提供自訂屬性處理的 global.asax 模組中，會覆寫 GetVaryCustomByString （）方法。 在該方法中，會傳回可唯一識別頁面快取版本的字串。 最後，我們會討論如何使用自訂值的快取，以數種方式來使用網站。

[&#9654;觀看影片（12分鐘）](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
