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
# <a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a><span data-ttu-id="965a4-104">[How Do I：]根據自訂資訊控制 ASP.NET 網頁的快取</span><span class="sxs-lookup"><span data-stu-id="965a4-104">[How Do I:] Control the Caching of an ASP.NET Page Based Upon Custom Information</span></span>

<span data-ttu-id="965a4-105">依[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="965a4-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="965a4-106">在這段影片中，Chris Pels 示範如何根據自訂資訊來控制快取 ASP.NET 網頁的準則。</span><span class="sxs-lookup"><span data-stu-id="965a4-106">In this video Chris Pels shows how to control the criteria for caching an ASP.NET page based upon custom information.</span></span> <span data-ttu-id="965a4-107">隨即建立範例頁面，然後使用 OutputCache 指示詞搭配包含自訂值的 VaryByCustom 屬性。</span><span class="sxs-lookup"><span data-stu-id="965a4-107">A sample page is created and then the OutputCache directive is used with the VaryByCustom attribute which contains a custom value.</span></span> <span data-ttu-id="965a4-108">接下來，在提供自訂屬性處理的 global.asax 模組中，會覆寫 GetVaryCustomByString （）方法。</span><span class="sxs-lookup"><span data-stu-id="965a4-108">Next, the GetVaryCustomByString() method is overridden in the global.asax module which provides the handling of the custom attribute.</span></span> <span data-ttu-id="965a4-109">在該方法中，會傳回可唯一識別頁面快取版本的字串。</span><span class="sxs-lookup"><span data-stu-id="965a4-109">In that method a string is returned that uniquely identifies the cached version of the page.</span></span> <span data-ttu-id="965a4-110">最後，我們會討論如何使用自訂值的快取，以數種方式來使用網站。</span><span class="sxs-lookup"><span data-stu-id="965a4-110">Finally, there is a discussion about how caching using a custom value can be used in several ways for a web site.</span></span>

[<span data-ttu-id="965a4-111">&#9654;觀看影片（12分鐘）</span><span class="sxs-lookup"><span data-stu-id="965a4-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
