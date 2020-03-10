---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: 在 ASP.NET Web Pages （Razor）網站中包裝和縮小資產 |Microsoft Docs
author: microsoft
description: 配套和縮制是讓您的網站更快速的方式。 配套可讓您結合多個 JavaScript （.js）檔案或多個級聯樣式表（。
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 5e42111ad71ec65581e56c73822e23ecd5fcbd58
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78635706"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="2af32-104">在 ASP.NET Web Pages (Razor) 網站中統合及縮小資產</span><span class="sxs-lookup"><span data-stu-id="2af32-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="2af32-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2af32-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="2af32-106">配套和縮制是讓您的網站更快速的方式。</span><span class="sxs-lookup"><span data-stu-id="2af32-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="2af32-107">「配套」可讓您結合多個 JavaScript （ *.js*）檔案或多個級聯樣式表（ *.css*）檔案，讓它們可以當做一個單位下載，而不是一次。</span><span class="sxs-lookup"><span data-stu-id="2af32-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="2af32-108">縮制 squeezes 空白字元並執行其他類型的壓縮，讓下載的檔案變得越小。</span><span class="sxs-lookup"><span data-stu-id="2af32-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="2af32-109">ASP.NET Web Pages 2 的 RC 版本不支援配套和縮制，因為包含必要元素的套件尚未在 Microsoft WebMatrix 中提供。</span><span class="sxs-lookup"><span data-stu-id="2af32-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="2af32-110">很抱歉造成您的不便。</span><span class="sxs-lookup"><span data-stu-id="2af32-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="2af32-111">套件預期會在 ASP.NET Web Pages 2 和 WebMatrix 2 的最終版本中提供。</span><span class="sxs-lookup"><span data-stu-id="2af32-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
