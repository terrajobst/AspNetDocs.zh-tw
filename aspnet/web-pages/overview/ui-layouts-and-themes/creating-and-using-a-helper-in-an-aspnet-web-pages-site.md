---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: 在 ASP.NET Web Pages （Razor）網站中建立和使用 Helper |Microsoft Docs
author: Rick-Anderson
description: 本文說明如何在 ASP.NET Web Pages （Razor）網站中建立協助程式。 Helper 是可重複使用的元件，其中包含程式碼和標記到效能 。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 380663951094c9fc7d5f0601e30995fa073a204b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563508"
---
# <a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a>在 ASP.NET Web Pages （Razor）網站中建立和使用 Helper

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何在 ASP.NET Web Pages （Razor）網站中建立協助程式。 *Helper*是可重複使用的元件，其中包含程式碼和標記來執行可能單調乏味或複雜的工作。
> 
> **您將瞭解的內容：** 
> 
> - 如何建立和使用簡單的 helper。
> 
> 以下是文章中引進的 ASP.NET 功能：
> 
> - `@helper` 語法。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）3
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 2。

## <a name="overview-of-helpers"></a>協助程式總覽

如果您需要在網站中的不同頁面上執行相同的工作，您可以使用 helper。 ASP.NET Web Pages 包含一些協助程式，還有更多您可以下載和安裝的資訊。 （ASP.NET Web Pages 中的內建協助程式清單列在[ASP.NET API 快速參考](https://go.microsoft.com/fwlink/?LinkId=202907)中）。如果現有的協助程式都不符合您的需求，您可以建立自己的 helper。

協助程式可讓您在多個頁面上使用通用的程式碼區塊。 假設在您的頁面中，您通常會想要建立與一般段落分開設定的便箋專案。 可能會將便箋建立為 `<div>` 元素，而此專案的樣式為具有框線的方塊。 您不需要在每次想要顯示附注時，將這個相同標記新增至頁面，而是可以將標記封裝為 helper。 然後您就可以在任何需要的地方插入含有一行程式碼的附注。

使用這樣的協助程式，可讓每個頁面中的程式碼更簡單且更容易閱讀。 它也可讓您更輕鬆地維護您的網站，因為如果您需要變更便箋的外觀，您可以在同一個位置變更標記。

## <a name="creating-a-helper"></a>建立 Helper

此程式會示範如何建立協助程式，以依照剛才所述的方式建立附注。 這是一個簡單的範例，但是自訂 helper 可以包含您所需的任何標記和 ASP.NET 程式碼。

1. 在網站的根資料夾中，建立名為 App 的資料夾 *\_程式碼*。 這是 ASP.NET 中的保留資料夾名稱，您可以在其中放置 helper 等元件的程式碼。
2. 在*應用程式\_Code*  資料夾中，建立新的*cshtml*檔案，並將它命名為*MyHelpers*。
3. 以下列內容取代現有的內容：

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    程式碼會使用 `@helper` 語法來宣告名為 `MakeNote`的新 helper。 這個特定的協助程式可讓您傳遞名為 `content` 的參數，其中可包含文字和標記的組合。 Helper 會使用 `@content` 變數，將字串插入至便箋主體。

    請注意，此檔案的名稱為*MyHelpers*，但協助程式名為 `MakeNote`。 您可以將多個自訂 helper 放入單一檔案。
4. 儲存並關閉檔案。

## <a name="using-the-helper-in-a-page"></a>在頁面中使用 Helper

1. 在根資料夾中，建立名為*TestHelper*的新空白檔案。
2. 將下列程式碼加入檔案：

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    若要呼叫您所建立的協助程式，請使用 `@`，後面接著 helper 所在的檔案名、句點，然後是 helper 名稱。 （如果您在*應用程式\_Code*資料夾中有多個資料夾，您可以使用語法 `@FolderName.FileName.HelperName`，在任何嵌套的資料夾層級中呼叫您的 helper）。 您在括弧內以引號括住的文字，就是協助專家會在網頁中顯示為便箋一部分的文字。
3. 儲存頁面，並在瀏覽器中執行。 Helper 會產生您在兩個段落之間呼叫 helper 的「附注專案」。

    ![螢幕擷取畫面：顯示瀏覽器中的頁面，以及協助程式產生的標記如何將方塊放在指定的文字周圍。](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.png)

## <a name="additional-resources"></a>其他資源

[以水準功能表作為 Razor helper](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341)。 Mike Pope 的這個 blog 專案會示範如何使用標記、CSS 和程式碼，將水準功能表建立為協助程式。

[在 WebMatrix 和 ASP.NET MVC3 的 ASP.NET Web Pages 協助程式中運用 HTML5](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx)。 Sam Abraham 的這個 blog 專案會顯示轉譯 HTML5 `Canvas` 元素的 helper。

[WebMatrix 中 @Helpers 和 @Functions 之間的差異](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix)。 Mike Brind 的這個 blog 專案描述 `@helper` 語法和 `@function` 語法，以及每個語法的使用時機。
