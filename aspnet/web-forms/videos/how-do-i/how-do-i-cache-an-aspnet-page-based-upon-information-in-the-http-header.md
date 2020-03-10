---
uid: web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
title: '[How Do I：] 依據 HTTP 標頭中的資訊快取 ASP.NET 網頁 |Microsoft Docs'
author: rick-anderson
description: 在這段影片中，Chris Pels 示範如何根據頁面的 HTTP 標頭中的資訊，將頁面保留在 ASP.NET 輸出快取中。 首先，可能的 HTTP 頁首 。
ms.author: riande
ms.date: 02/26/2009
ms.assetid: 0f8df1bd-080a-4eeb-980c-c2fbb05d30c2
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
msc.type: video
ms.openlocfilehash: 79c27f39793a4a3a94ea412838fb3844579e874d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624968"
---
# <a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a>[How Do I：] 依據 HTTP 標頭中的資訊快取 ASP.NET 網頁

依[Chris Pels](https://twitter.com/chrispels)

在這段影片中，Chris Pels 示範如何根據頁面的 HTTP 標頭中的資訊，將頁面保留在 ASP.NET 輸出快取中。 首先，系統會檢查潛在的 HTTP 標頭值。 然後會建立範例頁面，然後使用 OutputCache 指示詞搭配 VaryByHeader 屬性，其中包含值「接受語言」、HTTP 標頭，以根據使用者的瀏覽器語言來控制快取。 範例頁面會在 IE 中看到，它會設定為英文，然後在 FireFox 中設定為使用法文。 最後，會討論將快取定義移至 web.config 檔案中之 CacheProfile 的選項。

[&#9654;觀看影片（12分鐘）](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
