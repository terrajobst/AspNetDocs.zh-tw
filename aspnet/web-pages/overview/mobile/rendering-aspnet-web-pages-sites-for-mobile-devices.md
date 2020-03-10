---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: 行動裝置的轉譯 ASP.NET Web Pages （Razor）網站 |Microsoft Docs
author: Rick-Anderson
description: 本文說明如何在 ASP.NET Web Pages （Razor）網站中建立會在行動裝置上適當呈現的頁面。 您將瞭解的內容：如何 。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: c012348d65e48a275cb0e4808fef2a7f31e5fb33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563564"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a>行動裝置的轉譯 ASP.NET Web Pages （Razor）網站

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何在 ASP.NET Web Pages （Razor）網站中建立會在行動裝置上適當呈現的頁面。
> 
> 您將學到什麼：
> 
> - 如何使用命名慣例來指定頁面專為行動裝置所設計。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）3
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 2。

ASP.NET Web Pages 可讓您建立自訂顯示，以在行動裝置或其他裝置上呈現內容。

在 ASP.NET Web Pages 網站中建立裝置特定頁面的最簡單方式，就是使用檔案命名模式，如下所示： *FileName.* . #。 您可以建立兩個版本的網頁（例如，一個名稱為*myfile.txt* ，另一個名為*myfile.txt*）。 在執行時間，當行動裝置要求*myfile.txt*時，ASP.NET 會從*myfile.txt*呈現內容。 否則，會呈現*myfile.txt* 。

下列範例顯示如何藉由新增行動裝置的內容頁面來啟用行動轉譯。 *Page1. cshtml*包含內容以及導覽提要欄位。 *Page1*包含相同的內容，但省略提要欄位。

1. 在 ASP.NET Web Pages 網站中，建立名為*Page1. cshtml*的檔案，並以下列標記取代目前的內容。

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. 建立名為*Page1*的檔案，並以下列標記取代現有的內容。 請注意，行動版的頁面會省略流覽區段，以便在較小的螢幕上進行更佳的轉譯。

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. 執行桌面瀏覽器並流覽至*Page1. cshtml*。 ![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)
4. 執行行動瀏覽器（或行動裝置模擬器）並流覽至*Page1. cshtml*。 （請注意，您不會包含*mobile* 。 作為 URL 的一部分）。即使要求是*page1. cshtml*，ASP.NET 還是會呈現*page1*。

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> 若要測試行動頁面，您可以使用在桌上型電腦上執行的行動裝置模擬器。 這項工具可讓您測試網頁在行動裝置上的外觀（也就是，通常會有更小的顯示區域）。 其中一個模擬器範例是 Mozilla Firefox 的[使用者代理程式切換器附加](http://addons.mozilla.org/firefox/addon/user-agent-switcher/)元件，可讓您從桌上出版本的 firefox 模擬各種行動瀏覽器。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

[Windows Phone 模擬器](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)
