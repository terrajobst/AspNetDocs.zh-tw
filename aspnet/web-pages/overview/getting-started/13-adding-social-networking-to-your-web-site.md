---
uid: web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
title: 將社交網路新增至 ASP.NET Web Pages （Razor）網站 |Microsoft Docs
author: Rick-Anderson
description: 本章說明如何整合您的網站與社交網路服務。 在本章中，您將瞭解如何讓人員將您的網站加上書簽/連結 。
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 03c342f9-b35c-4d7c-b9ed-cd9aaaffedb6
msc.legacyurl: /web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 1637464b0473bba8133acbbf8918d92b4f552701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526933"
---
# <a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a>將社交網路新增至 ASP.NET Web Pages （Razor）網站

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何將 Facebook、Twitter、Reddit 和 Digg 的社交網路連結新增至 ASP.NET Web Pages （Razor）網站中的頁面，以及如何包含 Twitter 摘要、Xbox 玩家卡片和 Gravatar 影像。
> 
> 您將學到什麼：
> 
> - 如何讓人員加入書簽/連結您的網站。
> - 如何新增 Twitter 摘要。
> - 如何將 Facebook **Like**按鈕新增至頁面。
> - 如何呈現 Gravatar.com 影像。
> - 如何在您的網站上顯示 Xbox 遊戲者卡片。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）2
> - ASP.NET Web Helper 程式庫（NuGet 套件）
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 3，但使用 ASP.NET Web Helper 程式庫的元件除外。

<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a>在社交網路網站上連結您的網站

如果您的網站上有其他人，他們通常會想要與朋友分享。 您可以藉由顯示使用者可以按一下以在 Digg、Reddit、Facebook、Twitter 或類似網站上共用頁面的圖像（圖示）來簡化這項工作。

若要顯示這些字元，請將 `LinkSharecode` helper 新增至頁面。 造訪您頁面的人員可以按一下個別的圖像。 如果他們擁有具有該社交網路網站的帳戶，他們就可以在該網站上張貼您頁面的連結。

![圖片1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. 如在[ASP.NET Web Pages 網站中安裝](https://go.microsoft.com/fwlink/?LinkId=252372)協助程式中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果您尚未新增）。-建立名為*ListLinkShare*的頁面，並新增下列標記：

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    在此範例中，當 `LinkShare` helper 執行時，會以參數的形式傳遞頁面標題，然後將頁面標題傳遞到社交網路網站。 不過，您可以傳入任何想要的字串。 這個範例也會指定要包含在清單中的社交網路網站。 您可以指定與網站相關的社交網路網站。
2. 在瀏覽器中執行*ListLinkShare。* （在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）
3. 按一下您要註冊的其中一個網站的圖像。 此連結會帶您前往所選社交網路網站上的頁面，您可以在其中共用連結。 例如，如果您按一下 [Reddit] 連結，就會進入 Reddit 網站上的 [`submit to reddit`] 頁面。

     ![圖片2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a>新增 Twitter 摘要

如需使用 Twitter 協助程式與目前版本的 Twitter API 相容的詳細資訊，請參閱[twitter helper](../ui-layouts-and-themes/twitter-helper.md)。 這個範例示範如何撰寫您自己的 helper，讓您可以輕鬆地重複使用多頁的程式碼。

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a>顯示 Facebook &quot;，例如&quot; 按鈕

在某些情況下，最好的選擇是直接從社交網路提供者取得程式碼，而不是依賴 helper。 如果社交網路提供者更新其選項的速度比協助程式更新更快，更是如此。

若要將 Facebook 功能（例如 [贊] 按鈕）新增至您的網站，您可以從[developers.facebook.com](https://developers.facebook.com/)網站取出程式碼片段。 在 Facebook 網站上，您可以使用其工具來產生與您的網站相關的程式碼片段。

下列反白顯示的程式碼是從 developers.facebook.com 網站上的 [Like] 按鈕工具中抓取的程式碼。 您必須提供您自己的應用程式識別碼。

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a>呈現 Gravatar 影像

*Gravatar* （&quot;全域辨識的頭像&quot;）是可在多個網站上用來作為您的頭像&#8212;的映射，也就是代表您的圖片。 例如，Gravatar 可以識別論壇文章中的人員、blog 留言等等。 （您可以在 Gravatar 網站註冊自己的 Gravatar，網址為[http://www.gravatar.com/](http://www.gravatar.com/)）。如果您想要在網站上的人名或電子郵件地址旁顯示影像，您可以使用 Gravatar helper。

在此範例中，您是使用代表自己的單一 Gravatar。 另一種使用 Gravatar 的方式，是讓使用者在您的網站上註冊時，指定他們的 Gravatar 位址。 （您可以瞭解如何讓人們註冊[ASP.NET Web Pages 網站的安全性和成員資格](https://go.microsoft.com/fwlink/?LinkId=202904)。）然後每當您顯示該使用者的資訊時，就可以將 Gravatar 新增至顯示使用者名稱的位置。

1. 如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未這麼做）。
2. 建立名為*Gravatar*的新網頁。
3. 將下列標記新增至檔案： 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    `Gravatar.GetHtml` 方法會在頁面上顯示 Gravatar 影像。 若要變更影像的大小，您可以包含數位做為第二個參數。 預設大小為80。 小於80的數位會使映射變小。 大於80的數位會使影像變大。
4. 在 `Gravatar.GetHtml` 方法中，將 `<Your Gravatar account here>` 取代為您用於 Gravatar 帳戶的電子郵件地址。 （如果您沒有 Gravatar 帳戶，您可以使用該使用者的電子郵件地址）。
5. 在您的瀏覽器中執行頁面。 此頁面會顯示您所指定電子郵件地址的兩個 Gravatar 影像。 第二個影像小於第一個映射。 

    ![圖片4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a>顯示 Xbox 玩家的卡片

當人們在線上播放 Microsoft Xbox 遊戲時，每個使用者都有唯一的識別碼。 每個播放程式的統計資料會以玩家介面卡的形式保留，以顯示其評價、玩家分數和最近玩的遊戲。 如果您是 Xbox 玩家，可以使用 `GamerCard` 協助程式，在網站的頁面上顯示您的玩家卡片。

1. 如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未這麼做）。
2. 建立名為*XboxGamer*的新頁面，並新增下列標記。

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    您可以使用 [`GamerCard.GetHtml`] 屬性來指定要顯示之玩家卡片的別名。
3. 在您的瀏覽器中執行頁面。 此頁面會顯示您指定的 Xbox 玩家卡片。

    ![圖 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)
